---
layout: post
title:  "miniJen and RISC-V"
date:   2023-02-23 21:43:53 +0100
categories: miniJen jenkins risc-v
image: assets/images/2023/02/23/fosdem_2023_booth_display.jpg
---

![miniJen logo](/media/images/2023/02/16/image2.png){:style="display:block; margin-left:auto; margin-right:auto" height="100" width="100"}

## Short introduction

What is miniJen? It's the Jenkins multi-cpu-architectures smallest instance known to this day.

![miniJen as a FOSDEM display on the booth](/media/images/2023/02/16/fosdem_2023_booth_display.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="839"}

It's composed of a 4 [arm](https://en.wikipedia.org/wiki/Arm_(company)) [Cortex-A55](https://en.wikipedia.org/wiki/ARM_Cortex-A55) cores [RockChip](https://en.wikipedia.org/wiki/Rockchip) controller ([aarch64](https://en.wikipedia.org/wiki/AArch64#ARMv8.2-A)), a 4 arm [Cortex-A7a](https://en.wikipedia.org/wiki/ARM_Cortex-A7) cores [AllWinner](https://en.wikipedia.org/wiki/Allwinner_Technology) agent ([armv7l](https://en.wikipedia.org/wiki/ARM_architecture_family#AArch32)), a 4 arm [Cortex-A53](https://en.wikipedia.org/wiki/ARM_Cortex-A53) cores AllWinner agent (aarch64), and a single [RV64GCV](https://linux-sunxi.org/D1#cite_note-riscv_extensions-4) core AllWinner agent ([`RISC-V`](https://en.wikipedia.org/wiki/RISC-V)).

## A bit of personal history

I've been an arm fanboy for years, it all started in 2014 or so when I bought a [Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi). \
At that time, it remembered me of my younger days when I used to tinker with an [HP-48SX](https://en.wikipedia.org/wiki/HP_48_series) calculator, using [assembly language](https://literature.hpcalc.org/community/hp48sx-mldl.pdf), discovering new methods, new instructions, and new backdoors every other day. \
Later on, when resin.io (now [balena.io](https://blog.balena.io/resin-io-changes-name-to-balena-releases-open-source-edition/)) ported [Docker](https://en.wikipedia.org/wiki/Docker_(software)) to the [arm processor](https://linuxgizmos.com/open-source-resinos-adds-docker-to-armlinux-boards/), I then became obsessed with arm and docker. 

![Docker on arm](/media/images/2023/02/23/docker-on-arm.png){:style="display:block; margin-left:auto; margin-right:auto" width="839"}

I spent way too much time compiling FOSS for `arm32` and `aarch64`, and building docker images around them.
It was fun, it was exploratory, it was a way to learn new things... and it was a way to contribute to the FOSS community.
I made a lot of friends, and I gained a lot of knowledge. \
I sometimes had to recompile gcc with ... gcc in order to be able to recompile ffmpeg for example, and one thing leading to another, I had to recompile a library, then another, then a utility, then another library, then the kernel, then another library...
Boy, that was fun! \
These were good times. I may sound nostalgic, and I think I am.
It was hard, but you got immediate or delayed benefits because then everybody was benefiting from the community work.
Be it for energy saving, IoT, Edge Computing, server rooms, Cloud, or just for fun, arm was bound to be everywhere.
It was the future. 

Colleagues (who happen to be also friends, go figure) used to call me "_mister WhatIf_". Yes, I had way too many ideas, but if you want to find one of these days a good idea, you have to let tons of ideas, good or bad, make their way into the world. \
So yes, basically, I was spending most of my free time asking myself (and friends) "_What if...?_".
These "_What if...?_" lead most of the time to an implementation on an arm SBC, because they were cheap and available at that time. \
Some of these experiments were successful, and some were not (frankly, hosting a complete Gitlab server on a Raspberry Pi 3B was stupid), but I learned a lot from them.

