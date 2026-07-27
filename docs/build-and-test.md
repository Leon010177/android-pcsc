# Build and Test

## Build

The current implementation is built on Android using Termux.

The repository contains the patches required to adapt the upstream projects for Android USB access through `termux-usb`.

The complete build process is still being documented and is not yet fully reproducible from the repository alone.

## Runtime requirements

The current implementation requires:

- Android device
- Termux
- termux-api
- termux-usb
- pcsc-lite
- libccid
- OpenSC

USB permission must be granted through Android before starting the PC/SC stack.

## Testing

The following commands have been verified successfully:

```sh
opensc-tool -l
opensc-tool -a
pkcs11-tool --list-slots
pkcs11-tool --list-objects
```

Successful execution confirms that:

- the USB transport is operational;
- the PC/SC stack is functioning correctly;
- the PKCS#11 interface is available.

## Current limitations

The build procedure is still being cleaned up before publication.

Additional testing with different CCID devices is planned.
