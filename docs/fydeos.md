# FydeOS — the option built for this exact machine

FydeOS publishes a **device-specific image for the Surface Go (1st gen, 2018)**.
Not "should work on most x86 tablets" — a build named after this device, in a list
alongside the Surface Go 2, 3 and 4, which are kept as separate entries.

That is a level of attention no other option on this list gives the Surface Go 1,
and it is the reason this page exists.

## What FydeOS is

FydeOS is a ChromiumOS-derived operating system from a company of the same name.
It gives you the ChromeOS experience — fast boot, a touch-first shell, sandboxed
apps — on hardware Google never shipped ChromeOS on.

The distinction that matters here, and the reason it beats the obvious comparison:

| | ChromeOS Flex (Google) | FydeOS |
|---|---|---|
| Android apps | **No** — Google states it supports only "the deployment of some Android VPN apps" | **Yes** — "FydeOS supports Web, Android, and Linux apps seamlessly" |
| Stylus / active pen | **Not supported** ([Google's own list](https://support.google.com/chromeosflex/answer/11542901)) | Not stated; verify in the trial |
| Device-specific build for Surface Go 1 | No | **Yes** |
| Price | Free | 90-day trial, then a per-device licence |

**On a Surface, "no pen and no Android apps" removes most of the point.** ChromeOS
Flex is free and it is the wrong free thing for this device. That comparison is
why FydeOS deserves its own page rather than a line in a table.

## The editions, and what each costs

Taken from [FydeOS's pricing page](https://fydeos.io/pricing/) — read it yourself
before buying, prices change and this page does not.

| Edition | What it is | Cost |
|---|---|---|
| **FydeOS for You** | The device-specific build. Described by FydeOS as "our customized version for some designated devices. It has better adaptability and supports some device-specific functions." | **90 days free**, then "Perpetual license with 1 year of service, £14.99" |
| **FydeOS for PC / SBC** | The generic build for any x86 machine | "Free-ish" — with "£3.19 for major version upgrades via OTA" |
| **[openFyde](https://openfyde.io)** | The open-source upstream | Free. You build it yourself |

**Say the quiet part out loud: FydeOS for You is not free.** Most articles that
recommend it omit this. It is a 90-day trial followed by a per-device purchase —
£14.99 at the time of writing, one-off, not a subscription. On a machine you were
going to throw away, that is cheap. It is still a cost that Linux does not have,
and it is per device.

**openFyde is the no-licence route.** Same lineage, source available, and you
compile it. The price is your time, and building a ChromiumOS derivative is not a
weekend for someone who has not done it before. It is a real option for someone
who wants FydeOS's approach without the licence, and a poor one for someone who
just wants a working tablet on Saturday.

## Why it is credible on *this* device specifically

FydeOS's Android subsystem has a hardware requirement. From their
[Android apps documentation](https://fydeos.io/help/knowledge-base/getting-started/application-support/running-android-apps/):

- GPU: **"Intel series graphics cards or AMD Radeon series graphics cards"**.
  NVIDIA is not supported.
- CPU: **"Support SSE4.2 instruction set. Generally, Intel and AMD CPUs released
  after 2011 support SSE4.2."**

The Surface Go 1 has an **Intel HD Graphics 615** and a **Pentium Gold 4415Y**
(Kaby Lake, 2017). It satisfies both. This is not a machine where the Android
subsystem is a maybe — it is exactly the hardware class FydeOS targets.

That is worth stating plainly, because the same requirement is what makes FydeOS
a non-starter on plenty of other second-hand hardware.

## What FydeOS does not tell you, and what to do about it

The [Surface Go device page](https://fydeos.io/download/device/surface-go/) offers
the image — version 22.1 at the time of writing — and links to an installation
guide. **It does not publish a per-feature hardware support matrix.** There is no
official statement on this page about whether the touchscreen, the pen, the Type
Cover, the cameras or sleep behave correctly on the Surface Go 1.

This repository is not going to invent one.

The Surface Go's touchscreen uses IPTS, which needs specific driver work (see
[hardware.md](hardware.md)) — a device-specific build is exactly where you would
expect that work to have been done, and FydeOS maintains a
[board overlay for the Surface Go](https://github.com/FydeOS-for-You-overlays/overlay-surface-go)
(GPL-2.0; last commit 2020, so treat it as historical rather than as the live
source). But "would expect" is not "verified", and this page will not pretend
otherwise.

**The 90-day trial is the answer to this.** It is long enough to settle every
open question at zero cost, which is unusually generous and materially changes
the risk of choosing FydeOS. Do not pay before you have checked, in this order:

1. **Touchscreen** — the whole point of the device.
2. **Pen**, if you use one.
3. **Type Cover** keyboard and trackpad.
4. **Battery percentage**, and drain overnight with the lid closed.
5. **Wi-Fi and Bluetooth.**
6. **The Android apps you actually need.** See the warning below.
7. **Cameras** — assume they do not work. The IPU3 pipeline is the same dead end
   it is everywhere else, and a ChromiumOS derivative has no special access to a
   solution mainline Linux does not have. If they do work, that is a pleasant
   surprise worth reporting in an issue here.

## The Android apps warning, again

FydeOS's documentation does not state that Google Play is included. It describes
installing apps from the **FydeOS Store**, or — with Developer Mode enabled —
that you can "install an Android app store of your choice."

That phrasing should be read carefully. It is the same situation as
[BlissOS](android.md): **apps gated on Play Integrity — many banking apps, some
streaming services — are likely to refuse to run.** If your reason for wanting
Android is one specific app, install FydeOS in the trial and test *that app*
before anything else. Not the concept of Android apps. That app.

## Practical notes

- The image ships as a raw disk image (`.bin`, zipped) rather than an ISO. Most
  flashing tools take it directly; if yours insists on an ISO, use one that does
  not.
- Everything in [before-you-start.md](before-you-start.md) applies unchanged:
  retrieve your BitLocker recovery key and suspend encryption **before** touching
  Secure Boot, and make a Surface recovery USB you have actually booted.
- FydeOS is a proprietary build from a single company. openFyde is the escape
  hatch if that matters to you — and it is a real one, which is more than most
  proprietary OSes offer.

## Sources

Every claim on this page comes from one of these:

- [FydeOS — home](https://fydeos.io/) — "FydeOS supports Web, Android, and Linux apps seamlessly"
- [FydeOS for You — device list](https://fydeos.io/download/you/) — "our customized version for some designated devices"
- [FydeOS for You — Microsoft Surface Go](https://fydeos.io/download/device/surface-go/)
- [FydeOS — pricing](https://fydeos.io/pricing/) — trial length, £14.99, openFyde link
- [FydeOS — running Android apps](https://fydeos.io/help/knowledge-base/getting-started/application-support/running-android-apps/) — GPU and CPU requirements
- [openFyde](https://openfyde.io)
- [Google — ChromeOS Flex vs ChromeOS](https://support.google.com/chromeosflex/answer/11542901) — Android VPN apps only, no stylus support
- [FydeOS-for-You-overlays/overlay-surface-go](https://github.com/FydeOS-for-You-overlays/overlay-surface-go)
