If you have previously flashed the full firmware, you can make future
updates via USB stick.

When instructed to press both buttons, press Prev and Next.  You may
alternatively press Select, or the rotary encoder, if you have them.

- Remove all old ***.upd** files from the root of the USB stick.
- Copy the ***.upd** file from the root of the release archive to the root of
  the USB stick.
- Insert the USB stick into the Gotek and power on with both buttons pressed.
- You should now be in the bootloader (display shows "UPD" or "FF Update
  Flash").
- Release both buttons.
- The latest firmware will be programmed and the Gotek will reboot into it.
- Success!

Errors during update are reported on the LED display:
- **E01** No update file found
- **E02** More than one update file found
- **E03** Update file is invalid (bad signature or size)
- **E04** Update file is corrupt (bad CRC)
- **E05** Flash programming error
- **Fxx** FatFS error (probably bad USB drive or filesystem)

## Updating the Bootloader

The main bootloader can also be updated by USB stick. Note that it is
important for this operation to succeed, otherwise the Gotek will require
a full reflash by following the steps in
[Initial Programming](#Firmware-Programming). Therefore make sure the
Gotek has a stable power supply and a known good USB stick.

New features and bugfixes are rare. In general **you do not need to
update the bootloader** and can skip these steps.

- Remove all old ***.upd** files from the root of the USB stick.
- Copy the ***.upd** file from the **alt/bootloader/** subfolder of the
  release archive to the root of the USB stick.
- Insert the USB stick into the Gotek and power on with both buttons pressed.
- You should now be in the old bootloader (display shows "UPD" or
  "FF Update Flash").
- Release both buttons.
- The latest bootloader will be programmed and the Gotek will reboot into it.
- The display should again show "UPD" or "FF Update Flash".
- Remove the USB stick and follow the steps for normal firmware update.

In the extremely unlikely case that an error occurs during update,
"ERR" will be displayed. At this point the Gotek will require a
[full reflash](#Firmware-Programming) as the old bootloader has been
erased.
