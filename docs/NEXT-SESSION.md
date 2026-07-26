# Next Session Handoff

This document records the exact project state at the end of the previous working session. It is intended to allow development to continue without relying on chat history.

---

# Repository

**GitHub**

https://github.com/Leon010177/android-pcsc

**Local repository**

```text
~/Projects/android-pcsc
```

**Branch**

```text
main
```

The local branch tracks `origin/main`.

---

# Current Status

The Android PC/SC stack is operational using **Termux** and **termux-usb**.

The following components are working together:

- pcsc-lite
- libccid
- OpenSC
- PKCS#11
- termux-usb

Verified hardware:

- Yubico YubiKey (OTP + FIDO + CCID)

---

# Verified Commands

The following commands have been verified successfully:

```sh
opensc-tool -l
opensc-tool -a
pkcs11-tool --list-slots
pkcs11-tool --list-objects
```

Detected reader:

```text
Yubico YubiKey OTP+FIDO+CCID 00 00
```

---

# libccid Changes

Implemented:

- Read the USB file descriptor from `TERMUX_USB_FD`.
- Duplicate the descriptor using `dup()`.
- Wrap the descriptor with `libusb_wrap_sys_device()`.
- Create a synthetic USB device list.
- Skip `libusb_open()` for wrapped devices.
- Prevent freeing the synthetic device list.
- Prevent closing wrapped libusb handles.

Clean patch:

```text
patches/libccid-termux.patch
```

---

# pcsc-lite Changes

Implemented:

- Support startup using the wrapped USB file descriptor.
- Detect only the CCID interface.
- Register the wrapped USB device.
- Disable periodic USB rescanning while operating in wrapped mode.
- Preserve the normal desktop startup path.

Regression fixed:

The normal (non-Termux) startup path correctly calls:

```c
HPRescanUsbBus();
```

Clean patch:

```text
patches/pcsc-lite-termux.patch
```

---

# Last Runtime Observation

A later `termux-usb` launch exited because another `pcscd` instance was already running.

This was **not** caused by a crash in either `libccid` or `pcsc-lite`.

---

# Git Status

Repository successfully initialized.

Initial commit:

```text
54f2da1
Initial repository structure and project documentation
```

Successfully pushed to GitHub.

---

# Next Priorities

1. Verify the repository is clean.

   ```sh
   git status
   ```

2. Review both patch files.

3. Create a reliable startup script.

4. Verify the complete PC/SC stack.

5. Write:

   - `docs/build-guide.md`
   - `docs/troubleshooting.md`

6. Commit each logical change separately.

7. Push every tested commit.

---

# Working Rules

- One command at a time.
- No speculative fixes.
- Inspect output before modifying code.
- Test every change.
- Keep GitHub as the single source of truth.
- Keep patches synchronized with source changes.
