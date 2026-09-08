# The verdict

Five realistic options. Scored on what actually matters when the novelty wears
off, about three weeks in.

> **Revised.** This page originally listed four options and missed FydeOS, which
> publishes a build named after this exact device. That was a real omission in a
> repository whose whole argument is that the guides online are incomplete. The
> ranking below has been redone with it included, and it moved.

## The comparison

| | Windows 10 + ESU | Windows 11 (unsupported) | **Linux + `linux-surface`** | **FydeOS for You** | Android (BlissOS Surface) |
|---|---|---|---|---|---|
| Built for this exact device | ✅ | ✅ | ⚠️ patched kernel, generic distro | ✅ device-specific image | ⚠️ generic build + Surface kernel |
| Touchscreen | ✅ | ✅ | ✅ | likely — **verify in the trial** | ✅ (with the Surface kernel) |
| Pen | ✅ | ✅ | ✅ | verify in the trial | ⚠️ varies |
| Type Cover | ✅ | ✅ | ✅ | verify in the trial | ⚠️ varies |
| Cameras | ✅ | ✅ | ❌ | ❌ assume so | ❌ |
| Battery life | best | good | acceptable | unverified | unpredictable |
| Security updates | until ESU ends | not guaranteed | ✅ ongoing | ✅ vendor-maintained | ❌ no schedule |
| Feels fast on 4 GB | ⚠️ | ❌ | ✅ | ✅ | ✅ |
| Touch-first interface | ⚠️ | ⚠️ | ⚠️ | ✅ | ✅ |
| Runs Android apps | ❌ | ❌ | ✅ via Waydroid | ✅ natively | ✅ natively |
| Banking / DRM apps | ✅ | ✅ | ⚠️ Waydroid limits | ⚠️ Play not stated as included | ❌ likely blocked |
| Cost | ESU terms | free | free | **90 days free, then £14.99/device** | free |
| Effort to set up | none | 1 hour | 2 hours | ~1 hour | a weekend |
| Somebody to ask when it breaks | Microsoft | nobody | large community | a vendor | small community |

## The recommendation

The honest answer is that **there is no single winner any more** — there are two,
and which one is right is decided by what you do with the machine, not by which is
better made. Saying otherwise would be tidier and wrong.

### 🥇 FydeOS for You — if you want a tablet

It is the only option on this list that is simultaneously **touch-first**, **built
for this exact device**, **actively maintained by someone**, and **runs Android
apps natively**. Nothing else does more than three of those.

The Android subsystem's requirement — Intel or AMD Radeon graphics, a CPU with
SSE4.2 — is satisfied by the Surface Go 1's Intel HD 615 and Pentium Gold 4415Y.
This is squarely the hardware class FydeOS targets.

And the **90-day trial removes almost all of the risk**: you can settle every open
question about touch, pen, Type Cover and battery before paying anything.

**Against it:** £14.99 per device after the trial, where Linux is free. FydeOS
does not publish a per-feature support matrix for the Surface Go, so the trial is
not optional — it is the verification step. Google Play is not stated as included,
so a Play-Integrity-gated banking app may still refuse. Cameras are almost
certainly still dead.

**Choose it if:** the machine is going to be used as a tablet — reading, browsing,
video, Android apps on the couch. → [docs/fydeos.md](fydeos.md)

### 🥇 Linux with the `linux-surface` kernel — if you want a computer

Still the right answer for anyone who types on this thing. The specific driver work
this specific device needs has been done, is maintained by an active community, and
covers everything except the cameras — and the `linux-surface` project publishes
exactly the per-feature matrix that FydeOS does not.

It is free, there is no licence, no vendor, and no trial to remember to convert.
If you want Android apps, Waydroid gets you most of them without giving up any of
this.

**Against it:** the desktop is not touch-first, whatever GNOME's improvements. On a
10-inch screen held in two hands, that is a real daily cost.

**Choose it if:** you write, use a terminal, develop, or simply want a machine you
own outright with no licence attached. → [docs/linux.md](linux.md)

### 🥈 Windows 10 with ESU — if the device is peripheral

If the tablet gets used twice a month for reading, migrating it costs more than it
returns. Enrol in ESU, keep nothing sensitive on it, revisit when the programme
ends. This is proportionality, not defeatism.

**Choose it if:** you need the cameras, Windows Hello or LTE, or the device is not
worth an evening. → [docs/windows.md](windows.md)

