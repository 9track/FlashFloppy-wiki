- [General](#general)
- [Commodore Amiga](#commodore-amiga)

## General

- **My Gotek does not recognise any USB stick that I insert, and then
afterwards they all fail to work even in a PC**
  - You are feeding more than 5 volts power to the Gotek, and frying
all your USB sticks! This is commonly because either the connector is
inserted upside down, or because of a non-standard connector (eg
Amstrad CPC, Spectrum +3). Either way you fed 12 volts to the
Gotek. It usually survives, but USB sticks are instantly killed.

## Commodore Amiga

- **I installed a Gotek in my A1200 but it will not recognise
any floppy images**
  - Assuming your Gotek is properly jumpered (S0 only) then this is
usually because you have an Escom motherboard. Please check out
[this informative Youtube video][a1200_mod].

- **The AUTOBOOT file selector does not recognise my Gotek drive**
  - First please make sure you are running latest firmware and
AUTOBOOT (both are included in the [latest release](Downloads)).
If the problem persists then the drive's READY signal is probably
not reaching the Amiga. You can test this by booting [SysTest][systest],
running the floppy read test, and check for the "no READY signal" warning.
In this case either your ribbon cable is worn out, or you have an Escom
board in need of further modding (check out the additional jumper wire
in [this Youtube video][a1200_mod]).

[a1200_mod]: https://www.youtube.com/watch?v=G6fYOjTYvXM
[systest]: https://github.com/keirf/Amiga-Stuff/blob/master/README.md