Back to arm: when the future becomes the present, it's not that exciting anymore.
Arm is not yet as [boring](https://twitter.com/jonmasters/status/1523041597683683328) as X86, but most of the software now works on arm, from microcontrollers to the Cloud, and the very last conquest to be made ([laptops](https://arstechnica.com/gadgets/2022/02/lenovo-announces-the-first-arm-based-thinkpad/) and even [MacBook](https://www.apple.com/macbook-air-m2/)) has been won. \
If you don't own any arm hardware, nothing can stop you from developing for this architecture anymore thanks to [QEMU](https://www.qemu.org/docs/master/system/target-arm.html) and [Docker](https://docs.docker.com/build/building/multi-platform/). \
It's not that hard to compile the software for arm anymore.
It's not that exciting anymore.
It's not that fun anymore.
It's not that exploratory anymore.
It's not that rewarding anymore.
It's not that challenging anymore.
It's not that cool anymore.
It's not that sexy anymore.
It's not that... well, you get the point. \
I still love the arm ecosystem and all the people I've met, but it feels like the honeymoon time is gone, we're in a more platonic relationship now. It is stable, deep, and true, (I love the [arm community](https://www.arm.com/resources/developer-program)!) but the time has come to find another quest.

## The `RISC-V` quest

I've been lurking on the [`RISC-V`](https://en.wikipedia.org/wiki/RISC-V) community, projects, SoCs, SBCs, and vendors for a while now, and I've been following the [RISC-V Foundation](https://riscv.org/) for quite some time. \
But until recently, I didn't have any `RISC-V` hardware to play with, and I was not seeing myself buying a very expensive but lame `RISC-V` SBC without any project in mind. \
I was waiting for the right moment and the right project. \
I've been working with Jenkins since April 2022, and of course, my love of arm being what it is, my first contributions were about `arm32` and `aarch64` for the Jenkins project. \
I spotted during the 2022 summer an interesting `RISC-V` board called the [MQ-PRO](https://mangopi.org/mangopi_mqpro) from an unknown (to me) manufacturer called MangoPi. \
The price was right, and the specs were not that good, but the board was available. \
At that time, the software support was not that good, but I was not afraid of that (because of my personal history with arm). I did not buy it though, because I was not sure if I would have the time to work on it. \
At the beginning of September 2022, the amazing Michael Hurt organized a giveaway on his [Twitter account](https://twitter.com/Mingusdude).

![Michael Hurt Giveaway](/media/images/2023/02/23/giveaway.png)

I won the board thanks to [my proposal](https://twitter.com/Mingusdude/status/1565887135785312256) linked to Jenkins.

![poddingue's proposal](/media/images/2023/02/23/proposal.png)

At that time, I had no clear idea if [Java](https://builds.shipilev.net/openjdk-jdk-riscv/) would run on `RISC-V` (and of course no clue if Jenkins would run on top of that), and I also knew [Docker](https://carlosedp.medium.com/docker-containers-on-risc-v-architecture-5bc45725624b) was not yet officially available for RISC-V. \
That sounded way too fun not to try... especially since the board was basically free. \
I then felt the same level of excitement I used to feel when I was working on `arm32` and `aarch64`. \
Yes, this was once again possible, new territories to explore, new challenges to face, new friends to make, new knowledge to gain. 

![MQ-Pro Unboxing](https://youtu.be/qdHSuClqtic?width=720) 

## The `RISC-V` journey

### Prerequisites and first steps

I had seen in the [news](https://twitter.com/bretweber/status/1559631172623278081) that Ubuntu 22.04 was supplying a `RISC-V` image that could work for this board (designed for the [AllWinner Nezha](https://linux-sunxi.org/Allwinner_Nezha)). The Nezha was the first [D1](https://linux-sunxi.org/D1)-based board made available to the public. The MangoPi MQ-Pro came after that, but shares more or less the same set of components. \
As strange as it may seem (a `RISC-V` build by an `Arm`bian contributor), I also found an [image](https://forum.armbian.com/topic/21465-armbian-image-and-build-support-for-risc-v/) built by a regular contributor of Armbian, [balbes150](https://forum.armbian.com/profile/1215-balbes150/). I started by downloading [`Armbian_22.08.0-trunk_Nezha_jammy_current_6.1.0_xfce_desktop.img`](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=333) from December 06, 2002, burnt it thanks to [Balena Etcher](https://www.balena.io/etcher) and was able to [boot](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=663) the board. \
[bret.dk](https://twitter.com/bretweber) gave me an interesting pointer to [James A. Chambers](https://jamesachambers.com/) [blog post](https://jamesachambers.com/mangopi-mq-pro-d1-ubuntu-preview/) about the Ubuntu Preview for RISC-V. \
In the blog post from James A. Chambers, there is a paragraph about OpenJDK Availability for RISC-V, and we can see that there is a wide range of openJDK versions (from 11 to 20) available in here. 
That was unexpected, I thought I would have to compile everything from scratch, make changes to the build system, and so on.

![MangoPi MQ-Pro pic from the manufacturer](/media/images/2023/02/23/mq-pro.png){:style="display:block; margin-left:auto; margin-right:auto" width="500"}

As you can see, the board is very minimalistic, we only have two USB-C ports (one being used for power), a microSD card slot, and a mini HDMI port. \
My goal was to get this board on the Wi-Fi network, but how to do that without any Ethernet port? \
Most of the time when I use Armbian, I just plug an Ethernet cable, and I'm good to go, as the board uses DHCP by default. \
I just have to search for a new machine appearing on the router webpage, and issue an `ssh` command to connect to it. \
This time, I was kind of stuck. \
I had no USB-C keyboard, no mini-HDMI cable, and no Ethernet plug to use. \
What was I to do? \
Once again, bret.dk came to the rescue. \
Bret does tons of reviews on [his blog](https://bret.dk/) and I found [one](https://bret.dk/waveshare-raspberry-pi-usb-ethernet-hat-review/) about a Ethernet/USB hat for the Raspberry Pi Zero W. \
I bought the same hat, a USB-C hub just in case, and a mini-HDMI cable. \
The hat never worked for me for some reason, but the USB-C hub did.
It's an almost-no-name [generic hub](https://www.amazon.fr/gp/product/B08GM2H1Q2), but it worked.
I managed to get Ethernet on it, so that my board got an IP address from my router.

### Linux and Java installation

#### Linux

I could then [log in](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=969) thanks to `ssh`, create a admin user, and so on. \
I then [removed](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=1239) packages linked to `X11` that I don't need for my use case. \
Later on, I [configured](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=2111) a Wi-Fi connection, and [created](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=2220) a `jenkins` user. \
Next step was logically to [install](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=2391) the default openJDK 17 build provided by Ubuntu.

#### Java

I now know default openJDK 17 build is a Zero VM build, so I also [installed](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=2551) a nightly build of Temurin's openJDK [20](https://github.com/adoptium/temurin20-binaries/releases) and [19](https://github.com/adoptium/temurin19-binaries/releases). \
By the way, do you know what [Temurin](https://twitter.com/adoptium/status/1435519863091564547) is?
> Temurin is both a chemical similar to caffeine, and an anagram of "runtime". Oh, and a cool new free to use Java runtime from the Eclipse Foundation! Enjoy.

![Temurin is almost caffeine](/media/images/2023/02/23/temurin.png){:style="display:block; margin-left:auto; margin-right:auto" width="500"}

##### Zero VM

You may wonder what is a Zero VM build, and why I want to use something else. \
Zero VM builds come with pros and cons.
 * Zero VM is a Java Virtual Machine implementation that is designed to execute Java applications on systems that use architectures other than the x86 architecture. It is specifically _optimized_ for systems that use ARM, PowerPC, and other non-x86 architectures.
 * [Zero VM](https://openjdk.org/projects/zero/) is part of the [OpenJDK project](https://openjdk.org/), which is an open-source implementation of the Java SE platform. Zero VM uses a technique called "interpreter-only" mode, which allows it to run on platforms that do not support just-in-time (JIT) compilation. 
 * In interpreter-only mode, Zero VM executes Java bytecode directly, without compiling it to native code (it does not use any assembler). This approach typically results in slower performance compared to [JIT](https://developers.redhat.com/articles/2021/06/23/how-jit-compiler-boosts-java-performance-openjdk)-enabled VMs, but it has the advantage of being able to run on a wider range of platforms. That's why the developers got a working openJDK build _this early_ for RISC-V.

So, as much as I'm grateful for the Zero VM build, I'm also curious to see how Temurin's builds perform on this board.
Said in another way, the board is already so slow that using a Zero VM will make it unusable.
There, I said it. \
The default openJDK implementation is there just in case I need to use it for some reason, but I plan to only use Temurin's builds.

##### openJDK 19

As you may already know, JDK19 is almost [end of life](https://endoflife.date/java) (21st of March 2023), so I'm not going to use it for long, and Temurin does not provide steady `RISC-V` nightly builds. \
Speaking of end-of-life, I could not recommend enough [endoflife.date](https://endoflife.date/) which is an [open-source](https://github.com/endoflife-date/endoflife.date) project that aims to provide a simple way to find the end-of-life dates of software and operating systems.
It even provides an [API](https://endoflife.date/docs/api) to query the data.
Thanks a lot to [Mark Waite](https://www.jenkins.io/blog/authors/markewaite/) for letting me know about this project. \
Back to openJDK19, how did I find the last `RISC-V` published nightly build? \
While discussing with [Stewart Addison](https://twitter.com/sxaTech) on various GitHub issues related to Temurin on`RISC-V` (and `aarch64`) and later on through Temurin's [Slack channel](https://adoptium.net/slack/), we sympathized.
He mentioned that he had the same board as me, and gave me a link to the [latest`RISC-V` build](https://ci.adoptopenjdk.net/job/build-scripts/job/jobs/job/jdk19u/job/jdk19u-linux-riscv64-temurin/14/) he could find. \
So, that's the version [I'm using](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=2565) for now. \
Please note that your libc should be at least [`2.35`](https://sourceware.org/pipermail/libc-alpha/2022-February/136040.html) for this build to work. 

### The `RISC-V` Jenkins agent

#### Installation

I then [added an `ssh` key](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=3174) on the `RISC-V` machine that would become an agent, [created](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=3125) a new node within the Jenkins UI, and installed the [agent](https://www.youtube.com/watch?v=4KghHJEz5no&t=115s) on it. 

#### Testing

The last thing to do before asserting Jenkins works on `RISC-V` was to launch a [simple `RISC-V` job](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=3383). \
Spoiler alert, it did work! \
The next stop was to install a [Pipeline](https://www.jenkins.io/doc/book/pipeline/) that [downloads](https://github.com/gounthar/jenkins-temurin-riscv/blob/main/Jenkinsfile#L7) the latest [nightly build of Temurin openJDK20](https://github.com/adoptium/temurin20-binaries/tree/6855a34aca01a3368b3feaf138784ea3a4c08c99) and installs it on the `RISC-V` machine, overriding the one I installed earlier. \
This is done mostly thanks to the [`gh` command line tool](https://github.com/cli/cli) that can do wonders when it comes to interacting with GitHub on the command line.

`gh` is open-source, and it's available even for `RISC-V`, but not directly in the [`gh` GItHub releases](https://github.com/cli/cli/releases).
As far as I know, `go` is [not yet officially available](https://go.dev/dl/) for `RISC-V`, and `gh` is written in `go`. \
So... What's the catch? \
Well, it's open-source, and Ubuntu has a [source package](https://packages.ubuntu.com/source/lunar/gh) for it. \
Even if I can't see the binary package for `RISC-V` on the [Ubuntu package page](https://packages.ubuntu.com/lunar/gh), it magically appeared on my machine after a  `apt install gh`. 

The Pipeline uses openJDK19 to update openJDK20, and openJDK20 to update openJDK19. The main Jenkins process is still running on the Zero VM openJDK17. That's something I'll have to address later on. \
That part worked, I was pretty happy about the result. \
But what about a smoke test? \
I mean, I'm not going to use Jenkins on `RISC-V` if I can't build a real-life project with it, right? \
I asked in the community, and [Mark Waite](https://www.jenkins.io/blog/authors/markewaite/), [Basil Crow](https://www.jenkins.io/blog/authors/basil/) and [Damien Duportal](https://www.jenkins.io/blog/authors/dduportal/) all agreed that the best way to test Jenkins on `RISC-V` was to build a few Jenkins plugins with it. \
I started with an ambitious project, the [git plugin](https://plugins.jenkins.io/git/) itself.
Well, it was quite big and not ready for openJDK19, so I switched to a smaller one, the [git client plugin](https://plugins.jenkins.io/git-client/). 
Same player, play again. It did not go well either. \
I then switched to a very basic one, the [infrastructure test plugin](https://plugins.jenkins.io/jenkins-infra-test/), which is used to test the Jenkins infrastructure as its name implies. 
Bad luck once again, as it was not ready for openJDK19 either. \
In desperation, I switched to the [Platform Labeler](https://plugins.jenkins.io/platformlabeler/) which is ready for openJDK17, but... it required way too much memory to be built. \
Bummer! \
There, I was stuck. \
To this day, I haven't found a Jenkins plugin that can be built with openJDK19 on `RISC-V` with very little memory. \
I have yet to find another kind of smoke test that would prove Jenkins works on `RISC-V`... or wait until a plugin is ready for openJDK19.

## The `RISC-V` future for Jenkins

### Back to the future

When it comes to Jenkins and the `RISC-V` ecosystem, I swear I thought I was some kind of pioneer, like in the good old days of arm. \
Guess what, I'm not! \
I've finally done my homework, and found out that Jenkins has been running on `RISC-V` for a while now. 

* In a [blog post from May 2021](https://riscv.org/2021/05/risc-v-foundation-demonstrates-jenkins-on-risc-v-at-lfelc-spring-2021-virtual-summit/) (which has unfortunately disappeared), the [`RISC-V` Foundation](https://riscv.org/) demonstrated Jenkins running on a `RISC-V`  board with a Linux operating system. The demo used the OpenSBI bootloader and the OpenJDK `RISC-V`  Port to run Jenkins, and was able to successfully build and test a simple Java application. The post includes detailed instructions for setting up Jenkins on `RISC-V`  and running a build job.
* In a [video of the presentation](https://www.youtube.com/watch?v=Bb07GswNYxM) (which has unfortunately disappeared) given at the LFELC Spring 2021 Virtual Summit, we could see a demonstration of Jenkins running on `RISC-V`. The presentation was given by [Anup Patel](https://www.linkedin.com/in/anup-v-patel/?originalSubdomain=in), who was at that time amember of the `RISC-V` Technical Steering Committee. 
* There is [another video](https://www.youtube.com/watch?v=6GQw6N0HmZQ) (which has unfortunately disappeared) that shows Jenkins running on `RISC-V`, presented by [Keith Packard](https://en.wikipedia.org/wiki/Keith_Packard) at the `RISC-V` Workshop Taiwan 2021. The video shows Jenkins running on a [HiFive Unmatched](https://www.sifive.com/boards/hifive-unmatched) development board, which is based on the SiFive Freedom U740 `RISC-V` processor.
* In a [Reddit thread from January 2021](https://www.reddit.com/r/RISCV/comments/l8jl0a/jenkins_running_on_hifive_unmatched/) (which has unfortunately disappeared), a user reported running Jenkins on a HiFive Unmatched `RISC-V`  board using Ubuntu 20.04 and OpenJDK 11. The user reported that Jenkins worked well on the `RISC-V` board and was able to run build jobs without any issues.

Why have these experiments proofs been removed? Is that a coincidence or am I acting undercover to remove any evidence of Jenkins running on `RISC-V` before I attempt to do the same? \
Just kidding, I have no idea, but if three years ago some people were able to run Jenkins on `RISC-V`, I should be able to do the same today.

### When will `RISC-V` be a first-class citizen with Jenkins?

Remember, Jenkins is an open-source project, but above all, it's a community project. \
Who am I to tell you when `RISC-V` will be a first-class citizen with Jenkins? \
I'm just a guy who's trying to make it work. \
I think it's up to the community to decide when `RISC-V` will be officially supported by Jenkins. My guess would be when two major conditions are met:
* Temurin is officially available for `RISC-V`, which means we'll be able to download a binary package for `RISC-V` from the [official AdoptOpenJDK website](https://adoptium.net/temurin/releases/).
![Temurin supported architectures](/media/images/2023/02/23/temurin-supported-architectures.png){:style="display:block; margin-left:auto; margin-right:auto" width="839"}
* Docker is officially available for `RISC-V`, which means we'll be able to download a binary package for `RISC-V` from the [official Docker website](https://hub.docker.com/search?q=&type=image&image_filter=official).
![Docker supported architectures](/media/images/2023/02/23/docker-supported-architectures.png){:style="display:block; margin-left:auto; margin-right:auto" width="839"}

You may wonder, why do I need Temurin and Docker to be officially available for `RISC-V` before saying Jenkins [supports](https://www.jenkins.io/sigs/platform/) `RISC-V`? \
As you know, the Java motto says:
>  "Write once, run anywhere"

It's often abbreviated as "WORA". This motto reflects Java's ability to be compiled into bytecode that can run on any platform with a Java Virtual Machine (JVM), without requiring recompilation for each specific platform. The Jenkins war runs on top of the JVM; it is then considered CPU-architecture agnostic, which means it can run on any CPU architecture (as long as openJDK11+ can run on the machine, but take it with a grain of salt). \
The Jenkins infrastructure owns (or borrows) machines of the supported CPU architectures, and runs the war on them, so we can testify Jenkins works on these architectures. \
Jenkins also supplies [Docker images](https://hub.docker.com/r/jenkins/jenkins) for the supported CPU architectures, and tests them on the supported CPU architectures. \
Jenkins does not own any `RISC-V` machine, as far as I know.
We could provide a `RISC-V` docker image, as `docker buildx` allows us to build for various CPU architectures, but... Wouldn't it be kind of hasty?
We wouldn't be able to test on a Jenkins-owned, Jenkins-managed machine on a regular basis. \
It is then urgent to ... wait.