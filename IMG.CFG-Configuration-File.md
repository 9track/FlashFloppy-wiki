
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

- **cyls** = 1-254 (**Mandatory**)
  - Number of cylinders

- **heads** = 1-2 (**Mandatory**)
  - Number of heads (aka sides)

- **secs** = 1-256 (**Mandatory**)
  - Number of sectors per track

- **bps** = 128 | 256 | 512 | 1024 | 2048 | 4096 | 8192 (**Mandatory**)
  - Data bytes per sector

- **id** = 0-255[:0-255] (1*)
  - ID of the first sector on each track
  - Successive sectors are numbered sequentially upwards
  - Numbers may be expressed in hexadecimal with 0x prefix (eg. 0xab).
  - Format x:y allows specifying different ID (x, y) for each head/disk-side.
  - Format x specifies same ID (x) for both heads/sides of a double-sided disk.

- **mode** = fm | mfm*
  - Recording mode

- **interleave** = 1-255 (1*)
  - Sector interleave (default is 1:1, which is no interleave)
  
- **cskew** = 0-255 (0*)
  - Sector skew per cylinder (default is 0, which is no skew)

- **hskew** = 0-255 (0*)
  - Sector skew per head (default is 0, which is no skew)

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

- **file-layout** = interleaved* | sequential | reverse-sideN | sides-swapped
  - Image file track layout
  - Multiple values can be specified, separated by commas (eg. *sequential,reverse-side1*)
  - **sequential**: Sequential cylinder ordering: all side 0, then side 1
  - **interleaved**: Interleaved cylinder ordering: c0s0, c0s1, c1s0, c1s1, ...
  - **reverse-sideN**: Side-N cylinders are in reverse order (high to low) (N=0,1)
  - **sides-swapped**: Sides 0 and 1 ordering is swapped in the image file
