# Current Status

## Project Goal

Provide Android support for the standard PC/SC stack by enabling `pcsc-lite` and `libccid` to operate through Android's USB permission model without requiring root access.

## Current State

Project status: **Working prototype**

The complete PC/SC stack is operational on Android using Termux and `termux-usb`.

Verified components:

- termux-usb
- libusb
- libccid
- pcsc-lite
- OpenSC
- PKCS#11

Verified hardware:

- Yubico YubiKey (OTP + FIDO + CCID)

## Verified Commands

The following commands have been tested successfully:

```sh
opensc-tool -l
opensc-tool -a
pkcs11-tool --list-slots
pkcs11-tool --list-objects
```

## Current Limitations

- USB permission must be granted through `termux-usb`.
- The build procedure is not yet fully reproducible from the repository alone.
- Startup and reconnection automation are still under development.
- Testing has primarily been performed with a YubiKey.

## Related Documentation

Implementation details are documented in:

- `docs/android-termux.md`
- `docs/architecture.md`
- `docs/build-and-test.md`

## Next Milestones

- Complete code cleanup.
- Finalize reproducible build documentation.
- Expand testing with additional CCID devices.
- Prepare patches for upstream review.
