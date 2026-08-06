# Android PC/SC for Termux

> **Status:** Implementation complete; upstream review pending.
>
> **Start here:** docs/PROJECT_STATUS.md

## Overview

This project provides Android support for the standard PC/SC smart card stack by adapting `pcsc-lite` and `libccid` to work with Android's USB permission model through `termux-usb`.

The goal is to make standard CCID smart card devices, such as YubiKey, usable on Android without requiring root privileges while keeping modifications to upstream projects as small as possible.

## Current Status

Current status: **Working prototype**

Verified components:

- Android USB transport (`termux-usb`)
- libusb
- libccid
- pcsc-lite
- OpenSC
- PKCS#11

Verified hardware:

- Yubico YubiKey (OTP + FIDO + CCID)

## Architecture

```
YubiKey
    │
    ▼
Android USB Manager
    │
    ▼
termux-usb
    │
    ▼
TERMUX_USB_FD
    │
    ▼
libusb_wrap_sys_device()
    │
    ▼
libccid
    │
    ▼
pcsc-lite
    │
    ▼
PC/SC applications
```

## Features

- Android USB support without root
- Standard PC/SC interface
- Minimal upstream modifications
- Android-specific code isolated from the normal Linux path
- Standard OpenSC and PKCS#11 compatibility

## Repository Layout

```
patches/    Android support patches
docs/       Project documentation
README.md   Project overview
```

## Documentation

- `docs/project-scope.md`
- `docs/architecture.md`
- `docs/android-termux.md`
- `docs/security-model.md`
- `docs/yubikey.md`
- `docs/build-and-test.md`
- `docs/current-status.md`
- `docs/roadmap.md`

## Current Limitations

- USB permission must be granted through `termux-usb`
- Build process is still being documented
- Tested primarily with YubiKey
- Additional CCID device testing is planned

## Roadmap

See:

```
docs/roadmap.md
```

## License

This repository currently contains development work intended for future upstream contribution.
