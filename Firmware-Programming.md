The first installation of this firmware onto Gotek can be done either
by [serial](#serial-programming) or [USB](#usb-programming) link to
a host PC.

## Serial Programming

This method requires a USB-TTL serial adapter, which are readily
available on Ebay or from project webstores:
- [CAB-12977 from SparkFun](https://www.sparkfun.com/products/12977)
- Search "PL2303HX usb ttl adapter" on Ebay, available for around one dollar.

![USB-TTL Adapter](assets/usbttl.jpg)

The Gotek is then jumpered in system-bootloader mode and programmed
from the host PC. See the below picture for wiring and jumper
selection. This Gotek has had pins soldered to the programming
header. It is possible to make the required connections with no
soldering, but be careful that all wires are sufficiently well
connected. Also note that the ordering of the connections
(5V,GND,TX,RX) can vary across adapters, so be careful to note the
ordering on your own.

![Programming header](assets/programming_header.jpg)

The programming process is described, along with suitable
Windows software, on the
[Cortex firmware webpage](https://cortexamigafloppydrive.wordpress.com).
Of course, rather than using the Cortex HEX file, use the HEX file
contained in the FlashFloppy release archive.

If programming on Linux, you can follow the Cortex instructions to
physically set up your serial connection and bootstrap the Gotek, and
then use stm32flash to do the programming:

```
 # sudo stm32flash -w flashfloppy_fw/FF_Gotek*.hex /dev/ttyUSB0
```

## USB Programming

See this [Youtube video](https://www.youtube.com/watch?v=yUOyZB9cro4@feature=youtu.be)
for detailed instructions on this method. You will require a USB-A to
USB-A cable, and you should program the HEX file contained in the
FlashFloppy release archive.
