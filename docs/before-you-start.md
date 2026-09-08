# Before you touch anything

Read this page fully. Two of these steps, done in the wrong order, will lock you out
of your own machine.

## 1. BitLocker before Secure Boot — this is the one that bites

On a Surface running Windows, **device encryption (BitLocker) is often enabled by
default**, silently, with the recovery key stored in your Microsoft account.

BitLocker's key is sealed against the TPM *and* against the current boot
configuration. **Changing Secure Boot settings changes that configuration.** The next
boot into Windows will demand a 48-digit recovery key.

If you have not retrieved that key, and the machine is your only way into your
Microsoft account, you have a problem that no amount of clever partitioning solves.

**Do this, in this order:**

```
1. In Windows: Settings → Privacy & security → Device encryption
   → check whether it is ON.

2. Retrieve the recovery key NOW, from another device:
   https://account.microsoft.com/devices/recoverykey
   Write it down on paper. Not on the Surface.

3. Suspend or turn OFF device encryption BEFORE changing any UEFI setting.
   Settings → Device encryption → Off  (decryption takes a while on eMMC — let it finish)
```

Only then touch the firmware.

## 2. Back up, properly

"I don't have anything important on it" is what everyone says. Check anyway:

- Browser profiles and saved passwords not synced to an account
- Anything under `Documents`, `Desktop`, `Downloads`
- **Any 2FA authenticator app** — this is the one that ends badly. If your only TOTP
  authenticator is on this device, move it first, and verify the move works before
  wiping anything.
- Wi-Fi passwords: `netsh wlan export profile key=clear folder=C:\wifi`

## 3. Have a way back

Before you erase Windows, make the recovery image, from another PC:

- **Surface Recovery Image** — Microsoft publishes device-specific images:
  <https://support.microsoft.com/surface-recovery-image>
  You need the serial number, and you need to be signed in.
- Put it on a USB drive of at least 16 GB, formatted FAT32.
- **Verify it boots** before you wipe anything. A recovery drive you never tested is
  not a recovery drive.

This matters more on a Surface than on a generic PC: the recovery image contains
Surface-specific drivers and firmware that a plain Windows ISO does not. Reinstalling
from a generic Windows ISO gives you a machine with no working Type Cover, no cameras
and no power management until you hunt down the driver pack.

## 4. Entering the Surface UEFI

There is no F2 key. The sequence is:

```
1. Shut down completely (not sleep, not restart — Shift-click Restart, or hold power 20s)
2. Hold VOLUME UP
3. Press and release POWER
4. Keep holding VOLUME UP until the Surface logo and a spinner appear
```

You get the Surface UEFI menu. The settings that matter:

| Setting | Where | Note |
|---|---|---|
| **Secure Boot** | Security | Set to *Disabled* — or *Microsoft & 3rd party CA* for distros with a signed shim |
| **Boot order** | Boot configuration | Move *USB Storage* above *Internal Storage* |
| **Enable Alternate Boot** | Boot configuration | Lets Volume Down + Power boot straight to USB |
| **TPM** | Security | Leave it ON. Disabling it is not required and breaks more than it helps |

**You do not always need to disable Secure Boot.** Ubuntu, Fedora and Debian ship a
Microsoft-signed shim and boot fine with Secure Boot on. Android-x86 and BlissOS do
not — they need it off. Prefer leaving it on where you can: it is a real protection,
and turning it off is the step that triggers the BitLocker prompt above.

## 5. Booting from USB

```
1. Shut down completely
2. Insert the USB drive
3. Hold VOLUME DOWN
4. Press and release POWER
5. Release VOLUME DOWN when the logo appears
```

If it boots to Windows instead, the drive is not seen as bootable: check it is
GPT/FAT32 with an EFI bootloader, and that the drive is USB-A via the adapter or a
plain USB-C stick. The Surface Go 1 has one USB-C port and no USB-A — plan for a hub
if you need a keyboard during install and the Type Cover isn't working yet.

## 6. Set expectations about the storage

The 64 GB model uses **eMMC**, not an SSD. It is slow — roughly an order of magnitude
slower than the NVMe drive in a modern laptop for random writes. Any OS install on it
will feel sluggish, and no operating system choice fixes that. The 128 GB and 256 GB
models have a real SSD and are a meaningfully different machine.

If you have the 64 GB eMMC model, factor this into the decision: you are optimising a
device whose main bottleneck you cannot change.