### 🥉 Windows 11, unsupported install — narrow case

Works, boots, receives updates in practice with no guarantee, and is slower than
Windows 10 on this hardware. On the 64 GB eMMC model it is actively worse.

**Choose it if:** you need Windows-only software *and* something in Windows 11
specifically. Otherwise there is no reason over the option above.

### 5️⃣ Android via BlissOS — now hard to justify

Not a dead end, and the Surface builds are real: a `linux-surface`-patched kernel
and `iptsd`, which is genuine work. But **FydeOS now occupies the same ground and
does it better on every axis except price**: a build named after this device, a
company maintaining it, a defined update path, and a trial to evaluate it.

BlissOS's remaining argument is that it is free where FydeOS is not. That is a real
argument for £14.99, and a thin one.

**Choose it if:** you want a pure Android tablet, you refuse to pay a licence, and
you have verified in a live USB session that your must-have apps run.
→ [docs/android.md](android.md)

## Did the ranking move?

**Yes, in two places.**

1. **FydeOS enters at the top, jointly with Linux.** Previously the answer to "I
   want a tablet" was "Linux + GNOME is better and safer than Android". That was
   the best answer among the options considered, and it was the wrong answer to
   the question — because a build made for this device, with a touch-first shell
   and native Android apps, existed and was not on the list.
2. **BlissOS drops from fourth to last, and its case gets weaker.** It was
   defensible as "the only way to get a genuinely touch-first Android tablet out
   of this machine". It is no longer the only way, and it is the less maintained
   of the two.

**What did not move:** Linux stays at the top for general-purpose use. The licence
matters here — not because £14.99 is a lot, but because it is per device,
recurring across a fleet, and tied to a single vendor. For a machine you intend to
own and tinker with for years, free and community-maintained is a different
proposition from cheap and vendor-maintained, and reasonable people weight that
differently.

## The question that actually decides it

Not "which OS is best" — **"what do I use this device for?"**

| If you use it for… | Do this |
|---|---|
| Reading, browsing, video, on the couch | **FydeOS.** Trial it first; that is what the 90 days are for |
| Android apps, specifically | **FydeOS** — but test *your* apps in the trial, not the concept |
| Note-taking with the pen | Windows, or Linux + Xournal++. Test the pen before committing either way |
| Writing, terminal, light development | **Linux.** It is not close |
| Video calls | **Windows.** The cameras are the whole point and they only work there |
| A second screen / a machine for a child / occasional use | Windows 10 + ESU. Don't spend the evening |
| It sits in a drawer and you feel guilty | Sell it, or install something and give it to someone who will use it |

## What would change this page

- `linux-surface` losing maintenance → the recommendation collapses toward FydeOS.
- FydeOS publishing a per-feature support matrix for the Surface Go, or a reader
  reporting one from the trial → the biggest remaining uncertainty on this page
  disappears. **[Open an issue](../../issues) if you have run it.**
- IPU3 camera support landing usably on Linux → Linux wins rows it currently loses.
- FydeOS changing its licensing → recompute; the trial is doing a lot of work in
  the reasoning above.

---

**Sources for the factual claims on this page**

- [linux-surface — Supported Devices and Features](https://github.com/linux-surface/linux-surface/wiki/Supported-Devices-and-Features)
- [FydeOS — pricing](https://fydeos.io/pricing/) and [FydeOS for You — Surface Go](https://fydeos.io/download/device/surface-go/)
- [FydeOS — running Android apps](https://fydeos.io/help/knowledge-base/getting-started/application-support/running-android-apps/) (GPU and CPU requirements)
- [Google — ChromeOS Flex vs ChromeOS](https://support.google.com/chromeosflex/answer/11542901)
- [BlissOS — Surface builds documentation](https://docs.blissos.org/knowledgebase/other-bliss-variant/surface-builds/)
- [Microsoft — Windows 10 support ended on 14 October 2025](https://support.microsoft.com/en-us/windows/windows-10-support-has-ended-on-october-14-2025-2ca8b313-1946-43d3-b55c-2b95b107f281)
- [Microsoft — Windows 10 Extended Security Updates](https://www.microsoft.com/en-us/windows/extended-security-updates)
- [Microsoft — Surface Go (1st Gen) specifications](https://support.microsoft.com/en-us/surface/models/surface-go-1st-gen-specs-and-features)
