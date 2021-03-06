When an unrecoverable error occurs a message will be displayed on the
LED, LCD, or OLED screen.

### `F-F` / `FlashFloppy vx.y`

This is not explicitly an error code or condition, but the default display
if a valid USB stick is not inserted. Make sure your USB stick is properly
inserted, legacy partitioned (MBR rather than GPT) and FAT32 formatted.

### `Fnn` / `*FAT*nn*` / `*FATFS* nn`

A 2-digit error code defined by the FatFS library.

In HxC Compatibility mode this probably means you have stale slot
assignments in HXCSDFE.CFG. You should copy a fresh version of
HXCSDFE.CFG to your USB stick and reassign slots using the Autoboot
file selector.

In other cases this error usually indicates bad physical media or a bad
filesystem. Try formatting or replacing your USB drive.

### `Enn` / `*ERR*nn*` / `*ERROR* nn`

A 2-digit error code defined by the FlashFloppy firmware:
- **30** Disk Full: Some writes were lost. Delete some files or use a
  larger USB drive.
- **31** Bad Image File: The selected image is invalid or
  unsupported.
- **32** Bad HXCSDFE.CFG: The config file is invalid or unsupported.
  Copy a fresh version to the USB drive.
- **33** Bad IMAGE_A.CFG: The last-image file has become corrupted.
  Delete it from the USB drive and it will be automatically recreated.
- **34** No entries to navigate:
  - Direct Navigation mode found no valid directories or image files
  to display. Add some valid image files to the USB drive. Subfolders
  are accessible only when using an LCD/OLED display.
  - Indexed mode found no valid DSKA\*.\* image names. Add some valid
  image files to the USB drive.
- **35** Path too deep: Folders are nested too deeply to navigate.

### `RIB` / `Ribbon Cable May Be Upside Down?`

Floppy ribbon cable is inserted upside down. Power off and re-insert
the ribbon connector the other way up.

More rarely, this can occur when the Gotek is powered separately from,
and earlier than, the host machine. In this case the error will clear
automatically when the host machine is powered on. It is recommended
to avoid powering on the Gotek after the host machine.

### `USB` / `USB Power Fault`

Over-current condition on the USB port. The port is powered down until
a button is pressed.
