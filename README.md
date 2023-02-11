# miniJen
The Jenkins multi-architecture CPU instance 

Nope, it’s not a robot of some sort, it won’t move by itself. It’s not Cerebro from Professor Xavier; no, it can’t fly either.  
What you’re looking at is a Jenkins “cluster” or “instance”. It is composed of a controller (the “brain”) and three agents (the workers).

These boards are not microcontrollers, they are miniature computers running GNU/Linux, like the infamous Raspberry Pi.

The controller runs on a NanoPi R5S, sold as a router (thus the three RJ45 plugs).  
It’s a 4GB aarch64 (or armv8) 4 cores running friendlyCore, a distribution from the manufacturer (friendlyElec) on a 5.10.x kernel.  
The smallest board is a 4 cores arm32 agent with 512MB of RAM running Armbian with a 5.10.x kernel too.  
The pink board in front of you is a RISC-V board running Armbian with just 1 core and 1GB of RAM and a 6.10.x kernel.  
The latest board on the left is an aarch64 4 cores agent with 1GB of RAM running a fork of Armbian with kernel 5.16.x.

These boards are powered thanks to a Pine64 power supply (open-hardware, yes!), and you can see they don’t use much current. You can see Pine64’s booth in the “AW” building.

The boards are all connected thanks to WiFi supplied by a hotspot. You can spot their small WiFi antennas hanging.  
  
Our aarch64 controller supplies the Jenkins dashboard you see on the screen.

<img src="/media/image1.png" style="width:1.76563in;height:1.76563in" />

The frame looks strange, I know. I wanted to use a torus because it’s a cool-looking shape, and tentacles because it’s even more cool-looking than a torus.  
It has been designed thanks to openSCAD, an … open-source computer-aided design tool & language (yes, there is such a thing as 3D Design as code), and printed at home on a printer running an open-source firmware, Marlin.
