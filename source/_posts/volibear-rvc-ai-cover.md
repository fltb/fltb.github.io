---
title: "I Spent a Week Making Volibear Sing: Notes from an RVC AI Cover Project"
date: 2026-07-28 16:50:51
tags:
- AI
- RVC
- AI Cover
- Audio Processing
- Machine Learning
- Volibear
categories:
- AI
---

This project started purely for fun.

One day, after listening to a lot of AI covers online, I realized that although there were plenty of them, very few featured songs I actually liked. I also noticed that almost nobody had made covers with Volibear. Even the occasional ones I could find covered only a handful of songs. So I started wondering: could I train a model myself?

Might as well do it.

As it turned out, ideas that begin as “something to mess around with for an afternoon” have a remarkably consistent habit of swallowing the entire following week.

## Why I Chose RVC

There was no grand technical decision behind it. I searched around, eventually settled on RVC, and had very practical reasons for doing so: plenty of documentation, plenty of existing tools, mature training and inference workflows, and the ability to run it all on a single GPU. For someone who just wanted to hear a result as soon as possible, it was the best option available.

My final setup used RVC v2 at a 48 kHz sample rate, RMVPE for F0 extraction, and HuBERT v2 features. Training ran on a 12 GB RTX 4070. I initially trained for 200 epochs, but later found that 150 was usually enough; going further only wasted time without improving the result.

I eventually had AI consolidate the whole process into a series of scripts, so I could sit in a chat box and issue grand commands:

```text
Collect source audio
  → Clean and merge
  → RVC preprocessing and slicing
  → Extract F0
  → Extract HuBERT features
  → Train
  → Batch-convert test songs
  → Analyze spectra and listen manually
```

I could not be bothered with the WebUI, so I cloned RVC locally and had an AI Agent write scripts to take over the entire training pipeline. This also kept the data sources, parameters, and output models fixed for every version. I am a front-end developer—of course I know my way around a WebUI. It would only slow down my plan to go all-in on agents, haha.

## Where the Voice Data Came From

The first problem before training was, of course, the source material.

I ruled out the Chinese voice-over from the beginning. For one thing, extracting assets from the Chinese server was more troublesome. More importantly, Chinese voice actors had recently spoken out against AI voice conversion: large amounts of game dialogue were being turned into voice packs and derivative content, often without permission.

Their criticism was mainly aimed at certain large companies hiding behind “user uploads” to evade responsibility. But large companies have legal departments and platform policies; if a dispute actually happens, the individual hobbyist is usually the first one to get crushed. I had no intention of wading into that mess, so I went straight for the English voice-over.

Switching to English did not solve the copyright or ethical issues. I simply did not want to use the voices of Chinese actors who had explicitly objected to this kind of work, and I had no intention of making the project commercial. It was just something I wanted to play with.

Once that direction was set, I had OpenCode write a scraper to download Volibear's English game dialogue from the Wiki, along with the Inkshadow skin voice lines. After inspecting them, I found that the skin lines were unsuitable for training, so I added dozens of relevant lines from *Legends of Runeterra*. The final set contained 178 usable files: 132 from the main game and 46 from LOR.

The total duration was only a little over ten minutes, and every clip was short, punchy, heavily acted game dialogue. That was barely enough data to learn a timbre. For learning to sing, it was inadequate from the start—and that became the root of everything painful that followed.

## What the AI Agent Actually Did for This Project

I have to thank OpenCode, the AI Agent product, for its help during training.

By the time I wrote this post, its Subagents had deadlocked on edge cases often enough that I had moved to the lighter and more stable Oh My Pi. Still, OpenCode genuinely helped me a lot.

AI training projects have a particular character: very little of the work requires inspiration. Most of the time goes into downloading, renaming, filtering, transcoding, counting, batch execution, and occasionally stepping in to debug. None of those jobs is difficult on its own, but there are many of them, and one mistake anywhere can contaminate every experiment downstream. AI Agents are well suited to this kind of engineering labor: simple, messy, repetitive, and still required to be correct.

