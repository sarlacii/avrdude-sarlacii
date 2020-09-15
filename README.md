# avrdude-sarlacii
Avrdude v6.3 from "http://savannah.nongnu.org/projects/avrdude" is the base.

Additions by Karin and Julian to support additional devices.

Automake and compile process:
make maintainer-clean
autoreconf --install
./configure --enable-linuxgpio --disable-parport
make
make install

After configure script runs, you should see:

Configuration summary:
----------------------
DO HAVE    libelf
DO HAVE    libusb
DO HAVE    libusb_1_0
DO HAVE    libftdi1
DON'T HAVE libftdi
DON'T HAVE libhid
DO HAVE    pthread
DISABLED   doc
DISABLED   parport
ENABLED    linuxgpio
