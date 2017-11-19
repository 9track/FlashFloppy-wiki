- [Speaker](#speaker)
- [Eject/Select Button](#ejectselect-button)
- [LCD Display](#lcd-display)
- [OLED Display](#oled-display)
- [Rotary Encoder](#rotary-encoder)
- [Enhanced Gotek](#enhanced-gotek)

## Speaker

A speaker can be attached to the Gotek to sound whenever the drive
heads move. This simplest method is to connect a piezo sounder
directly to the JB header pins, as shown in this video:

[![FlashFloppy speaker install](http://img.youtube.com/vi/UevBaQvG_4Y/0.jpg)](http://www.youtube.com/watch?v=UevBaQvG_4Y "FlashFloppy speaker install")

If you want to connect a magnetic speaker instead, you must buffer via
an NPN transistor. If you don't know what this means just be sure to
use a piezo sounder, easily found on Ebay, and connect it directly as
shown above.

## Eject/Select Button

FlashFloppy supports a third button in addition to the basic up/down
controls. This should be a standard momentary microswitch, connected
to the header pins JA.

The button's effect depends on the current state of operation:
- When an image is loaded, the button will immediately eject it
- When selecting an image, the button will immediately confirm the
  currently-selected image

## LCD Display

As an alternative to the Gotek 7-segment display, FlashFloppy supports
the ubiquitous 1602 LCD with I2C backpack board. These are available
from many Ebay sellers. The connections should be made just as for HxC
Gotek firmware, including pullup resistors (if required - see below).

You can locate SCL, SDA, and GND on your Gotek PCB as below. These
connect to the corresponding header pins on your LCD I2C backpack
module.

![LCD data/clock interface](assets/header_closeup.jpg)

VCC (aka 5V) can be found in various places, including just behind the
floppy power connector.

![LCD VCC](assets/jumpers.jpg)

The SCL and SDA lines must be connected to VCC ("pulled up" to VCC)
via 4.7k resistors.  Note that many I2C boards have the pullup
resistors on board and in this case you do not need to attach your own
external pullups. You can confirm this by checking the resistance
between SDA/SCL and VCC. If it is less than 10k you do not need to add
pullups.

If you do require the pullup resistors, these can be soldered to the
backside of the Gotek PCB between VCC and each of SDA and
SCL. Alternatively can be soldered to the back of the I2C module
header as below.

![LCD Pullup Resistors](assets/pullups.jpg)

## OLED Display

Another alternative to the Gotek 7-segment display is a 0.91" 128x32
display, as sold for Arduino projects by many Ebay sellers. You will
require a display with I2C interface: you should see it has a 4-pin
header marked GND, VCC, SCL, SDA.

These displays can simply connect to the 7-segment display's header,
reusing the existing jumper wires, as in the picture below.

![OLED Display Front](assets/oled1.jpg)

Beware of OLED displays marked **DIYMORE OLED-091**:

![DIYMORE Display](assets/diymore_oled.jpg)

Many users have found that these displays fail to initialise unless
given a longer startup time by adding the following line to FF.CFG:
```
startup-delay = 2000
```
In some cases a delay up to 3000 has been required.

## Rotary Encoder

As an alternative to using the up/down buttons you can instead connect
a rotary encoder. The picture below shows how to connect it, either
directly or via a PCB module (eg KY040).

If connecting directly note that by convention GND is always the
middle pin in the row of three. If there is a further row of
two pins then these are connected to an internal push switch: you can
wire these pins to jumper JA to use the switch as an
[eject/select button](#ejectselect-button).

![Rotary Encoder Connection](assets/rotenc.jpg)

Rotating the dial should now have the same effect as pushing the
buttons: anti-clockwise for down, and clockwise for up.

Troubleshooting:
- Directional controls are inverted: swap the A and B (aka CLK, DT) wires.
- PCB modules only: Both directions move up (or down):
  - Connect + to 3.3V (marked in picture above); or
  - Remove pull-up resistors from the back of the PCB; or
  - Remove the encoder from the PCB and solder wires directly.

## Enhanced Gotek

Gotek clone designers can choose to add various enhancements to the
standard Gotek, all supported by the FlashFloppy firmware. Note that
these instructions are intended for PCB designers and cannot be
retrofitted to a standard Gotek without fine soldering skills. Regular
Gotek users should therefore skip this section.

### Summary

- **PC12-15:** Board Identifier
- **PA3:** Second Drive Select
- **PA15:** Motor-On Signal
- **PA4-5:** USB Power Switch

### Board Identifier

Pins PC12-15 are used to identify an enhanced Gotek. On a standard
Gotek board these pins are disconnected and floating. On an enhanced
Gotek they should all be connected to VSS (GND).

### Second Drive Select

FlashFloppy may in future emulate two drives in a single Gotek. To
support this pin PA3 may be connected to a second drive-select line
and pulled up by 1K to VCC (5v). If second-drive select is not
supported then the pull-up is still required, to avoid PA3 floating.

### Motor-On Signal

FlashFloppy may in future use the motor-on signal to improve emulation
accuracy. To support this pin PA15 may be connected to the motor-on
line (eg floppy pin 16) and pulled up by 1K to VCC (5v). If the
motor-on signal is not supported then the pull-up is still required,
to avoid PA15 floating.

### USB Power Switch

A power switch with active-low enable and open-drain fault output may
be connected as follows:
- PA4: active-low enable (output to USB power switch)
- PA5: open-drain active-low fault signal (input from USB power switch)

These connections are optional and either pin may instead be left
disconnected and floating (the STM32 will pull them to a defined
level).

A suitable power switch is STMicroelectronics STMPS2141.