I decided whether a result was actually good and whether the next experiment was worth running. The Agent built the data pipeline, training scripts, batch inference, and analysis tools. Even when it occasionally started drooling on itself, it was still much faster than manually organizing hundreds of audio files.

## One RVC Trap That Made Me Laugh

The RVC version I had contained one remarkably well-hidden trap: during F0 feature extraction, it hard-coded the device to the CPU and then ran the job with multiple threads.

The CPU stayed pinned while the GPU did almost nothing, which looked wrong. The library being called supported GPU execution, and RMVPE itself was a natural fit for CUDA. I followed the call chain and, sure enough, found `device="cpu"`. Apparently somebody had found it too slow and then added multithreading on top.

In other words, everyone using that RVC WebUI had been sitting around waiting for the CPU to extract F0 across multiple threads. The thought made me laugh. If I had not known a little PyTorch myself, I would have stepped on exactly the same rake.

I laughed, changed it to CUDA, and moved on. I originally considered opening a PR, but then remembered that I would need to do a self-review and check compatibility and generality. I could not be bothered, put it aside, and left it there until writing this post reminded me again.

I also wanted to trace how that multithreaded “optimization” had been introduced, but my local checkout was only a `depth=1` shallow clone with no history. When I went back to GitHub, I found that on July 21, 2026, the history of `RVC-Project/Retrieval-based-Voice-Conversion-WebUI` had been replaced by a force-pushed overwrite-style commit. The old Git history was no longer accessible from the current repository. At least the new commit had fixed device selection and no longer hard-coded the CPU.

All I can say is that the author treats Git a little like tar and GitHub a little like cloud storage. In the past, I might have condemned this as a violation of Git conventions and a lack of engineering responsibility. These days, I do not really care. The fact that they are still willing to maintain the project is good enough.

## The First Model: Being Able to Speak Does Not Mean Being Able to Sing

As soon as the first model finished training, I ran a few songs I liked through it. The first major test was Avicii's *Without You*.

I initially assumed it was just an ordinary pop song. Only later did I learn that modern electronic music like this is anything but simple. I had chosen the hard mode for myself:

- The original vocal had undergone extensive production and mixing; it was not a clean, natural, untreated voice in the first place.
- Before conversion, the vocal and instrumental had to be separated. Synthesized vocals and complex mixes are themselves difficult for source-separation algorithms, and models such as UVR5 can leave phase and spectral residue behind.
- RVC's base model learns ordinary voice conversion. It does not automatically understand the vocal design used in commercially produced electronic music.
- Volibear's training set contained speech only: no sustained notes, slides, vibrato, breathing, or melodic phrases.
- The character has a very low voice, and the source material covered only a narrow pitch range. High-pitched data was almost nonexistent.
- The game dialogue also contained thunder, storms, and low-frequency impact effects. Once the model learned those as part of the timbre, they reappeared whenever it sang.

The result was, unsurprisingly, a disaster: muddy words, distorted high notes, and bizarre cries in the gaps. Even inside the frequency range the model could barely handle, it produced the synthetic sound of a badly tuned Vocaloid. The whole performance sounded torn apart.

Only later did I appreciate how specialized the arrangement, recording, and mixing of modern electronic music really are. A pipeline made from “scripts + a voice-conversion model” cannot compete with the production quality of a mature commercial release, especially a song like *Without You*.

RVC works better with pop, folk, and some rock where the vocals have received less processing and the boundary between voice and accompaniment is clearer. Song choice also has to fit the trained timbre and range. At minimum, the song should sound like something the character could plausibly sing. If it sits far outside the character's range, sustains high notes for too long, uses an extremely bright timbre, or heavily processes the original vocal, the model simply cannot sing it.

The fantasy we started with—train a model once, then have the character sing anything we want—does not really exist. The engineering difficulty is too high.

Things the model clearly cannot do are actually easy to handle: accept that it cannot do them, give up, and stop trying.

The truly dangerous ideas are the ones that “still seem optimizable in theory.” Those were what burned the rest of my week.

## Turning “It Sounds Bad” into Something Comparable

