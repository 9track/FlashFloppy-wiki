
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

- **interface** = shugart | ibmpc | jc*
  - Pin assignments of the floppy-drive interface
  - **shugart**: Shugart interface (Amiga, Atari ST, many others)
  - **ibmpc**: IBM PC interface, no output on pin 2
  - **ibmpc-hdout**: IBM PC, high-density-select output on pin 2
  - **jc**: Specified by jumper JC (closed = IBM PC, open = Shugart)

- **host** = unspecified* | akai | ensoniq | gem
  - Host platform: Improves image-format detection for generic types
    such as IMG
  - **akai**: Akai synths (S01, S20, S950)
  - **ensoniq**: Ensoniq synths (ASR/TS series, and others)
  - **gem**: General Music (S2, S3, S2R)
  - **unspecified**: Detection based on image-name suffix only

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

- **twobutton-action** = zero* | eject | rotary
  - Actions of first two buttons
  - **zero**: 1: Prev, 2: Next, Both: Slot 0
  - **eject**: 1: Prev, 2: Next, Both: Eject/Insert
  - **rotary**: 1: Up-dir, 2: Select, Both: -

- **rotary** = none | simple* | gray
  - Type of rotary encoder connected to pins PC10 and PC11
  - **none**: No rotary encoder is connected
  - **simple**: Cheap rotary encoder, both outputs HIGH at each detent
  - **gray**: Higher quality encoder with proper Gray code quadrature output

### Display:

- **display-type** = auto* | lcd-16x02 | oled-128x32[-rotate][-narrow]
  - **auto**: Auto-detect (7-seg LED, LCD, OLED)
  - **lcd-16x02**: 16x2 backlit LCD with I2C backpack
  - **oled-128x32**: 128x32 I2C OLED
    - **-rotate**: OLED view is rotated 180 degrees
    - **-narrow**: OLED view is restricted to Gotek display cutout

- **oled-font** = 6x13* | 8x16
  - Select 6px- or 8px-wide OLED display font
  - 6x13 font permits:
    - More characters per row
    - Use of Gotek display cutout (with *display-type=oled-128x32-narrow*)

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