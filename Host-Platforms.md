- [General Notes](#general-notes)
- [Acorn Archimedes](#acorn-archimedes)
- [Acorn BBC Micro](#acorn-bbc-micro)
- [Akai Synthesisers](#akai-synthesisers)
- [Amstrad CPC](#amstrad-cpc)
- [Amstrad PCW](#amstrad-pcw)
- [Atari ST](#atari-st)
- [Commodore Amiga](#commodore-amiga)
- [DEC](#dec)
- [Dragon](#dragon)
- [E-mu ESI-32](#e-mu-esi-32)
- [Ensoniq](#ensoniq)
- [General Music (GEM) Synthesisers](#general-music-gem-synthesisers)
- [IBM PC](#ibm-pc)
- [Korg](#korg)
- [Memotech](#memotech)
- [MSX](#msx)
- [NEC PC-98](#nec-pc-98)
- [Roland](#roland)
- [Sequential Circuits Prophet 3000](#sequential-circuits-prophet-3000)
- [Spectrum](#spectrum)
- [Tandy Color Computer](#tandy-color-computer)
- [TI-99/4A](#ti-994a)
- [UKNC, DVK](#uknc-dvk)

## General Notes

Most systems require Shugart interface (the default) and select line 0
(jumper on S0). Such systems will work out of the box with a
factory-fresh Gotek programmed with FlashFloppy firmware, requiring
only a physical jumper at the rear to be moved from S1 to S0.

If this does not work then also try the following:
- Jumper at S1 only
- Jumpers at JC and S0
- Jumpers at JC and S1

If the system still does not work and the Gotek green LED is
permanently lit then you may need to try connecting the ribbon cable
'upside down'.

This gives a total of eight possible jumper/ribbon configurations to
try, and there are further instructions for certain specific systems
listed below.

A final note: In most cases FlashFloppy requires a straight floppy
cable with no 'twist' between the connectors. If you do use a twisted
cable, you should jumper MO instead of S0. The exception is the one
case that the twist was designed for: connecting FlashFloppy as Drive
B to a PC-compatible floppy header.

## Acorn Archimedes

Some later models, A5000 onward, use index pulses to determine
whether a disk is inserted in the drive. If you are seeing spurious
"drive empty" messages then add the following to FF.CFG:
```
index-suppression = no
```

To use ADFS D/E/F sector images, which usually have suffix ADF, you
must explicitly configure the host type in FF.CFG as Amiga sector
images share the same suffix:
```
host = acorn
```

Some ADF images may not be exactly the correct size (usually 800kB or
1.6MB) and thus not be detected as valid by FlashFloppy. These can be
modified to the exact correct size using the `dd` utility on Mac or
Linux. For example, for an 800kB image:
```
# dd if=/dev/zero of=fixed.adf bs=5120 count=160
# dd if=bad.adf of=fixed.adf bs=5120 count=160 conv=notrunc
```

## Acorn BBC Micro

BBC Micro systems using the original single-density 8271 controller
require regular index pulses to avoid disk-not-ready errors
([described here][bbc-problem]). These errors are reported on the
video screen as `Drive fault 10 at xx/xx`.

This issue is solved by specifying the following FF.CFG option:
```
index-suppression = no
```

## Akai Synthesisers

Akai systems require explicit configuration in FF.CFG to recognise IMG
files correctly:
```
host = akai
```

The correct jumper selection is usually S0, with the following
interface selections in FF.CFG, depending on model:
```
interface = ibmpc-hdout # S3000
interface = akai-s950   # S950, S2800
interface = shugart     # SO1
```

Akai S1100 sends a signal to the floppy drive on pin 2, hence this pin
must be configured `nc`:
```
pin02 = nc              # S1100
pin34 = rdy             # S1100
```

## Amstrad CPC

FlashFloppy works with a wide range of CPC DSK images, however
compatibility is not perfect with copy-protected images. If you have
an original image which does not work, this is often due to 'GAPS
protection' where extra data is stored in the gaps between
sectors. These images can sometimes be fixed to work with
FlashFloppy by running a script included in the FlashFloppy
distribution, for example:
```
# python scripts/edsk_fix_gaps.py crazy_cars.dsk crazy_cars_fixed.dsk
```

#### Physical Connection of a Standard Gotek

See [here][cpc-pins] for guidance on connecting the CPC's 26-pin cable
to the Gotek 34-pin header. Also note that the CPC's power cable has
+5v and +12v reversed: you **must** use an adapter or otherwise
somehow insert the power connector backwards. If you do not, you will
**damage your Gotek** and **destroy any USB stick** that you insert!

Note that Gotek clones designed specifically for CPC (or Spectrum +3)
will use the data and power connectors as-is, and the above should be
ignored.

## Amstrad PCW

PCW uses a non-standard 26-pin header as described [here
(CPCWiki)][shugart-26], requiring an adapter to connect to the Gotek
34-pin header. Please note that this is **NOT** the same as the CPC
26-pin header, and if you use a CPC-compatible adapter or cable you
may damage your Gotek or your PCW!

#### Fixing Boot-Time Hangs

Later versions of LocoScript and CP/M require Drive A to correctly
respond to the Motor signal (Gotek pin 16), by deasserting Ready
(Gotek pin 34) when the motor is off. Unfortunately the Gotek usually
ignores Motor, and the PCW will hang during boot waiting for the drive
to respond correctly. [This page][pcw-hack] (in Italian, so use Google
Translate) explains how to modify the Gotek to fix this
problem. Section 8.3 of [this document][pcw-hw] gives more technical
information on the floppy-drive probe logic which causes this issue.

Alternatively, an option for correct motor emulation is provided in
FF.CFG: `motor-delay = 200`. Note that a standard Gotek needs a
[circuit modification](Hardware-Mods#motor-signal) to connect the
motor signal. This is an alternative to the extra external circuitry
described in the previous paragraph.

## Atari ST

No special configuration is required. Interface is Shugart (the default) and
drive-select jumper should typically be at position S0.

## Commodore Amiga

### Internal Drive (DF0)

To replace an existing Amiga internal drive usually requires a jumper
on S0 only. One exception are Escom A1200 boards, which are modded to
use PC drives: if you have one of these then you require a jumper on
JC (or `interface = ibmpc` in FF.CFG). For improved compatibility you
can undo the Escom mod as [described by RetroGameModz][a1200_mod].

### External Drive (DF1-DF3)

Replacing an external drive depends on the enclosure or cable being
used. Amiga external drive enclosures usually include the circuitry to
allow the Amiga to identify the presence of the drive. In this case
the Gotek with S0 jumper is usually a straight swap for the old floppy
drive. If using a passive cable such as this [Ebay item][amiga_cable]
then be aware that this identification circuitry is missing, but for
arcane reasons identification will typically happen to work as long as
the Gotek has an image mounted when the Amiga boots. If you are having
problems with your drive being identified, see
[Forcing Drive Identification](#forcing-drive-identification) below.

### High-Density Disks

Amiga Kickstart versions 2.05 and later support high-density disks
with 1760kB formatted capacity. This enhancement required a customised
(and nowadays expensive!) HD drive modified to rotate at half speed
and emit a special ID sequence to the Amiga when an HD disk is inserted.

FlashFloppy supports this enhancement for 1760kB ADF images, but the
high-density ID sequence must be [explicitly enabled in
FF.CFG](#forcing-drive-identification).

If using an Amiga external drive enclosure, please bear
in mind that the enclosure's interface board usually emits a fixed
double-density ID sequence which will make HD images unreadable. In
this case you must disconnect the enclosure's ID circuitry on its
interface PCB:
* Cut the PCB connection to external connector, pin 1.
* Connect a jumper wire between internal connector pin 34 and external
  connector, pin 1.

### Forcing Drive Identification

Amiga hosts expect a drive ID sequence from external and
Amiga-high-density drives on pin 34 of the floppy interface when the
drive motor is disabled (pin 34 carries the Ready/RDY signal
when the drive motor is enabled). In contrast, FlashFloppy's default
interface mode (`interface = shugart`) permanently attaches RDY
to pin 34, regardless of motor.

This default behaviour usually works fine:
* Drive ID signalling is not a strict requirement for DF0
* External drive enclosures often implement the drive-ID circuitry
* A mounted disk image asserts RDY which happens to
  match the Amiga ID sequence for a DD drive anyway

However, there are a couple of cases where this default behaviour may
*not* suffice:
* Using high-density disk images (1760kB formatted capacity)
* Using as an external drive with a passive interface cable, if
  FlashFloppy does not assert RDY during boot (eg. eject-at-power-on,
  no USB stick, or too slow to initialise)
  
In these cases FlashFloppy can be forced to emit the drive ID on pin
34 at all times, replacing RDY, by adding `interface = amiga` to
FF.CFG.

When HD images are not being used, and when FlashFloppy is being used
as DF0 or without problems as DF1-DF3, then it is best to use the
default interface type (`interface = shugart`) as this gives more
accurate behaviour on pin 34 in normal use while the drive motor is
enabled. Exact emulation of pin 34 behaviour is not possible on
unmodified Gotek hardware as the motor signal is not connected to
Gotek's microcontroller. More accurate support, for modified or
enhanced Gotek setups, may be implemented in future.

## DEC

DEC systems require `host = dec` in FF.CFG for correct IMG layout detection.
The RX33 and RX50 formats are supported.

## Dragon

No special configuration is required in order to use Dragon VDK disk
images.

If you wish to use DSK images for Tandy Coco, with appropriate ROM and
disk controller, then you will need `host = tandy-coco` in FF.CFG.

## E-mu ESI-32

Requires jumpers at S0 and JC. Works with 1.44MB (HD) IMG files.

## Ensoniq

Ensoniq systems use custom 800kB and 1600kB disk formats which are
supported as IMG files if the host-type is configured in FF.CFG:
```
host = ensoniq
```

The common EDE/EDA/EDS/EDT/EDV image formats are not directly supported
by FlashFloppy. These can be converted to HFE or IMG format using HxC
software. Notes:
* `host = ensoniq` is required in FF.CFG for IMG-format support
* IMG format is not supported for Mirage or SQ-80 (ie. 880kB) formats
* IMG format is especially preferred for 1600kB HD disks

Some Ensoniq series (notably the ASR and TS series) require an IBM-PC
interface with density-select output. These require a jumper on S0
**only**, and the following additional line in FF.CFG:
```
interface = ibmpc-hdout
```

Ensoniq EPS series typically requires a jumper on S0 **only**, and
the following additional lines in FF.CFG:
```
interface = shugart
pin02 = auto
```
However there is one isolated user report of pin 2 being inverted, so
if there are disk-change problems then you might try changing the
second line to `pin02 = nchg`. Revert back to `auto` if this doesn't
help.

## General Music (GEM) Synthesisers

GEM systems using the 1.6MB high-density disk format require explicit
configuration in FF.CFG to recognise IMG files correctly:
```
host = gem
```

## IBM PC

IBM PC compatibles have a non-Shugart interface which must be explicitly
configured in FlashFloppy:
* IBM-PC interface mode must be configured
  * Strap jumper JC at the rear of the Gotek; **or**
  * Specify via FF.CFG: `interface = ibmpc`
* Strap select-line jumper S1 at the rear of the Gotek
  * S0, S2, MO should all be left open

Please note that some IBM PC clones, although software compatible, use
the Shugart interface for their floppy drives. These typically require
a jumper at S0 only. Known models this affects include:
* Amstrad PPC512, PPC640

## Korg

Korg synths require `host = akai` in FF.CFG for correct IMG layout detection.

## Memotech

Memotech systems require the following options in FF.CFG:
```
host = memotech         # auto-detect IMG layout
index-suppression = no  # SDX/FDX require regular index pulses 
```

## MSX

MSX systems require `host = msx` in FF.CFG for correct IMG layout detection.

## NEC PC-98

PC-98 FDI and HDM disk images are supported directly. For raw IMG files
(rare), `host = pc98` needs to be set in FF.CFG.

For most machines the default Shugart interface is correct (jumper
only at position S0 at rear of Gotek). Internal pinout varies between
PC-98 machines but many use a 26-pin laptop floppy drive
connector. Appropriate adapters can be sourced from eBay or wired
directly as follows:
```
(26-pin) -> (34-pin + power)
1 -> 5V
2 -> 8
4 -> 10
6 -> 2
7 -> 12
8 -> 34
10 -> 16
12 -> 18
14 -> 20
15 -> GND
16 -> 22
18 -> 24
20 -> 26
22 -> 28
24 -> 30
26 -> 32
```

## Roland

Roland synths typically work out of the box with no special configuration
required in FF.CFG.

## Sequential Circuits Prophet 3000

Requires `host = akai` in FF.CFG for correct IMG layout detection.

## Spectrum

FlashFloppy boasts 100% compatibility with the TOSEC collection of DSK
images, however some are missing 'weak sector' information and must be fixed
up before use. If you find a game title fails to boot then you can fix
the image in two ways.

1. Using Simon Owen's [SAMdisk][samdisk]
```
# SAMdisk robocop.dsk robocop_fixed.dsk --fix
```

2. Using the Python script included in the FlashFloppy distribution
```
# python scripts/edsk_fix_speedlock.py robocop.dsk robocop_fixed.dsk
```

#### Spectrum +3: Physical Connection of a Standard Gotek

See [here][cpc-pins] for guidance on connecting the Spectrum +3's 26-pin cable
to the Gotek 34-pin header. Also note that the +3's power cable has
+5v and +12v reversed: you **must** use an adapter or otherwise somehow insert
the power connector backwards. If you do not, you will **damage your Gotek**
and **destroy any USB stick** that you insert!

Note that Gotek clones designed specifically for CPC and Spectrum +3
will use the data and power connectors as-is, and the above should be
ignored.

## Tandy Color Computer

Requires `host = tandy-coco` in FF.CFG to indentify DSK images as JVC format.

## TI-99/4A

Requires `host = ti99` in FF.CFG to identify DSK images as V9T9 format.

## UKNC, DVK

These Soviet PDP-11 clones have a modified IBM track format which must
be explicitly configured via `host = uknc` in FF.CFG.

[a1200_mod]: https://www.youtube.com/watch?v=G6fYOjTYvXM
[amiga_cable]: https://www.ebay.co.uk/itm/272363110859
[bbc-problem]: http://www.sprow.co.uk/bbc/floppydrives.htm
[cpc-pins]: http://www.cpcwiki.eu/index.php/DIY:Floppy_Drives
[samdisk]: http://simonowen.com/samdisk/
[shugart-26]: http://www.cpcwiki.eu/forum/amstrad-cpc-hardware/gotek-(flashfloppy)-wiring-for-a-pcw9512
[pcw-hack]: https://fabriziodivittorio.blogspot.com/2018/05/installazione-gotek-su-amstrad-pcw-9512.html
[pcw-hw]: https://www.seasip.info/Unix/Joyce/hardware.pdf