Once I realized how poor the quality was, I thought: great, time to start measuring everything.

First, I needed a way to compare models. Listening alone can work, but human hearing is easily influenced by volume, song choice, excerpt, and expectations. I am also lazy and could not keep listening forever.

After several rounds of discussion with DeepSeek inside OpenCode, I built a batch benchmark. I prepared multiple relatively clean vocal tracks in different styles, ran the same inputs through every model, calculated spectral metrics, and then combined those results with manual listening.

The metrics that actually distinguished the models were:

- **Spectral centroid stability**: tracks how much perceived brightness varies over time. A lower value usually means less trembling and fewer sudden shifts between bright and dull.
- **Spectral centroid**: roughly indicates whether the voice is bright or dark. Higher is not automatically better, but it shows when a model is becoming muffled.
- **Share of energy from 0–500 Hz**: too much usually means low-frequency swelling, producing a muddy sound like someone singing with their face buried in a blanket.
- **Share of energy from 0.5–2 kHz**: this range is more directly related to vocal clarity.
- **Share of energy above 8 kHz**: useful for spotting high-frequency spikes and anomalies introduced by source separation or the vocoder.

I also tried HNR, spectral flatness, zero-crossing rate, jitter, and shimmer. Later, I found that UVR5-separated vocals suffered enough phase damage that autocorrelation-based HNR returned an almost constant `-30 dB`, making it useless for comparison. Jitter and shimmer were also contaminated by unstable F0 extraction. The audio-processing pipeline mangled the data much more aggressively than I had expected. It could invalidate a whole set of metrics designed for natural voices, while two outputs that sounded similar could differ numerically far more than anticipated.

The final rule was simple: metrics were for screening and locating problems; my ears chose the finished result. I had hoped to be lazy and find one number that could decide whether a song sounded good. Then I could drop a `/loop` into the chat before bed and let the AI optimize by itself. By the next morning, either the result or the bill would be guaranteed to shock me into collapsing in my chair. No such luck. So much for intelligent labor.

## From v1 to v7.2: What Actually Changed in Each Round

Rather than turn dozens of experiments into a diary, I have summarized only the versions that materially affected the result.

### v1 / v2: Getting the Pipeline Running

The earliest versions trained directly on the collected game dialogue. v1 still contained some data that I later removed. v2 cleaned the set down to 178 files and adjusted the high-pass filter implementation.

The results showed that differences between static filtering implementations such as `filtfilt` and `lfilter` produced no detectable improvement in the final sound. They were not entirely meaningless, but they were not the real bottleneck.

### v3: 0.2 Seconds of Silence, the First Obvious Improvement

After many rounds of discussion, I suddenly noticed a problem: game voice lines are tightly trimmed. A file often begins on the first phoneme and ends immediately after the last one. The model had never seen what a voice naturally starting or stopping should sound like.

RVC performs its own internal slicing, so I added 0.2 seconds of silence to both ends of every training clip. This let the model learn fades, endings, and pauses at segment boundaries.

This version later became `volibear_original`. The improvement was obvious: articulation and sentence endings became much more stable. It was the first time I fell for the illusion that “a few more optimizations will solve everything.”

That illusion turned out to be expensive.

### v4: Denoising Did Not Produce a Second Miracle

After the success of silence padding, I added spectral denoising and trained `volibear_denoised`.

There was no obvious improvement. More epochs, different filters, and various preprocessing ideas all failed to reproduce the dramatic effect of silence padding. I stayed stuck here for a long time because every proposal sounded “useful in theory,” yet made almost no difference once trained.

Not every operation that makes data cleaner makes a model better. The game audio was already fairly clean, so denoising had little left to contribute and could even erase details of the timbre.

### v5: Adding Data from the Same Voice Actor

There was little more to gain by repeatedly cleaning ten-odd minutes of Volibear dialogue, so I started looking for a way to expand the dataset.

Volibear's English voice actor is David Sobolov. I went through his other roles and eventually found a near-hour-long YouTube voice-over video containing a Washford performance in a similar register. After vocal extraction, it gave me about 35.9 minutes of new material.

