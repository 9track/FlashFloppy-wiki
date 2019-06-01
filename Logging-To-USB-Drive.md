
In some cases, the FlashFloppy firmware can give diagnostic
information when you experience problems or performance issues. The
FlashFloppy release archive includes an alternative firmware with
diagnostic logging which is written to the file FFLOG.TXT on the USB
drive.

### Programming the Alternative Firmware

Follow steps for [Firmware Update](Firmware-Update) but use the update
file contained in the **alt/logfile** subfolder of the FlashFloppy
distribution.

**NOTE:** Please update back to the normal firmware after diagnosing
your issue.

### Using the Alternative Firmware

Logging is cached in a 2kB RAM buffer and flushed to the USB drive only
when a disk image is inserted or ejected. Thus to diagnose an issue:
1. Reproduce the issue
2. Eject the disk image (eg. navigate to another image)
3. Finally, pull the USB drive to inspect FFLOG.TXT

If you fail to follow these steps in this order, the cached logging may be lost.
