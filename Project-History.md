**October 2014**: The FlashFloppy project was begun as a Free and
Open Source replacement for the abandoned free Cortex
firmware. I had a good deal of previous experience with retro
floppy-disk formats having implemented [Disk-Utilities][disk_utils], a
deep analyser and transcoder for a wide variety of disk image formats.

My aim then was to implement a more capable Gotek firmware, working
with many of the formats already supported by my existing tool set,
and compatible with a wide range of host systems. I had no prior
experience with the STM32 microcontroller used in the Gotek, but lots
of low-level programming experience in assembly and C, so I decided to
forgo using the vendor-supplied STM32 libraries and implement every
part of the system myself and make it fully Free and Open.

Thus proceeded several months of initial development time, working out
how to bring up the various peripherals on the STM32. This stalled on
the USB interface, which of course requires a USB stack: a major
project in itself. Thus began a detour in which I designed my own
hardware based on a cheaper STM32 chip and with an SD card interface
(much easier to drive) and a touch screen interface!

**April 2015**: HxC project releases a
[commercial firmware for Gotek][hxc_readme]. 

**May 2015**: I import the FatFS library for filesystem handling,
which is distributed under a generous MIT license. I glue it to
the SD block layer, and start to implement the floppy-interface
logic itself.

**August 2015**: The floppy interface supports reading ADF, HFE
and Supercard Pro image files.

**September 2015 - May 2017**: Project lies largely dormant while I
mess with hardware designs, using cheaper STM32F103 boards, such
as the $2 "blue pill".

**April 2017**: Manuel Teira reignites my interest in the Gotek
hardware when he contacts me to ask about integrating a USB stack. A
little research discovers a convenient vendor-supplied USB Host
library which could be deployed.

**June 2017**: Integrating USB into the FlashFloppy codebase
is a tough job for a third party. So I decide to take the task
myself, revive the FlashFloppy-on-Gotek code, commit the STM32 USB
Host stack, and plumb it into FatFS. FlashFloppy is alive on Gotek!

**July 2017**: I implement floppy write support, writing data back to
ADF and HFE image files. An update bootloader, for flashing new
firmware from a USB stick. And finally, compatibility with the
[HxC file selector][hxc_sel] based on the published configuration
[protocol][hxc_protocol] and [format][hxc_format]. First public
release of FlashFloppy immediately follows!

From this point on the [RELEASE NOTES][release_notes] tell the ongoing story.

[disk_utils]: https://github.com/keirf/Disk-Utilities/blob/master/README.md
[hxc_readme]: http://hxc2001.com/download/floppy_drive_emulator/USB_HFE_hxc_floppy_emulator_firmware_release_notes.txt
[hxc_sel]: https://github.com/jfdelnero/HXCFE_file_selector
[hxc_protocol]: http://hxc2001.com/download/floppy_drive_emulator/SDCard_HxC_Floppy_Emulator_Direct_Access_mode.pdf
[hxc_format]: http://hxc2001.com/download/floppy_drive_emulator/SDCard_HxC_Floppy_Emulator_HXCSDFE_CFG_file.pdf
[release_notes]: https://github.com/keirf/FlashFloppy/blob/master/RELEASE_NOTES
