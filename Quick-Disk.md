
**[v3.x Releases Only]**

FlashFloppy features an alternative firmware emulating the 2.8-inch
"Quick Disk" drive, used in a wide range of 80s synthesizers
by companies such as Akai, Korg and Roland.

### Programming the Quick Disk Firmware

Follow steps for [Firmware Update](Firmware-Update) but use the update
file contained in the **alt/quickdisk** subfolder of the FlashFloppy
distribution.

On successful update, when USB stick is ejected you should see **q-d**
on the Gotek display (this replaces **F-F** on the standard 3-digit
LED display). On an LCD or OLED display **[QD]** is shown.

### Connecting to the Quick Disk Host

Wiring is as follows. Note the conventional QD pin numbering and wire
colours. However this may vary on some hosts (for example, Korg
typically numbers the pins in the opposite order).

|QD Pin  |Wire Colour| QD Interface   |Gotek Pin|
|--------|-----------|----------------|---------|
|   1    | Brown     | /Write Protect |   28    |
|   2    | Red       | /Write Data    |   22    |
|   3    | Orange    | Write Gate     |   24    |
|   4    | Yellow    | /Motor On      |   16    |
|   5    | Green     | Read Data      |   30    |
|   6    | Blue      | /Ready         |   34    |
|   7    | Violet    | /Media Sw      |    2    |
|   8    | Grey      | /Reset         |   20    |
|   9    | White     | +5v (Power)    |  +5v    |
|  10    | Black     | Ground (GND)   |  GND    |

All other pins can be left unconnected.

### Using the Quick Disk Firmware

Usage is straightforward and very similar to the regular firmware.
* QD firmware supports only QD images (**.QD** file extension)
* A blank QD image is provided in **alt/quickdisk**
* FF.CFG is processed as usual, but do not modify drive-related
  options