v5 mixed 178 Volibear files with 778 Washford clips: 956 files and more than 2,800 training segments in total. Once the new material outweighed the game dialogue, thunder and background effects from the original voice lines no longer dominated the dataset. The model became noticeably more usable.

This produced `volibear_sobolov`, the first genuinely reliable base for every experiment that followed.

### v5+: Longer Segments Were Cleaner, but Also Bass-Heavy

The problem with v5 was that the slicing script cut the audio too aggressively, leaving an average segment length of only about 2.9 seconds. Short segments were good for reproducing the input timbre, but they rarely captured complete breaths or continuous delivery.

I reorganized the Washford material into 151 longer clips of 5–15 seconds, combined them with the 178 Volibear files, and trained `volibear_sobolov_v2`, which I called v5+ internally.

This version had better continuity and cleaner harmonics, but it introduced a new cost: the share of low-frequency energy increased noticeably, making the voice more prone to sounding muffled. The conclusion was not “longer clips are always better,” but a practical tradeoff:

- Short clips stay closer to the input timbre and keep the centroid stable, but produce more noise and fragmentation.
- Long clips make continuous delivery and cleaner harmonics easier to learn, but can cause low-frequency swelling.

### v6: Pitch Augmentation, a Complete Failure

Because the original data covered such a narrow range, I pitch-shifted the training material by ±2 and ±4 semitones, hoping to expose the model to a wider F0 range.

The result was unambiguous: it did not learn to sing higher, and even ordinary speech became unstable. Both stability and perceived quality were clearly worse, so I deleted the entire version.

The idea looked reasonable but missed one important point: mathematically shifting frequencies does not create realistic vocal production, resonance placement, or singing technique. It provides “a higher note,” but not “how a human sings that note.”

v6 therefore gave me a clear conclusion: pitch augmentation did not work for this voice, and I would not touch it again.

### v7: Using the Model to Create “Pseudo-Singing” Data

At this point, the project hit another wall. David Sobolov had no publicly available singing material that I could directly use in this particular voice. Almost everything I could find was speech. Without singing data, the model had no way to learn sustained notes, vibrato, slides, or melodic phrases.

Half resigned, I borrowed an idea from LLM data distillation and self-training: if I could not find real singing material, I could first make an existing model sing, then feed the better results back into the training set.

Strictly speaking, this was not the same thing as LLM distillation, but the idea was similar: use an existing model to generate data containing the target structures, then let the next model learn those structures. The pseudo-singing data was not intended to redefine “Volibear's timbre”—the game lines and same-actor material already handled that. Its purpose was to expose the feature space to sustained notes, vibrato, slides, and natural breathing.

I used v5 rather than the more bass-heavy v5+ to convert clean vocals. v7 added roughly 150 seconds each from John Legend's *All of Me* and Tracy Chapman's *Fast Car*, then trained them together with the v5+ base dataset. Pseudo-singing made up about 14% of the complete training data.

This version brought spectral centroid stability down to about 848 Hz, the best of every version, proving that the pseudo-singing approach worked.

It also had an obvious problem. The selected passages from John Legend and Tracy Chapman were both fairly dark, and the final model learned the same darkness. v7 had an average spectral centroid of about 827 Hz and placed roughly 57% of its energy below 500 Hz. The singing was stable, but somewhat muffled.

### v7.1: Over-Filtering Removed the Useful Data Too

I then tried cutting the pseudo-singing into phrases and applying notch filters, quality gates, and deduplication so that only the “cleanest” material remained.

Of 286 candidate clips, only about three minutes survived. The pseudo-singing share fell to roughly 12%, and model stability actually regressed by about 119 Hz.

Further analysis showed that phrases generated by the same single-voice model are naturally very similar in spectral terms, with cosine similarity commonly above 0.92. Spectral deduplication therefore marked almost everything as a duplicate. F0 deduplication was no better: Volibear's useful range covered only about 100–250 Hz, so everything still converged into the same small region.

The conclusion was that the filters had no idea what counted as a useful singing pattern. They could only delete clips according to a few statistics. By the end, the information had been deleted along with the noise. The remaining dataset was certainly “pure,” but not useful for training.

