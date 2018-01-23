FlashFloppy supports three different operating modes:
- [**Native mode**](#native-mode): No need for any configuration files.
  Allows direct selection of any valid image file on your USB stick.
- [**HxC Autoboot mode**](#hxc-autoboot-mode): Configured via HxC file
  selector and config file.
- [**Indexed mode**](#indexed-mode): Switches between image names of the
  form DSKA0000 and so on.
  
## Native mode

In this mode you need no configuration files or selector
software (however, as in all operating modes, you may optionally
configure FlashFloppy via [FF.CFG][ffcfg]).

Behaviour depends on which display type you have connected:
- **7-Segment LED:**
FlashFloppy will automatically assign all valid images in
the root folder of your USB stick to slots which you can switch
between using the Gotek buttons.
- **LCD/OLED:**
FlashFloppy will allow you to select between any valid image file and
any folder within the current directory. Selecting a folder will make
that the new current directory, and list any image files and
subfolders within.

## HxC Autoboot mode

This mode requires HXCSDFE.CFG and an AUTOBOOT.HFE image compatible
with your system. These files are available for Amiga, Atari ST
and Amstrad CPC from the [HxC project][hxc_web]:
- **Download:** [ZIP File][hxc_dl]
- **Subfolder:** Next_WIP_Alpha_Firmware_And_Tools

Within the subfolder find the AUTOBOOT.HFE file for your platform, and
use the HXCSDFE.CFG file in the same subfolder if present, else use
the generic file from the Autoboot-mode subfolder. These files must be
placed in the root of your USB drive.

The Gotek buttons cycle between the assigned slots in the config
file. To reassign slots boot the file selector: this is immediately
accessible in slot 0 by pressing both Gotek buttons at any
time. Configuration with the host selector software is
straightforward: assign files from your USB stick to drive A
"slots". On reboot, these slots are accessible via the up and down
buttons on the front of the Gotek. Holding a button will cycle faster
through the populated slots. Pressing both buttons will take you
immediately to the file selector.

## Indexed mode

This mode is configured via [FF.CFG][ffcfg]:
**nav-mode = indexed**.

FlashFloppy will switch between image names of the form
DSKA0000.\*, DSKA0001.\*, and so on. Each image which will be automatically
assigned to the corresponding numbered slot. Note that any supported
image type can be used.

[ffcfg]: Configuration#ffcfg-configuration-file
[hxc_web]: http://hxc2001.com/
[hxc_dl]: http://hxc2001.com/download/floppy_drive_emulator/HXCFEUSB_HFE_beta_firmware.zip
