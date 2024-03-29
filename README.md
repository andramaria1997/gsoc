Google Summer of Code
================================================

Project: ASoC codec driver
The goal of this project is to write a driver for I2S Stereo Decoder - UDA1334A

Code license: GPL
Development board: PICO-PI-IMX8M

--------------------------------------------------------------------------------

# The Sound of Code - the journey begins

Hello, World!

Since we are going to take this journey together, let’s get to know each other
better! I’m a 3rd year Romanian student pursuing a Computer Science degree,
probably just like any other student part of Google Summer of Code program.

My first interaction with open-source community was becoming a Romanian
Open-Source Education member, 7 months ago. I got involved in promoting and
organizing open-source related events and I started to feel like I’m part of
more than just an organization: a strongly connected community. The idea of
open exchange, collaborative participation and community-oriented development
makes me feel like I’m part of a huge family of which every software developer
in this world is a part of. I believe that ideas should be available to others
and shared with everyone, not held private. I believe that the process of
software developing should be brainstorming, not independent.

I found out about this program from other students at my university that
participated at past GSoC editions, so I wanted to join. Here I am today, about
to start working at a driver for a stereo decoder which, if successful, is
going to be accepted into Linux kernel ASoC maintainer’s tree.

Wish me luck!

--------------------------------------------------------------------------------

# First baby steps

Hello, World!

Thank you for coming back!

I’m going to talk about my first steps into Linux Kernel programming and how
I started to prepare myself for working on the project, considering the fact
that I’ve never done kernel programming before. The first thing to do was,
obviously, take a look at some tutorials. At my university, Operating Systems
course is split into two main courses, the first one on user space programming
and the second one on kernel space programming. So, I chose to solve a part of
the latter course’s
[`laboratories`](https://linux-kernel-labs.github.io/master/labs/introduction.html). What is more, I slowly started to read [`Linux Device Drivers – Where
kernel meets the driver`](https://www.oreilly.com/openbook/linuxdrive3/book/).

I learned to work with kernel structures, to write and compile modules and how
a driver interacts with a device through a device file. I found the way that
“content_of” macro makes the elegant kernel design of linked lists possible
really impressive. It is one of the most intelligent usage of Data Structures
I’ve ever seen. I don’t know yet how exactly this black magic sorcery works,
but be sure I’ll find out.

Also, about the non-tech part of Google Summer of Code experience, Community
Bonding period was quite pleasant. I got to know my mentor Daniel Baluta better
and thanks to him I tried Indian food for the first time. :)

See you next time! 😀

--------------------------------------------------------------------------------

# Basic booting of IMX8MQ-PICO-PI

Hello, World!

Glad to see you again!

It’s been one month since the coding period for GSoC 2019 started, so it’s time
to show the world the progress I made. First things first, the hardware came
with linux kernel version 4.9 installed, which was not the latest version, so,
too old to start to work on the driver. Therefore, the first thing to be done
was to boot linux-next kernel on it. Challenge: find a way to do it, since the
board had no SD card slot attached and I was not brave enough to overwrite
something that boots, risking to end up with nothing functional. So, what I
chose to do was to compile kernel Image locally on my machine(x86 architecture)
for imx8-mm-pico-pi (arm64 architecture) in FIT format, load it in board's RAM
memory, then boot it from there.

![images/loadimage.png](images/loadimage.png/)  

Aaand success! :D

![images/firstboot.png](images/firstboot.png/)  

I wrote a small tutorial on [`how to boot linux-next on 
imx8-mm-pico`](https://github.com/andramaria1997/gsoc/blob/master/boot-linux-next.md)
the way I did.

Ethernet and USB are functional. From now, I guess I can start working on the
driver.

--------------------------------------------------------------------------------

# Booting support is now upstream!

Hello, World!

What's new? Well, I managed to boot linux-next on the board without compiling
FIT image, load it on the board through Ethernet and then boot it. I used uuu
tool to boot through serial mode using .dtb file and kernel Image. I updated
the tutorial on how to boot linux-next on imx8mq-pico-pi (mentioned in the
previous post) accordingly.

What is more, imx8mq-pico-pi.dts file which offers support for booting
linux-next on the board, is now applied into kernel! The two patches are found here: [`.dts file`](https://git.kernel.org/pub/scm/linux/kernel/git/shawnguo/linux.git/commit/?h=for-next&id=356c27227b3b6aa824dcf11ffe632095e3cffe8a) and [`documentation`](https://git.kernel.org/pub/scm/linux/kernel/git/shawnguo/linux.git/commit/?h=for-next&id=1a47dc0240bf177878251fae10aabccbaa5a4f20).

Upstreaming process is difficult, but realisable and worth it. I will come back
soon with updates regarding the progress on working at the driver. :)

--------------------------------------------------------------------------------

# Uda1334 codec driver is now available

Hello, World!

As I promised, I came back with updates regarding the driver. I know it took
a long time to get back to you, but to make up for it the news are better than
expected: it is done!

I started from [`wm8524`](https://statics.cirrus.com/pubs/proDatasheet/WM8524_v4.1.pdf) audio codec because it is extremely similar with [`uda1334`](https://www.nxp.com/docs/en/data-sheet/UDA1334ATS.pdf)
and it is already upstreamed. From this point, I slowly started to compare the
two mentioned codecs and find differences between functionalities using their
datasheets. Step by step, now the sound of code is on. You can find the patches
[`here`](https://lkml.org/lkml/2019/7/31/381).

What was difficult: testing De-emphasis property. De-emphasis is a sound property
that is supposed to attenuate noise from sounds that fit into a given range of
frequencies. Some of my colleagues and I could hear it, but others not, so we
had a funny time trying to figure out if it is effective or not.

I attached to this repo imx8mq-pico-pi.dts file having an example of what nodes
are necesarry and how to configure them so as uda1334 codec driver would probe.
I hope it is useful :)

What is left, well, waiting for final review and results.

Until next time!

--------------------------------------------------------------------------------

# It was fun

Hello, World!

Google Summer of Code experience has come to an end. I had a great summer.
I strongly recomend gsoc program to any other student that wants a summer full
of coding and traveling at the same time, and also learn a lot of things from
Open Source Community. Eventually, continue to be a part of it! :)

What I learned? How to build linux kernel Image, about the kernel API, how to
write a device driver and how that can be embedded or configured as a loadable
module, how device tree source is used in probing necessary modules, booting
methods (FIT format using mkimage and boot the whole rootfs through serial mode
using a tftp server and uuu tool), advanced git experience, linux kernel
upstreaming process and last but not least, a little bit of sound processing.

I had great mentoring and I want to thank Daniel Baluta for this. I had a lot
to learn from him, the work with him doesn't feel stressful and any other
student that had or will have him as a mentor is very lucky. I am proud to be
one of them :D

The project is successful. All the patches are applied into asoc tree.  
Booting support:  
https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=d6de65fde51644f6ed6b1c0c05fef6a2da5ff768  
https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=1a47dc0240bf177878251fae10aabccbaa5a4f20

And the driver:  
https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=356c27227b3b6aa824dcf11ffe632095e3cffe8a  
https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=caa918ef14065b812737f3ee4ac349dcfff196e6

Thank you for following me until the end. :)
