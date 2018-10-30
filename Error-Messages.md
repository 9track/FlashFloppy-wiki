When an unrecoverable error occurs a message will be displayed on the
LED, LCD, or OLED screen.

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

### `RIB` / `Ribbon Cable Is Upside Down`

Floppy ribbon cable is inserted upside down. Power off and re-insert
the ribbon connector the other way up.

### `USB` / `USB Power Fault`

Over-current condition on the USB port. The port is powered down until
a button is pressed.
