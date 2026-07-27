# Android / Termux Support

## Overview

Android does not provide direct access to USB devices in the same way as a standard Linux system.

Instead, USB permission is granted through the Android USB framework. The `termux-usb` utility exposes an authorised USB file descriptor through the `TERMUX_USB_FD` environment variable.

This project adapts the standard PC/SC stack to use that file descriptor instead of performing normal Linux USB device discovery.

## Android-Specific Changes

### libusb

The Android USB file descriptor is converted into a standard libusb device by using:

- `libusb_wrap_sys_device()`

This allows the remainder of the software stack to continue using the normal libusb API.

### libccid

`libccid` was modified to:

- detect `TERMUX_USB_FD`
- duplicate the supplied file descriptor
- wrap it with `libusb_wrap_sys_device()`
- bypass normal Linux USB opening
- avoid closing wrapped Android handles incorrectly
- preserve the original Linux code path when Android support is not active

### pcsc-lite

`pcsc-lite` was modified to:

- recognise the Android USB path
- avoid Linux USB enumeration when `TERMUX_USB_FD` is available
- initialise the reader using the wrapped libusb device
- preserve the original Linux behaviour when Android support is not enabled

## Design Goals

The Android implementation follows several principles:

- minimise changes to upstream projects
- isolate Android-specific code
- preserve compatibility with existing Linux systems
- keep the execution path simple to debug
- avoid platform-specific behaviour outside the Android code path

## Verification

The modified implementation has been verified using:

- OpenSC
- PKCS#11 tools

The Android PC/SC stack successfully exposes a YubiKey through the standard PC/SC interface without requiring root privileges.
