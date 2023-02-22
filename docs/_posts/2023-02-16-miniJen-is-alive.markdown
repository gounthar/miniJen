---
layout: post
title:  "miniJen is alive!"
date:   2023-02-16 21:43:53 +0100
categories: miniJen jenkins
---

![miniJen logo](/media/image2.png){:style="display:block; margin-left:auto; margin-right:auto" height="100" width="100"}

# miniJen
The Jenkins multi-architecture CPU instance

![miniJen as a FOSDEM display on the booth](/media/fosdem_2023_booth_display.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="839"}

## What is that contraption?

Nope, it’s not a robot of some sort, it won’t move by itself.
It’s not [Cerebro](https://en.wikipedia.org/wiki/Cerebro) from Professor Xavier; no, it can’t [fly](https://all3dp.com/2/raspbery-pi-drone-simply-explained/) either.
What you’re looking at is a Jenkins “[cluster](https://www.jenkins.io/doc/book/installing/kubernetes/)” or “[instance](https://www.jenkins.io/doc/#what-is-jenkins)”.
It is composed of a [controller](https://www.jenkins.io/doc/book/using/using-agents/#using-jenkins-agents) (the “brain” or conductor) and three [agents](https://www.jenkins.io/doc/book/using/using-agents/) (the workers or musicians).

During [FOSDEM](https://fosdem.org/2023/), we displayed the `aarch64` Jenkins controller dashboard on an another computer screen using the same Wi-Fi network.


These boards are not [microcontrollers](https://en.wikipedia.org/wiki/Microcontroller), they are miniature computers running [GNU/Linux](https://en.wikipedia.org/wiki/Linux), like the infamous [Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi).

## Hardware

The controller runs on a [NanoPi R5S](https://www.friendlyelec.com/index.php?route=product/product&product_id=287), sold as a [router](https://en.wikipedia.org/wiki/Router_(computing)) (thus the three [RJ45](https://en.wikipedia.org/wiki/Modular_connector#8P8C) connectors).

![NanoPi R5S pic from the manufacturer](https://wiki.friendlyelec.com/wiki/images/8/8f/NanoPi_R5S-01B.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="500"}

It’s a 4GB [`aarch64`](https://en.wikipedia.org/wiki/AArch64) (or `armv8`) [4 cores](https://wiki.friendlyelec.com/wiki/index.php/File:Rockchip_RK3568B2_Datasheet_V1.0.pdf) running [friendlyCore](https://wiki.friendlyelec.com/wiki/index.php/FriendlyCore_(based_on_ubuntu-core_with_Qt)), a distribution from the manufacturer ([friendlyElec](https://friendlyelec.com/)) on a [5.10.x kernel](https://cdn.kernel.org/pub/linux/kernel/v5.x/ChangeLog-5.10).

The smallest board is a 4 cores [`arm32`](https://en.wikipedia.org/wiki/ARM_architecture_family#32-bit_architecture) agent with 512MB of RAM running [Armbian](https://en.wikipedia.org/wiki/Armbian) with a 5.10.x kernel too.

![NanoPi Duo2 pic from the manufacturer](https://wiki.friendlyelec.com/wiki/images/0/04/NanoPi_Duo2-2.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="500"}

It's also a board coming from the [friendlyElec](https://friendlyelec.com/) manufacturer, the [NanoPi Duo2](https://www.friendlyelec.com/index.php?route=product/product&path=69&product_id=244&sort=p.price&order=ASC).

The pink board next to the `arm32` board is a [`RISC-V`](https://en.wikipedia.org/wiki/RISC-V) board running [Armbian](https://forum.armbian.com/topic/21465-armbian-image-and-build-support-for-risc-v/) with just 1 core, 1GB of RAM and a [6.1.x kernel](https://cdn.kernel.org/pub/linux/kernel/v6.x/ChangeLog-6.1).

![MangoPi MQ-Pro pic from the manufacturer](https://mangopi.org/_media/img_0363_-2048.jpg?w=800&tok=39dc16){:style="display:block; margin-left:auto; margin-right:auto" width="500"}

It's a MangoPi [MQ-Pro](https://mangopi.org/mqpro) from [MangoPi](https://mangopi.org/), one of the first `RISC-V` boards available.

The latest board just next to the `RISC-V` board with a slightly different shade of pink is an `aarch64` board also from [MangoPi](https://mangopi.org/).

[![MangoPi MQ-Quad pic from a taobao store](http://img.alicdn.com/imgextra/i1/479269519/O1CN01kCi5J32KBkxWQCuuc_!!479269519.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="500"}](https://world.taobao.com/item/662901818090.htm)

It is a 4 cores agent with 1GB of RAM running a fork of Armbian with [kernel 5.16.x](https://cdn.kernel.org/pub/linux/kernel/v5.x/ChangeLog-5.16).
It's a [MangoPi MQ-Quad](https://mangopi.org/mqquad).

## Don't try to fool me, there are no cables between the boards!

The boards all have Wi-Fi, and they are all connected to the same Wi-Fi network, provided by a router or my phone, depending on the location.
You can spot their small Wi-Fi antennas hanging in the first pic, except for the router which has no integrated Wi-Fi (it uses a [USB Wi-Fi dongle](https://www.realtek.com/en/products/communications-network-ics/item/rtl8821cu) you can see in the pic).
One day, the R5S controller will also be a router for miniJen, but for now, it’s just a Jenkins controller.
How come the controller can contact and control the agents? We're not using IP addresses, but hostnames ending in `.local`, thanks to the [Avahi](https://en.wikipedia.org/wiki/Avahi_(software)) daemon.

## What is that big box with cables?

These boards are powered thanks to a [Pine64](https://www.pine64.org/) [power supply](https://www.pine64.org/pinepowerdesktop/) ([open-source hardware](https://en.wikipedia.org/wiki/Open-source_hardware), yes!).
Most of the time, you can see they don’t use much current ([pics, or it didn't happen!](https://www.urbandictionary.com/define.php?term=pics%20or%20it%20didn%27t%20happen)).

## 3D printed parts

![The 3DDesign on the 2nd of February 2023](/media/round-booth-display-2023-02-02-transparent.png){:style="display:block; margin-left:auto; margin-right:auto" width="839"}

The frame looks strange, I know. I wanted to use a torus because it’s a cool-looking shape, and tentacles because it’s even more cool-looking than a torus.  
It has been designed thanks to [openSCAD](https://openscad.org/), an … open-source [computer-aided design](https://en.wikipedia.org/wiki/Computer-aided_design) tool & language (yes, there is such a thing as 3D Design as code), and printed at home on a [printer](https://eryone.com/fdm/show/1.html) running an open-source firmware, [Marlin](https://marlinfw.org/).

Should you want to replicate this at home, you can find the [source code](https://github.com/MerryKombo/3DDesign/tree/MQ-Pro/assets/Booth%20Display) on my [GitHub](https://github.com/gounthar).
## Genesis and near future

I have made a few [live streams](https://www.youtube.com/@jeanquinze/streams) during the build of miniJen, and should do some more for the upcoming modifications.
I also have a few videos on the same [channel](https://www.youtube.com/@jeanquinze/featured) about Jenkins and other boards, so don't hesitate to have a look.

[![miniJen logo](/media/image1.png){:style="display:block; margin-left:auto; margin-right:auto" height="100" width="100"}](https://www.youtube.com/@jeanquinze/streams)