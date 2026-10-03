<div align="center">

# Android ID and Emulator Hider

**Spoof device identity. Hide root and Xposed. Pass the check.**

An Xposed/LSPosed module, by [DroidRooter](https://droidrooter.com).

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#compatibility)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

</div>

---

## Why Android ID and Emulator Hider

Plenty of apps refuse to run, or quietly limit themselves, the moment they
think the device is an emulator, rooted, or running a hook framework. This
module changes what those checks see — at both the Java and native layer —
so the app behaves as it would on an untouched retail phone.

- Pick from **12 real device profiles** (Pixel, Galaxy, POCO, OnePlus, Redmi,
  Nothing), each built from a verified GSMA IMEI allocation and a real
  factory build fingerprint — not invented values.
- Toggle each protection independently, per app, from one screen.
- Run **Device Check** to see, live, exactly what a scanning app would read
  off your device right now.

Core masking is free, always. A one-time purchase unlocks custom profiles,
safe mode, and a few extra identifiers — see **Unlock Pro** in the app.

## What it covers

| Protection | What it changes |
|---|---|
| Device identity | Model, brand, manufacturer, fingerprint, build props, Android ID, serial |
| Emulator traces | qemu/goldfish properties, files, kernel driver names, `/proc/mounts` |
| Processor | ABI list, `os.arch`, and the raw `/proc/cpuinfo` vendor/model (x86 hosts) |
| Graphics | GPU vendor and renderer string |
| Sensors | Sensor names and vendors |
| Battery | Level, health, status, capacity, sysfs values |
| Input devices | Device names, `/proc/bus/input/devices` |
| Phone radio | IMEI, IMSI, SIM operator/country, line number, baseband version |
| Camera | Camera count and facing (front/back), per camera ID |
| Location | Fallback for apps that query last-known location and get nothing back |
| Root | `su`, Magisk, KernelSU and related binaries/paths; `ro.debuggable`/`ro.secure` |
| Xposed | LSPosed/Vector traces in `/proc/self/maps`, package manager, logcat |

## Requirements

- A rooted device with an LSPosed-compatible framework that supports the
  modern **libxposed API 102**, such as [LSPosed](https://github.com/LSPosed/LSPosed)
  or [Vector](https://github.com/JingMatrix/Vector).
- Android 8.0 or newer.

> [!IMPORTANT]
> This module is built on the modern libxposed API. Legacy Xposed and
> EdXposed are not supported.

## Installation

1. Download the latest APK from [Releases](../../releases/latest) and install it.
2. Open your Xposed manager, enable **Android ID and Emulator Hider**, and add
   it to scope — **it needs itself in scope** to protect its own Device Check
   screen, in addition to any app you want protected.
3. Force-stop and reopen each app you've scoped.

## Usage

1. Open the app. The status card at the top says **Protected** once the
   framework has hooked the process.
2. Pick a device profile — Pixel 8, Galaxy S24, POCO X3 Pro, and nine others.
3. Toggle individual protections on or off under **Protection**.
4. Tap **Device Check** to see exactly what a scanning app would read —
   build props, fingerprint, CPU, sensors, battery — compared against the
   active profile, live.

## Compatibility

| Android | API | Status |
|---|---|---|
| 16 | 36 | Verified on a real device |
| 15 | 35 | Verified on a real device |
| 14 | 34 | Verified on a real device and emulator |
| 13 | 33 | Verified on a real device |
| 12 and below | 31 and below | Supported (minSdk 26), not independently verified |

"Verified" means the module was installed, scoped, and confirmed active (hooks
firing, no crashes) on that Android version during development.

## FAQ

**Does this make a real device look like an emulator, or an emulator look
like a real device?**
Either. The masking is identity-based, not environment-based — it changes
what Java/native APIs report, regardless of what's actually running
underneath.

**Will this bypass Play Integrity or SafetyNet?**
No. Hardware attestation is backed by the device's TEE/StrongBox and is out
of reach for a userspace Xposed hook — that needs a separate, dedicated
approach entirely.

**Why do I need to scope the app to itself?**
Without it, the app's own process is never hooked, so its Device Check
screen would show your device's real values instead of the active profile's
— making the one feature meant to verify the masking give a false reading.

**Can I use a profile that doesn't match my phone's real hardware (e.g. ARM
profile on an x86 emulator)?**
Yes — every profile masks the processor, so Build.SUPPORTED_ABIS, `os.arch`,
and the raw `/proc/cpuinfo` vendor string all switch to match the profile,
not the host.

## Limits

- Anything that doesn't go through a hooked Java/native API — raw sockets,
  server-side checks, hardware attestation — sees the real device.
- Changes apply the next time a protected app launches; an already-running
  app needs a restart.
- This repository hosts releases only. Source is closed.

## Disclaimer

This module is meant for privacy, testing, and compatibility with your own
apps. You are responsible for how you use it. Do not use it to break an
app's terms, get around paid services, or defraud anyone. The software is
provided as is, without warranty.

## Acknowledgements

- [libxposed](https://github.com/libxposed) for the modern Xposed API and
  service library.
- [LSPosed](https://github.com/LSPosed/LSPosed) and
  [Vector](https://github.com/JingMatrix/Vector) for the frameworks it runs on.

## From DroidRooter

Android ID and Emulator Hider is a project of **DroidRooter**, a small team
building tools for rooted Android.

- **Website:** [droidrooter.com](https://droidrooter.com)
- **Telegram:** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook:** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM, DroidRooter's virtual camera:**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) feeds your
  own video or images to apps in place of the camera.
- **VirtualNet, DroidRooter's per-app network spoofer:**
  changes what apps are told about your Wi-Fi/mobile connection, open source.
- **Smali Patcher Reborn:** patches your ROM's `services.jar` on-device
  (Magisk/KernelSU/APatch) for mock location and secure windows, Android 10–17 —
  successor to Smali Patcher / SmaliPatcherEx.

If this app helps you, follow DroidRooter for more.

## License

Proprietary — all rights reserved. Binary distribution only; source is not
published.
