
## General Notes

Most systems require Shugart interface (the default) and select line 0
(jumper on S0). Such systems will work out of the box with a
factory-fresh Gotek programmed with FlashFloppy firmware, requiring
only a physical jumper at the rear to be moved from S1 to S0.

## Akai Synthesisers

Akai systems using the 1.6MB high-density disk format require explicit
configuration in FF.CFG to recognise IMG files correctly:
```
host = akai
```

## BBC Micro

BBC Micro systems using the original single-density 8271 controller
require regular index pulses to avoid disk-not-ready errors
([described here][bbc-problem]). This can be solved by updating DFS
to the unofficial version 1.21, or the following FF.CFG options:
```
track-change = realtime
index-during-seek = yes
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
