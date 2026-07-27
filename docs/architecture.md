# Architecture

## Overview

The project adapts the standard Linux PC/SC stack to Android by replacing direct USB device access with the Android USB permission model provided by `termux-usb`.

Instead of discovering and opening USB devices through the Linux USB subsystem, Android applications receive an already-authorised USB file descriptor (`TERMUX_USB_FD`), which is then wrapped into a libusb device.

## Data Flow

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
(OpenSC, PKCS#11, etc.)
```

## Components

### termux-usb

Obtains Android USB permission and exports the authorised USB file descriptor through the `TERMUX_USB_FD` environment variable.

### libusb

Wraps the Android USB file descriptor using `libusb_wrap_sys_device()` and exposes a standard libusb device interface.

### libccid

Uses the wrapped libusb device instead of performing normal Linux USB discovery.

### pcsc-lite

Provides the standard PC/SC service used by smart card applications.

## Design Principles

- Keep Android-specific changes isolated.
- Preserve upstream Linux behaviour whenever possible.
- Avoid unnecessary platform-specific code.
- Keep the modified execution path simple and easy to debug.
