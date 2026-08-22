<div align="center">

<img src="./media/kernelsu-logo.svg" alt="KernelSU Logo" width="128"/>

# Awesome KernelSU

**A curated list of KernelSU resources: official documentation, variants, modules, tools, and device kernels.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/fynks/awesome-kernelsu?style=flat-square&logo=github)](https://github.com/fynks/awesome-kernelsu/stargazers)
[![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)

</div>

## Contents

- [What is KernelSU?](#what-is-kernelsu)
- [Getting Started](#getting-started)
- [Installation Modes](#installation-modes)
- [Metamodules](#metamodules)
- [KernelSU Variants](#kernelsu-variants)
- [Modules \& Tools](#modules--tools)
- [Device Kernels](#device-kernels)
- [Building from Source](#building-from-source)
- [Documentation](#documentation)
- [Community](#community)
- [Troubleshooting](#troubleshooting)
- [FAQs](#faqs)  
- [License](#license)
- [Acknowledgments](#acknowledgments)


## What is KernelSU?

**KernelSU** is a kernel-based root solution for Android. Unlike userspace tools such as Magisk, it runs inside the Linux kernel and grants root access to apps directly in kernel space.

### Key Features

- **Root Access Control** - Only permitted apps can access or see su; all other apps remain unaware of it
- **Kernel-Level Isolation** - Root access operates in kernel space, preventing userspace tampering and detection
- **Metamodule System** - Pluggable module infrastructure for systemless /system modifications
- **Advanced Permission Control**: Granular app-level root access management with customizable profiles
- **App Profile System**: Customizable groups, capabilities, and SELinux rules for fine-grained root privilege control
- **Module Configuration System**: Built-in key-value store for modules to save persistent or temporary settings

> [!NOTE]
> Official KernelSU targets Android **GKI 2.0** devices (kernel 5.10+). Compatibility ultimately depends on the device's **KMI**, not just the kernel version- see the [installation guide](https://kernelsu.org/guide/installation.html).


<br>

> **Learn More**: [Comprehensive KernelSU Guide](https://awesome-android-root.zhoe.org/rooting-guides/kernelsu-guide) | [Official Documentation](https://kernelsu.org/) | [Official Module Repo](https://modules.kernelsu.org)


## Getting Started

### Prerequisites

Before installing KernelSU, ensure you have:
- **Unlocked bootloader** (required for all installation methods)
- **Complete data backup** (always backup before modifying your device)
- **ADB and Fastboot tools** installed on your computer
- **Compatible device** (check compatibility below)

> [!TIP]
> **New to bootloader unlocking?** Check out the comprehensive guide at [Awesome-Android-Root](https://awesome-android-root.zhoe.org/rooting-guides/how-to-unlock-bootloader)

### New to KernelSU?

1. **Check Compatibility**
   -Install the [KernelSU Manager](https://github.com/tiann/KernelSU/releases/latest) and open it:
      - `Not installed` → officially supported.
      - `Unsupported` → you must build a kernel yourself (see [Unofficially supported devices](https://kernelsu.org/guide/unofficially-support-devices.html) and [Device Kernels](#device-kernels)).

2. **Choose Installation Mode**
   - **GKI Mode**: Replaces device kernel (universal compatibility, works on Samsung Knox)
   - **LKM Mode**: Loads as kernel module (preserves optimizations, easy updates)
   > See [Installation Modes](#installation-modes)

3. **Download Manager**
   - Get the official Manager APK for your chosen variant (links in [Variants](#kernelsu-variants) section)

4. **Install KernelSU**
   - Follow the [installation guide](#-installation) for your chosen method

5. **Install Metamodule**
   - Required only if you use modules that modify `/system` files (e.g. `meta-overlayfs`). See [Metamodules](#metamodules).

6. **Verify Installation**
   - Open KernelSU Manager and confirm root status

## Installation Modes

On GKI devices KernelSU historically supports two modes. The official guide recommends:

- **LKM**- for phones.
- **GKI**- for emulators, WSA, and Waydroid.

### LKM (Loadable Kernel Module)

Loads KernelSU as a kernel module without replacing the original kernel.

- Keeps the stock kernel and manufacturer optimizations.
- Updates and OTA can be done in-app (including "install to inactive slot").
- Does not replace the boot partition, so it does not trigger AVB.
- Can be temporarily uninstalled without a reboot.
- Patches the **ramdisk**- on Android 13+ devices this means the **`init_boot`** partition, not `boot`.

### GKI (Generic Kernel Image)

Replaces the original kernel with a GKI image.

- Works without official firmware, as long as the **KMI** matches.
- Useful for devices where LKM cannot work (e.g. Samsung devices with KNOX enabled).

> [!NOTE]
> Since v3.0, official KernelSU has **dropped GKI image builds** (the [build guide](https://kernelsu.org/guide/how-to-build.html) is now archival) and recommends building the LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk). Official releases ship LKM modules and the Manager, not `boot.img` files. Forks (KernelSU-Next, SukiSU-Ultra, etc.) still provide GKI builds.

<details>
<summary>Click here for quick comparison</summary>

| **GKI Mode**                            | **LKM Mode**                                |
| --------------------------------------- | ------------------------------------------- |
| Universal GKI device compatibility      | Preserves original kernel and optimizations |
| Works on Samsung Knox devices           | Easy in-app updates                         |
| Independent of firmware updates         | OTA-friendly                                |
| Better for heavily modified devices     | No AVB/dm-verity issues                     |
| More stable on custom ROMs              | Can disable without reboot                  |
| Loses manufacturer kernel optimizations | Preserves manufacturer tuning               |
| Requires manual fastboot flashing       | Requires official firmware                  |
| Must reflash after major updates        | May not work on all devices                 |
|                                         | Less compatible with modified firmware      |

</details><br>

> [!TIP]
> **Full instructions:** [Official installation guide](https://kernelsu.org/guide/installation.html)- including KMI and security-patch-level explanations.

## Metamodules

A **metamodule** is a special module that provides the module *mounting* infrastructure. Since v3.0, official KernelSU no longer mounts modules itself- it delegates mounting to a metamodule.

> [!IMPORTANT]
> A metamodule is needed **only for modules that modify `/system` files** (the `system` directory). Modules that only use scripts, `sepolicy`, or `system.prop` work without one. Only **one** metamodule can be installed at a time.

Note the scope: metamodule-based mounting applies to **official KernelSU** (v3.0+) and **ReSukiSU**. **KernelSU-Next** and **SukiSU-Ultra** still ship built-in mounting (Magic Mount / OverlayFS).

### Available metamodules

| Metamodule | Mounting | Notes |
|------------|----------|-------|
| [**meta-overlayfs**](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) | OverlayFS | **Official reference implementation**- recommended starting point. Also on the [official module repository](https://modules.kernelsu.org/module/meta-overlayfs). |
| [**mountify**](https://github.com/backslashxx/mountify) | OverlayFS | Third-party; supports APatch/Magisk too. |
| [**meta-hybrid_mount**](https://github.com/Hybrid-Mount/meta-hybrid_mount) | OverlayFS + Magic Mount | Third-party; dual-engine with auto-fallback ("Hybrid Mount"). |


### Installing Your First Metamodule

**Step-by-Step Installation:**

1. **Download metamodule ZIP** from GitHub releases (meta-overlayfs recommended)
2. **Open KernelSU Manager** > Modules
3. **Tap "Install from storage"** (➕ button)
4. **Select the metamodule ZIP** file
5. **Reboot device**

The active metamodule will be displayed in your module list with a special designation.

> [!TIP]
> Browse the full, current list of metamodules and modules at the **[official module repository](https://modules.kernelsu.org/)**.

**Details & switching procedure:** [Official metamodule guide](https://kernelsu.org/guide/metamodule.html)



## KernelSU Variants

> [!WARNING]
> Everything below **Official KernelSU** is a **community fork/derivative**, not an official project. Features of one variant do not apply to the others.


### Official KernelSU

[![GitHub](https://img.shields.io/badge/GitHub-tiann%2FKernelSU-blue?logo=github&style=flat-square)](https://github.com/tiann/KernelSU)
[![Documentation](https://img.shields.io/badge/Docs-kernelsu.org-green?style=flat-square)](https://kernelsu.org/)
[![Release](https://img.shields.io/github/v/release/tiann/KernelSU?style=flat-square)](https://github.com/tiann/KernelSU/releases)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU)

> The original KernelSU implementation for modern Android devices

<details open>
<summary><b>📋 View Details</b></summary>

- **Target:** GKI 2.0 devices (kernel 5.10+). WSA, ChromeOS, and container-based Android are supported.
- **Architectures:** `arm64-v8a` and `x86_64`.
- **Module mounting:** metamodule-based (v3.0+).
- **Non-GKI:** dropped since v1.0 (last version `v0.9.5`); the [integration guide](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) is archival.
- **Notable changes:** seccomp+ioctl supercall (v2.0), `selinux hide` (v3.2.x), optional "jailbreak" mode via Magica (v3.2+).

> [!CAUTION]
> Recent kernel versions introduced a breaking change that can make KernelSU fail or **kernel-panic on `x86_64`**. Check the [official repository](https://github.com/tiann/KernelSU) for current status.

**Resources:**
- [Download Manager APK](https://github.com/tiann/KernelSU/releases/latest)
- [Official Documentation](https://kernelsu.org/)
- [Official Module Repository](https://modules.kernelsu.org)
- [Telegram Channel](https://t.me/KernelSU)
- [Report Issues](https://github.com/tiann/KernelSU/issues)

</details>


### KernelSU-Next


[![GitHub](https://img.shields.io/badge/GitHub-KernelSU--Next-blue?logo=github&style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next)
[![Documentation](https://img.shields.io/badge/Docs-kernelsu--next.github.io-green?style=flat-square)](https://kernelsu-next.github.io/webpage/)
[![Release](https://img.shields.io/github/v/release/KernelSU-Next/KernelSU-Next?style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next/releases)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU__Next-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU_Next)

> Enhanced fork with extended compatibility, modern UI, and innovative features.

<details>
<summary><b>📋 View Details</b></summary>

- **Kernel support:** 4.4–6.6 (non-GKI 4.x–5.4 LTS; GKI 5.10–6.6; 6.6+ experimental).
- **Module mounting:** built-in **Magic Mount + OverlayFS**, switchable from settings.
- **Features:** module backup & restore, auto-updates, bulk install, hide hosts (unmount), SuSFS controls, SU-allowlist backup.
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86_64` (same `x86_64` panic caveat as upstream).
- **Community device list:** [Unofficially supported devices](https://kernelsu-next.github.io/webpage/pages/devices.html)

**Resources:**
- [Download Manager APK](https://github.com/KernelSU-Next/KernelSU-Next/releases)
- [Official Website](https://kernelsu-next.github.io/webpage/)
- [Supported Devices](https://kernelsu-next.github.io/webpage/pages/devices.html)
- [Telegram Community](https://t.me/KernelSU_Next)
- [Report Issues](https://github.com/KernelSU-Next/KernelSU-Next/issues)

</details>

### SukiSU-Ultra

[![GitHub](https://img.shields.io/badge/GitHub-SukiSU--Ultra-blue?logo=github&style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
[![Documentation](https://img.shields.io/badge/Docs-sukisu.org-green?style=flat-square)](https://sukisu.org/)
[![Release](https://img.shields.io/github/v/release/SukiSU-Ultra/SukiSU-Ultra?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
[![Telegram](https://img.shields.io/badge/Telegram-SukiKSU-blue?style=flat-square&logo=telegram)](https://t.me/Sukiksu)


> Kernel-based root solution with KPM support, built-in SUSFS, and broad GKI/non-GKI compatibility.

<details>
<summary><b>📋 View Details</b></summary>


- **Kernel support:** non-GKI 4.4+; GKI 5.10+; 3.x (3.4–3.18) experimental.
- **Module mounting:** built-in **Magic Mount**.
- **KPM** (Kernel Patch Module) support- run code in kernel space (based on KernelPatch).
- **SUSFS** management built into the Manager (the kernel still needs SUSFS patches).
- **Architectures:** `arm64-v8a`, `armeabi-v7a` (bare), `x86_64` (some).

**Resources:**
- [Download Manager APK](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
- [Official Website](https://sukisu.org/)
- [Installation Guide](https://sukisu.org/guide/installation)
- [Telegram Group](https://t.me/Sukiksu)

</details>

### ReSukiSU

[![GitHub](https://img.shields.io/badge/GitHub-ReSukiSU-blue?logo=github&style=flat-square)](https://github.com/ReSukiSU/ReSukiSU)
[![Release](https://img.shields.io/github/v/release/ReSukiSU/ReSukiSU?style=flat-square)](https://github.com/ReSukiSU/ReSukiSU/releases)

> A newer fork of SukiSU-Ultra focused on multi-manager support and a metamodule-based module system.

<details>
<summary><b>📋 View Details</b></summary>

- **Module mounting:** metamodule-based.
- **Multi-manager:** works with the KernelSU, MKSU, RKSU, and SukiSU managers.
- **Kernel support:** GKI 2.0 (5.10+); 3.4+ with manual build.
- **Releases:** pre-release/CI builds so far (latest tag `v4.2.0-rc1`)- check the repository.

**Resources:**
- [Download Manager APK](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
- [Official Website](https://sukisu.org/)
- [Installation Guide](https://sukisu.org/guide/installation)
- [Telegram Group](https://t.me/Sukiksu)

</details>

### Wild KSU- archived

> [!NOTE]
> The **Wild KSU** fork ([WildKernels/Wild_KSU](https://github.com/WildKernels/Wild_KSU)) is **archived** (last release v3.1.2). It is no longer maintained as a root variant. The **WildKernels** team still ships KernelSU/SUSFS device kernels- see [Device Kernels](#device-kernels).

### Comparison

| Feature                   | Official KernelSU             | KernelSU-Next                  | SukiSU-Ultra                                     | ReSukiSU               |
| ------------------------- | ----------------------------- | ------------------------------ | ------------------------------------------------ | ---------------------- |
| **Status**                | Official, active              | Active fork                    | Active fork                                      | Active fork            |
| **Kernel support**        | GKI 2.0 (5.10+); 4.14+ manual | 4.4–6.6                        | 5.10+ GKI; 4.4+ non-GKI/manual; 3.x experimental | 5.10+ GKI; 3.4+ manual |
| **Android version**       | 12+ (GKI); 10+ community      | 9+                             | 7+                                               | 7+                     |
| **Module mounting**       | Metamodule (3.0+)             | Metamodule + dual mount toggle | Magic Mount / Metamodule                         | Metamodule             |
| **KPM**                   | ❌                             | ❌                              | ✅                                                | ✅                      |
| **SUSFS**                 | Via kernel patch              | Via kernel patch               | Built-in management                              | Built-in management    |
| **Multi-manager**         | ❌                             | ❌                              | ❌                                                | ✅ (KSU/RKSU/MKSU/Suki) |
| **Architectures**         | arm64, x86_64                 | arm64, arm, x86_64             | arm64, arm, x86_64 (some/partial)                | arm64, arm, x86_64     |
| **Installation modes**    | LKM (GKI image deprecated)    | GKI / LKM                      | GKI / LKM                                        | GKI / LKM              |
| **Module backup/restore** | ❌                             | ✅                              | ❌                                                | ❌                      |
| **Auto updates**          | ⚠️ LKM only                   | ✅                              | ⚠️ Manual                                        | ⚠️ Manual              |
| **Root hiding**           | Metamodule-based              | Advanced (unmount)             | SUSFS built-in                                   | SUSFS built-in         |
| **UI/UX**                 | Material 3 + Magica           | Material You                   | Enhanced + WebUI                                 | Enhanced               |
| **Legacy support**        | ❌                             | ⚠️ Limited                     | ✅ Extensive                                      | ✅ Extensive            |
| **Best for**              | Modern devices                | Power users                    | KPM / legacy / hiding                            | Multi-manager setups   |

> [!NOTE]
> SUSFS is a **separate** kernel-patch addon ([gitlab.com/simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu))- it is not part of KernelSU itself. "Built-in management" means the Manager can control SUSFS on a SUSFS-patched kernel; it does not bundle the kernel patches.


### Which Variant Should You Choose?

<table>
<tr>
<td width="25%" valign="top">

**Choose Official KernelSU if:**

✅ Modern device (2021+)<br>
✅ GKI 2.0 support<br>
✅ Want maximum stability<br>
✅ Prefer official support<br>
✅ OTA compatibility priority

</td>
<td width="25%" valign="top">

**Choose KernelSU-Next if:**

✅ Kernel 4.4–6.6<br>
✅ Want latest features<br>
✅ Prefer modern UI<br>
✅ Auto-updates desired<br>
✅ Advanced module mgmt

</td>
<td width="25%" valign="top">

**Choose Wild KSU if:**

✅ Kernel 4.4–6.6<br>
✅ Root hiding priority<br>
✅ Want SUSFS integrated<br>
✅ Customization focused<br>
✅ Nightly build access

</td>
<td width="25%" valign="top">

**Choose SukiSU-Ultra if:**

✅ Need KPM support<br>
✅ Legacy non-GKI device<br>
✅ Want built-in SUSFS<br>
✅ Banking app hiding<br>
✅ 32-bit ARM device

</td>
</tr>
</table>

## Modules & Tools

> The primary source for modules is the **[official module repository](https://modules.kernelsu.org/)**.

### Zygisk & frameworks

KernelSU has no built-in Zygisk; use a standalone implementation for Zygisk modules.

- [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext)- standalone Zygisk implementation.
- [**ReZygisk**](https://github.com/PerformanC/ReZygisk)- open-source, transparent Zygisk implementation.
- [**LSPosed**](https://github.com/LSPosed/LSPosed)- Xposed framework (requires Zygisk).

### Module managers

- [**MMRL**](https://github.com/MMRLApp/MMRL)- modern module manager with a built-in repository, updates, backup/restore, and WebUI support.

### Root hiding

- [**SUSFS**](https://gitlab.com/simonpunk/susfs4ksu)- kernel patches + userspace addon providing root-hiding mechanisms (experimental; requires a SUSFS-patched kernel).
- [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module)- addon root-hiding service for KernelSU.

> [!WARNING]
> These provide *root-hiding mechanisms* and **may improve** compatibility with apps that perform root checks. They do **not** guarantee passing Play Integrity or bypassing any given banking app, and often require additional configuration.

## Device Kernels

Prebuilt kernels save you from compiling. **Always verify the exact device model, Android version, kernel version, and security-patch level before flashing.**

> For anything not listed here, check the maintained community list of [KernelSU-Next unofficially supported devices](https://kernelsu-next.github.io/webpage/pages/devices.html), the [XDA KernelSU tag](https://xdaforums.com/tags/ksu/), or GitHub topic/search results.

| Project | Devices | Notes |
|---------|---------|-------|
| [WildKernels- GKI](https://github.com/WildKernels/GKI_KernelSU_SUSFS) | GKI 2.0 (5.10+) devices | KernelSU + SUSFS; active |
| [WildKernels- Sultan](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) | Google Pixel | Sultan base + SUSFS; active |
| [WildKernels- OnePlus](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) | OnePlus devices | KernelSU + SUSFS; active |
| [WildKernels- Samsung](https://github.com/WildKernels/Samsung_KernelSU_SUSFS) | Samsung devices | KernelSU + SUSFS; active |
| [YuzakiKokuban- Samsung](https://github.com/YuzakiKokuban) | Galaxy S23/S24/S25, Tab S10 | KernelSU kernel sources (`sm8550`, `sm8650`, `sm8750`, `mt6989`); active |
| [KernelSU LKM- OnePlus 12](https://github.com/snowwolf725/KernelSU_LKM_For_Oneplus12) | OnePlus 12 | LKM for OxygenOS/ColorOS; active |
| [topnotchfreaks- msm-5.15](https://github.com/topnotchfreaks/kernel_msm-5.15) | Redmi Note 12/13 4G, Redmi Pad SE, Redmi 15/POCO M7 | SukiSU-Ultra + KPM + SUSFS variants; active |

**Kernel selection checklist:** exact device match · matching Android/kernel version · security-patch level (anti-rollback can brick on older patches) · active maintenance · a copy of your stock `boot.img` for recovery.

## Building from Source

- **Official KernelSU:** build the LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk) (recommended since v3.0). The GKI and non-GKI build guides are archival- [How to build](https://kernelsu.org/guide/how-to-build.html) · [Integrate for non-GKI](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html).
- **Forks** (KernelSU-Next, SukiSU-Ultra, ReSukiSU) still support direct kernel integration- see each repository's `kernel/setup.sh`.
- **Tools:** [AnyKernel3](https://github.com/osm0sis/AnyKernel3) (packaging/flashing) · [kernel_build_action](https://github.com/dabao1955/kernel_build_action) (GitHub Actions builds).
- **Vendor kernel sources:** [Google](https://android.googlesource.com/kernel/) · [Xiaomi](https://github.com/MiCode/Xiaomi_Kernel_OpenSource) · [OnePlus](https://github.com/OnePlusOSS) · [Samsung](https://opensource.samsung.com).

## Documentation

- [What is KernelSU?](https://kernelsu.org/guide/what-is-kernelsu.html)
- [Installation](https://kernelsu.org/guide/installation.html)
- [Metamodules](https://kernelsu.org/guide/metamodule.html)
- [Module guide](https://kernelsu.org/guide/module.html) · [Module WebUI](https://kernelsu.org/guide/module-webui.html) · [Module configuration](https://kernelsu.org/guide/module-config.html)
- [App Profile](https://kernelsu.org/guide/app-profile.html)
- [Difference with Magisk](https://kernelsu.org/guide/difference-with-magisk.html)
- [Unofficially supported devices](https://kernelsu.org/guide/unofficially-support-devices.html)
- [FAQ](https://kernelsu.org/guide/faq.html) · [Rescue from bootloop](https://kernelsu.org/guide/rescue-from-bootloop.html)

## Community

**Telegram**

- [@KernelSU](https://t.me/KernelSU)- official announcements channel.
- [@KernelSU_group](https://t.me/KernelSU_group)- official community group.
- [@Sukiksu](https://t.me/Sukiksu)- SukiSU community.
- [@ReSukiSU](https://t.me/ReSukiSU)- ReSukiSU community.

**Other**

- [GitHub Discussions](https://github.com/tiann/KernelSU/discussions) · [Issue tracker](https://github.com/tiann/KernelSU/issues)
- [r/KernelSU](https://www.reddit.com/r/KernelSU/) on Reddit
- [XDA Developers- KernelSU tag](https://xdaforums.com/tags/ksu/)


## Troubleshooting

> [!NOTE]
> Before troubleshooting, ensure you have a backup of your stock boot image. This is crucial for recovery.

### Common Issues

| Issue                        | Possible Cause                        | Solution                                             |
| ---------------------------- | ------------------------------------- | ---------------------------------------------------- |
| **Bootloop**                 | Incompatible kernel/module            | Flash stock boot.img via fastboot, disable modules   |
| **App Crashes**              | SELinux policy conflicts              | Check and adjust SELinux policies in app profiles    |
| **Module Not Working**       | No metamodule installed (KSU 3.0+)   | Install a metamodule first; verify module compatibility |
| **Root Not Detected**        | Manager not installed properly        | Reinstall KernelSU Manager, verify kernel version    |
| **Play Integrity Failing**   | Root detection                        | Install Shamiko or SuSFS, configure hiding properly  |
| **Update Failed**            | Insufficient storage/corrupt download | Clear cache, re-download, ensure adequate storage    |
| **Banking Apps Not Working** | Root detection                        | Configure app profiles, install hiding modules       |
| **System Unstable**          | Conflicting modules                   | Disable modules one by one to identify culprit       |

### Emergency Recovery

> [!WARNING]
> If your device is in a bootloop, follow these steps immediately to restore functionality.

<details>
<summary><b>🚨 Click to expand: Bootloop Recovery & Emergency Procedures</b></summary>

#### Bootloop Recovery

**Immediate Steps:**
```bash
# 1. Enter fastboot mode (Power + Volume Down)
# 2. Connect device to PC
# 3. Flash stock boot image
fastboot flash boot stock_boot.img

# 4. If needed, clear cache
fastboot erase cache

# 5. Reboot
fastboot reboot
```

**Alternative via Recovery:**
1. Boot into TWRP/custom recovery
2. Flash stock boot image from recovery
3. Wipe cache and dalvik cache
4. Reboot system

**Prevention:**
- Always keep stock boot image backup
- Test kernels with temporary boot first: `fastboot boot test_boot.img`
- Create TWRP backups before major changes
- Keep emergency download mode access available

#### Module-Related Issues

**Safe Mode Boot:**
1. Create file `/data/adb/modules/.disable_modules` before boot
2. This disables all modules for troubleshooting
3. Remove problematic modules
4. Delete the disable file and reboot

**Commands:**
```bash
# Disable all modules
adb shell su -c "touch /data/adb/modules/.disable_modules"
adb reboot

# Remove specific module
adb shell su -c "rm -rf /data/adb/modules/[module_name]"
adb reboot

# View module logs
adb shell su -c "cat /data/adb/modules/[module_name]/install.log"
```

</details>

### Debugging Commands

<details>
<summary><b>🔍 Click to expand: Debug Commands & Diagnostics</b></summary>

```bash
# Check KernelSU status
cat /proc/version | grep KernelSU
su -c "kernelsu --version"

# Kernel logs
dmesg > /sdcard/dmesg.log
cat /proc/last_kmsg > /sdcard/last_kmsg.log

# KernelSU specific logs
logcat -s "KernelSU" > /sdcard/kernelsu.log
logcat -b all > /sdcard/full_logcat.log

# Module installation logs
cat /data/adb/modules/*/install.log > /sdcard/module_logs.log

# Check SELinux status
getenforce
sestatus

# List loaded modules
ls -la /data/adb/modules/
cat /data/adb/modules/*/module.prop

# Check mount points
mount | grep overlay
mount | grep /system

# Verify root access
su -c "id"
su -c "whoami"

# Check kernel config
zcat /proc/config.gz | grep KSU

# Monitor system resources
top -n 1
free -h
df -h
```

</details>

### Device-Specific Issues

<details>
<summary><b>📱 Click to expand: Device-Specific Troubleshooting</b></summary>

#### Samsung Devices
- **Knox Triggered**: Some Samsung devices trip Knox warranty bit (irreversible)
- **Secure Boot**: May need to disable secure boot verification in kernel
- **Encryption Issues**: Some kernels incompatible with Samsung encryption
- **OEM Unlock**: Ensure OEM unlocking is enabled in Developer Options

#### OnePlus Devices
- **Fastboot Commands**: Use `fastboot oem unlock` for bootloader
- **Generic GKI**: OnePlus devices generally do not support generic GKI builds - use manufacturer-specific kernels
- **Anti-Rollback**: Be careful about security patch levels; flashing older kernels can brick devices
- **Slot System**: A/B partition devices need careful slot management

#### Xiaomi Devices
- **Anti-Rollback**: Be careful with MIUI version downgrades (brick risk)
- **Bootloader Unlock**: Xiaomi requires a waiting period via the Mi Unlock Tool
- **MIUI Optimizations**: Some MIUI features conflict with KernelSU
- **Vendor Mismatch**: Ensure kernel matches vendor version

#### Google Pixel Devices
- **Hardware Attestation**: Strong Play Integrity enforcement on newer Pixels
- **Verified Boot**: Orange state warning on boot (normal)
- **Titan M Security**: Hardware security module affects root hiding
- **OTA Updates**: Easy to re-root after OTAs with KernelSU

</details>

### Performance Issues

<details>
<summary><b>⚡ Click to expand: Performance Troubleshooting</b></summary>

#### System Slowdown

**Diagnosis:**
1. **Identify problematic modules**: Disable modules one by one
2. **Check CPU throttling**: Monitor thermals and frequency scaling
3. **Review I/O performance**: OverlayFS overhead on slow storage
4. **Analyze system logs**: Look for kernel errors or warnings

**Commands:**
```bash
# Monitor CPU usage
top -m 10

# Check I/O stats
iostat -x 1 10

# View thermal zones
cat /sys/class/thermal/thermal_zone*/temp

# Check for errors
dmesg | grep -i error
logcat | grep -i error
```

#### Random Reboots

**Troubleshooting:**
1. **Check kernel logs**: `dmesg` and `/proc/last_kmsg`
2. **Monitor memory usage**: Look for OOM (Out Of Memory) killer activity
3. **Verify hardware stability**: Stress test without KernelSU
4. **Test minimal config**: Remove all modules temporarily

</details>

### App Compatibility

<details>
<summary><b>🏦 Click to expand: Banking & Gaming App Compatibility</b></summary>

#### Banking/Payment Apps

**Solutions:**
1. **Configure app profiles**: Restrict root access for sensitive apps
2. **Enable advanced hiding**: Install SuSFS or Shamiko modules
3. **Check Play Integrity**: Use Play Integrity API tester
4. **Hardware attestation**: Some devices use hardware-based detection (harder to bypass)

**Recommended Setup:**
```bash
# Install hiding modules
# 1. Install Shamiko module
# 2. Install SuSFS4KSU module
# 3. Configure DenyList in manager
# 4. Reboot device
# 5. Test with Play Integrity checker
```

#### Game Apps

**Anti-cheat Detection:**
- Some games detect root and ban accounts
- Use hiding modules carefully
- Configure app profiles to deny root access
- Consider using non-rooted profiles for gaming

</details>

### Getting Help

<details>
<summary><b>💬 Click to expand: Support Resources & Log Collection</b></summary>

#### Information to Provide

When seeking help, include:
1. **Device Information**: Model, Android version, kernel version
2. **KernelSU Variant**: Official, Next, Wild KSU, or SukiSU-Ultra + version number
3. **Installation Method**: How you installed KernelSU
4. **Metamodule**: Which metamodule is installed (KernelSU 3.0+)
5. **Reproduction Steps**: Detailed steps to reproduce the issue
6. **Logs**: Relevant log files (dmesg, logcat, module logs)
7. **Module List**: All installed modules and versions

#### Log Collection Script

```bash
#!/system/bin/sh
# Collect comprehensive logs for troubleshooting

LOGDIR="/sdcard/kernelsu_logs_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$LOGDIR"

# System info
getprop > "$LOGDIR/system_props.txt"
uname -a > "$LOGDIR/kernel_info.txt"
cat /proc/version > "$LOGDIR/kernel_version.txt"

# KernelSU info
su -c "kernelsu --version" > "$LOGDIR/kernelsu_version.txt" 2>&1

# Logs
dmesg > "$LOGDIR/dmesg.log"
logcat -d > "$LOGDIR/logcat.log"
cat /proc/last_kmsg > "$LOGDIR/last_kmsg.log" 2>/dev/null

# Module info
ls -laR /data/adb/modules > "$LOGDIR/modules_list.txt"
cat /data/adb/modules/*/module.prop > "$LOGDIR/modules_props.txt" 2>/dev/null

# Mount info
mount > "$LOGDIR/mount_points.txt"
df -h > "$LOGDIR/disk_usage.txt"

echo "Logs collected in: $LOGDIR"
```

</details>

#### Support Priority

1. **Official Documentation**: Check [kernelsu.org](https://kernelsu.org/) FAQ
2. **GitHub Discussions**: Search existing issues and discussions
3. **Telegram Groups**: Ask in appropriate variant-specific group
4. **XDA Forums**: Device-specific threads
5. **Reddit**: r/KernelSU for general questions

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

## FAQs

**Frequently asked questions about KernelSU - Quick answers to common queries.**

### General Questions

<details open>
<summary><b>What is a Metamodule and why do I need one?</b></summary>

**From KernelSU 3.0+**, the built-in module mounting system was removed. A **metamodule** is now required to provide module mounting infrastructure.

**Why this change?**
- **Reduced detection**: KernelSU itself doesn't mount modules, making it harder to detect
- **Flexibility**: Choose your preferred mounting method (OverlayFS, Magic Mount, Hybrid)
- **Stability**: Core KernelSU remains stable while mounting systems evolve

**Quick Start:**
1. Download [meta-overlayfs](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) (recommended for beginners)
2. Install via KernelSU Manager > Modules
3. Reboot device
4. Now you can install regular modules

See [Understanding Metamodules](#understanding-metamodules) for complete details.

</details>

<details>
<summary><b>What is KernelSU and how does it differ from Magisk?</b></summary>

KernelSU is a **kernel-based root solution** operating in kernel space, while Magisk operates in userspace.

**Key Differences:**

| Aspect | KernelSU | Magisk |
|--------|----------|--------|
| **Architecture** | Kernel-level | Userspace |
| **Security** | Superior isolation | Good but less isolated |
| **Module System** | Metamodule-based (3.0+) | Magic Mount (built-in) |
| **Installation** | GKI / LKM modes | Boot patching |
| **Compatibility** | Requires compatible kernel | Universal |
| **Future-proof** | Built for modern Android | Legacy support focus |

</details>

<details>
<summary><b>Which installation mode should I use: GKI or LKM?</b></summary>

**Choose based on your device and needs:**

**LKM Mode (Recommended for most):**
- ✅ Keeps manufacturer kernel optimizations
- ✅ Easy updates via app
- ✅ OTA-friendly
- ✅ Works with stock firmware
- ⚠️ Requires official firmware

**GKI Mode:**
- ✅ Universal compatibility
- ✅ Works on Samsung Knox devices
- ✅ Better for custom ROMs
- ⚠️ Loses manufacturer optimizations
- ⚠️ Manual updates required

See [Installation Modes](#installation-modes) for detailed comparison.

</details>

<details>
<summary><b>Which KernelSU variant should I use?</b></summary>

**Quick Selection Guide:**

- **Modern devices** (Android 12+, kernel 5.10+) → **Official KernelSU**
- **Mid-range devices** (Android 9–11, kernel 4.4–6.6) → **KernelSU-Next**
- **Root hiding focus** (Android 9+, kernel 4.4–6.6) → **Wild KSU**
- **KPM / legacy / built-in SUSFS** (Android 7+, broad kernel support) → **SukiSU-Ultra**
- **Multi-manager / SukiSU ecosystem** → **ReSukiSU**

See [KernelSU Variants](#kernelsu-variants) for detailed comparison.

</details>

<details>
<summary><b>Is KernelSU safer than Magisk?</b></summary>

**Yes, in several ways:**

- ✅ Kernel-level operation prevents userspace attacks
- ✅ App Profile system for granular permission control
- ✅ Zero system modification maintains integrity
- ✅ Hardware security integration (ARM TrustZone)
- ✅ seccomp + ioctl hooks (v2.0+) eliminate many side-channel detection vectors
- ✅ Metamodule architecture reduces detection surface

However, both are safe when properly configured.

</details>

<details>
<summary><b>Can I use Magisk modules with KernelSU?</b></summary>

**Compatibility varies:**

| Module Type | Compatibility |
|-------------|---------------|
| **Simple modules** | ✅ Most work without changes (with metamodule) |
| **Complex modules** | ⚠️ May need adaptation for metamodule system |
| **Zygisk modules** | ⚠️ Require ZygiskNext or ReZygisk |
| **Hardware-specific** | ✅ Usually compatible |

**Remember**: You must install a [metamodule](#understanding-metamodules) first for any modules to work on KernelSU 3.0+.

</details>

<details>
<summary><b>Will KernelSU break OTA updates?</b></summary>

**Generally no:**

- ✅ System partition remains unmodified
- ⚠️ Boot partition may need re-patching after OTA
- ✅ LKM mode has OTA survival features (install to inactive slot before rebooting)
- ⚠️ Manual re-installation may be required for major updates

Always keep your patched boot image backup!

</details>

---

### Installation & Setup

<details>
<summary><b>What changed in KernelSU 3.0 and how does it affect me?</b></summary>

**Major Changes in KernelSU 3.0+:**

1. **⚠️ Module mounting removed from core**: Fresh installations now require a [metamodule](#understanding-metamodules) for modules to work
2. **⚠️ Official GKI image mode dropped**: Build LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk); the GKI build guide is archival (forks still ship GKI builds)
3. **📦 Official module repository**: Verified, security-reviewed modules at [modules.kernelsu.org](https://modules.kernelsu.org)
4. **🛡️ Reduced detection surface**: seccomp + ioctl hooks (v2.0) plus metamodule architecture make detection harder
5. **🪄 Magica jailbreak mode (v3.2+)**: Optional deeper system access
6. **🔧 Flexible mounting**: Choose between OverlayFS, Magic Mount, or hybrid metamodules

**What you need to do:**
- **Fresh installations**: Must install a metamodule before modules will work
- **Existing installations**: Continue to work normally (no action needed)
- **Upgrading**: May need to install a metamodule if modules stop working

**Recommended metamodule**: [meta-overlayfs](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) for most users

See [Understanding Metamodules](#understanding-metamodules) for complete details.

</details>

<details>
<summary><b>How do I check if my device is compatible?</b></summary>

**Check your kernel version:**

```bash
# Via ADB
adb shell uname -r

# On device terminal
uname -r
```

Then refer to the [Compatibility Matrix](#compatibility-check) to find the right variant.

</details>

<details>
<summary><b>Do I need to uninstall Magisk before installing KernelSU?</b></summary>

**Yes, strongly recommended:**

1. ✅ Uninstall all Magisk modules
2. ✅ Uninstall Magisk completely
3. ✅ Flash stock boot image
4. ✅ Then install KernelSU

They will conflict if installed together.

</details>

<details>
<summary><b>Can I have both Magisk and KernelSU installed?</b></summary>

**No.** They modify the boot process differently and will conflict. Choose one solution for your device.

</details>

<details>
<summary><b>How do I backup before installing?</b></summary>

**Essential backups:**

1. 💾 Full TWRP backup (if available)
2. 💾 Backup stock boot.img (critical!)
3. 📝 Document installed modules
4. 💾 Export app data
5. 💾 Save important files to external storage

</details>

---

### Modules & Features

<details>
<summary><b>Where can I find KernelSU modules?</b></summary>

**Top Sources:**

- [**MMRL**](https://github.com/MMRLApp/MMRL) - Modern module manager with repository
- [**Awesome Android Root**](https://awesome-android-root.pages.dev/android-root-apps/?filters=%5BK%5D) - Curated collection
- **GitHub** - Search "kernelsu module"
- **Telegram** - Community-shared modules
- **XDA Forums** - Device-specific modules

**⚠️ Remember**: For KernelSU 3.0+ fresh installations, you must first install a [metamodule](#understanding-metamodules) before regular modules will work!

</details>

<details>
<summary><b>My modules aren't working after installing KernelSU 3.0+, why?</b></summary>

**You need a metamodule!**

KernelSU 3.0+ removed built-in module mounting. Fresh installations require a metamodule to provide mounting infrastructure.

**Solution:**
1. Download [meta-overlayfs](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) (recommended)
2. Install via KernelSU Manager > Modules
3. Reboot device
4. Now regular modules will work

See [Understanding Metamodules](#understanding-metamodules) for details and alternatives.

</details>

<details>
<summary><b>Can I switch between different metamodules?</b></summary>

**Yes, but with caution:**

⚠️ Only ONE metamodule can be active at a time.

**To switch:**
1. Uninstall all regular modules
2. Uninstall current metamodule
3. Reboot device
4. Install new metamodule
5. Reboot again
6. Reinstall regular modules

**Popular choices:**
- **meta-overlayfs**: Official, recommended for most
- **mountify**: Advanced, cross-platform support
- **meta-hybrid_mount**: Maximum compatibility with auto-fallback

</details>

<details>
<summary><b>What are App Profiles and how do I use them?</b></summary>

**App Profiles** provide granular root permission control:

- ⚙️ Custom UID/GID assignment
- 🔒 Capability restrictions
- 🛡️ SELinux context customization
- ⏰ Time-based access control
- 🔐 Namespace isolation

Configure in KernelSU Manager under each app's settings.

Learn more: [App Profile System Guide](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#app-profile-system)

</details>

<details>
<summary><b>What is KPM (Kernel Patch Module) in SukiSU-Ultra?</b></summary>

**KPM** allows running code directly in kernel space, similar to Loadable Kernel Modules (LKM). It provides the ability to do inline-hook and syscall-table-hook in kernel space - capabilities not available in other KernelSU variants. This is an exclusive feature of SukiSU-Ultra.

Enable it by setting `CONFIG_KPM=y` when building the kernel.

</details>

---

### Troubleshooting

<details>
<summary><b>My device is in bootloop, what do I do?</b></summary>

**Emergency recovery:**

```bash
# 1. Enter fastboot mode (Power + Volume Down)
# 2. Connect to PC
# 3. Flash stock boot image
fastboot flash boot stock_boot.img

# 4. Reboot
fastboot reboot
```

**This is why you ALWAYS keep a stock boot.img backup!**

</details>

<details>
<summary><b>Banking apps aren't working, how do I fix this?</b></summary>

**Root hiding setup:**

1. Install **Shamiko** or **SuSFS** module
2. Configure **DenyList** in KernelSU Manager
3. Add banking apps to DenyList
4. Hide KernelSU Manager app
5. Test with Play Integrity checker

See [Troubleshooting](#-troubleshooting) for detailed steps.

</details>

<details>
<summary><b>How do I verify KernelSU is working?</b></summary>

**Quick verification:**

```bash
# Check kernel
cat /proc/version | grep KernelSU

# Test root
su -c "id"

# Or open KernelSU Manager and check status
```

</details>


## Contributing

Contributions are welcome- new tools, modules, maintained device kernels, and documentation fixes. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Disclaimer

Rooting and kernel modification can void warranties, brick devices, and expose security vulnerabilities. This list is provided for **educational and informational purposes only**- you assume all risks.

KernelSU and its derivatives are independent, community-driven projects. They are not affiliated with or endorsed by Google, Android, or any device manufacturer.


### Legal & Safety Information

**Educational Purpose Only**

This documentation is provided for **educational and informational purposes only**. Users are solely responsible for:

- Understanding and complying with local laws
- Following device warranty terms
- Maintaining device security
- Device modifications and consequences

**No Warranty or Liability**

Contributors and maintainers are **NOT liable** for:

- Device damage or bricking
- Data loss or corruption
- Warranty violations
- Legal consequences
- Security vulnerabilities

---

### Safety Best Practices

<details>
<summary><b>🛡️ Click to expand: Essential Safety Guidelines</b></summary>

**Always Do:**

| Action | Why It Matters |
|--------|----------------|
| ✅ **Create complete backups** | Essential for recovery |
| ✅ **Read documentation thoroughly** | Understand before acting |
| ✅ **Test on non-critical devices** | Avoid daily driver risks |
| ✅ **Keep stock firmware** | Emergency recovery option |
| ✅ **Research device-specific issues** | Know your device limitations |
| ✅ **Understand security implications** | Protect your data |

**Never Do:**

| Action | Risk |
|--------|------|
| ❌ **Proceed without backups** | Irreversible data loss |
| ❌ **Grant root to untrusted apps** | Security compromise |
| ❌ **Install unknown modules** | Malware/instability |
| ❌ **Ignore security warnings** | Serious vulnerabilities |
| ❌ **Modify without understanding** | System damage |

</details><br>

> [!IMPORTANT]
> KernelSU and its derivatives are **independent, community-driven projects**. They are not affiliated with, endorsed by, or connected to Google, Android, device manufacturers, or any other commercial entities.

---

## License

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

**This project is licensed under the [MIT License](LICENSE).**

---

## Acknowledgments

**Special thanks to all contributors who made KernelSU possible.**

**Project Creators**

- [**tiann**](https://github.com/tiann) - Creator of KernelSU, visionary behind kernel-based root solutions
- [**topjohnwu**](https://github.com/topjohnwu) - Magisk creator, inspiration for systemless modifications

**Derivative Maintainers**

- **KernelSU-Next Team** - Enhanced fork development and innovation
- **Wild KSU Team (WildKernels)** - Customization and root hiding focused fork
- **SukiSU-Ultra Team** - KPM integration, legacy device support and compatibility
- **ReSukiSU Team** - Multi-manager support and metamodule integration

**Community Contributors**

- Module developers creating useful tools
- Documentation translators and writers
- Community moderators and support staff
- Everyone who shares knowledge

**Special Recognition**

- All kernel developers maintaining device-specific builds
- Community members providing support
- Contributors to this awesome list

---

**Made with ❤️ by the KernelSU Community**

<sub>Last Updated: August 2026 | Maintained by [Fynks](https://github.com/fynks)</sub>

<br>

**[⬆ Back to Top](#awesome-kernelsu)**

</div>
