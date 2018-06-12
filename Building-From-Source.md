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

## Docker

Urban Jonnson has uploaded a Docker image which will create the
FlashFloppy distribution zip file from the following command line:
```
 # docker run -v $(pwd):/output --rm -ti planeturban/docker-flashfloppy
```
