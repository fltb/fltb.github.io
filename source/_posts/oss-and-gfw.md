---
title: Great Firewall of China, Open Source and Socialism
date: 2023-07-06 17:22:07
tags:
- Great Firewall of China
- Feeling
- Open Source
- Programming
- Socialism
categories:
- Politics
---

**Thanks to [gkcoll](https://www.gkcoll.xyz) for the first version of [translation](https://www.gkcoll.xyz/542.html)!**

I am pessimistic about the future of domestic Open Source communities in China. I won't mention other large or small obstacles for now but focus on of the elephant in the room specifically, which is Great Firewall of China(GFW).

This article is divided into two parts to explain. the first part lists the crimes of policies represented by Great Firewall of China and clarify how they hinder open source community development. The second part operates how the open source communities runs, combines with socialism theory, to tell the intention of the current policies, and tries to explain the reasons behind them and put forward some rough plans.

The main purpose of the article is to attract valuable insights. If there are any flaws, please point them out and make suggestions for improvement.

## How Great Firewall of China harms the Open Source Community


As of now, the computer penetration rate in China is relatively low. This is a fundamental limitation, as it is impossible to develop software on a mobile phone. Additionally, the general public's computer literacy is generally insufficient，as evidenced by the discussion of "Internet addiction" and "Game addiction prevention". These factor need to be further discussed，but they are too broad in scope. So let's set them aside now，and focus on how the existing policies are directly hindering the development of the open source community in China. These obstacles, unlike the previous ones, are purely man-made issues, which can be removed by in a day. The Great Firewall of China, which is standard for the Great Firewall, uses a group of operator level methods like by hijacking connections and DNS pollution to prevent Chinese people from accessing some websites abroad.

Next, I will refer to the paradigm given in [Participating in Open Source Communities *How to be a good corporate citizen when participating in an open source project*](https://www.linuxfoundation.org/resources/open-source-guides/participating-in-open-source-communities) to point out how Great Firewall of China is preventing people joining the Open Source Community. 

<blockquote>
<p>If there is an underlying theme for this guide and for OS in general, it’s that every project is different. Every time you join an OS project, you’ll need to spend some time <strong>orienting yourself to the project and learning how it works</strong>.</p>
<p>For organizations participating in an OS project, each employee will need to go through this learning process for each project they participate in. Here are a few things that can help you get started off on the right foot.</p>
<ul>
<li>Join the community. Each community will have slightly different ways of participating and different channels. Read the documentation to find out about the community and join the key communication channels. These channels may include mailing lists, forums, IRC, Slack, bug trackers, source code repositories, and more.</li>
<li>Lurk first. After you’ve joined the community, spend a significant amount of time lurking and reading the archives to soak up the culture before you start contributing. You’ll want to understand the norms and expectations of this community before you participate. The more time you spend reading and listening, the more likely it is that your first contribution will be well received.</li>
<li>Understand the governance. Read the documentation or website sections about project governance and leadership before contributing. You’ll want to understand how decisions are made within the project and who makes the decisions for various types of contributions.</li>
<li>Start small. Tackle a simple bug or documentation fix to start. It will be easier to learn the process and correct mistakes on a small contribution that isn’t critical to your organization’s needs. Make your mistakes on small and less significant contributions as you work up to the more complex contributions that your organization needs.</li>
</ul>
<p>Now that your organization has figured out how to make those first small contributions, you’ll need to build on those contributions to begin making larger contributions and having a bigger impact in the project.</p>
<ul>
<li><strong>Build relationships at events.</strong> Relationships on a personal and organizational level are an important aspect of participating in an open source community. One of the best ways to build lasting relationships with other project members is by attending events. There is nothing quite like meeting someone in person to help understand them as a human being on the other side of their email address or online handle. These events have a varied mix of people from project leaders and passionate users of the product to direct participation from many of the organizations through sponsorships, booths, and demos to show how the organization contributes. Most of these events would not be possible without financial support from sponsoring organizations that allow us to get together and learn from each other while helping to achieve the goals of the project.</li>
<li><strong>Include the community</strong> early and often. Some organizations make the mistake of <strong>developing big chunks of code in house and then dumping them into the open source project</strong>, which is almost never seen as a positive way to engage with the community. The reality is that open source projects can be complex, and what seems like an obvious change might have far reaching side effects in other parts of the project. Any significant change is likely to require some <strong>community discussion</strong> before it moves to implementation to make sure that there are no side effects and that the solution is aligned with the broader goals for the project. While you discuss it with the community, it can help to focus on the problem, rather than a specific solution, before you invest too much time in the creation of a body of code.</li>
<li><strong>Contribute upstream.</strong> This refers to the practice of sending any changes you make to an open source project back to the original maintainers for inclusion into an upcoming release of the software. If your organization is new to open source, you may need to spend some time educating your employees about the importance of upstreaming contributions. In some cases, people may think it will be easier to do a quick and dirty patch to get something working in your infrastructure and not bother with cleaning it up and going through the process of getting it accepted into the upstream project.</li>
</ul>
</blockquote>

For individual developers, Great Firewall of China have these charges:

- Increase the difficulty of getting started with the open source project.
- Blocks the communication between domestic open source communities and international open source communities (in terms of participating in communities and contributing upstream).
- Blocks the communication between open source communities and ordinary users.

### Connection issues

Many programming websites and software repositories are blocked by Great Firewall of China for unknown reasons. This list includes a huge amount of popular websites. And some websites, like github and jsdelivr, are blocked "softly", meaning that their connection are not stable. It's possible that you can connect to GitHub one minute, but then the next minute you get a connection timeout error. Connections can be blocked or slowed frequently when you try to install some dependencies via pip, npm or other package managers in China. 

So programers in China have to do a lot of useless works to solve these troubles that won't happen in most countries. Since jsdelivr have been blocked, they will self-host some libraries to waste resources of servers, or they need to find github mirrors because of the connection issues. I can make a long list for all these annoying problems. Beginners may have to spend a few days setting up a development environment if they don't have any help. How many beginners have been discouraged by the abundance of advertisements and plagiarism on Chinese websites when facing a development problem? Meanwhile, foreign beginners can often find helpful answers on Stack Overflow in less than half an hour.

The Great Firewall of China has cut off the flow of new talent to open source communities in China. That's really bad.

Sometimes it can lead to local security vulnerabilities, such as [XcodeGhost](https://www.macrumors.com/2015/09/20/xcodeghost-chinese-malware-faq/).

> A malicious version of Xcode was uploaded to Chinese cloud file sharing service Baidu and downloaded by some iOS developers in China.  
> Chinese developers then unknowingly compiled iOS apps using the modified Xcode IDE and distributed those infected apps through the App Store.  
> Those apps then managed to pass through Apple's code review process, enabling iOS users to install or update the infected apps on their devices.

If developers in China can connect to xcode's website directly, then these sort of bad things won't happen at all.

### Development

If the problems mentioned above can be solved through various legal means, then what about communication with the community? Currently, all other ways to communicate with developers are unavailable, except for IRC, self-hosted forums, email, and GitHub Issues. This includes popular platforms such as Telegram, Discord, Reddit, Matrix, Twitter, Facebook, and Instagram. The former platforms are also limited to formal discussions about the software itself.

In other words, we can only get the source code and binary files of the software, and at most suggest something about the software itself. We cannot personally contact the developers, have a more in-depth communication with them, and integrate into the open source culture. This means that we cannot learn how to develop, what to develop, or influence the direction of the project. We can only be passive observers.

Even GitHub has been soft-blocked, which has already affected the development of the software itself. Surely no one doesn't know that mirrors cannot create pull requests or issues.

As for contributing to upstream projects, if we only focus to the legal way, it's pointless to even discuss it. I'm also curious about how to write acceptable code for upstream without getting involved and understanding the development direction.

Some people may have ridiculous ideas about developing with pure domestic open source community. But what do we rely on? CSDN, Gitee, and QQ? Whoever is confident, let them go ahead. Even if you really make an interesting project, if you can't promote it to the world, the demand in China is not enough to support high-quality open source software. Then there is no need to talk about development. Only who can fool the non-technical officers of the relevant department can get support and survives.

For individual, the only choice is to against the law:

> Computer information networks that directly connect to the Internet must use international access channels provided by the state public telecommunications network of the Ministry of Posts and Telecommunications.  
> No units or individuals are allowed to establish or use other channels to connect to the Internet on their own.  
> —— *Interim Provisions on the Management of International Networking of Computer Information Networks*

A programmer had to be illegal before he could develop is the worst condemnation of the Chinese open source community. But some people, like spectators who don't know open source and developers who cheat themselves, still says that The GFW is "reasonable and necessary". That's absurd.

### User

What we mentioned above is all about the developer, so next we will talk about the users. Softwares must have users, and the community needs users too. But the Great Firewall of China have cut down this link ruthlessly.

There are a bunch of admirable projects in Chinese open source community, for example, the Ventoy Project, which allow users to create bootable USB drive for multiple ISO files. In the English interface, it only provides a single download link to Sourceforge. In the Chinese interface, there are many download links. This is because Chinese users cannot access Sourceforge, and the quality of third-party cloud storage services in China is also very poor. Here is the list：

- <https://github.com/ventoy/Ventoy/releases/>
- <https://gitee.com/longpanda/Ventoy/releases/>
- <https://mirrors.nju.edu.cn/github-release/ventoy/Ventoy> Nanjing University's mirror
- <https://mirrors.sdu.edu.cn/github-release/ventoy_Ventoy> Shandong University's mirror
- <https://www.lanzoui.com/b01bd54gb> Lanzouyun cloud storage
- <https://www.123pan.com/s/rjSKVv-8YtN> 123yun cloud storage, password: vtoy
- <https://pan.baidu.com/s/1UzHMzn6SToxHRYw7HR16_w> BaiduNetdisk, password: vtoy

Thanks to Great Firewall of China, even downloading the software could be a challenge. If a Chinese user want to try some open source software, then he will find himself stuck because it only have a github releases or source forge download link, which is cut down by the Great Firewall. Or even worse, the whole website are cut  down, like Scratch. You can not demand a ordinary user to have ability to bypass the Great Firewall like developers, right? 

Some phishing website are happy about this. Since the official website are unreachable, they can pretend they are official. Some website provide a bunch of malware alongside that, others even sell some open source software: Python? ￥70! Scratch? ￥80！(around $10). What's more, the malware is more likely to get the higher rank on Chinese search engines than the official website, because they paid protection fees fot the search engine like Baidu, while official website do not.

For ordinary user, they have no way to access the global open source community. In this case, except for few project still at an average level like Deepin Linux, user can only hear some policy-driven watch source software from domestic companies. We call them *watch source* because are not real open source software. Their only purpose is to fool the public's eyes and have more chance to get the official subsidies called Xinchuang. Users and communities are nonsense in their eyes.

As a result, people in China know less about the open source. That's really bad for us.

### Summary

As the link between the open source community and the ordinary user are cut off and the individual developers have to overcome many difficulties to get involved in the community, it is meaningless to talk about the future development of the open source community in China. We need to face the problem of how to develop new people and survive at first.

Maybe companies that rely on subsidies and advertising are happy about this. In the case fo a weak community, they can take advantage of the information gap to make a bit secondary development based on the open source project and make money of them under the guise of "self-developed". No matter what the purpose of the force behind the Great Firewall are, they have lead to the fact that they sells the future of the domestic open source community and put them into someone's pockets.

## 现有政策的真实意图

### 开源到底是什么？

要想历数政策的问题，就要先从开源的运作模式出发。开源是一种生产资料公有制的实践，这里当然是社会主义的。很多人受到各种自由主义的影响，对于社会主义唯恐避之不及，或者干脆将 Great Firewall of China 背后的势力和社会主义混为一谈。又有些“社会主义者”对于正在发生的，可以说是公有制历史上面具有划时代意义的运动漠然视之。这里作为所谓的 Socialist Programmer，我决定对这个问题阐述我自己的想法。

下面参考 [什么是开源 (What is open source)](https://opensource.com/resources/what-open-source) 中有关开源的阐述。


> 开源软件是任何人都可以检查、修改和增强源代码的软件。
>
> “源代码”是大多数计算机用户从未见过的软件部分；它是计算机程序员可以操纵的代码，用于改变软件（“程序”或“应用程序”）的工作方式。有权访问计算机程序源代码的程序员可以通过向其添加功能或修复不能始终正常工作的部分来改进该程序。
>
> 有些软件的源代码只有创建它的人、团队或组织——并保持对它的**独占控制**——才能修改。人们称这种软件 **“专有”或“闭源”** 软件。
>
> 只有专有软件的原始作者才能合法地复制、检查和更改该软件。为了使用专有软件，计算机用户必须同意（通常通过签署他们第一次运行该软件时显示的许可证）他们不会对软件作者未明确允许的软件进行任何操作。Microsoft Office 和 Adob​​e Photoshop 是专有软件的示例。
>
> 开源软件是不同的。它的作者将其源代码提供给其他想要查看该代码、复制它、从中学习、更改它或共享它的人。LibreOffice和GNU Image Manipulation Program是开源软件的例子。
>
> 正如他们对专有软件所做的那样，用户在使用开源软件时必须接受许可条款——但开源许可的法律条款与专有许可的法律条款有很大不同。
> 开源许可证影响人们使用、研究、修改和分发软件的方式。一般而言，开放源代码许可证授予计算机用户**出于他们希望的任何目的使用开放源代码软件的许可**。一些开源许可证——有些人称之为“copyleft”许可证——规定任何发布修改后的开源程序的人都必须同时发布该程序的源代码。此外，一些开放源代码许可证规定，任何人修改并与他人共享程序，也必须共享该程序的源代码，而无需为此收取许可费。
>
> 通过设计，开源软件许可证促进协作和共享，因为它们允许其他人对源代码进行修改并将这些更改合并到他们自己的项目中。他们鼓励计算机程序员**随时访问、查看和修改开源软件**，只要他们在分享他们的工作时允许其他人做同样的事情。

总体来说，开源是和专有相对的概念，开源软件可以被分享，可以被任意地使用和修改再发布，而不会有法律上面的风险。

这是模糊了“自由软件”原则的“开源软件”的阐述。这些原则 [GNU 的自由软件](https://www.gnu.org)当中得到更加明确的说明：

> 不论目的为何，有运行该软件的自由（自由之零）。  
> 有研究该软件如何工作以及按需改写该软件的自由（自由之一）。取得该软件源代码为达成此目的之前提。  
> 有重新发布拷贝的自由，这样你可以借此来敦亲睦邻（自由之二）。  
> 有向公众发布改进版软件的自由（自由之三），这样整个社群都可因此受惠。取得该软件源码为达成此目的之前提。

在这里，我们看到了一个公有制的体系。在这里，软件不再可以被私人占有并用来支配他人。但是在说明这个原则之前，应当先说明一个典型的私有制体系是怎么运行的。

在[《1844年经济学哲学手稿》](https://www.marxists.org/chinese/marx/marxist.org-chinese-marx-1844.htm#10)当中有这样一段话：

> 没有自然界，没有**感性的外部世界**，工人就什么也不能创造。它是工人的劳动得以实现、工人的劳动在其中活动、工人的劳动从中生产出和借以生产出自己的产品的材料。  
> 但是，自然界一方面这样在意义上**给劳动提供生活资料**，即没有劳动加工的对象，劳动就不能存在，另一方面，自然界也在更狭隘的意义上提供生活资料，即**维持工人本身的肉体生存**所需的数据。  
>因此，工人越是通过自己的劳动占有外部世界、感性自然界，他就越是在两个方面**失去生活资料**：第一，感性的外部世界越来越不成为属于他的**劳动的对象**，不成为他的**劳动的生活资料**；第二，这个外部世界越来越不给他提供**直接意义的生活资料**，即维持劳动者的肉体生存的手段。

这里指出来两个事实：

- 只有依靠已有的劳动才能生存
- 只有依靠已有的劳动才能再创造新的东西（再生产）

开源的软件，作为劳动的产品，虽然不能维持个人的生存，但是可以用来生产新的产品。一种情况是使用像 GCC 这样的开发工具，一种情况是直接 fork 某个软件二次开发。这就防止了某个独立于开发者和用户之外的人支配使用这个软件的产出。

我们先用一个简化的情况来分析。假设现在只有 VC++ 一种编译器，被 MS 占有，垄断并且收取天价版权费，那么会发生这样的情况：

1. 开发者只有进入公司才能开发 VC++ 。
2. 开发者只有进入公司或者缴纳天价版权费才能使用 VC++ 。

在 (1) 的情况下面因为这个软件的版权属于公司，所以给公司开发越多，VC++ 越强大，开发者相对就越弱小，那么 (2) 的情况也会加强，从而导致公司对开发者的全面控制，以至个人离开公司就不能开发软件，而小型团队需要把自己的获利的大部分交给公司。即使有多个专有软件相互竞争，情况也不会好多少，除非其中之一在事实上采取类似开源软件的做法。而现实中 GCC 的存在使上面的情况不能成立。

使用 VC++ 做假设是因为 MS 曾经敌视开源的态度深入人心，所以就地取材了。我只是指出这样的事实：开源使得大公司利用占垄断地位的专有软件作为资本并控制软件社区谋取利益成为不可能。在开源的秩序里面，个人的劳动不再用来反对他们自己，而是用来建立一个公共劳动库，使得开发者而不是公司的一方强大起来。软件能有现在的发展可以归功于开源，所以——只是顺便提一下——开源使得程序员竞争力下降的说法在整体上是站不住脚的。

### 他们究竟在做什么？

现在有些人正在套用他们在其他领域的“成功”经验，把一些紧箍咒加到国内的开源社区上，试图让开源按照他们的想法发展。典型的政策有：软**墙 Github** 推广 Gitee, 在 Gitee 上面推行**审核**，给一些**看起来**符合他们想法的项目（全是各种公司的项目）补贴。前面两种做法无疑是限制个人开发者，后面则是鼓励企业。某种意义上确实也体现了中国特色（国家）社会主义的本质特色了。

有些人试图使用以下的理由去为当前的政策辩护：

- 需要一个“国产”“中国”“民族”的开源平台，防止西方（还不如直接说美国）制裁
- Github 以及其他被墙的平台上面上面存在一些“危险”的内容。（根据我的观察，大概是目田壬的胡言和分离主义的乱语，顶天加上一些 High 了的邪教疯子罢了，看起来无感甚至好笑，不懂为啥这么大反应）

接下来我将分点批驳。

#### “民族”的开源平台？

他们似乎想要建立一个所谓“国产”“中国”“民族”的开源平台，并以此绑架开发者。但是，开源平台本身是**不能**带上这些属性的。

一个纯粹的开源平台的运作模式，就是在用户和开发者，开发者和开发者中间充当中介。软件在发布时已经不被作者私人占有（虽然法律上面保留著作权，但是已经不能用来限制用户），成为了公共软件库的一部分。所以平台更**不能**代替作者取得这样的权利。虽然 Github 整体上是一个商业平台，但是它本身又包含了一个开源平台，所以它的开源平台的部分也遵守这些规律。

既然开源软件是公有的，那么它就不能同时又是民族的。开源软件作者本人都不能占有软件本身，平台也就不能取得作者无法取得的权利去用来反对什么人，所谓来自平台的“民族”“国家”的限制就更无从说起。如果——像很多毫无根据的担忧一样——美国政府禁运开源软件，那么会发生下面的情况：美国政府违反了他们自己制定的版权法律，去声明他们拥有对作者放弃版权的软件的处理权力，在理论上他们自己不合法了;美国政府管不到其他国家的镜像站，在实际上他们也做不到阻止某个国家的人使用美国人开发的开源软件。所以美国政府并不像有些人臆想的一样愚蠢，在其指使 Github 对一些国家地区的禁运中，受影响的只是私有仓库和一些其他的**商业**用途，[开源社区的部分没有受到影响](https://docs.github.com/zh/site-policy/other-site-policies/github-and-trade-controls)：

> GitHub 致力于继续为在叙利亚、克里米亚以及顿涅茨克和卢甘斯克分离主义地区拥有个人和组织帐户的他发人员提供**免费的公共存储库服务**。 这包括有限制地**访问免费服务**，例如用于开源项目（和相关公共页面）的公共存储库、公共 Gist 以及分配的免费操作分钟数，但只能用于个人通信，而不得用于商业目的。

这样我们可以看出，建立一个“自主可控”的平台就是无稽之谈。开源平台本身就是自主可控的，有国界的不是开源，是 Github 的商业部分。只要 Github 不想在道义上面自杀，不想步 Freenode 的后尘，就必须和开发者站在一起。只要美国政府不想放弃美国在互联网上目前具有的优势，就不能做出限制开源的愚蠢行动。当然限制某些地区使用 Github 的商业功能也是帝国主义战略的一环，不过不在本文的范围之内。至少开源社区不会卷入帝国主义互殴，因为加入了的就**不能称之为开源**了。

#### “危险”的言论？

一些人真诚地尝试让我们相信，现在的 Great Firewall of China 是某种“保护伞”，让我们和一些危险的言论隔离开来以保护我们。然而这句话的“危险”“隔离”和“保护”都是有问题的，根本禁不起进一步探究。

首先“危险”的是邪教么？这种说法听起来就像这些势力**只**通过互联网宣扬他们的灵丹妙药一样。事实上这甚至**不是主要的方式**。就拿个人经历来说，我在菜场（浙江，温州）买菜的时候找钱也能拿到一张印着“五字真言”的50元，后来拿去银行了。了解他们的主要活动方式只要百度一下就可以了。比如在[邪教组织有哪些活动方式](https://www.cqcb.com/county/changshouqu/changshouquxinwen/2018-08-01/997213.html)里面提到的（这种韵文还挺好玩的）：

> 暗中串联建立组织。  
> 建立窝点制发资料。  
> 为“讲真相”四处煽动。  
> 制造谣言混淆视听。  
> 假借维权制造混乱。  
> 散布信息威胁骚扰。  
> 大搞“三退”虚张声势。  
> 内外勾结充当走卒。

可以说**地下组织**才是这些活动主要的方式。既然敌人已经在内部了，就应当内部在消灭。为一个无用的措施波及开源社区，不是太____了么？

那么是自由派么？确实这些人也是主要的打击对象。他们意识到拳头是冲着他们来的，但是由于不学无术，他们连替自己辩护都只能复读“自由”“民主”“威权”“钳制思想”，四舍五入约等于废话，连一个实际的行动原则都出不来。这样的一盘散沙的野生目田有什么可取之处值得如此的警惕。别的不说，就拿香港的溃败来说，据说 **200 万**人次的参与放在一个总人口 700 万的城市里面竟然连“反修例”都搞不定，这不是处于主体地位的自由派的耻辱又是什么呢？没有一个处于中心的组织领导有力的行动，又怎么对抗“威权”？靠游行和辩论只能把自己送进监狱里面，不能取得那些应当得到的东西。这里无非是说明自由派根本没有 pink 想象中的力量，从而化解他们想象中的 Great Firewall of China 的合法性来源。

是分离主义者么？理论上他们也在打击范围内。但是认为这些 Cosplay 爱好者拥有什么可以实践他们主张的力量在某种程度上面也和他们一个水平了。这些人和上面讲的自由派一样只是一些复读机，根本没有从严肃的理论和实际的形式上面为他们朝思暮想的分离寻找借口，更不要提什么实际措施了，所以也只能吸引和 pink 差不多的东西。

如果说有些普通人会被上述的奇思妙想所吸引，Great Firewall of China 又能做什么？pink 无非是想要证明，官方的叙事是如此失败，以至于可以输给疯子和复读机。

上面只是一些基本的观点，有时间可以进一步论述，对于以开源为主题的本文来说展开到上面的程度已经够了。

## 真实的意图 & 怎么办？

那些躲藏在背后的势力一直没有对其意图作出任何解释，让各种信男信女兔子兔孙满大街找借口，好像这样可以打马虎眼，装死挺过去，事情也基本在他们的预料之内。

这些理由还不能解释 jsdelivr, npm, pypi 这类仅仅用来下载软件库的网站的墙。要想出这个的理由应该太为难他们了。所以这里要请出一个幽灵，让祂来解释背后的原因。

中国目前的状态可以说是一个火药桶。在[《随着青年失业率上升，中国经济增长放缓》(*China growth rate falters as youth unemployment rises*, WSWS)](https://www.wsws.org/en/articles/2023/05/31/lsxh-m31.html)这篇文章里面可以体现出来。Google 机翻如下：

> 根据高盛最近的一份报告，中国城市青年失业率现在大约是 COVID 之前 10% 的两倍，这很可能被低估了。这一比率在未来几个月可能会迅速上升，随着毕业季的开始，届时将有创纪录的 1160 万年轻人进入劳动力市场，这一数字可能会跃升 3-4 个百分点。 

>去年三月，无疑反映了官方的政策转向，共青团发表了一篇文章，攻击毕业生固执己见，拒绝在工厂“拧紧螺丝”，谴责他们的“消极”态度，并告诉他们“脱掉他们的长衫，进入工厂和农田。”  
> 该声明引起了社交媒体的强烈抗议，其中一条评论询问作者是否“愿意放弃目前的工作，成为一名街道清洁工或工厂工人”。

> 一位微信评论者写道：“你们应该落实劳动法，解决劳动者真正关心的问题。”  
> 这种轰轰烈烈的反对派尚未采取公开的政治形式。  
> 以习近平为首的统治寡头最担心这种发展，因为中国的发展现实与资本主义复辟代表工人阶级和群众前进道路的主流意识形态发生冲突。

在阶级斗争的压力下面，任何“不和谐”的思想都会被视为火种严加防范。开源社区的理念，因为其**公有制**的性质，因为它的组织解放出开发者的生产力，显然可以划在这类思想里面。开源社区的人，在参与社区的工作的时候，受到这种理念的影响，自然就成为“危险”了。挂着羊头的 CCP 无比熟悉这样的情形，就像[《在“人民报”创刊纪念会上的演说》](https://www.marxists.org/chinese/marx/mia-chinese-marx-18560414.htm)提出的：

> 蒸汽、电力和自动纺机甚至是比巴尔贝斯、拉斯拜尔和布朗基诸位公民更危险万分的革命家。

在这种基础上，无论开源社区的人如何“去政治化”和“中立”，在这个大前提下面，显然是得不到 CCP 的信任的。他们宁可相信自己的应声虫——也就是大小企业——能够撑起国内的开源软件，并对跟班们的“忠诚”发放奖赏。（[然而有些家伙还是被敲打了，比如统信](https://www.oschina.net/news/198698)）

很不幸的一点是，程序员们似乎很能“忍”。对于 996 “声势浩大”的声讨其实也暴露出这一群体的软弱：他们竟然没有罢工。因为以“万”作为单位的收入也带来了小资特有的软弱，消融了哪怕面对哪怕一点点丢掉工作的风险的勇气：[为什么不联起手来罢工击杀996制度 ](https://cnodejs.org/topic/5dcb943eece3813ad9ba80d0)。

对这些人加以管束的危险，显然比任由火星蔓延的危险要大得多。至于开源社区的发展，在维持自身统治的面前算不上什么。如果说他们最近愿意去喊一些口号，花一点钱来“发展”开源，不过是受到帝国主义对抗的压力罢了，又关程序员们什么事情呢？他们只需要满足自己的幻想就可以了。所以 CCP 采取目前的做法对于他们自己而言肯定是最合理的做法。

既然目前开源社区的理念，出于阶级斗争的压力，已经被统治阶级认为是挑战自己地位的一种思潮，那么社区也只好采取政治的方法回应了。在矛盾已经上升到了敌我矛盾的情况下面，如果不能拿出可以使对手屈服的力量，就不要指望可以得到什么施舍。在不足以掀起这种运动的情况下面，最有效的方法当然是克服小资思想的影响，参与更加广泛的组织，联合全体被压迫的人，“完全‘没有财产的’人……同现存的有钱有教养的世界相对立”的人，也就是**工业无产阶级**的力量去行动。事实上后者[已经在自己行动](https://maps.clb.org.hk/?i18n_language=zh_CN&map=1&startDate=2022-12&endDate=2023-06&eventId=&keyword=&addressId=&parentAddressId=&address=&parentAddress=&industry=&parentIndustry=&industryName=)了，只是缺乏一个统一的组织去领导，就看有没有能人能够**建立这样的组织**了。拥有这样的力量，还有什么诉求是不能加以考虑的呢？

我很清楚自己水平的局限，所以就请公认的能人伊里奇来告诉我们[《怎么办？》](https://www.marxists.org/chinese/lenin/1901-1902/index.htm)了。

最后就用一句耳熟能详的话结尾吧：

> 全世界无产者，联合起来！
