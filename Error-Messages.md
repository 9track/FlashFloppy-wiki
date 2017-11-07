When an unrecoverable error occurs a message will be displayed on the
LED, LCD, or OLED screen. Usually this will be of the form `Enn`,
`*ERR*nn*`, or `*ERROR* nn` where nn is a 2-digit number:

- **01-19 FAT/Media Errors:** If these occur repeatedly it is usually
  caused by bad physical media or a bad filesystem. Try formatting or
  replacing your USB drive.
- **30 Disk Full:** Some writes were lost. Delete some files or use a
  larger USB drive.
- **31 Bad Image File:** The selected image is invalid or
  unsupported.

Other error messages:
- `USB`/`USB Power Fault`: Over-current condition on the USB port. The
  port is powered down until a button is pressed.
