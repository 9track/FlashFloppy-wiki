FlashFloppy has many configurable settings which can be specified in
an INI-style configuration file called FF.CFG. An example is
provided in the examples/ subfolder of the FlashFloppy distribution.

## FF.CFG Options

Default values are marked by asterisk.

- **interface** = shugart | pc | default*
  - Pin assignments of the floppy interface
  - **shugart**: Shugart protocol (pin 2 = dskchg, pin 34 = rdy) as
      used by Amiga, Atari ST and many other systems.
  - **pc**: IBM/PC protocol (pin 2 = unused, pin 34 = dskchg) as used on PCs.
  - **default**: As specified by jumper JC (closed = PC, open = Shugart).

- **ejected-on-startup** = yes | no*
  - Disk image loaded or ejected at power on

- **da-report-version** = string
  - Report the specified version number to host software
  - For example: da-report-version = v3.0.0.0

- **autoselect-file-secs** = 0-255 (2*)
  - Auto-select the current file/slot after N seconds
  - N=0: disable auto-select

- **autoselect-folder-secs** = 0-255 (2*)
  - Auto-select the current folder after N seconds
  - N=0: disable auto-select

- **nav-loop** = yes* | no
  - When navigating slots or a folder, loop at start/end of the list

- **display-off-secs** = 0-255 (60*)
  - Turn LCD/OLED display off after N seconds of inactivity
  - N=0: always off
  - N=255: always on

- **display-on-activity** = yes* | no
  - Automatically switch LCD/OLED display on when there is drive activity

- **display-scroll-rate** = 100-65535 (400*)
  - LCD/OLED long filename scroll rate in milliseconds per update
  - Larger value means slower scroll

- **step-volume** = 0-20 (10*)
  - Speaker volume (connected at jumper JB) when drive heads are moved
