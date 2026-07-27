# Security Model

## Purpose

This repository provides the infrastructure required to use standard PC/SC smart card devices on Android through `termux-usb`.

It does not implement cryptographic applications itself.

## Trust Model

The project relies on the following trusted components:

- Android USB permission system
- `termux-usb`
- `libusb`
- `pcsc-lite`
- `libccid`
- The smart card device (for example, a YubiKey)

The repository does not attempt to replace or bypass Android's security model.

## Security Principles

- USB access is granted only after Android authorises the device.
- No root privileges are required.
- Android-specific code is isolated from the normal Linux code path.
- Existing PC/SC APIs remain unchanged for applications.

## Non-Goals

This repository does not provide:

- encrypted storage
- key management
- PIN management
- authentication workflows
- file encryption
- secure backup
- application-level security policies

These capabilities are expected to be implemented by applications that use the Android PC/SC layer provided by this project.
