# Linux on the Surface Go 1 — the option that works

This is the recommendation. Not because Linux is better in the abstract, but because
the [`linux-surface`](https://github.com/linux-surface/linux-surface) project has done
the specific work this specific device needs, and keeps doing it.

## What you get

Everything on the [hardware page](hardware.md) that is marked ✅: touchscreen, pen,
Type Cover keyboard and trackpad, Wi-Fi, Bluetooth, battery reporting, sensors,
rotation, hardware buttons, microSD, and suspend.

What you don't get: **the cameras**, and performance-mode switching. Decide now
whether the cameras matter. On a device most people use as a reading and browsing
tablet, they usually don't — but "usually" isn't "you".

## The essential step

A stock distribution kernel will give you a machine with no touchscreen and no Type
Cover. You must install the `linux-surface` kernel. The project provides package
repositories for Debian/Ubuntu, Arch and Fedora, and their README is the authoritative
installation procedure:

> <https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup>

Do not follow a copy of those instructions from a blog post. The repository keys and
package names change; the wiki is maintained.

The three things it installs:
- the patched kernel (IPTS/ithc touch, Surface Aggregator, power management fixes),
- `iptsd`, the userspace touch daemon,
- `linux-surface-secureboot-mok`, if you want to keep Secure Boot enabled — which you
  should, and which avoids the BitLocker prompt entirely if you're dual-booting.

## Choosing a distribution

The kernel is the same everywhere. What differs is how well the *desktop* handles a
10-inch touchscreen — which is the whole point on this machine.

| Distribution | Why | Against |
|---|---|---|
| **Fedora Workstation (GNOME)** | Best touch and gesture support of any Linux desktop today. On-screen keyboard is genuinely usable. Auto-rotation works | Ships new kernels quickly, which occasionally races ahead of `linux-surface` packaging |
| **Ubuntu (GNOME)** | Same desktop, slower moving, largest amount of help available when stuck | Snap-based Firefox is sluggish on this CPU — install the deb or use Flatpak |
| **Debian stable + GNOME** | The steadiest. Good if you want to install it once and forget it | Older GNOME, so slightly worse touch |
| **Arch** | Newest `linux-surface` packages, full control | You will maintain it. On a secondary device this gets old |
| **KDE Plasma (any base)** | Excellent tablet mode, very configurable | Heavier on 4 GB. Viable but tune it |
| **Anything XFCE/LXQt "lightweight"** | Fast | **No touch story at all.** On a tablet this is the wrong trade — you save RAM and lose the input method |

**Recommendation:** Fedora Workstation on the 8 GB model, Debian stable + GNOME on the
4 GB model. Avoid the instinct to reach for a "lightweight" desktop: on this device the
scarce resource is screen size and input, not CPU.

## Realistic expectations

- **Battery life:** worse than Windows. Windows tunes S0ix for this exact device;
  Linux does its best generically. Expect a meaningful reduction — how much depends on
  kernel version and workload. `powertop --auto-tune` and TLP help.
- **Overnight drain:** if it's bad, **unpair your Bluetooth LE devices**. The Marvell
  chip on this device has a firmware bug that blocks system power saving whenever a BLE
  device is paired. This is documented by `linux-surface` and catches everyone.
- **Fractional scaling:** at 1800 × 1200 on 10 inches you want 150 %. GNOME on Wayland
  handles this; some X11 apps will look soft. Not a dealbreaker, but not invisible.
- **Video:** hardware decode works (Gen9 GPU, VA-API). Install `intel-media-driver`.
  Without it, 1080p YouTube will use software decode and the fans — there are none —
  will not save you.
- **Speed:** the 64 GB eMMC model stays slow. Linux reduces memory pressure; it does
  not make eMMC faster.

## Android apps, the sensible way: Waydroid

If the goal was Android applications, this is how to get them without giving up the
machine.

[Waydroid](https://waydro.id) runs a full Android system in a container, sharing the
host kernel, on a Wayland session. Applications appear as normal windows or full
screen. It is fast because there is no emulation — the Surface Go is x86, and so is
the Android image.

```sh
# Fedora / Ubuntu: follow https://docs.waydro.id/usage/install-on-desktops
# Then, first run:
waydroid init            # add -s GAPPS for a Google-apps image
waydroid session start
waydroid show-full-ui
```

What to expect:
- Most apps work. Touch, keyboard and clipboard integrate with the host.
- Google Play certification requires registering the device ID with Google — the
  Waydroid documentation covers this. Without it, Play Store logins fail.
- **Play Integrity–gated apps (many banking apps) will still refuse.** Waydroid does
  not solve that; nothing on this device does.
- ARM-only apps need a translation layer (libhoudini / libndk), which is a separate
  and less reliable step. Most mainstream apps ship x86 builds; games often don't.

The point stands: Waydroid gives you the Android applications you wanted while keeping
a maintained OS, working Type Cover, and a device that is still a laptop when you need
one. That combination is not available from a bare Android install.

## Installation order that avoids trouble

1. [before-you-start.md](before-you-start.md) — BitLocker, backups, recovery USB.
2. Write the ISO to USB. Boot it (Volume Down + Power) and **use the live session for
   ten minutes**: check Wi-Fi and that the screen is not upside down.
   Touch will *not* work yet — that's expected, the live image has a stock kernel.
3. Install. Keep Secure Boot on if the distro supports it.
4. **Immediately** add the `linux-surface` repository and install the kernel, `iptsd`
   and the Secure Boot MOK package, then reboot into the new kernel.
5. Verify in this order: touch → pen → Type Cover → battery percentage → rotation →
   close the lid and check drain after an hour.
6. Only then delete the Windows partition, if that's the plan.

Step 6 is deliberately last. Leave yourself two weeks of dual-boot before you commit.