### v7.2: The Choice of Pseudo-Songs Ultimately Determined the Timbre

v7.2 did not add more complicated algorithms. It returned to the simplest question: if v7 was too dark, why not choose two brighter pseudo-songs?

I selected Dido's *Thank You* and Birdy's *Skinny Love*, again taking about 150 seconds from each. Pseudo-singing remained around 14% of the data, and the rest of the training setup was essentially unchanged. I ultimately selected the checkpoint from epoch 140.

The results were:

| Model | Spectral centroid | Centroid stability | 0–500 Hz | 0.5–2 kHz | Perceived result |
| --- | ---: | ---: | ---: | ---: | --- |
| v7 | About 827 Hz | **About 848 Hz** | About 57.1% | About 35.2% | Most stable, but dark and muffled |
| v7.2 | **About 933 Hz** | About 890 Hz | **About 50.2%** | **About 41.5%** | Brighter and clearer, with much less bass swelling |

v7.2 was slightly less stable than v7, but the gains in clarity and brightness were unmistakable. It sounded better overall, so I chose it as the final release.

This produced the most valuable conclusion of the entire project: **pseudo-singing is not just a matter of “adding some singing data.” The songs you choose directly control the final timbre of the model.**

The Dido and Birdy material was brighter, so the model became brighter. The John Legend and Tracy Chapman material was darker, so the model leaned toward a darker, more bass-heavy sound.

Apparently, writing a pile of scripts I barely understood to filter the data was less effective than choosing two songs myself. Audio data processing is simply too difficult.

## More Ideas That Looked Useful but Were Not

I tried plenty of other things during that week. None were worth continuing:

- Pitch augmentation by ±2 or ±4 semitones: v6 had already proved it ineffective.
- MDXNet dereverberation on already-clean game dialogue: unnecessary.
- An 8 kHz low-pass filter on the output: the model had little useful content above 8 kHz anyway, so it only made the sound darker.
- Adjusting RVC's `protect` and `filter_radius`: spectral changes stayed below 1%, with no meaningful audible difference.
- Phrase-level spectral deduplication: outputs from a single-voice model are naturally similar, so it deleted nearly everything.
- F0 deduplication: the pitch range was too narrow to distinguish anything.
- STFT-based frequency-band blending of two models: the crossover damaged harmonic structure.
- So-called “de-hoarsening” through harmonic/noise decomposition: it damaged UVR5 vocals more than it repaired them.

These failures were not a complete waste of time. At least they established what I should stop doing, so I will not feel compelled to train another version every time I notice a new parameter.

## The Final Model Still Did Not Become a Universal Singer

After all these experiments, I finally understood why almost nobody makes Volibear covers: it is too hard.

After all that time and compute, I ended up with a model that was only barely usable and still difficult to control. v7.2 could sing far more songs, and its articulation, clarity, and continuity were all much better than the first version. It still was not a general-purpose model that could “just sing” anything. High notes and extreme timbres could still trigger bizarre cries, complex electronic vocals still failed easily, and song choice still mattered more than parameters.

It is like a singer with a distinctive voice but unreliable technique: you have to understand his comfort zone and choose the right song, or he starts making monster noises.

I still made a few covers and uploaded them to Bilibili. They should be easy to find. Almost nobody else makes content for this character, so searching for “Volibear AI cover” or “沃利贝尔 AI 翻唱” is unlikely to bury them.

## Artwork: After Generating a Thousand Images, I Chose Gemini

That covers the singing. Next came the artwork and video.

The artwork was simpler. I first tried ComfyUI and downloaded a Volibear LoRA from Civit AI. OpenCode connected to the ComfyUI API, translated my natural-language requests into prompts, and generated images in batches.

After forty or fifty scenes and nearly a thousand images, I switched to Google Gemini.

Not one of those thousand images consistently met the standard of a finished poster. Composition, anatomy, armor, and style all went mad in different ways. This was not surprising: I had seen nearly every image available to train that LoRA. I already knew what it could generate and what kinds of scenes it handled well. Whatever those were, they were not the music posters I wanted, haha.

