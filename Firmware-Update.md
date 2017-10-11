If you have previously flashed the full firmware, you can make future
updates via USB stick.

- Remove all old *.UPD files from the root of the USB stick.
- Copy the *.UPD file from the root of the release archive to the root of
  the USB stick.
- Insert the USB stick into the Gotek and power on with both buttons pressed.
- You should now be in the bootloader ("UPD"). Release both buttons.
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
[Initial Programming](#initial-programming). Therefore make sure the
Gotek has a stable power supply and a known good USB stick.

New features and bugfixes are rare. In general **you do not need to
update the bootloader** and can skip these steps.

**I repeat: do not follow these steps unless you are sure of what you are
doing.**

- **Program the 'Reloader'**
  - Remove all old *.UPD and *.RLD files from the USB stick.
  - Copy the contents of the release's reloader/ folder to the root of
  the USB stick.
  - Insert the USB stick into the Gotek and power on with both buttons
  pressed.
  - You should now be in the bootloader ("UPD"). Release both buttons.
  - The 'reloader' will be programmed and the Gotek will reboot into it.
- **Program the latest Bootloader**
  - You should now be in the reloader ("RLD"). Press and release both buttons.
  - The latest bootloader will be programmed. The Gotek will then reboot.
- **Program the latest Main Firmware**
  - You are now in the reloader again. Power off.
  - Remove the *.UPD and *.RLD files from the USB stick.
  - Copy the *.UPD file from the root of the release archive to the USB
  stick.
  - Insert the USB stick into the Gotek and power on with both
  buttons pressed.
  - You should now be in the bootloader ("UPD"). Release both buttons.
  - The latest firmware will be programmed and the Gotek will reboot into it.
- **Success!**
