### Introduction

The DragonBoard410c by Arrow Electronics / 96Boards contains an 64-bit Cortex A53 Snapdragon 410E CPU, 1GB RAM, 8 GB of internal storage, Wifi, Bluetooth, GPS and an Adreno 306 OpenGL ES 3.0 GPU graphics core.

The DragonBoard 410c comes pre-installed with Android, however for running Processing it is necessary to install Linux instead. You can find instructions how to install the Linaro-supported Debian operating system [here](http://www.96boards.org/db410c-getting-started/Downloads/Debian.md/).

### Download

Install Processing by running the following in a terminal:

    curl https://processing.org/download/install-arm.sh | sudo sh

### Graphics

The DragonBoard410c hardware is capable of OpenGL ES 3.0 and OpenGL 2.0 type graphics. The Linaro-supported Debian operating system is making use of the free and open-source [freedreno](https://github.com/freedreno) driver for this.

![Screenshot by @xranby](http://labb.zafena.se/jogamp/aarch64/processing-3.2.3-aarch64-2016-12-12.png)

### Troubleshooting

[Thread by @xranby on 96Boards forum](https://discuss.96boards.org/t/processing-3-2-3-using-gpu-acceleration-on-dragonboard410c/1093#gsc.tab=0)