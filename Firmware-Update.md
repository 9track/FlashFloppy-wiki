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

## Old Method to Update the Bootloader (before v2.11a)

When instructed to press both buttons, press Prev and Next.  You may
alternatively press Select, or the rotary encoder, if you have them.

- **Program the 'Reloader'**
  - Remove all old ***.upd** and ***.rld** files from the USB stick.
  - Copy the contents of the release's **reloader/** folder to the root of
  the USB stick.
    - **[v2.x]** Please note the folder has moved to **alt/reloader**
  - Insert the USB stick into the Gotek and power on with both buttons
  pressed.
  - You should now be in the bootloader ("UPD"). Release both buttons.
  - The 'reloader' will be programmed and the Gotek will reboot into it.
- **Program the latest Bootloader**
  - You should now be in the reloader ("RLD"). Press and release both buttons.
  - The latest bootloader will be programmed. The Gotek will then reboot.
- **Program the latest Main Firmware**
  - You are now in the reloader again. Power off.
  - Remove the ***.upd** and ***.rld** files from the USB stick.
  - Copy the ***.upd** file from the root of the release archive to the USB
  stick.
  - Insert the USB stick into the Gotek and power on with both
  buttons pressed.
  - You should now be in the bootloader ("UPD"). Release both buttons.
  - The latest firmware will be programmed and the Gotek will reboot into it.
- **Success!**

### Aside: What these steps do

Some people get confused by the above sequence of steps and it might
help to give them a mental model of what's going on. First, realise
that the Flash memory contains two programs: the **Bootloader** and
the **Main Firmware**. The Bootloader's sole purpose is to allow
update of the Main Firmware. The Main Firmware of course runs the
floppy-drive emulation, and doesn't know how to update anything. The
trick in updating the Bootloader is to replace the Main Firmware with
an alternative program (the **Reloader**) whose sole purpose is to
update the Bootloader.

The main sequence of steps in updating the Bootloader is then:

- **Old Bootloader** overwrites **Old Main Firmware** with **Reloader**
- **Reloader** overwrites **Old Bootloader** with **New Bootloader**
- **New Bootloader** overwrites **Reloader** with **New Main Firmware**
