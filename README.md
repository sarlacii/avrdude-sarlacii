# avrdude-sarlacii
Avrdude v6.3 from "http://savannah.nongnu.org/projects/avrdude" is the base.

Additions by sarlacii and team to support additional devices (Atmel ATA8510).

## Automake and compile process:

First, clean up from any previous autoconf, configure or compile.
If there is nothing to do, this command fails. Ignore in that case and carry on.

    make maintainer-clean

Then reconfigure and make the project:

    autoreconf --install
    # Configure defaults set --enable-linuxgpio --disable-parport
    ./configure
    make
    make install

After the ./configure script runs, you should see:

    Configuration summary:
    ----------------------
    DO HAVE    libelf
    DO HAVE    libusb       --> You may only have the older 0.1 version USB libs. That's fine.
    DO HAVE    libusb_1_0   --> In this example both are present
    DO HAVE    libftdi1     --> If you DON'T HAVE libftdi1, then make sure you DO HAVE libftdi
    DON'T HAVE libftdi      --> likewise with libftdi... .
    DON'T HAVE libhid
    DO HAVE    pthread
    DISABLED   doc
    DISABLED   parport
    ENABLED    linuxgpio

### Libraries required for compilation (openSuse-specific - change to match your distro):

    zypper install libelf1 libelf-devel
    zypper install libusb-1_0-0 libusb-1_0-devel libusb-0_1-4 libusb-compat-devel
    zypper install libftdi1 libftdi1-devel
    # HID not required - was (PClinuxOS) apt-get install lib64hid-devel lib64hid0
    
### Tools required for building the project:
    
    zypper install gcc bison flex make automake autoconf
    zypper install binutils binutils-devel
    zypper install elfutils
    # Optional for make distcheck
    zypper install makeinfo

## Device notes:

### ATA8510:

The default bit clock period for avrdude results in unstable programming of the device flash/eeprom. Programming also takes a very long time, with non-obvious errors. So make sure to program with the "-B" option. A value of 125kHz is recommended, same as the Atmel Studio default: i.e. "-B 125kHz". The suffix "kHz" will cause avrdude to set the bit clock period from the specified frequency, as opposed to the default which is an integer bit clock period in micro-seconds (us).

### SAMD20-J18 / SAM4S8B:

Added additional device signatures for later versions of silicon.
