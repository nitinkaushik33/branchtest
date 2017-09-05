### Introduction

The (original) **Raspberry Pi** contained an ARMv6 CPU, 256 or 512 MB RAM. The **Raspberry Pi 2** contains a quad-core ARMv7 CPU, 1 GB of RAM. The **Raspberry Pi 3** contains a quad-core ARMv8 (64-bit) CPU, which can also be operated in an ARMv7 compatible mode. It contains the same 1 GB of RAM. The **Raspberry Pi Zero** and **Raspberry Pi Zero W** feature the same ARMv6 CPU as the original Raspberry Pi, and 512 MB RAM. They all contain the same Broadcom VideoCore IV graphics processor.

All models primarily run a modified version of the Debian Linux distribution named [Raspbian](http://www.raspbian.org/) that was made to run on the ARMv6 CPU (and higher).

On the Pi 2 and 3 it is also possible to run other, unmodified Linux distributions, such as Debian or Fedora, since those settled on the ARMv7 architecture as their "baseline" for modern ARM support. Yet on those distributions you might not have the necessary kernel modules and graphics library to make full use of the Pi's peripherals. This page thus specifically talks about running Processing on Raspbian. (see also: [General notes about running Processing on ARM](Supported-Platforms#arm-linux))

The Pi 3 is currently used in an ARMv7 compatible mode by the Raspbian distribution, and we very much recommend this configuration for the time being. Starting with version 3.3.1, Processing can however as well be run on dedicated 64-bit operating systems - those might be labeled "arm64" or "aarch64". The general caveat relating running other, unmodified Linux distributions applies here as well. (_[Found an issue with our arm64 build?](https://github.com/processing/processing/issues/new?labels=arm64&assignee=gohai)_)

### Download

You can download a full Raspbian image with Processing pre-installed [**here**](https://github.com/processing/processing/releases/download/processing-0262-3.3.5/processing-3.3.5-linux-raspbian.zip). This image is based on Processing 3.3.5 and Raspbian release *August 2017*, and works on all versions of the Pi.

**Important**: Since the image contained in the ZIP file is larger than 4 GB it is necessary to use extraction utilities that can handle large files, such as [The Unarchiver](http://unarchiver.c3.cx/unarchiver) on OS X. (Try this if extracting yields a file with CPGZ extension.)

See the *Writing an image to the SD card* section on [this page](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) for how to transfer the contents of the extracted IMG file onto a microSD card. This differs depending on the operating system you are using.

*Alternatively*, if you already have an existing installation of Raspbian you want to keep, you can install Processing by running the following in a terminal:

    curl https://processing.org/download/install-arm.sh | sudo sh

### Graphics

The Pi's graphics core exposes OpenGL ES 2.0, which is supported by Processing P2D and P3D renderer, thanks to specific enablement in the underlying library, JOGL. The graphics driver are built around a closed-source driver (found in `/opt/vc`), which limits our ability to troubleshoot bugs for the moment.

Due to a limitation of this driver, P3D is currently limited to using 2 lights.

Certain sketches might run out of video memory and throw an exception mentioning `GL_OUT_OF_MEMORY`. You might be able to work around this by changing the *memory split* - the amount of memory allocated for the GPU from all system memory. To do so, open the **Raspberry Pi Configuration** (under *Menu*, *Preferences*), navigate to the *Performance* tab, change the amount of "GPU memory" and then restart your Pi.

Since a couple of releases Raspbian also includes an experimental, open source [OpenGL driver](https://dri.freedesktop.org/wiki/VC4/) for the Pi 2 & 3. This driver is still in development, but might be worth trying out when experiencing issues with the default one. To enable or disable the driver, run `sudo raspi-config` and select the *GL Driver* option under *Advanced Options*. Note that the new driver currently lacks some features of the existing one, such as the ability to drive screens attached to the DSI interface, support for camera modules or hardware-enabled video decoding.

### Hardware I/O

Processing has a new [Hardware I/O](https://processing.org/reference/libraries/io/index.html) library that was extensively tested with the Pi.

#### GPIO

There is no special configuration necessary to use the digital pins with [digitalRead()](https://processing.org/reference/libraries/io/GPIO_digitalRead_.html), [digitalWrite()](https://processing.org/reference/libraries/io/GPIO_digitalWrite_.html) etc.

Keep in mind that the Pi uses **3.3V level**, rather then the 5V of the Arduino Uno. The pins are said not to be 5V tolerant, so make sure to keep your voltages to 3.3V.

Each pin is rated up to **16 mA per pin**, with **50 mA total**, across all pins. (The Arduino UNO is 20 mA @ 5V per pin.) Make sure not to draw more current.

The Hardware I/O library's [GPIO](https://processing.org/reference/libraries/io/GPIO.html) class uses GPIO numbers with its methods. Those are not the same as the physical pin numbers of the pin header. (see [pinout](https://pi.gadgetoid.com/pinout))

#### I2C

The Pi has one (publicly exposed) hardware I2C interface. To use it in Processing (with the [I2C](https://processing.org/reference/libraries/io/I2C.html) class in processing.io), open the **Raspberry Pi Configuration** (under *Menu*, *Preferences*), navigate to the *Interfaces* tab, enable I2C and then restart your Pi.

After restarting, [I2C.list()](https://processing.org/reference/libraries/io/I2C_list_.html) should return one interface: e.g. `i2c-1` on the Pi 2. The interface is located on pins 3 (SDA) and 5 (SCL) on the Pi's header. (see [pinout](https://pi.gadgetoid.com/pinout)) Ground is conveniently located right next to it, on pin 6. Use it together with the 3.3V supply on pin 1, since that is the level that the Pi expects.

#### LEDs

The Pi has two on-board LEDs, `led0` and `led1`, which can be controlled through the [LED](https://processing.org/reference/libraries/io/LED.html) class in Processing.

Since the regular user (named `pi`) is by default not permitted to write to the LED device, you must enable this **once** by running

    sudo sed -i 's|exit 0|chmod -R a+rw /sys/class/leds/*\nexit 0|' /etc/rc.local

After a restart, the devices should be read- and writable by any user. (This can be confirmed by running `ls -l /sys/class/leds/led0/brightness`. The resulting line should start with `-rw-rw-rw-`.)

On the Pi, `led0` is the green (I/O activity) light, while `led1` is the red (power) light. They only can be turned on and off, so [brightness()](https://processing.org/reference/libraries/io/LED_brightness_.html) values besides 0.0 and 1.0 have no effect.

#### SPI

The Pi two hardware SPI interfaces, but which share all but the SS (*Slave Select*) pins. To use it in Processing (with the [SPI](https://processing.org/reference/libraries/io/SPI.html) class in processing.io), open the **Raspberry Pi Configuration** (under *Menu*, *Preferences*), navigate to the *Interfaces* tab, enable SPI and then restart your Pi.

After restarting, [SPI.list()](https://processing.org/reference/libraries/io/I2C_list_.html) should return two interfaces `spidev0.0` and `spidev0.1`.

The interfaces' pins are located on the Pi's header on pins 19 (MOSI), 21 (MISO), 23 (SCLK), 24 (SS, aka CE0) and 26 (SS, aka CE1). (see [pinout](https://pi.gadgetoid.com/pinout)) When using `spidev0.0`, pin 24 (CE0) is being pulled low during a transaction, while pin26 (CE1) remains unchanged. When using `spidev0.1`, pin 26 (CE1) is being pulled low, while pin24 (CE0) remains unchanged. (This is to be able to address two devices on the same data & clock lines.)

#### Servo motors

Using the Hardware I/O library's [SoftwareServo](https://processing.org/reference/libraries/io/SoftwareServo.html) class, any pin can be used to control standard RC servo motors.

It is recommended to power the motors from an external power source, as shown in [this wiring diagram](https://github.com/processing/processing/blob/master/java/libraries/io/examples/ServoSweep/setup_better.png). See the [ServoSweep](https://github.com/processing/processing/tree/master/java/libraries/io/examples/ServoSweep) example for more information.

### Upload to Pi tool

The [Upload to Pi](https://github.com/gohai/processing-uploadtopi) Processing tool automatically uploads sketches to attached Raspberry Pi devices and executes them there. (also available from the Contribution Manager)

See the [Readme](https://github.com/gohai/processing-uploadtopi/blob/master/README.md) file for all features and configuration options. Please file issues [here](https://github.com/gohai/processing-uploadtopi/issues/new).

### Serial

The Pi has one exposed serial port, on pins 8 (TXD) and 10 (RXD). (see [pinout](https://pi.gadgetoid.com/pinout)) Like all other pins, these operate on 3.3V TTL levels, instead of the RS-232 voltage levels normally expected from a computer's "serial port".

To enable the serial port device to be used with Processing, start the text-based Raspberry Pi Configuration tool by executing the following command in a terminal:

    sudo raspi-config

With the arrow-keys and Enter, navigate to *Interfacing Options*, *Serial*. In the dialog that appears, answer *No* to the question whether or not to use the port for a login shell. Answer *Yes* to the question whether the serial port hardware should be enabled. Reboot the Raspberry Pi for the changes to have effect.

On all Raspberry Pis that don't have Bluetooth: The serial port will be available to Processing's [Serial](https://processing.org/reference/libraries/serial/index.html) library under the name `/dev/ttyAMA0`.

On all Raspberry Pi devices that do have Bluetooth, such as the Pi 3 and the Pi Zero W: The serial port will be available to Processing's [Serial](https://processing.org/reference/libraries/serial/index.html) library under the name `/dev/ttyS0`. (On those boards, the high-speed `/dev/ttyAMA0` device is used internally for the Bluetooth functionality.)

### Touchscreen

The [simpletouch library](https://github.com/gohai/processing-simpletouch/releases/download/latest/processing-simpletouch.zip) makes it possible to use any multi-touch-enabled display or trackpad with Processing, as long as the device is supported by the Linux kernel. This library is available through the Contribution Manager under the name "Simple Touch".

This works well with the official [Raspberry Pi display](https://www.raspberrypi.org/blog/the-eagerly-awaited-raspberry-pi-display/), and allows for tracking of up to 10 fingers.

[Two example sketches](https://github.com/gohai/processing-simpletouch/tree/master/examples) the library comes with explain how to use it. Please file issues [here](https://github.com/gohai/processing-simpletouch/issues/new).

### Video library

Use the new [GL Video](https://github.com/gohai/processing-glvideo) library to make use of the Raspberry Pi's accelerated video decoding hardware. (also available from the Contribution Manager)

[Examples](https://github.com/gohai/processing-glvideo/tree/master/examples) show the various ways the library can be used. Please file issues [here](https://github.com/gohai/processing-glvideo/issues/new).

### Video library: Capture

If you're receiving the error `IllegalArgumentException: No such Gstreamer factory: v4l2src` with the (regular) Video library, try installing the necessary packages by executing `sudo aptitude install gstreamer0.10-plugins-good` in a terminal.

*Alternatively*, the [GL Video](https://github.com/gohai/processing-glvideo) library also contains some (very limited) functionality for using capture hardware. See [this example](https://github.com/gohai/processing-glvideo/tree/master/examples/SimpleCapture) for details.

If you want to use the Raspberry Pi camera with the [GL Video](https://github.com/gohai/processing-glvideo) library, add the following line to your `/etc/modules` file and reboot:

    bcm2835_v4l2

After the reboot your camera should show up as `/dev/video0`.

### Other libraries (OpenCV, OpenKinect, PureData, Sound, etc)

See [General notes about running Processing on ARM](Supported-Platforms#arm-linux).