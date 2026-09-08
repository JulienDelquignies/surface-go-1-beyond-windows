# Hardware reality check

What is actually inside a Surface Go 1st generation, and which parts make life hard
for anything that isn't Windows.

## Specifications

| | |
|---|---|
| **Released** | August 2018 |
| **Models** | 1824 (Wi-Fi), 1825 (LTE) |
| **CPU** | Intel Pentium Gold 4415Y — 2 cores / 4 threads, Kaby Lake, 1.6 GHz, 6 W TDP |
| **GPU** | Intel HD Graphics 615 (Gen9) |
| **RAM** | 4 GB or 8 GB LPDDR3, soldered |
| **Storage** | 64 GB **eMMC**, or 128/256 GB SSD (M.2 2230, technically replaceable) |
| **Display** | 10 inch, 1800 × 1200, 3:2, 217 ppi, 10-point touch |
| **Pen** | Surface Pen (MPP), via IPTS |
| **Wi-Fi / BT** | Marvell AVASTAR — Wi-Fi 5 + Bluetooth 5 |
| **Cameras** | 5 MP front (Windows Hello IR), 8 MP rear — Intel IPU3 pipeline |
| **Ports** | 1 × USB-C, Surface Connect, 3.5 mm, microSD, Surface Type Cover connector |

The CPU is the reason for everything that follows: the Pentium Gold **4415Y** is not
on Microsoft's Windows 11 supported processor list — the lowest supported Pentium Gold
is the **4425Y**. One model number away. There is no BIOS update, TPM setting or
registry key that changes this in a supported way.

## The four hostile parts

### 1. The touchscreen — IPTS

This is the single most important fact on this page.

The Surface Go does not expose its touchscreen as a standard USB HID device. It uses
**Intel Precise Touch & Stylus (IPTS)**, where raw capacitive data is delivered to the
host and processed in software. On Windows, that software is a Microsoft driver. On
anything else, it requires:

- a kernel driver (`ipts` / `ithc`, from the [`linux-surface`](https://github.com/linux-surface/linux-surface) project), **and**
- a userspace daemon, `iptsd`, which turns raw data into touch and pen events.

Neither is in a mainline kernel. **This is why every generic "install Linux/Android on
any x86 tablet" guide produces a tablet with no working touch.**

### 2. The Surface Aggregator Module

Surface devices route a surprising amount through an embedded controller called SAM
(Surface Aggregator Module / SSAM): the Type Cover keyboard and trackpad, battery
reporting, thermal sensors, some of the power management.

Without the `surface-aggregator` drivers — again from `linux-surface`, and merged into
mainline only progressively — you get a tablet with no keyboard and no battery
percentage. On the Surface Go 1 specifically, the Type Cover works once those drivers
are in place.

### 3. The cameras

The front and rear cameras go through Intel's **IPU3** image processing unit. This has
been a known dead end on Linux for years: the kernel driver exists, but the sensor
drivers, tuning data and userspace pipeline needed to produce a usable image are not
there for this hardware.

The `linux-surface` device matrix lists cameras as **not working** on the Surface Go 1.
Treat this as permanent. If you need the cameras, you need Windows.

### 4. Modern standby only

The Surface Go 1 supports **S0ix** (modern standby) and not S3 (suspend-to-RAM). This
is a firmware decision, not a configuration.

S0ix requires the OS to actively put every component into a low-power state. Windows
does this. Linux does it partially, and how well depends on the kernel version and the
distro's tuning. The practical symptom is battery drain while the lid is closed —
sometimes acceptable, sometimes 10 % overnight. The `linux-surface` kernel improves
this substantially over a stock kernel, but it is the part of the experience most
likely to disappoint.

A footnote in the `linux-surface` device matrix is worth knowing: the Marvell Wi-Fi/BT
chip has a **firmware bug that prevents system power saving when any Bluetooth Low
Energy device is paired**. If your battery drains overnight, unpair your BLE mouse
before blaming the kernel.

## What the linux-surface project reports for Surface Go 1

Summarised from the project's [supported devices matrix](https://github.com/linux-surface/linux-surface/wiki/Supported-Devices-and-Features)
— check it yourself, it is maintained and this page is a snapshot:

| Feature | Status |
|---|---|
| Touchscreen | ✅ (needs `linux-surface` kernel + `iptsd`) |
| Pen | ✅ |
| Type Cover keyboard & trackpad | ✅ |
| Wi-Fi | ✅ |
| Bluetooth | ✅ (needs `linux-surface` kernel) |
| Sleep / suspend | ✅ (S0ix, quality varies) |
| Battery status | ✅ |
| Sensors (accelerometer, ambient light) | ✅ |
| Hardware buttons | ✅ |
| microSD reader | ✅ |
| **Cameras** | ❌ |
| **Performance modes** | ❌ |

That is a good result — better than most 2018 x86 tablets. It is also the *ceiling*:
no operating system on this device will do better than this list, because this list is
what the drivers can do.

## The bottleneck nobody mentions

On the 64 GB model, the **eMMC storage** is the limiting factor for perceived speed,
more than the CPU or the 4 GB of RAM. Installing a lighter operating system reduces
memory pressure but does not make the storage faster. If the machine feels slow today
and it has eMMC, expect it to still feel slow afterwards — better, but slow.

The 128 GB and 256 GB models have a real M.2 2230 SSD, which is replaceable with care
(it is under the kickstand, behind a screw hidden by the kickstand hinge). That is a
genuinely worthwhile upgrade on those models, and impossible on the 64 GB one.