Strictly speaking, ComfyUI could meet my requirements. I was simply too lazy to build the workflow graph by hand. I wanted OpenCode to drive ComfyUI, pull the gacha lever, and judge the results by itself—which made the whole thing much harder.

In the end, this kind of make-a-wish requirement still called for a polished commercial platform. Gemini directly produced compositions much closer to a finished cover. The final video used a version with the title and author information for its opening seconds, then switched to a text-free key visual with lyrics overlaid.

## Video: When Kdenlive Broke, I Nearly Started Editing Subtitles in Blender

The video assembly process had its own absurd detour.

Kdenlive collapsed under the thunderous combination of Debian + KDE + Wayland + NVIDIA. Preview, encoding, and interface problems piled on top of one another. With no good option left, I briefly started using **Blender to edit video subtitles**.

That was madness. Blender can certainly edit video, but I am lazy enough already. Making me edit a video in Blender would drive me insane.

Eventually, I returned to the simplest possible solution:

```text
Cover image / key visual
  + AI cover audio
  + Manually synchronized SRT lyrics
  + Python calling FFmpeg
  = A 1080p video ready to upload to Bilibili
```

The first ten seconds showed the title, artist, and AI Cover information, after which the video switched to the key visual. Subtitles used white text with a black outline, fixed near the bottom of the frame. There were no elaborate transitions or numerous shots, but the process was stable and reproducible. After changing the lyric timing, I could simply generate the video again.

By the end of all that, I had no energy left to promote it. I threw the videos onto Bilibili, sent them to a few friends, and called it done.

## Why I Wrote a Blog Post Instead of Uploading the Whole Project to GitHub

At this point, someone might ask: if the scripts, models, and pipeline already exist, why not clean everything up and put it on GitHub?

Because it is a 90+ GB experimental crime scene. It contains 57 GB of training logs, model weights, benchmark outputs, game dialogue, commercial songs, separated stems, generated images, and a `pack.zip` that alone is 206 MB. I have not yet developed the habit of treating GitHub as cloud storage.

The voice clips, songs, and model weights cannot be published together either. That would be plain old copyright infringement, kid. RVC itself already has an upstream repository, while the scripts I actually wrote are full of local paths, one-off experiments, and the remains of failed ideas. Clone the repository as-is and you would probably be signing up for a technical archaeology expedition.

A real release would require a clean code-only repository containing only scripts, configuration, and documentation, with every dataset and model excluded. That would cost too much time, and I doubt many people will become interested in covering songs with this character anytime soon. Anyone who genuinely is interested can email me; I would be more than happy to help.

For now, the blog post is enough. The lessons can be shared without packaging the experimental crime scene. Maybe I will clean it up one day when I encounter the project while clearing space from my drive.

## Finally

This project began as “make the bear sing a couple of songs I like” and ended as an entire pipeline for data collection, training, evaluation, audio processing, image generation, and video assembly.

At the end, I asked AI to summarize what I had learned:

1. A model cannot magically learn abilities absent from its training data.
2. Data boundaries and segment organization sometimes matter more than additional training epochs.
3. High-quality material from the same voice actor is more valuable than large amounts of similar but mismatched data.
4. Pseudo-singing can supply singing patterns, but its proportion and song selection directly alter the output timbre.
5. Metrics can help locate problems, but the final decision still requires manual listening with consistent inputs.
6. The greatest value of a failed experiment is that I do not have to repeat it later.

Judged solely by the result, the final model still was not mature. It could not sing every song or completely avoid making monster noises. But the difference was substantial: the first version tore every high note apart and went mad in empty spaces, while v7.2 could reliably finish a range of pop, folk, and rock songs.

Measured against the goal of creating a universal Volibear singer, the week was still a failure. I never achieved that goal, because the goal itself was unrealistic.

Measured against “I just want to hear this character sing a few songs,” it was not much of a failure at all. I did hear it in the end, and almost nobody else online had made anything like it.

That is enough. I am done.
