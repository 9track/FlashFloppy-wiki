When an unrecoverable error occurs a message will be displayed on the
LED, LCD, or OLED screen.

### `Fnn` / `*FAT*nn*` / `*FATFS* nn`

A 2-digit error code defined by the FatFS library. Usually indicates
bad physical media or a bad filesystem. Try formatting or replacing
your USB drive.

### `Enn` / `*ERR*nn*` / `*ERROR* nn`

A 2-digit error code defined by the FlashFloppy firmware:
- **30** Disk Full: Some writes were lost. Delete some files or use a
  larger USB drive.
- **31** Bad Image File: The selected image is invalid or
  unsupported.

### `USB` / `USB Power Fault`

Over-current condition on the USB port. The port is powered down until
a button is pressed.
