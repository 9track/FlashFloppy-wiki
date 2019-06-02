## New Major Stable Release v2.12 (2nd June 2019)

The v2 release series has been declared stable, ending support for v1
and introducing a host of new features and optimisations for all users
of FlashFloppy.

**\*\*\* All users are recommended to update at the [Downloads Page][dl]
\*\*\***

* Automatic folder sorting in direct navigation mode
* Flexible track layout configuration in [IMG.CFG](IMG.CFG-Configuration-File)
* Direct support for new image types:
  * ATR (Atari 8-bit)
  * OUT (Roland)
  * XDF (FAT-based eXtended Disk Format, 3.5" HD 1840kB)
* Flexible Indexed-Mode image naming (no longer restricted to DSKA0000)
* 3-digit LED: Track number display during drive activity
* OLED: Auto-detection of OLED controller type
* Buffer cache above USB mass-storage
  * I/O performance is faster and more predictable
  * For most image types, USB stick will rest while drive is not accessed
* Support for [Blackberry-style trackballs][bbtb]
* Improved write performance and robustness
* Optional accurate [motor emulation][me]
* A suite of alternative firmwares for diagnostics and special functions:
  * [IO-Test][iot]: Test the Gotek I/O pins for correct function
  * [Log File][lf]: Diagnostic logging to test file on USB drive
  * [Bootloader Update][blu]: Slick update of the FlashFloppy bootloader

[bbtb]: Hardware-Mods#blackberry-trackball
[me]: Hardware-Mods#motor-signal
[iot]: Testing-IO-Pins
[lf]: Logging-To-USB-Drive
[blu]: Firmware-Update#updating-the-bootloader
[dl]: Downloads
