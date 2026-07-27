# Architecture Decisions

This document records important design decisions made during the development of the Android PC/SC implementation.

## Android USB access

Android does not allow desktop-style USB device discovery and opening.

Instead, USB access is granted through an already authorised file descriptor obtained from `termux-usb`.

The implementation therefore adapts the USB stack to operate on the supplied file descriptor while keeping the normal upstream behaviour unchanged whenever Termux mode is not active.

## Minimal upstream changes

The project intentionally minimizes modifications to upstream source code.

Android-specific behaviour is isolated behind explicit runtime checks so that the normal Linux code path remains unchanged.

## Repository scope

This repository focuses only on Android PC/SC support.

Applications built on top of this infrastructure are intentionally outside the scope of this project.
