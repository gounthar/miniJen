---  
layout: post      
title:  "miniJen live streams"      
date:   2023-03-09 11:43:53 +0100      
categories: miniJen jenkins live-streams      
image: assets/images/2023/02/23/fosdem_2023_booth_display.jpg
---   
![miniJen logo](/media/images/2023/02/16/image2.png){:style="display:block; margin-left:auto; margin-right:auto" height="100" width="100"}

## Short Introduction

What is miniJen? It's the Jenkins multi-cpu-architectures smallest instance known to this day.

![miniJen as a FOSDEM display on the booth](/media/images/2023/02/16/fosdem_2023_booth_display.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="839"}

It's composed of a 4 [arm](https://en.wikipedia.org/wiki/Arm_(company)) [Cortex-A55](https://en.wikipedia.org/wiki/ARM_Cortex-A55) cores [RockChip](https://en.wikipedia.org/wiki/Rockchip) controller ([aarch64](https://en.wikipedia.org/wiki/AArch64#ARMv8.2-A)), a 4 arm [Cortex-A7a](https://en.wikipedia.org/wiki/ARM_Cortex-A7) cores [AllWinner](https://en.wikipedia.org/wiki/Allwinner_Technology) agent ([`armv7l`](https://en.wikipedia.org/wiki/ARM_architecture_family#AArch32)), a 4 arm [Cortex-A53](https://en.wikipedia.org/wiki/ARM_Cortex-A53) cores AllWinner agent (`aarch64`), and a single [RV64GCV](https://linux-sunxi.org/D1#cite_note-riscv_extensions-4) core AllWinner agent ([`RISC-V`](https://en.wikipedia.org/wiki/RISC-V)).

## Live streams

From the idea to the real thing, it took me a few months.   
During this period, I made a few [live streams](https://www.youtube.com/@jeanquinze/streams) on my [Jean Quinze YouTube channel](https://www.youtube.com/@jeanquinze/featured), one [unboxing video](https://www.youtube.com/watch?v=qdHSuClqtic&t=14s) related to the project, and the same live streams were running on my [Twitch channel](https://www.twitch.tv/poddingue) too.

I started with [an unboxing video](https://www.youtube.com/watch?v=yRGtqB0-iHY&t=1420s) of the boards I chose ([MangoPi MQ-Pro](https://mangopi.org/mangopi_mqpro), [MangoPi MQ-Quad](https://mangopi.org/mqquad), [FriendlyElec R5S](https://wiki.friendlyelec.com/wiki/index.php/NanoPi_R5S), and [FriendlyElec Duo2](https://wiki.friendlyelec.com/wiki/index.php/NanoPi_Duo2)) to create a multi-arch Jenkins cluster/instance for [FOSDEM](https://hackaday.com/2023/03/01/fosdem-2023-an-open-source-conference-literally/).

<iframe width="560" height="315" src="https://www.youtube.com/embed/yRGtqB0-iHY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

I also [showed the round displays](https://www.youtube.com/live/yRGtqB0-iHY?feature=share&t=278) I thought about using to display the Jenkins dashboard.  
Then I also [showed](https://www.youtube.com/live/yRGtqB0-iHY?feature=share&t=907) my first try at building harnesses for the boards.

In the next live stream, I talked about my [attempts](https://www.youtube.com/live/872Th2E-bRo?feature=share&t=371) at designing a 3D structure to hold the boards and the displays thanks to [OpenSCAD](https://openscad.org/), and the printed [result](https://www.youtube.com/live/872Th2E-bRo?feature=share&t=464).

<iframe width="560" height="315" src="https://www.youtube.com/embed/872Th2E-bRo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

I also [unboxed](https://www.youtube.com/live/872Th2E-bRo?feature=share&t=1086) my Vision Five2 `risc-v` board which I won't use for this project, and my [Radxa Zero](https://www.youtube.com/live/872Th2E-bRo?feature=share&t=1395) that I will use for another project.

In the [following video](https://www.youtube.com/watch?v=Sw3By1sY2xw), I showed a few more parts I printed ([like the feet](https://www.youtube.com/live/Sw3By1sY2xw?feature=share&t=298)) and screwed a few boards on the first torus.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Sw3By1sY2xw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

I also talked about the [use of inserts](https://www.youtube.com/live/Sw3By1sY2xw?feature=share&t=638) instead of directly tapping the [PLA](https://en.wikipedia.org/wiki/Polylactic_acid).  
I then spent some time on the [3D design](https://www.youtube.com/live/Sw3By1sY2xw?feature=share&t=815) of miniJen thanks to [OpenSCAD](https://en.wikipedia.org/wiki/OpenSCAD).  
I then [unboxed](https://www.youtube.com/live/Sw3By1sY2xw?feature=share&t=939) my [Pine64](https://www.pine64.org/) [PinePower](https://www.pine64.org/pinepowerdesktop/) that will help power up those four SBCs.  
I then [installed armbian](https://www.youtube.com/live/Sw3By1sY2xw?feature=share&t=1464) on the `risc-v` board.

In the [next video](https://www.youtube.com/watch?v=xtI1nwwe70A&t=670s), I [reinstalled](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=324) Linux on the MangoPi MQ-Pro board, [OpenJDK17](https://en.wikipedia.org/wiki/OpenJDK), [Temurin](https://en.wikipedia.org/wiki/Adoptium) OpenJDK19 and 20, and [installed a Jenkins agent](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=2220) on it.

<iframe width="560" height="315" src="https://www.youtube.com/embed/xtI1nwwe70A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Later on, I [connected it](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=3147) to the controller. To finish, I ran a very simple [first `risc-v` job](https://www.youtube.com/live/xtI1nwwe70A?feature=share&t=3524).


In the [next video](https://www.youtube.com/watch?v=hgVVU3qJHIE&t=8s), I installed another torus on miniJen, and later on [installed Linux](https://www.youtube.com/live/hgVVU3qJHIE?feature=share&t=1234) and a Jenkins controller on the FriendlyElec R5s.

<iframe width="560" height="315" src="https://www.youtube.com/embed/hgVVU3qJHIE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

I started by [installing OpenJDK17](https://www.youtube.com/live/hgVVU3qJHIE?feature=share&t=1749), then a [weekly release](https://www.youtube.com/live/hgVVU3qJHIE?feature=share&t=1884) of Jenkins.

In the [last video](https://www.youtube.com/watch?v=biLgBwrNzsQ) to this day, just before FOSDEM, I showed that the [3d-printing](https://www.youtube.com/live/biLgBwrNzsQ?feature=share&t=198) part was mostly over.

<iframe width="560" height="315" src="https://www.youtube.com/embed/biLgBwrNzsQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

I [imported jobs](https://www.youtube.com/live/biLgBwrNzsQ?feature=share&t=513) from another Jenkins controller.  
I said a word about the Pine64 PinePower, the MangoPi boards, and the FriendlyElec boards.

I also detailed the various SBCs I use (`aarch64`, `armv7`, `risc-v` ).  
I then [installed](https://www.youtube.com/live/biLgBwrNzsQ?feature=share&t=706) what was missing on each board to get a Jenkins agent working (java, ...), [linked](https://www.youtube.com/live/biLgBwrNzsQ?feature=share&t=1514) the boards altogether within Jenkins, and then got them to execute their [first job](https://www.youtube.com/live/biLgBwrNzsQ?feature=share&t=1779).   
[In the end](https://www.youtube.com/live/biLgBwrNzsQ?feature=share&t=2882), I had a working Jenkins controller and 3 Jenkins agents, all running on different CPU architectures, all of that ready for FOSDEM.