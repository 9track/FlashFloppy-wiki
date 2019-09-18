Initial setup has two basic steps:
- Set up the physical interface to the host system
- Configure the operating mode for image navigation

## Physical Interface

By default FlashFloppy will emulate the Shugart floppy interface. This
is compatible with a broad range of systems including Amiga, Atari ST,
Amstrad CPC, and many other devices. Shugart-compatible systems will
typically expect the Gotek to respond as 'unit 0'. Therefore place the
selection jumper at location S0 at the rear of the Gotek.

IBM PC compatibles use a slightly modified interface which places the
disk-changed signal on a different pin. To select this interface mode
place a jumper at location JC at the rear of the Gotek. The host
system may expect the Gotek to respond as 'unit 1': in this case place
the selection jumper at location S1 at the rear of the Gotek.

An alternative method to specify the interface mode (Shugart or PC) is
via the [FF.CFG file][ffcfg].

See [Host Platforms](Host-Platforms) for detailed instructions and
troubleshooting for specific host systems.

## USB Storage

FlashFloppy requires a USB drive formatted with FAT32 (note that ExFAT
and NTFS are *not* supported). Most USB sticks are factory-formatted
appropriately. If erasing the entire drive on a Mac, be sure to select
the legacy "Master Boot Record" partitioning scheme.

## Image Navigation Modes

FlashFloppy supports three different operating modes. For the best
experience across the widest range of host systems, [Native
mode](#native-mode) is recommended in combination with an [LCD][lcd] or
[OLED][oled] display.

- [**Native mode**](#native-mode): No need for any configuration files.
  Allows direct selection of any valid image file on your USB stick.
- [**Indexed mode**](#indexed-mode): Switches between image names of the
  form DSKA0000 and so on.
- [**HxC Compatibility mode**](#hxc-compatibility-mode): A legacy mode
  requiring an image-selector program to run on the host
  system to pre-assign disk images to numbered slots.

## Native mode

In this mode you need no configuration files or selector
software (however, as in all operating modes, you may optionally
configure FlashFloppy via [FF.CFG][ffcfg]).

Behaviour depends on which display type you have connected:
- **LCD/OLED:**
FlashFloppy will allow you to select between any valid image file and
any folder within the current directory. Selecting a folder will make
that the new current directory, and list any image files and
subfolders within.
- **7-Segment LED:**
FlashFloppy will automatically assign all valid images in
the root folder of your USB stick to slots which you can switch
between using the Gotek buttons.

In all cases, the following folders and images are ignored and
will not be listed for navigation:
- Any name beginning with a dot (**.**)
- Any file which is not a valid image (eg. unrecognised filename extension)
- Any folder or image with the FAT "Hidden" attribute set
- Root folder called **FF/**
- Any folder called **__MACOSX/** (these get strewn around by macOS)

## Indexed mode

This mode is configured via [FF.CFG][ffcfg]:
**nav-mode = indexed**.

FlashFloppy will switch between image names of the form
DSKA0000\*.\*, DSKA0001\*.\*, and so on. Each image which will be automatically
assigned to the corresponding numbered slot. Note that any supported
image type can be used.

Note that an arbitrary filename is allowed after the DSKAnnnn prefix
(eg. DSKA0000_myimage.img). Additionally, the DSKA prefix can be changed
in FF.CFG (*indexed-prefix=*).

## HxC Compatibility mode

This mode selects between pre-assigned slots in an HXCSDFE.CFG file.
These slots are configured by an image-selector program running on the
host system, either in ROM or (more typically) an AUTOBOOT.HFE image
compatible with your system, copied to the root of your USB
drive. Supported systems include [Amiga](#amiga), [Atari
ST](#atari-st), and [Amstrad CPC](#amstrad-cpc). Note that for
enhanced compatibility, the correct files for Amiga and Atari ST are
included in the FlashFloppy release distribution.

The Gotek buttons cycle between the assigned slots in the config
file. To reassign slots boot the file selector: this is immediately
accessible in slot 0 by pressing both Gotek buttons at any
time. Configuration with the host selector software is
straightforward: assign files from your USB stick to drive A
"slots". On reboot, these slots are accessible via the up and down
buttons on the front of the Gotek. Holding a button will cycle faster
through the populated slots. Pressing both buttons will take you
immediately to the file selector.

**Important Note**: HxC assigns images to slots by physical location
on the USB stick, rather than by full path name. This means that if
you move files around within the filesystem, the slot assignments will
break with unpredictable results (FlashFloppy [error messages][error],
garbage disk images, etc). You **must not** copy a new image over an
old, or file-by-file copy one USB stick to another, unless you
subsequently refresh the slot assignments in HXCSDFE.CFG.

#### Amiga

Copy the following files to the root of your USB drive:
- HxC_Compat_Mode/Amiga/AUTOBOOT.HFE
- HxC_Compat_Mode/HXCSDFE.CFG

#### Atari ST

Copy the following files to the root of your USB drive:
- HxC_Compat_Mode/Atari_ST/AUTOBOOT.HFE
- HxC_Compat_Mode/HXCSDFE.CFG

#### Amstrad CPC

The latest files can be found on the [CPC scene website][cpc_hxc].

#### File Selector in Host ROM

Copy the following file to the root of your USB drive:
- HxC_Compat_Mode/HXCSDFE.CFG

[ffcfg]: FF.CFG-Configuration-File
[lcd]: Hardware-Mods#lcd-display
[oled]: Hardware-Mods#oled-display
[error]: Error-Messages
[cpc_hxc]: http://norecess.cpcscene.net/news/hxc-floppy-emulator-manager-v35-released
