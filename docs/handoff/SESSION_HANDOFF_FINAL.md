# android-pcsc upstream handoff

## Date

2026-08-05

## Main project

Repository:

https://github.com/Leon010177/android-pcsc

Local path:

~/Projects/android-pcsc

## Project goal

Prepare and upstream Android/Termux USB support for the PC/SC stack.

The implementation consists of two independent upstream contributions:

- libccid
- pcsc-lite

Android USB access is provided through the TERMUX_USB_FD file descriptor supplied by termux-usb.

---

# libccid

Upstream repository:

https://salsa.debian.org/rousseau/CCID

Local repository:

~/Projects/upstream-libccid

Branch:

termux-usb-fd

Commit:

33dcfa0

Patch:

0001-libccid-support-Termux-USB-file-descriptors.patch

Status:

- Patch rebased onto current upstream
- Commit created
- format-patch created
- Modified source compiles successfully
- Branch pushed to Salsa fork
- Merge Request submitted

Merge Request:

https://salsa.debian.org/rousseau/CCID/-/merge_requests/10

---

# pcsc-lite

Upstream repository:

https://salsa.debian.org/rousseau/PCSC

Local repository:

~/Projects/upstream-pcsc-lite

Branch:

termux-usb-fd

Commit:

367ad6e9

Patch:

0001-pcsc-lite-support-Termux-USB-file-descriptors.patch

Status:

- Patch rebased onto current upstream
- Commit created
- format-patch created
- Modified source compiles successfully
- Branch pushed to Salsa fork
- Merge Request submitted

Merge Request:

https://salsa.debian.org/rousseau/PCSC/-/merge_requests/5

---

# Validation already completed

Validated successfully on Android/Termux with a physical YubiKey.

Verified using:

- pcscd started with termux-usb
- opensc-tool -l
- opensc-tool -a
- pkcs11-tool --list-slots
- pkcs11-tool --list-objects

---

# Known unrelated upstream issues

libccid:

Android does not provide issetugid().

This is unrelated to the TERMUX_USB_FD patch.

pcsc-lite:

Android does not provide secure_getenv()/issetugid().

This is unrelated to the TERMUX_USB_FD patch.

These portability issues must stay separate from the submitted Merge Requests.

---

# Current upstream status

Both Merge Requests are OPEN.

Current work is finished.

Do not modify the submitted commits unless upstream review requires a new revision.

---

# Next session

1. Check both Merge Requests for comments.
2. Respond to maintainer feedback.
3. If changes are requested, prepare v2 patches.
4. If accepted, record merge commits.
5. Update android-pcsc documentation after upstream review.

---

# Files to upload next session

Upload only:

- SESSION_HANDOFF_FINAL.md

Then write:

Turpinām darbu.