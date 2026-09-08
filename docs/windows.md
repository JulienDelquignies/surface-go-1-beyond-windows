# Staying on Windows

The option people dismiss first and shouldn't. It is the only one where the cameras,
Windows Hello, LTE and the pen all work as designed, because the drivers were written
for this exact device.

## The support situation, stated plainly

- **Windows 10 reached end of support on 14 October 2025.** No free security updates,
  no technical assistance, no feature updates.
- **Windows 11 is not available.** The Pentium Gold 4415Y is not on Microsoft's
  supported processor list; the lowest supported Pentium Gold is the 4425Y. This is a
  hard list, not a performance judgement.
- **Extended Security Updates (ESU)** provide critical and important security updates
  for Windows 10 22H2 beyond that date. There is a consumer programme and a commercial
  one, with different durations and prices; enrolment for the programme runs until it
  ends on **12 October 2027**.

Check Microsoft's current
[ESU page](https://www.microsoft.com/en-us/windows/extended-security-updates) for
today's terms — the consumer offer in particular has had conditions attached (a
Microsoft account, or Rewards points, or a fee) that have changed since launch.

**What this means practically:** ESU is a defined runway, not a solution. It buys time
to decide, and the decision comes back.

## The unsupported install

You can force Windows 11 onto unsupported hardware — the `AppraiserRes.dll` swap, the
`LabConfig` registry keys, Rufus's "extended installation" option. It works, in the
sense that it boots.

Being honest about it:

- Microsoft states unsupported devices are not entitled to updates and may not receive
  them. In practice most have kept receiving them; "in practice, so far" is the whole
  guarantee.
- Feature updates frequently need the same bypass repeated, manually.
- On a 4 GB / 64 GB eMMC Surface Go, Windows 11 is **slower** than Windows 10, and the
  storage overhead of servicing is a real problem on a 64 GB disk.

It is a legitimate choice if you accept the terms. It is not a better answer than
Linux, and on the 64 GB model it is a worse one.

## Making a 4 GB / 64 GB Surface Go usable on Windows

If you're staying, the machine can be made pleasant. The bottleneck is storage and
RAM, so target those.

**Reclaim disk space** (in order of return):

```powershell
# Compact the OS — worthwhile on eMMC, costs a little CPU
compact.exe /CompactOS:always

# Remove old servicing components
Dism.exe /Online /Cleanup-Image /StartComponentCleanup /ResetBase

# Disable hibernation: frees a file the size of your RAM
powercfg /hibernate off

# Cap System Restore, or disable it if you have real backups
vssadmin resize shadowstorage /for=C: /on=C: /maxsize=3GB
```

Then: Settings → System → Storage → **Storage Sense** on; move OneDrive to
*Files On-Demand*; uninstall anything you have not opened in three months.

**Reduce memory pressure:**

- Disable startup apps (Task Manager → Startup) down to essentially nothing.
- Settings → System → About → Advanced → Performance → **Adjust for best performance**,
  then re-enable only "Smooth edges of screen fonts".
- Use **Microsoft Edge** rather than Chrome here. On 4 GB, Edge's sleeping-tabs and
  efficiency mode genuinely matter, and it's better integrated with the platform.
  This is not brand loyalty; it's the memory footprint.
- Cap browser tabs. On 4 GB this is the single biggest lever, and no OS change beats it.

**Keep the eMMC healthy:** leave at least 15 GB free. eMMC performance collapses when
nearly full, far more sharply than an SSD's does.

## When staying on Windows is the right call

- You need the cameras or Windows Hello.
- You need LTE on the 1825 model.
- You use the pen with Windows-specific software (OneNote's ink, Windows Ink workspace).
- Someone else uses the device and cannot be a beta tester.
- It's a secondary device where the effort of migrating exceeds the benefit.

That last one is a real argument, and worth saying out loud: if the tablet gets used
twice a month for reading, "keep Windows 10, don't put anything sensitive on it, enrol
in ESU or accept the risk" is a defensible answer. The unsupported-OS risk is real but
it is proportional to what you do with the machine.
