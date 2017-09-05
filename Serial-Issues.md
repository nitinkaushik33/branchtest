The Processing serial library allows for easily reading and writing data
to and from external machines. It allows two computers to send and
receive data and gives you the flexibility to communicate with custom
microcontroller devices, using them as the input or output to Processing
programs. The serial port is a nine pin I/O port that exists on many PCs
and can be emulated through USB.

### Using the Serial Port

**All Platforms**

-   If you're using a program to check to see if the serial port is
    working, then it won't be available to Processing. That means that
    if you're using HyperTerminal or whatever to see if your serial
    device is working, then you need to quit out of that application
    before using that port with Processing.

-   Serial.list() will only list the ports that are currently available.
    So if you have a program that's using the serial port that you want
    to use for your Processing sketch, it's not going to be available,
    or even listed.

**Mac OS X**

-   In the past, I've used a keyspan 28X dual port adapter, and
    Serial.list() returns things like

`/dev/cu.USA28X21P1.1. `

You'll probably have something similar. Don't mind the frightening
names.

-   Tom Igoe was kind enough to note that you'll be in a world of hurt
    if you disconnect your serial adapter while a sketch is
    running—it'll prolly freeze the machine and require a forced reboot.
    This scenario may seem unlikely, but you might run into it if your
    adapter is plugged into a USB keyboard, and you have the keyboard
    plugged into a monitor/keyboard switcher. You know, those cheap KVMs
    that everyone likes to talk about in relation to the Mac Minis? The
    ones that actually cost \~\$150 and up?

**Linux**

-   If you're having
    trouble getting things to run, i.e. the port menu stays grayed out
    or you get error message spew to the console when starting the
    application saying "Permission denied" and "No permission to create
    lock file", this is because you probably need to add yourself to
    both the uucp or lock groups so that processing can write to
    /var/lock so it doesn't get in a fight with other applications
    talking on the serial port.

-   Alan Kilian contributes this description:

1.  I did an ls -l /dev/ttyS0 and saw that the group was set to uucp.
2.  Then I edited /etc/groups, I found the uucp group, and I added my
    login ID to the uucp line.
3.  I logged out, and logged back in again.
4.  The "groups" command now showed I was in group uucp, and when I
    started processing, the serial port menu item was not greyed-out.

It's important that you're in both groups, and that you completely log
out and log back in again.

*NOTE*: In modern versions of Ubuntu (14.04, 16.04...) and derivatives, the group to add yourself must be "dialout"
(at least, to communicate to Arduino UNO or similar, which is seen as a /dev/ttyACMx device)

-   Running processing as root will often get rid of the errors, but
    that's obviously not a good solution for a million reasons (among
    them: beta code that runs as root and handles files? yeah great...)
