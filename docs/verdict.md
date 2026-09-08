# The verdict

Four realistic options. Scored on what actually matters when the novelty wears off,
about three weeks in.

## The comparison

| | Windows 10 + ESU | Windows 11 (unsupported) | **Linux + `linux-surface`** | Android (BlissOS Surface) |
|---|---|---|---|---|
| Touchscreen | ✅ | ✅ | ✅ | ✅ (with the Surface kernel) |
| Pen | ✅ | ✅ | ✅ | ⚠️ varies |
| Type Cover | ✅ | ✅ | ✅ | ⚠️ varies |
| Cameras | ✅ | ✅ | ❌ | ❌ |
| Windows Hello | ✅ | ✅ | ❌ | ❌ |
| LTE (model 1825) | ✅ | ✅ | ⚠️ | ❌ |
| Battery life | best | good | acceptable | unpredictable |
| Sleep/wake | ✅ | ✅ | ⚠️ mostly | ⚠️ |
| Security updates | until ESU ends | not guaranteed | ✅ ongoing | ❌ no schedule |
| Feels fast on 4 GB | ⚠️ | ❌ | ✅ | ✅ |
| Touch-first UI | ⚠️ | ⚠️ | ⚠️ | ✅ |
| Runs Android apps | ❌ | ❌ | ✅ via Waydroid | ✅ natively |
| Banking / DRM apps | ✅ | ✅ | ⚠️ Waydroid limits | ❌ likely blocked |
| Effort to set up | none | 1 hour | 2 hours | a weekend |
| Effort to maintain | none | recurring | low | yours alone |
| Someone to ask when it breaks | Microsoft | nobody | large community | small community |

## The recommendation

### 🥇 Linux with the `linux-surface` kernel — for most people

Because the specific work this specific device needs has been done, is maintained, and
covers everything except the cameras. You get an actively supported OS with real
security updates on hardware that would otherwise be stranded, and if you want Android
applications you add Waydroid on top and keep everything else.

**Choose it if:** you can live without the cameras, and you're comfortable spending an
evening on setup. → [docs/linux.md](linux.md)

### 🥈 Windows 10 with ESU — if the device is peripheral

If the tablet is used occasionally for reading and browsing, migrating it costs more
than it returns. Enrol in ESU, keep nothing sensitive on it, and revisit when the
programme ends. This is not defeatism; it's proportionality.

**Choose it if:** you need the cameras, Windows Hello or LTE, or the device isn't
worth an evening. → [docs/windows.md](windows.md)

### 🥉 Windows 11, unsupported install — narrow case

Works, boots, receives updates in practice with no guarantee, and is slower than
Windows 10 on this hardware. On the 64 GB eMMC model it is actively worse.

**Choose it if:** you need Windows-only software *and* something in Windows 11
specifically. Otherwise there's no reason over the option above.

### 4️⃣ Android — last, and here's the honest version

It is not a dead end. BlissOS ships Surface-specific builds using a `linux-surface`-
patched kernel and `iptsd`, and people do run them successfully. If the goal is
strictly "a 10-inch Android tablet", it is the only option that delivers a genuinely
touch-first interface, and that argument is real.

But you are trading an actively maintained OS for a small project's build, losing the
cameras anyway, losing any update schedule, and probably losing the banking and
streaming apps that made you want Android. And the thing you wanted — Android apps —
is available on option 1 via Waydroid without any of those costs.

**Choose it if:** you want the tablet experience specifically, you accept there is no
update channel, and you've verified in a live USB session that your must-have apps
run. → [docs/android.md](android.md)

## The question that actually decides it

Not "which OS is best" — **"what do I use this device for?"**

| If you use it for… | Do this |
|---|---|
| Reading, browsing, video, on the couch | Android is defensible; Linux + GNOME is better and safer |
| Note-taking with the pen | Windows, or Linux + Xournal++ — test the pen before committing |
| Writing, terminal, light development | **Linux.** It is not close |
| Video calls | **Windows.** The cameras are the whole point and they only work there |
| A second screen / a machine for a child / occasional use | Windows 10 + ESU. Don't spend the evening |
| It sits in a drawer and you feel guilty | Sell it, or install Linux and give it to someone who'll use it |

## What would change this page

- `linux-surface` losing maintenance → the recommendation collapses to Windows.
- IPU3 camera support landing usably on Linux → Linux wins on every row that matters.
- A BlissOS Surface build with a real release cadence and Play Integrity → Android
  becomes a genuine contender for tablet use.

None of those look imminent. If one happens, open an issue and this page changes.

---

**Sources for the factual claims on this page**

- [linux-surface — Supported Devices and Features](https://github.com/linux-surface/linux-surface/wiki/Supported-Devices-and-Features)
- [BlissOS — Surface builds documentation](https://docs.blissos.org/knowledgebase/other-bliss-variant/surface-builds/)
- [Microsoft — Windows 10 support ended on 14 October 2025](https://support.microsoft.com/en-us/windows/windows-10-support-has-ended-on-october-14-2025-2ca8b313-1946-43d3-b55c-2b95b107f281)
- [Microsoft — Windows 10 Extended Security Updates](https://www.microsoft.com/en-us/windows/extended-security-updates)
- [Microsoft — Surface Go (1st Gen) specifications](https://support.microsoft.com/en-us/surface/models/surface-go-1st-gen-specs-and-features)
