# Surface Go (1st gen) after Windows 10 — an honest assessment

The Surface Go 1 (2018, Pentium Gold 4415Y) cannot run Windows 11, and Windows 10
reached end of support on **14 October 2025**. That leaves a perfectly good 10-inch
tablet on an operating system that no longer receives free security updates.

This repository documents what you can actually do about it — including **what does
not work**, which is most of what you'll read online.

**Short answer:** there are two good answers, not one. **FydeOS for You** publishes
an image built for this exact device — touch-first, ChromeOS-based, Android apps
included, 90-day trial then £14.99 per device. **Linux with the `linux-surface`
kernel** is free, community-maintained, and better if you actually type on the
thing. Installing bare Android (BlissOS) is now the weakest option, and ChromeOS
Flex is the wrong free thing here — Google's own documentation says it supports
neither general Android apps nor the pen.

> 🇫🇷 **En bref (français)** — La Surface Go 1 n'est pas éligible à Windows 11 et
> Windows 10 n'est plus supporté depuis le 14 octobre 2025. Il y a **deux** bonnes
> réponses, et le choix dépend de l'usage.
>
> **Pour s'en servir comme d'une tablette : [FydeOS](docs/fydeos.md).** C'est la seule
> option qui publie une image faite **pour cette machine précise** (« FydeOS for You —
> Microsoft Surface Go »). Fondé sur ChromeOS, interface pensée pour le tactile, et il
> fait tourner les **applications Android** — contrairement à ChromeOS Flex de Google,
> qui ne les gère pas et ne gère pas non plus le stylet. Le sous-système Android exige
> une carte graphique Intel ou AMD : l'Intel HD 615 de la Surface Go coche la case.
> **Ce n'est pas gratuit** : 90 jours d'essai, puis une licence **par appareil** —
> 14,99 £ selon la page tarifaire officielle. `openFyde` est la variante libre, sans
> licence, mais à compiler soi-même.
>
> **Pour s'en servir comme d'un ordinateur : Linux avec le noyau `linux-surface`.**
> Gratuit, maintenu par une communauté active, tout fonctionne sauf les caméras, et
> **Waydroid** donne les applications Android par-dessus.
>
> Installer Android nu (BlissOS) est désormais l'option la plus faible : FydeOS occupe
> le même terrain avec une image dédiée et un éditeur derrière. Les caméras sont
> mortes dans tous les cas (bloc IPU3). Le raisonnement complet :
> [docs/verdict.md](docs/verdict.md).

---

## Start here

| Document | What it answers |
|---|---|
| [The verdict](docs/verdict.md) | The four options, scored, with the reasoning |
| [Hardware reality check](docs/hardware.md) | What's actually inside, and which parts are hostile to non-Windows OSes |
| [FydeOS](docs/fydeos.md) | The build made for this device: ChromeOS-based, Android apps, what it costs, and what its docs don't tell you |
| [Android on Surface Go](docs/android.md) | The honest state of BlissOS: what exists, what breaks, what you lose |
| [Linux on Surface Go](docs/linux.md) | Free and community-maintained. Install notes and the traps |
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

Most of them also skip **FydeOS**, which ships a build named after this device — and
those that mention it skip the part where it stops being free after 90 days. This
repository was guilty of the first omission until it was pointed out; the
[verdict](docs/verdict.md) says so and shows what changed.

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
