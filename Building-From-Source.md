FlashFloppy can be built from source either [manually](#manual-method)
in a suitable Linux environment, or using a pre-built
[Docker image](#docker).

## Manual Method

This project is cross-compiled on an x86 Ubuntu Linux system. However
other similar Linux-base systems (or a Linux virtual environment on
another OS) can likely be made to work quite easily.

The Ubuntu package prerequisites include:
- git
- gcc-arm-none-eabi
- python-pip
- srecord
- stm32flash
- zip, unzip
- wget

If the stm32flash package is unavailable on your system then it must
be downloaded from Sourceforge and built locally.

The Python library prerequisites include:
- crcmod
- intelhex

To install the prerequisites on Ubuntu:
```
 # sudo apt install git gcc-arm-none-eabi python-pip srecord stm32flash zip unzip wget
 # pip install --user crcmod intelhex
```

To build the FlashFloppy firmware:
```
 # git clone https://github.com/keirf/FlashFloppy.git
 # cd FlashFloppy
 # make dist
```

## Making a Debug Build

FlashFloppy can be configured to emit debug logging via the same
serial interface used for
[serial programming](Firmware-Programming#method-1-serial-programming).
Follow the above instructions but replace the final `make` line as
follows:
```
 # debug=y make dist
```

The default baud rate is 3Mbps. If this is too fast for your
host you can reduce it (for example, to 115200) by modifying the
definition of `BAUD` at the top of `src/console.c`.

## Docker

Urban Jonnson has uploaded a Docker image which will create the
FlashFloppy distribution zip file from the following command line:
```
 # docker run -v $(pwd):/output --rm -ti planeturban/docker-flashfloppy
```
