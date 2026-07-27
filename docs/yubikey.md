# YubiKey Integration

## Purpose

This project uses a YubiKey as a standard CCID smart card device accessed through the PC/SC interface.

The objective is to enable existing smart card applications to communicate with the device on Android without requiring application-specific modifications.

## Current Status

The Android PC/SC integration has been verified with a YubiKey using:

- OpenSC
- PKCS#11 tools

The modified Android PC/SC stack successfully exposes the YubiKey through the standard PC/SC interface.

## Design Principles

- Use standard PC/SC interfaces whenever possible.
- Avoid YubiKey-specific modifications.
- Keep compatibility with existing smart card software.
- Preserve upstream project behaviour outside the Android-specific code path.

## Supported Communication Path

```
YubiKey
    ↓
Android USB Permission
    ↓
termux-usb
    ↓
TERMUX_USB_FD
    ↓
libusb
    ↓
libccid
    ↓
pcsc-lite
    ↓
PC/SC Application
```

## Future Applications

The Android PC/SC support developed in this repository can serve as the foundation for future cryptographic applications using YubiKey devices.

Those applications are outside the scope of this repository.
