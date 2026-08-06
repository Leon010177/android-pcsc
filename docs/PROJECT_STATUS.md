# Project Status

## Status

Implementation complete; upstream review pending; maintenance only.

This repository provides the Android/Termux PC/SC infrastructure required to use CCID devices such as YubiKey through the standard PC/SC, OpenSC and PKCS#11 interfaces.

Application-level secure storage, call-recording encryption, chat protection, photo protection, backup workflows and Tasker automation belong to a separate project.

## Verified result

Validated communication path:

Android USB permission
→ termux-usb
→ TERMUX_USB_FD
→ libusb
→ libccid
→ pcsc-lite
→ OpenSC / PKCS#11

Verified with:

- opensc-tool -l
- opensc-tool -a
- pkcs11-tool --list-slots
- pkcs11-tool --list-objects

## Upstream

CCID Merge Request:
https://salsa.debian.org/rousseau/CCID/-/merge_requests/10

PCSC Merge Request:
https://salsa.debian.org/rousseau/PCSC/-/merge_requests/5

Both submissions are currently under upstream review.

## Documentation entry point

Read in this order:

1. README.md
2. docs/PROJECT_STATUS.md
3. docs/architecture.md
4. docs/android-termux.md
5. docs/build-and-test.md
6. docs/handoff/SESSION_HANDOFF_FINAL.md

## Future work

Future application-level security work belongs to a separate repository.
