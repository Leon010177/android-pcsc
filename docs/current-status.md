# Current Status

## Project goal

Run pcsc-lite and libccid on Android through Termux and termux-usb without root access.

The implementation should keep upstream behaviour intact where possible and add only the changes required for Android USB access.

## Current state

Project status: **Working prototype**

The complete PC/SC stack is operational with a YubiKey using Android's USB permission model.

Working components:

- pcsc-lite
- libccid
- OpenSC
- PKCS#11
- termux-usb

## Verified functionality

The implementation has been tested successfully with:

- `opensc-tool -l`
- `opensc-tool -a`
- `pkcs11-tool --list-slots`
- `pkcs11-tool --list-objects`

Detected reader:

- Yubico YubiKey OTP+FIDO+CCID

## libccid changes

The libccid USB backend was adapted to accept a USB file descriptor provided by `termux-usb`.

Implemented changes include:

- Read the authorised USB file descriptor from `TERMUX_USB_FD`.
- Duplicate the descriptor with `dup()`.
- Create a libusb device handle with `libusb_wrap_sys_device()`.
- Use a synthetic device list for the wrapped Android USB device.
- Skip `libusb_open()` when the wrapped handle is already available.
- Avoid freeing the synthetic device list through the normal libusb path.
- Avoid closing the wrapped libusb handle through the normal device-close path.

These changes are required because Android grants USB access through an already opened file descriptor instead of allowing normal desktop-style device discovery and opening.

## pcsc-lite changes

The pcsc-lite hotplug implementation was adapted for the Termux USB workflow.

Implemented changes include:

- Support startup with a USB file descriptor supplied through the environment.
- Filter discovered USB interfaces to the CCID interface.
- Register the wrapped USB device during startup.
- Skip periodic USB bus rescanning while operating in Termux wrapped-device mode.
- Preserve the normal `HPRescanUsbBus()` startup path when Termux mode is not active.

The normal non-Termux code path remains available.

## Test environment

- Android
- Termux
- termux-api
- termux-usb
- Yubico YubiKey with OTP, FIDO and CCID interfaces

## Known limitations

- USB permission must be granted through `termux-usb`.
- The current workflow is started through a wrapper script.
- Device reconnection and automatic daemon restart are not yet automated.
- Testing has currently been performed with a YubiKey.
- The build process is not yet fully reproducible from the repository alone.

## Next steps

- Store cleaned patches in the repository.
- Add startup and restart scripts.
- Document the complete build procedure.
- Add troubleshooting documentation.
- Test with additional CCID devices.
