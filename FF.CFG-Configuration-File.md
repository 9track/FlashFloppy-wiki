
FlashFloppy has many configurable settings which can be specified in
an INI-style configuration file called FF.CFG, placed in the root
folder or FF/ subfolder of your USB drive. An example is provided in
the examples/ subfolder of the FlashFloppy distribution.

## Defaults

Out of the box, FlashFloppy loads the default values described in the
Options list, below. When these are modified by values in FF.CFG they
are recorded into the Gotek's Flash memory and become the new default
values when the drive is next powered on.

If you wish to return to 'factory defaults', press the Prev and Next
buttons (or Select, or the rotary encoder, if you have them) for three
seconds with no USB stick inserted. The display will show "RST" or
"Reset Flash Configuration", and FlashFloppy will return to factory
defaults when the buttons are released.

## Options

Default values are marked by asterisk.

### Drive Emulation:

- **interface** = shugart | ibmpc | ibmpc-hdout | akai-s950 | amiga | jc*
  - Pin assignments of the floppy-drive interface
  - **shugart**: Shugart interface (Amiga, Atari ST, many others)
  - **ibmpc**: IBM PC interface, no connection on pin 2
  - **ibmpc-hdout**: IBM PC, high-density-select output (Gotek->host) on pin 2
    - Do not select this option unless explicitly required for your system!
    - It is not required for IBM PC compatibles. Use **ibmpc** instead.
  - **akai-s950**: Akai S950
  - **amiga**: Drive ID hack on pin 34. Use **shugart** instead when possible.
    - See [Amiga-specific hints](Host-Platforms#commodore-amiga) for advice
      on this setting.
  - **jc**: Specified by jumper JC (closed = IBM PC, open = Shugart)

- **host** = unspecified* | acorn | akai | ...
  - Host platform: Improves image-format detection for generic types
    such as IMG and DSK
  - **acorn**: Acorn ADFS
  - **akai**: Akai synths (S01, S20, S950), Korg synths, SC Prophet 3000
  - **casio**: Casio synths (FZ-1)
  - **dec**: DEC (RX33, RX50)
  - **ensoniq**: Ensoniq synths (ASR/TS series, and others)
  - **fluke**: Fluke (9100)
  - **gem**: General Music (S2, S3, S2R)
  - **kaypro**: Kaypro
  - **memotech**: Memotech
  - **msx**: MSX
  - **nascom**: Nascom (1, 2)
  - **pc98**: NEC PC-98
  - **pc-dos**: PC DOS Format (geometry determined from Bios Parameter Block)
  - **tandy-coco**: Tandy Color Computer (CoCo)
  - **ti99**: TI-99/4A
  - **uknc**: UKNC, DVK (Soviet PDP-11)
  - **unspecified**: Detection based on image-name suffix only

- **pin02** = auto* | nc | low | high | rdy | nrdy | dens | ndens | chg | nchg
  - Manually assign an output signal (Gotek->host) to floppy interface pin 2
  - **auto**: Automatically determined from *interface =* setting
  - **nc**: Unused / No Connection
  - **low**, **high**: Constant low (0v) or high (5v) voltage
  - **rdy**, **nrdy**: Drive ready, or logical complement
  - **dens**, **ndens**: Density mode (HD = 0v), or logical complement
  - **chg**, **nchg**: Disk changed, or logical complement

- **pin34** = auto* | nc | low | high | rdy | nrdy | dens | ndens | chg | nchg
  - Manually assign an output signal (Gotek->host) to floppy interface pin 34

- **write-protect** = yes | no*
  - Are images write protected when initially mounted?
    - Protection can be toggled by holding eject for 2 seconds
  - **yes**: Forcibly write-protect images
  - **no**: Respect the FAT read-only attribute

- **side-select-glitch-filter** = 0-255 (0*)
  - Filter glitches in the SIDE-select signal shorter than N microseconds
  - Useful on some old hardware (eg. CP/M systems)

- **track-change** = instant* | realtime
  - Rotational offset of data after a track change
  - **instant**: No rotation during track change
  - **realtime**: Emulate rotation of disk while track is changing

- **index-suppression** = yes* | no
  - Are index pulses suppressed when RDATA and WDATA inactive?
  - Older systems may depend on constant index pulses (eg. BBC Micro)

- **head-settle-ms** = 0-255 (12*)
  - Milliseconds from head-step start to RDATA active

### Startup & Initialisation:

- **ejected-on-startup** = yes | no*
  - Disk image loaded or ejected at power on

- **image-on-startup** = last* | static | init
  - Which image (or folder) is selected at startup
  - **last**: Last-selected item at power off (recorded in IMAGE_A.CFG)
  - **static**: Static pathname specified in IMAGE_A.CFG
  - **init**: First item in root folder

- **display-probe-ms** = 0-65535 (2000*)
  - Time in milliseconds to attempt to probe an attached display
  - If you have a 2-digit LED display, or no display:
    Set to 0 for faster startup

### Image Navigation:

- **autoselect-file-secs** = 0-255 (2*)
  - Auto-select the current file/slot after N seconds
  - N=0: disable auto-select

- **autoselect-folder-secs** = 0-255 (2*)
  - Auto-select the current folder after N seconds
  - N=0: disable auto-select

- **nav-mode** = native | indexed | default*
  - Navigation mode for selecting images or slots
  - **native**: Navigate through all valid images and folders
  - **indexed**: Navigate through DSKA0000, DSKA0001, ...
  - **default**: As native unless overridden by HxC-compat-mode config

- **nav-loop** = yes* | no
  - When navigating slots or a folder, loop at start/end of the list

- **twobutton-action** = zero* | eject | rotary | rotary-fast | reverse
  - Actions of first two buttons
  - Multiple values can be specified, separated by commas (eg. *rotary,reverse*)
  - **zero**: 1: Prev, 2: Next, Both: Slot 0
  - **eject**: 1: Prev, 2: Next, Both: Eject/Insert
  - **rotary**: 1: Up-dir, 2: Select/Eject/Insert, Both: -
  - **rotary-fast**: 1: Prev (accelerated), 2: Next (accelerated), Both: Up-dir
  - **reverse**: Reverse operation of the buttons (useful if installed upside down)

- **rotary** = none | quarter | half | full* | reverse
  - Type of rotary encoder connected to pins PC10 and PC11
  - Multiple values can be specified, separated by commas (eg. *half,reverse*)
  - **none**: No rotary encoder is connected
  - **quarter**, **half**, **full**: Fraction of a Gray-code cycle performed per detent/click
    - Select **half** if default value (**full**) requires 2 clicks per move
    - Select **quarter** if default value (**full**) requires 4 clicks per move
  - **reverse**: Reverse direction of the knob (useful if wired backwards!)

### Display:

- **display-type** = auto* | lcd-NNx02 | oled[-128xNN][-rotate][-narrow][-sh1106]
  - **auto**: Auto-detect (7-seg LED, LCD, OLED)
  - **lcd-NNx02**: NNx2 backlit LCD with I2C backpack (16 <= NN <= 40)
  - **oled-128xNN**: 128xNN I2C OLED (NN = 32 | 64)
    - **-rotate**: OLED view is rotated 180 degrees
    - **-narrow**: OLED view is restricted to Gotek display cutout
    - **-sh1106**: SH1106 controller (default is SSD1306)

- **oled-font** = 6x13* | 8x16
  - Select 6px- or 8px-wide OLED display font
  - 6x13 font permits:
    - More characters per row
    - Use of Gotek display cutout (with *display-type=oled-128x32-narrow*)

- **oled-contrast** = 0-255 (143*)
  - OLED contrast/brightness

- **display-off-secs** = 0-255 (60*)
  - Turn LCD/OLED display off after N seconds of inactivity
  - N=0: always off
  - N=255: always on

- **display-on-activity** = yes* | no
  - Automatically switch LCD/OLED display on when there is drive activity

- **display-scroll-rate** = 100-65535 (200*)
  - LCD/OLED long filename scroll rate (ms per update)
  - Larger value means slower scroll

- **display-scroll-pause** = 0-65535 (2000*)
  - LCD/OLED long filename scroll start/end pause (ms)
  - N=0: Endless looping scroll

- **nav-scroll-rate** = 0-65535 (80*)
  - LCD/OLED long filename scroll rate during navigation (ms per update)

- **nav-scroll-pause** = 0-65535 (300*)
  - LCD/OLED long filename pause before scroll starts during navigation (ms)

### Miscellaneous:

- **step-volume** = 0-20 (10*)
  - Speaker volume (connected at jumper JB) when drive heads are moved

- **da-report-version** = quoted-string
  - Report the specified version number to host software
  - Empty string ("") means report the firmware version number
  - For example: da-report-version = "v3.0.0.0"

- **extend-image** = yes* | no
  - Automatically extend a truncated image file at mount/insert time
    - Applies to SSD, DSD, TRD images only
