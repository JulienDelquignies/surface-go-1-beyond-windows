# Surface Go (1st gen) after Windows 10 — an honest assessment

The Surface Go 1 (2018, Pentium Gold 4415Y) cannot run Windows 11, and Windows 10
reached end of support on **14 October 2025**. That leaves a perfectly good 10-inch
tablet on an operating system that no longer receives free security updates.

This repository documents what you can actually do about it — including **what does
not work**, which is most of what you'll read online.

**Short answer:** installing Android on it is possible but is the *worst* of the
realistic options. Linux with the `linux-surface` kernel is the best one, and if you
want Android apps, run them on top of that with Waydroid rather than replacing the OS.

> 🇫🇷 **En bref (français)** — La Surface Go 1 n'est pas éligible à Windows 11 et
> Windows 10 n'est plus supporté depuis le 14 octobre 2025. Mettre Android dessus est
> techniquement faisable (BlissOS a des images spécifiques Surface) mais c'est la
> moins bonne option : projet de niche, caméras mortes, applications bancaires
> bloquées, aucune garantie de mise à jour. La bonne réponse est **Linux avec le noyau
> `linux-surface`** — tout fonctionne sauf les caméras — et **Waydroid** par-dessus si
> vous voulez vraiment des applications Android. Détails dans
> [docs/verdict.md](docs/verdict.md).

---

## Start here

| Document | What it answers |
|---|---|
| [The verdict](docs/verdict.md) | The four options, scored, with the reasoning |
| [Hardware reality check](docs/hardware.md) | What's actually inside, and which parts are hostile to non-Windows OSes |
| [Android on Surface Go](docs/android.md) | The honest state of it: what exists, what breaks, what you lose |
| [Linux on Surface Go](docs/linux.md) | The option that works. Install notes and the traps |
| [Staying on Windows](docs/windows.md) | ESU, and how to make a 4 GB / 64 GB eMMC machine usable |
| [Before you touch anything](docs/before-you-start.md) | **Read this first.** BitLocker + Secure Boot will lock you out if you get the order wrong |

## Why this repository exists

Search results for "Android on Surface Go" are dominated by three genres: videos that
stop at the boot animation, forum posts from 2019 about hardware that has since
changed, and tutorials that omit the step where BitLocker demands a recovery key you
don't have.

None of them tell you the thing that matters: **the Surface Go's touchscreen is not a
standard HID device.** It uses Intel Precise Touch & Stylus (IPTS), which needs a
patched kernel and a userspace daemon. Every generic "install Android x86 on any PC"
guide produces a tablet you cannot touch.

## Scope and honesty

- This targets the **Surface Go 1st generation (2018)** — models 1824 (Wi-Fi) and
  1825 (LTE). Surface Go 2, 3 and 4 have different silicon and different answers.
- Where something is uncertain or version-dependent, it says so rather than guessing.
- Sources are linked. The `linux-surface` project's device matrix is the authority on
  hardware support, not this repository — check it before acting.
- No affiliate links, no "buy me a coffee", no ads.

## Licence

MIT — see [LICENSE](LICENSE). The documentation is offered in the same spirit: copy
it, correct it, argue with it via an issue.
