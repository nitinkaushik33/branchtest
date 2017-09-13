### Introduction

The C.H.I.P. by Next Thing Co contains an ARMv7 CPU, 512 MB RAM, 4 GB of internal storage, WiFi, Bluetooth, and an ARM Mali 400 graphics core. The _Alpha C.H.I.P._ by Next Thing Co contains the same specifications but 8 GB of internal storage.

The basic board doesn't have an HDMI port, but instead analog (composite) video through a 2.5mm TRRS (Tip-ring-ring-sleeve) connector, which breaks out into a familiar RCA connector, the latter with connections for composite video (yellow) as well as audio (red and black).

Since the CHIP only has a single USB port, it might be useful to have a USB hub on hand, in order to attach e.g. a mouse, a keyboard, external storage and additional devices.

The ARMv7 architecture is supported by various Linux distributions, such as Debian or Fedora, so one can run different flavors of Linux or potentially other operating systems on the CHIP. Next Thing Co also makes a flavor of Debian available under the name *CHIP Operating System*, which is what this page and their very handy [documentation](http://docs.getchip.com/) assumes.

The CHIP Operating System leaves currently approximately 3.1 GB of internal storage to the user, to be used by Processing, sketches, data etc.

### Getting started

#### TRRS-to-RCA cable

There are variants of this cable where the signals are arranged differently on the TRRS connector, so not every part, e.g. off eBay, will work. Consult the CHIP documentation for [details](http://docs.getchip.com/#about-the-trrs-connector).

#### NTSC vs PAL

The CHIP defaults to outputting a NTSC (480i) video format, which will work for most displays in North America, and many projectors that are able to handle both NTSC as well as PAL.

If you, however, require a PAL (576i) video format, it is necessary to change a setting in the so-called bootloader, which can be accomplished by connecting a cable to the Serial (UART) pins of the CHIP, and interrupting the startup process by sending a character upon boot-up. The procedure is explained in detail [here](http://docs.getchip.com/#ntsc-or-pal).

Using an old Arduino board, with the ATmega chip temporarily removed, is a thrifty alternative to buying a UART cable. Connect the Arduino's digital pin 0 (RX) to the CHIP's UART1-RX, the Arduino's digital pin 1 (TX) to the CHIP's UART1-TX, and both grounds (GND) together. (see CHIP [pinout](http://docs.getchip.com/#pin-headers))

#### Updating the CHIP

It is recommended to ensure you're running the latest version of the CHIP's software. This can be conveniently done through your web browser, by visiting [flash.getchip.com](http://flash.getchip.com/) and following the instructions there. Note that this only works using Google's Chrome browser, and will erase any of your data already stored on the CHIP's on-board memory.

If flashing doesn't succeed, you might find it necessary to use a USB 2.0 hub in between your computer and the CHIP. This, and further caveats, are documented in the [Flash CHIP With an OS](http://docs.getchip.com/chip.html#flash-chip-with-an-os) section of the documentation.

After flashing the desired image you can optionally also install individual package-level updates, which are released more regularly, by running the following in a terminal:

    sudo apt-get update
    sudo apt-get upgrade

### Download

Install Processing by running the following in a terminal:

    curl https://processing.org/download/install-arm.sh | sudo sh

### Graphics

Processing's P2D and P3D renderer can make use of the CHIP's hardware-accelerated OpenGL ES 2.0 type graphics when running version 4.4 or higher of the CHIP Operating System.

### Hardware I/O

Processing's [Hardware I/O](https://processing.org/reference/libraries/io/index.html) library works with the CHIP's peripherals.

#### GPIO

The pins XIO-P0 to XIO-P7 (see [pinout](http://docs.getchip.com/#how-you-see-gpio)) can be accessed as pins 1016 to 1023 with [digitalRead()](https://processing.org/reference/libraries/io/GPIO_digitalRead_.html), [digitalWrite()](https://processing.org/reference/libraries/io/GPIO_digitalWrite_.html) etc.

**Note**: The pin numbers (really: GPIO numbers) changed with recent kernel updates. If you're having having troubles, e.g. when using the Pocket C.H.I.P., which appears to still use an earlier operating system release, also try the following numbers for the time being: 408 to 415.

Currently it is necessary to run Processing with root privileges to access the GPIO pins. For this you need to start Processing like this in a terminal

    sudo processing

#### I2C

The CHIP has two exposed hardware I2C interfaces, TWI1 and TWI2 (see [pinout](http://docs.getchip.com/#pin-headers)). These correspond to `i2c-1` and `i2c-2`.

#### LEDs

The CHIP's LEDs currently can't be controlled from software.

#### SPI

The CHIP is [said](http://docs.getchip.com/#how-many-accessible-pins-does-chip-have) to have an SPI port, but this is currently not exposed by the CHIP Operating System.

#### PWM

The CHIP has one PWM channel, but it is currently no exposed by the CHIP Operating System.

### Serial

The Pi has one serial port, exposed as UART1-TX and UART1-RX. (see [pinout](http://docs.getchip.com/#pin-headers)) Like all other pins, these operate on 3.3V TTL levels, instead of the RS-232 voltage levels normally expected from a computer's "serial port". This port is called `/dev/ttyS0`.

In order to make use of it in Processing  it is currently necessary to give the default user `chip` permissions to do so. Run the following commands in a terminal once, and restart when done:

    sudo usermod -a -G tty chip

By default, this serial port is used as a serial terminal, allowing remote access and control of the CHIP, similar to a local terminal window. We need to disable this functionality repurpose the port with:

    sudo systemctl stop serial-getty@ttyS0.service

Or, to permanently disable this functionality:

    sudo systemctl disable serial-getty@ttyS0.service

This can later be undone by with:

    sudo systemctl enable serial-getty@ttyS0.service

### Other libraries (OpenCV, OpenKinect, Touchscreen, Video, etc)

See [General notes about running Processing on ARM](Supported-Platforms#arm-linux).

[Processing sketches optimized for the PocketCHIP](https://github.com/Lana-chan/chip-processing) by [@Lana-chan](https://github.com/Lana-chan/)