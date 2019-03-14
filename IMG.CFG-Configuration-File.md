
**[v2.x Releases Only]**

FlashFloppy can usually automatically determine the layout of IMG/IMA
files, based on their size and (optionally) a hint about the host they
target (FF.CFG: *host=*).

However, there are such a wide range of systems that FlashFloppy cannot
hope to support them all automatically. For example, the CP/M operating
system does not have a standard disk layout, and these systems among
others require a degree of manual configuration.

The solution is an INI-style configuration file called IMG.CFG, placed
in the root folder or FF/ subfolder of your USB drive. An example is
provided in the examples/ subfolder of the FlashFloppy distribution.

## Tags

The file is divided into sections, each starting with a *tag name* in
square brackets. This section defines the track layout (geometry) for
all images named *.tagname.img and *.tagname.ima.

An optional *[default]* section can be defined, which matches all IMG/IMA
files that do not match any other defined tag, including untagged files
(ie. *img and *.ima).

If an IMG/IMA file does not match any tag, and no default tag is defined,
FlashFloppy uses normal geometry auto-detection based on the file's size
and the optional *host=* setting in FF.CFG.

## Geometry Options

Within each tagged section, a set of geometry parameters, mandatory and
optional, are specified. These are listed below.

For optional parameters, the default values are marked by asterisk.

- **cyls** = 1-85 (**Mandatory**)
  - Number of cylinders

- **heads** = 1-2 (**Mandatory**)
  - Number of heads (aka sides)

- **secs** = 1-64 (**Mandatory**)
  - Number of sectors per track

- **bps** = 128 | 256 | 512 | 1024 | 2048 | 4096 | 8192 (**Mandatory**)
  - Data bytes per sector

- **id** = 0-255[:0-255][,0-255[:0-255]] (1*)
  - ID of the first sector on each track
  - Successive sectors are numbered sequentially upwards
  - Numbers may be expressed in hexadecimal with 0x prefix (eg. 0xab).
  - Format x,y allows specifying different IDs for cylinder 0 vs cylinders 1+.
  - Format x:y allows specifying different ID (x, y) for each head/disk-side.
  - Format x specified same ID (x) for both heads/sides of a double-sided disk.
    - eg. 1:10,0x21:0x30 means c0h0=1, c0h1=10, cNh0=0x21, cNh1=0x30 (N > 0)

- **mode** = fm | mfm*
  - Recording mode

- **interleave** = 1-255 (1*)
  - Sector interleave (default is 1:1, which is no interleave)
  
- **skew** = 0-255 (0*)
  - Sector skew across tracks (default is 0, which is no skew)

- **rpm** = 1-1000 (300*)
  - Rotational RPM

- **gap3** = 0-255 (0*)
  - Sector post-data gap, in bytes.
  - N=0: Auto-select based on recording mode, sector size, and size of track

- **iam** = yes* | no
  - Index Address Mark included at the start of each track?

- **rate** = 0-1000 (0*)
  - Data rate in kHz (kbit/s).
    - eg. 250 is MFM DD, 500 is MFM HD, 125 is FM SD.
  - N=0: Auto-select based on recording mode and size of track
