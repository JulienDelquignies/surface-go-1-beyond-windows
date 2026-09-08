# Android on the Surface Go 1 — what's real

The question this repository started from. The short version: **it is possible, and
it is the weakest of the four options.** Here is why, without the enthusiasm.

## What actually exists

There is no "Android for Surface Go". There are x86 Android distributions, and one of
them has Surface-specific builds.

| Project | State | Relevance here |
|---|---|---|
| **[BlissOS](https://blissos.org)** | Active. Android 11 / 12 / 13-era builds, plus **dedicated Surface builds** | The only *bare Android* option — but see [FydeOS](fydeos.md), which runs Android apps on a build made for this device |
| **[Android-x86](https://www.android-x86.org)** | Effectively dormant; last stable releases are years old and Android 9-era | Historical interest only |
| **[PrimeOS](https://primeos.in)** | Active but gaming-desktop focused, Android-x86 derived | No Surface touch support |
| **Bare AOSP** | You would be porting it yourself | Not a weekend project |

### The BlissOS Surface builds

This is the part most guides get wrong, so it's worth stating precisely: BlissOS
publishes builds that use **"almost the same LTS kernel but with extra patches from
the `linux-surface` project"**, and that ship **`iptsd`**, the same userspace touch
daemon Linux uses. That is what makes the touchscreen work.

The project's own guidance is that you take a recent generic Intel ISO with Gearlock,
then install the Surface kernel package from Gearlock recovery after first boot.
Consult the [BlissOS Surface documentation](https://docs.blissos.org/knowledgebase/other-bliss-variant/surface-builds/)
for the current procedure — it changes between releases, and a procedure copied from a
2021 video will not apply.

Useful detail from their knowledge base: if touch stops responding while running, you
can reload the modules from a console rather than rebooting:

```sh
su
rmmod ipts_surface && rmmod intel_ipts && modprobe intel_ipts && modprobe ipts_surface
```

The fact that this command needs to exist tells you something about the day-to-day
experience.

## What you lose

Assume all of these unless you have verified otherwise on your exact build:

| | |
|---|---|
| **Cameras** | Gone. IPU3, same dead end as on Linux. Both of them |
| **Windows Hello / IR** | Gone |
| **Play Store, Play Protect certification** | Not guaranteed. GApps must usually be added, and the device will not be Play Integrity certified |
| **Banking, payment and streaming apps** | Many refuse to run on an uncertified device or a device that fails Play Integrity. Netflix and similar will drop to SD or refuse, because Widevine L1 is not available |
| **LTE (model 1825)** | Do not expect the modem to work |
| **Reliable sleep** | Modern-standby handling in these builds is not a priority for the project |
| **Security updates** | There is no update channel with a schedule. You update when the project publishes, or you don't |
| **Support if it breaks** | A forum, a Telegram group, and your own patience |

## What you gain

Being fair to the option:

- A genuinely touch-first interface. This is the real argument, and it is not nothing:
  Android is the only one of the four options actually designed for a 10-inch
  touchscreen held in two hands.
- Light on 4 GB of RAM.
- Instant-on feel, when sleep behaves.
- Android apps natively, at full speed — no container, no translation layer.

## Why it still comes last

Three reasons, in order of weight:

**1. You are betting the device on a small volunteer project.** The Surface builds
depend on one team tracking `linux-surface` patches into an Android kernel. If that
stops — and x86 Android projects have stopped before; Android-x86 itself is the
cautionary tale — you are on a frozen, unpatched OS with no migration path.

**2. The apps you actually want may refuse to run.** Losing the cameras is
predictable and you can decide it doesn't matter. Discovering three months later that
your bank's app, your work MFA app, or your streaming subscription won't work on an
uncertified device is the failure mode that makes people reinstall Windows.

**3. There are two better ways to get Android apps.**

- **[FydeOS](fydeos.md)** runs them natively, on a ChromeOS-based system with a build
  named after this exact device and a company maintaining it. It costs £14.99 per
  device after a 90-day trial — which is the only thing BlissOS still has over it.
- **Linux + [Waydroid](https://waydro.id)** runs them in a container on a free,
  community-maintained system where the hardware support is documented feature by
  feature. See [the Linux page](linux.md).

Both give you a real update channel, which BlissOS does not.

## If you're going to do it anyway

Fair enough — it's your device, and the tablet argument is legitimate. Do it in this
order:

1. Read [before-you-start.md](before-you-start.md) completely. BitLocker first.
2. **Try it from USB before installing.** BlissOS boots live. Check, in this order:
   touch, then Type Cover, then Wi-Fi, then battery percentage, then sleep and wake.
   If touch doesn't work in the live session, it will not magically work after
   installation.
3. **Dual-boot rather than wipe**, at least for the first month. On the 64 GB eMMC
   model there isn't room for that, which is itself an argument.
4. Write down the exact build ID you used. When you need to ask for help, "the latest
   BlissOS" is not an answer anyone can work with.
5. Keep the Surface recovery USB. You will probably use it.

## What I'd want to see before recommending it

If you get it working well, an issue or PR on this repository with the following would
genuinely help other people, and would change this page:

- Exact build ID and kernel package version
- Whether touch, pen, Type Cover, Wi-Fi, Bluetooth, battery %, rotation and sleep work
- Overnight battery drain, as a percentage
- Whether Play Integrity passes, and whether a banking app runs
- How long it survived before something broke

That last line is the one that matters, and it's the one no video ever includes.
