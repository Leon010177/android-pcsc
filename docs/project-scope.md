# Project Scope

## Purpose

This project adds Android/Termux support to the standard PC/SC stack by enabling `pcsc-lite` and `libccid` to use USB devices through `termux-usb` and the `TERMUX_USB_FD` file descriptor.

The goal is to make CCID smart card devices, such as YubiKey, usable on Android without requiring root privileges while keeping the implementation as close as possible to the upstream projects.

## Scope

This repository focuses on:

- Android support for `pcsc-lite`
- Android support for `libccid`
- USB access through `termux-usb`
- Maintaining compatibility with existing Linux behaviour
- Reproducible builds and testing
- Clear technical documentation

## Out of Scope

This repository does not contain end-user applications or automation.

Examples include:

- Tasker workflows
- Call recording automation
- File encryption automation
- Backup workflows
- User interface components

These projects are intended to build on top of the Android PC/SC support provided here.

## Long-Term Vision

The work in this repository provides a reusable Android PC/SC foundation for hardware-backed cryptographic applications.

The long-term objective is to enable secure Android workflows based on YubiKey devices, allowing future projects to build reliable encryption and authentication solutions on top of a standard PC/SC interface.
