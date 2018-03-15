
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

## Acorn Archimedes

Some or all models may use regular index pulses to determine whether
a disk is inserted in the drive. If you are seeing spurious "drive
empty" messages then you need to add the following to FF.CFG:
```
index-suppression = no
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

Akai systems using the 1.6MB high-density disk format require explicit
configuration in FF.CFG to recognise IMG files correctly:
```
host = akai
```

## E-mu ESI-32

Requires jumpers at S0 and JC. Works with 1.44MB (HD) IMG files.

## Ensoniq

Ensoniq systems use custom 800kB and 1600kB disk formats which are
supported as IMG files if the host-type is configured in FF.CFG:
```
host = ensoniq
```

Some Ensoniq series (notably the ASR and TS series) require an IBM-PC
interface with density-select output. These require a jumper on S0
**only**, and the following additional line in FF.CFG:
```
interface = ibmpc-hdout
```

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


[bbc-problem]: http://www.sprow.co.uk/bbc/floppydrives.htm
