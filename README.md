<div align="center">

<img src="./media/kernelsu-logo.svg" alt="KernelSU Logo" width="200"/>
<br>

# Awesome KernelSU

**A comprehensive curated list of KernelSU resources, tools, modules, and documentation**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/fynks/awesome-kernelsu?style=flat-square&logo=github)](https://github.com/fynks/awesome-kernelsu/stargazers)
[![Browse Kernels](https://img.shields.io/badge/🔍_Browse-Prebuilt_Kernels-2563eb?style=flat-square)](#prebuilt-kernels)
[![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)


<br>

[**Intro**](#what-is-kernelsu) &nbsp; • &nbsp; [**Prebuilt Kernels**](#prebuilt-kernels) &nbsp; • &nbsp; [**Variants**](#kernelsu-variants) &nbsp; • &nbsp; [**Docs**](#-documentation) &nbsp; • &nbsp; [**Community**](#-community)

<br>

</div>


## What is KernelSU?

**KernelSU is a kernel-based root solution for Android** that operates inside the Linux kernel, providing more control over userspace apps than traditional rooting methods.

> [!IMPORTANT] Critical Notice - KernelSU 3.0+ Changes
> **KernelSU 3.0+ Major Changes**: From version 3.0 onwards, KernelSU and its forks (KernelSU-Next, Wild KSU, and now SukiSU-Ultra / ReSukiSU) have removed built-in module mounting. Fresh installations now **require a metamodule** for modules to function. See [Understanding Metamodules](#understanding-metamodules) for details.
>
> **GKI image mode deprecated (official):** Since v3.0, official KernelSU has dropped GKI *image* mode for faster iteration - the GKI build guide is now archival. **LKM mode** (built with [Ylarod/ddk](https://github.com/Ylarod/ddk)) is the recommended path. Forks still ship GKI builds.

### Key Features

- **Root Access Control** - Only permitted apps can access or see su; all other apps remain unaware of it
- **Kernel-Level Isolation** - Root access operates in kernel space, preventing userspace tampering and detection
- **Metamodule System** - Pluggable module infrastructure for systemless /system modifications
- **Advanced Permission Control**: Granular app-level root access management with customizable profiles
- **App Profile System**: Customizable groups, capabilities, and SELinux rules for fine-grained root privilege control
- **Module Configuration System**: Built-in key-value store for modules to save persistent or temporary settings

<br>

> **Learn More**: [Comprehensive KernelSU Guide](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide) | [Official Documentation](https://kernelsu.org/) | [Official Module Repo](https://modules.kernelsu.org)


## Table of Contents
- [What is KernelSU?](#what-is-kernelsu)
- [Getting Started](#getting-started)
- [Installation Modes](#installation-modes)
- [Understanding Metamodules](#understanding-metamodules)
- [KernelSU Variants](#kernelsu-variants)
- [Comparison](#comparison)
- [Prebuilt Kernels](#prebuilt-kernels)
- [Installation](#-installation)
- [Documentation](#-documentation)
- [Modules and Tools](#modules-and-tools)
- [Building from Source](#️-building-from-source)
- [Community](#-community)
- [Troubleshooting](#-troubleshooting) • [FAQ](#-faq) • [Contributing](#-contributing)
- [Disclaimer](#disclaimer) • [License](#license)

## Getting Started

### Prerequisites

Before installing KernelSU, ensure you have:
- **Unlocked bootloader** (required for all installation methods)
- **Complete data backup** (always backup before modifying your device)
- **ADB and Fastboot tools** installed on your computer
- **Compatible device** (check compatibility below)

> [!TIP]
> **New to bootloader unlocking?** Check out the comprehensive guide at [Awesome-Android-Root](https://awesome-android-root.pages.dev/rooting-guides/how-to-unlock-bootloader)

### New to KernelSU?

1. **Check Compatibility**
   - Kernel 5.10+ for official KernelSU (Android 12+)
   - Kernel 4.4–6.6 for KernelSU-Next (Android 9+)
   - Kernel 4.4–6.6 for Wild KSU (Android 9+) - root hiding focused
   - Kernel 3.4+ (GKI and non-GKI) for SukiSU-Ultra (Android 7+; 3.x experimental)

2. **Choose Installation Mode**
   - **GKI Mode**: Replaces device kernel (universal compatibility, works on Samsung Knox)
   - **LKM Mode**: Loads as kernel module (preserves optimizations, easy updates)
   - See [Installation Modes](#installation-modes) for detailed comparison

3. **Download Manager**
   - Get the official Manager APK for your chosen variant (links in [Variants](#kernelsu-variants) section)

4. **Install KernelSU**
   - Follow the [installation guide](#-installation) for your chosen method

5. **Install Metamodule**
   - **CRITICAL**: KernelSU 3.0+ requires a metamodule for modules to work
   - See [Understanding Metamodules](#understanding-metamodules) section

6. **Verify Installation**
   - Open KernelSU Manager and confirm root status

### Device Selection Guide

| Device Age | Kernel Version  | Recommended Variant   | Primary Benefits                       |
| ---------- | --------------- | --------------------- | -------------------------------------- |
| 2021+      | 5.10+ (GKI 2.0) | **KernelSU Official** | Maximum stability, official support    |
| 2018–2021  | 4.4–6.6         | **KernelSU-Next**     | Enhanced features, broad compatibility |
| 2018–2021+  | 4.4–6.6         | **Wild KSU**          | Customization & root hiding focus      |
| Pre-2018   | 3.4+ (non-GKI)  | **SukiSU-Ultra**      | Legacy support, KPM, built-in SUSFS    |

### Essential First Steps

After successful installation:

1. **Install Metamodule**: Choose and install a [metamodule](#understanding-metamodules) (meta-overlayfs recommended for most users)
2. **Configure App Profiles**: Set up [App Profiles](https://kernelsu.org/guide/app-profile.html) for granular root permission management
3. **Install Module Manager**: Use [MMRL](https://github.com/MMRLApp/MMRL) for easier module management
4. **Setup Root Hiding**: Install SuSFS module for banking/payment app compatibility
5. **Join Community**: Connect with [Telegram community](https://t.me/KernelSU_group) for support and updates
6. **Create Backup**: Make a backup of your patched boot image for recovery

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Installation Modes

KernelSU supports two installation modes on GKI-compatible devices, each with distinct advantages.

### GKI Mode

**How it works:** Replaces device's original kernel with KernelSU Generic Kernel Image.

> [!NOTE]
> **Official KernelSU dropped GKI *image* mode support in v3.0** (the build guide is now archival) and recommends LKM via [Ylarod/ddk](https://github.com/Ylarod/ddk). Forks (KernelSU-Next, Wild KSU, SukiSU-Ultra) still actively ship GKI builds. Note: if both GKI and LKM are present, GKI takes priority and LKM is ignored.

**Advantages:**

- ✅ Universal GKI device compatibility
- ✅ Works on Samsung Knox devices
- ✅ Independent of firmware updates
- ✅ Better for heavily modified devices
- ✅ More stable on custom ROMs

**Disadvantages:**

- ❌ Loses manufacturer kernel optimizations
- ❌ Requires manual fastboot flashing
- ❌ Must reflash after major updates

**Best for:** Samsung devices, emulators, WSA, custom ROMs, devices without official firmware

---

### LKM Mode (Loadable Kernel Module)

**How it works:** Loads KernelSU as a kernel module without replacing the kernel.

**Advantages:**

- ✅ Preserves original kernel and optimizations
- ✅ Easy in-app updates
- ✅ OTA-friendly (install to inactive slot)
- ✅ No AVB/dm-verity issues
- ✅ Can disable without reboot
- ✅ Better performance (keeps manufacturer tuning)

**Disadvantages:**

- ❌ Requires official firmware
- ❌ May not work on all devices
- ❌ Less compatible with modified firmwares

**Best for:** Most modern phones with stock/near-stock firmware

---

### Which Mode to Choose?

| Scenario | Recommended Mode | Reason |
|----------|------------------|--------|
| Stock firmware phones | **LKM** | Preserves optimizations, easy updates |
| Samsung devices | **GKI** | Knox compatibility |
| Custom ROMs | **GKI** | Better modified firmware support |
| Emulators/WSA | **GKI** | Universal compatibility |
| Heavily modified | **GKI** | More reliable |

> **Detailed Guide**: See the [complete installation modes comparison](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#installation-modes) for more information.

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Understanding Metamodules

> [!IMPORTANT]
> **CRITICAL CHANGE IN KERNELSU 3.0+**: KernelSU no longer has built-in module mounting. Fresh installations **REQUIRE** a metamodule for modules that modify `/system` files to function - without one, such modules install but are **NOT** mounted. Modules that only use scripts, `sepolicy`, or `system.prop` still work without a metamodule.

### What is a Metamodule?

A **metamodule** is a special type of KernelSU module that provides core infrastructure for the module system. Unlike regular modules that modify system files, metamodules control **how** regular modules are installed and mounted.

> [!NOTE]
> This now applies across the ecosystem: official KernelSU, KernelSU-Next, Wild KSU, **and** SukiSU-Ultra / ReSukiSU all delegate module mounting to the installed metamodule. Browse verified metamodules and modules at the **[Official Module Repository](https://modules.kernelsu.org)**.

### Why Metamodules?

The metamodule architecture provides several key benefits:

- **🛡️ Reduced Detection Surface**: KernelSU itself doesn't perform mounts, reducing detection vectors for banking apps
- **🔧 Flexibility**: Users can choose mounting implementation (OverlayFS, Magic Mount, hybrid)
- **💪 Stability**: Core KernelSU remains stable while mounting implementations can evolve independently
- **🚀 Innovation**: Community can develop alternative mounting strategies

### Single Metamodule Constraint

> [!WARNING]
> **Only ONE metamodule can be installed at a time**. To switch metamodules:
> 1. Uninstall all regular modules
> 2. Uninstall current metamodule
> 3. Reboot device
> 4. Install new metamodule
> 5. Reinstall regular modules

### Available Metamodules

| Metamodule | Description | Best For |
|------------|-------------|----------|
| [**meta-overlayfs**](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) | Official reference implementation using OverlayFS | Most users, standard setup, recommended starting point |
| [**mountify**](https://github.com/backslashxx/mountify) | OverlayFS with tmpfs/ext4 sparse support, cross-platform (APatch/Magisk) | Reduced detection, multi-root support, advanced users |
| [**meta-hybrid_mount**](https://github.com/YuzakiKokuban/meta-hybrid_mount) | Dual engine (OverlayFS + Magic Mount) with conflict monitor, diagnostics & auto-fallback | Maximum compatibility, stealth mode |

### Installing Your First Metamodule

**Step-by-Step Installation:**

1. **Download metamodule ZIP** from GitHub releases (meta-overlayfs recommended)
2. **Open KernelSU Manager** > Modules
3. **Tap "Install from storage"** (➕ button)
4. **Select the metamodule ZIP** file
5. **Reboot device**

The active metamodule will be displayed in your module list with a special designation.

### Metamodule Compatibility

With a metamodule installed:

- ✅ Most Magisk modules work (when using a compatible metamodule)
- ⚠️ Zygisk modules require [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext) or [ReZygisk](https://github.com/PerformanC/ReZygisk)
- ✅ Growing native KernelSU module support
- ✅ Module metadata stored in `/data/adb/modules/`
- ✅ Module content stored in `/data/adb/metamodule/mnt/` (with meta-overlayfs)

> **Complete Guide**: For detailed metamodule information, mounting strategies, and troubleshooting, visit the [KernelSU Managing Modules Guide](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#managing-modules)

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## KernelSU Variants

### Official KernelSU

[![GitHub](https://img.shields.io/badge/GitHub-tiann%2FKernelSU-blue?logo=github&style=flat-square)](https://github.com/tiann/KernelSU)
[![Documentation](https://img.shields.io/badge/Docs-kernelsu.org-green?style=flat-square)](https://kernelsu.org/)
[![Release](https://img.shields.io/github/v/release/tiann/KernelSU?style=flat-square)](https://github.com/tiann/KernelSU/releases)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU)

> The original KernelSU implementation for modern Android devices

<details open>
<summary><b>📋 View Details</b></summary>

**Best For:** Modern flagship devices (2021+) prioritizing stability and official support

**✨ Key Features:**
- Official GKI 2.0 support (kernel 5.10+) via **LKM mode** (GKI *image* mode deprecated since v3.0 - build LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk))
- Older kernels (4.14+) supported with manual compilation (archival, unmaintained)
- **seccomp + ioctl** hooks (v2.0+) reduce side-channel detection
- **Magica** jailbreak mode (v3.2+) for deeper system access
- Official curated [module repository](https://modules.kernelsu.org) with security review
- Battle-tested stability, regular updates by the original author
- Translations now handled via LLM (no longer Weblate)

**Technical Specs:**
- **Kernel Support:** 5.10+ (GKI 2.0 official); 4.14+ with manual build (archival)
- **Android Version:** 12+ (official GKI); 10+ (community builds)
- **Architecture:** arm64-v8a, x86_64 ⚠️ *(x86_64 support is being dropped - check website)*
- **Special Support:** WSA, ChromeOS, container-based Android

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/tiann/KernelSU/releases/latest)
- [📖 Official Documentation](https://kernelsu.org/)
- [📦 Official Module Repository](https://modules.kernelsu.org)
- [💬 Telegram Channel](https://t.me/KernelSU)
- [🐛 Report Issues](https://github.com/tiann/KernelSU/issues)

</details>

---

### KernelSU-Next

[![GitHub](https://img.shields.io/badge/GitHub-KernelSU--Next-blue?logo=github&style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next)
[![Documentation](https://img.shields.io/badge/Docs-kernelsu--next.github.io-green?style=flat-square)](https://kernelsu-next.github.io/webpage/)
[![Release](https://img.shields.io/github/v/release/KernelSU-Next/KernelSU-Next?style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next/releases)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU__Next-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU_Next)

> Enhanced fork with extended compatibility, modern UI, and innovative features.

<details>
<summary><b>📋 View Details</b></summary>

**Best For:** Power users wanting cutting-edge features and broader device compatibility

**✨ Enhanced Features:**
- Extended kernel support (4.4–6.6, GKI & non-GKI; 6.6+ experimental)
- **Dynamic module mount** - switch between Magic Mount and OverlayFS with a single toggle
- **Module backup & restore** - recover accidentally uninstalled modules
- **Auto-updates** - Manager app updates itself; **bulk install** multiple modules at once
- **Hide hosts** - block adblock detection via app-profile unmount
- Material You UI with dynamic theming
- Configurable OverlayFS (adjustable sparse image size, default 6GB)
- SuSFS controls (KPROBES hooks hiding mode)
- WebUI X framework for advanced module interfaces
- Crowdin translation support; very active development

> [!WARNING]
> **x86_64 Known Issue**: Recent kernel versions cause KernelSU-Next to fail and potentially trigger a kernel panic on x86_64. Check the [official website](https://kernelsu-next.github.io/webpage/) for current status.

**Technical Specs:**
- **Kernel Support:** 4.4–6.6 (Non-GKI 4.4–5.4 LTS, 3.x experimental; GKI 5.10–6.6, 6.6+ experimental)
- **Android Version:** 9+
- **Architecture:** arm64-v8a, armeabi-v7a, x86_64 ⚠️
- **Update Frequency:** Very active development

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/KernelSU-Next/KernelSU-Next/releases)
- [📖 Official Website](https://kernelsu-next.github.io/webpage/)
- [📱 Supported Devices](https://kernelsu-next.github.io/webpage/pages/devices.html)
- [💬 Telegram Community](https://t.me/KernelSU_Next)
- [🐛 Report Issues](https://github.com/KernelSU-Next/KernelSU-Next/issues)

</details>

---

### Wild KSU

[![GitHub](https://img.shields.io/badge/GitHub-Wild__KSU-blue?logo=github&style=flat-square)](https://github.com/WildKernels/Wild_KSU)
[![Release](https://img.shields.io/github/v/release/WildKernels/Wild_KSU?style=flat-square)](https://github.com/WildKernels/Wild_KSU/releases)

> Customization and root hiding focused fork built on KernelSU-Next.

<details>
<summary><b>📋 View Details</b></summary>

**Best For:** Users wanting enhanced customization, root hiding, and SUSFS integration

**✨ Key Features:**
- Fork of KernelSU-Next with customization and root hiding focus
- Integrated SUSFS support (latest: v1.5.12 in GKI builds)
- Multi-manager support (WKSU, KernelSU-Next compatible)
- Scope-minimized manual hooks (v1.4)
- Extended kernel support (4.4–6.6, GKI & non-GKI)
- Multi-architecture support (arm64, arm, x86_64)
- GKI and LKM mode support
- Active development with nightly builds
- Crowdin translation support
- Baseband-guard (BBG) support in GKI builds

**Technical Specs:**
- **Kernel Support:** 4.4–6.6 (Non-GKI & GKI)
- **Android Version:** 9+
- **Architecture:** arm64-v8a, armeabi-v7a, x86_64
- **Status:** Active development - test before daily driving

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/WildKernels/Wild_KSU/releases/latest)
- [🌙 Nightly Builds](https://nightly.link/WildKernels/Wild_KSU/workflows/build-manager-ci/wild/Manager)
- [📖 Documentation](https://kernelsu.org/guide/what-is-kernelsu.html)
- [🐛 Report Issues](https://github.com/WildKernels/Wild_KSU/issues)

</details>

---

### SukiSU-Ultra

[![GitHub](https://img.shields.io/badge/GitHub-SukiSU--Ultra-blue?logo=github&style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
[![Documentation](https://img.shields.io/badge/Docs-sukisu.org-green?style=flat-square)](https://sukisu.org/)
[![Release](https://img.shields.io/github/v/release/SukiSU-Ultra/SukiSU-Ultra?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
[![Telegram](https://img.shields.io/badge/Telegram-SukiKSU-blue?style=flat-square&logo=telegram)](https://t.me/Sukiksu)


> Kernel-based root solution with KPM support, built-in SUSFS, and broad GKI/non-GKI compatibility.

<details>
<summary><b>📋 View Details</b></summary>

**Best For:** Users requiring KPM support, built-in root hiding, and wide device compatibility including legacy non-GKI devices

**✨ Unique Features:**
- GKI 2.0 support (5.10+) and non-GKI support (4.4+); 3.4–3.18 with backports
- **KPM (Kernel Patch Module)** - run code in kernel space, inline-hook & syscall-table-hook (based on KernelPatch, KPM-only after removing KSU-redundant features)
- Built-in SUSFS for root hiding (manageable without an extra module)
- **Metamodule-based mounting** - like upstream, SukiSU now delegates module mounting to the installed metamodule (core no longer mounts)
- LKM mode support on GKI devices
- Enhanced Manager with SUSFS management panel, custom background, DPI adjustment
- Next-gen WebUI via MMRL
- Multi-architecture incl. **armeabi-v7a (bare)** - broader 32-bit ARM support than other variants
- Crowdin translation support; actively maintained

**Technical Specs:**
- **Latest:** v4.1.x (2026)
- **Kernel Support:** 5.10+ (GKI official); 4.4+ (manual build); 3.4–3.18 (experimental backports)
- **Android Version:** 7+ (non-GKI); 12+ (GKI official)
- **Architecture:** arm64-v8a, armeabi-v7a (bare), x86_64 (some)
- **Update Frequency:** Active community-driven development

> [!NOTE]
> GKI method is recommended for Xiaomi, Redmi, and Samsung. It is **not suitable** for Meizu, OnePlus, Realme, and Oppo (these require custom builds).

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
- [📖 Official Website](https://sukisu.org/)
- [📚 Installation Guide](https://sukisu.org/guide/installation)
- [💬 Telegram Group](https://t.me/Sukiksu)

</details>

---

### ReSukiSU

[![GitHub](https://img.shields.io/badge/GitHub-ReSukiSU-blue?logo=github&style=flat-square)](https://github.com/ReSukiSU/ReSukiSU)
[![Release](https://img.shields.io/github/v/release/ReSukiSU/ReSukiSU?style=flat-square)](https://github.com/ReSukiSU/ReSukiSU/releases)

> A newer fork of SukiSU-Ultra focused on multi-manager support and a metamodule-based module system.

<details>
<summary><b>📋 View Details</b></summary>

**Best For:** Users in the SukiSU ecosystem wanting multi-manager flexibility

**✨ Key Features:**
- **Multi-manager support** - works with Official KernelSU, RKSU, MKSU, and SukiSU managers
- **Metamodule-based** module system (pluggable, systemless)
- KPM support (inherited from SukiSU-Ultra)
- Built-in SUSFS management
- Expanding APatch compatibility (work in progress)

**Technical Specs:**
- **Kernel Support:** 5.10+ (GKI 2.0); 4.4+/3.4+ with manual build & backports
- **Architecture:** arm64-v8a, armeabi-v7a, x86_64
- **Status:** Active development - test before daily driving

**🔗 Resources:**
- [📥 Releases](https://github.com/ReSukiSU/ReSukiSU/releases)
- [🐛 Report Issues](https://github.com/ReSukiSU/ReSukiSU/issues)

</details>

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

### Compatibility Matrix

| Feature | Official KernelSU | KernelSU-Next | Wild KSU | SukiSU-Ultra | ReSukiSU |
|---------|-------------------|---------------|----------|--------------|----------|
| **Kernel Support** | 5.10+ (GKI 2.0); 4.14+ manual | 4.4–6.6 | 4.4–6.6 | 5.10+ GKI; 4.4+ manual; 3.x exp. | 5.10+ GKI; 3.4+ manual |
| **Android Version** | 12+ (GKI); 10+ community | 9+ | 9+ | 7+ | 7+ |
| **Architecture** | arm64, x86_64 ⚠️ | arm64, arm, x86_64 ⚠️ | arm64, arm, x86_64 | arm64, arm (bare), x86_64 (partial) | arm64, arm, x86_64 |
| **Installation Modes** | LKM (GKI image deprecated) | GKI / LKM | GKI / LKM | GKI / LKM | GKI / LKM |
| **Module System** | Metamodule (3.0+) | Metamodule + dual mount toggle | Metamodule (3.0+) | Metamodule | Metamodule |
| **Module Backup/Restore** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Auto Updates** | ⚠️ LKM only | ✅ | ✅ Nightly | ⚠️ Manual | ⚠️ Manual |
| **Root Hiding** | Metamodule-based | Advanced (unmount) | SUSFS integrated | SuSFS built-in | SuSFS built-in |
| **KPM Support** | ❌ | ❌ | ❌ | ✅ | ✅ |
| **Multi-Manager** | ❌ | ❌ | ✅ (WKSU/Next) | ❌ | ✅ (KSU/RKSU/MKSU/Suki) |
| **UI/UX** | Material 3 + Magica | Material You | Material You | Enhanced + WebUI | Enhanced |
| **Legacy Support** | ❌ | ⚠️ Limited | ⚠️ Limited | ✅ Extensive | ✅ Extensive |
| **Best For** | Modern devices | Power users | Root hiding | KPM / legacy / hiding | Multi-manager setups |

> ⚠️ x86_64: Both KernelSU and KernelSU-Next have known breaking changes on recent x86_64 kernels (official is dropping x86_64 support). Check the respective project websites for current status.

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

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## Comparison

### KernelSU vs Alternative Root Solutions

| Feature | KernelSU | Magisk | APatch |
| :--- | :--- | :--- | :--- |
| **Architecture** | Kernel-level | Userspace | Kernel-level |
| **Module System** | Metamodule (3.0+) | Magic Mount | OverlayFS |
| **Installation Mode** | LKM (GKI image deprecated) | Boot Patch | Boot Patch |
| **Kernel Support** | 5.10+ (GKI 2.0); 4.14+ manual | Any | 3.18–6.1 |
| **arch Support** | arm64, x86_64 ⚠️ | Universal | arm64 |
| **Security Model** | App Profile | Root Toggle | SuperKey |
| **Root Hiding** | Metamodule-based | Deprecated | Kernel-level |
| **KPM Support** | ❌ | ❌ | ✅ |
| **Update Method** | Manual / LKM | OTA | Manual |
| **System Modification** | Zero | Minimal | Zero |
| **OTA Compatibility** | Excellent | Good | Excellent |
| **Module Mounting** | Requires Metamodule | Built-in | Built-in |
| **Development Status** | Active | Active | Active |
| **Learning Curve** | Medium | Easy | Hard |
| **Community Size** | Large | Very Large | Small |

### Advantages of KernelSU Ecosystem

<details>
<summary><b>✨ Click to expand: Detailed Advantages & Benefits</b></summary>

#### Security Benefits

1. **Kernel-Level Isolation**: Root access operates in kernel space, preventing userspace tampering
2. **App Profile System**: Granular per-application permission control with temporal restrictions
3. **Hardware-Level Protection**: Utilizes ARM TrustZone and hardware security features
4. **Verified Boot Compatible**: Maintains system integrity verification where possible
5. **Advanced Hiding**: Kernel-level hiding is harder to detect than userspace methods

#### Technical Advantages

1. **Zero System Modification**: No changes to system partitions, preserving OTA capabilities
2. **OverlayFS Efficiency**: More efficient than bind mounting with better performance
3. **Future-Proof Design**: Built for modern Android security models and requirements
4. **Developer-Friendly**: Clean APIs and comprehensive documentation
5. **Modular Architecture**: Easy to extend and customize

#### Ecosystem Maturity

1. **Multiple Derivatives**: Options for different use cases and device compatibility
2. **Active Development**: Regular updates and feature additions across all variants
3. **Growing Module Repository**: Expanding collection of high-quality modules
4. **Community Support**: Knowledgeable community with expert developers
5. **Documentation**: Comprehensive guides in multiple languages

</details>

### Migration Considerations

<details>
<summary><b>🔄 Click to expand: Migration from Magisk or Legacy Solutions</b></summary>

#### From Magisk to KernelSU

**Advantages:**
- Enhanced security and hiding capabilities
- Better performance with OverlayFS
- Future-proof architecture for modern Android
- Maintained OTA compatibility

**Considerations:**
- Module compatibility may require updates
- Different app profile management approach
- Learning curve for new concepts (especially metamodules)
- Some Magisk-specific features unavailable

**Migration Steps:**
1. Backup all data and current setup
2. Document installed modules and configurations
3. Uninstall Magisk completely
4. Flash stock boot image
5. Install KernelSU using preferred method
6. Install a metamodule (required for KernelSU 3.0+)
7. Reinstall compatible modules
8. Configure app profiles

#### From SuperSU/Legacy Solutions

**Essential Steps:**
- Complete system restoration recommended
- Fresh start with modern practices
- Understanding of new security model
- Backup and data migration planning

**Benefits:**
- Dramatically improved security
- Modern Android compatibility
- Systemless approach
- Active development and support

</details>


<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>


---

## Prebuilt Kernels

Pre-built kernels save you from manual compilation and come optimized for specific devices. Browse by device manufacturer to find your perfect match.

> [!IMPORTANT]
> **Safety First:** Always verify kernel compatibility with your exact device model and Android version before flashing. Wrong kernels can cause bootloops or device damage.

> [!TIP]
> **Pro Tip:** Check each kernel's release page for device-specific builds, changelogs, and installation instructions. Many provide AnyKernel3 flashable zips for hassle-free installation.

### Brand GKI Compatibility at a Glance

| Brand | Generic GKI | Notes |
|-------|-------------|-------|
| **Samsung** | ✅ (GKI mode) | Knox tripped, but KernelSU works |
| **Xiaomi / Redmi / POCO** | ✅ | GKI or custom builds |
| **Google Pixel** | ✅ | Also see Sultan kernels |
| **Motorola** | ✅ | GKI-compatible models |
| **OnePlus / Oppo / Realme** | ⚠️ Custom kernel | Generic GKI generally not supported |
| **Meizu** | ❌ Avoid GKI | Requires custom builds |

### Quick Navigation

Jump to your device manufacturer:
- [Official GKI](#-official-gki-builds)
- [WildKernels](#wildkernels-multi-device)
- [Xiaomi](#xiaomi-devices)
- [Samsung](#samsung-devices)
- [OnePlus](#oneplus-devices)
- [Motorola](#motorola-devices)
- [Google Pixel](#google-pixel-devices)
- [Huawei](#huawei-devices)
- [LG](#lg-devices)

---

### 🏆 Official GKI Builds

Official kernels from KernelSU project maintainers.

<table>
<tr>
<td width="50%">

**KernelSU Official GKI**

![Kernel](https://img.shields.io/badge/Kernel-5.10+-blue?style=flat-square)
![Android](https://img.shields.io/badge/Android-12+-green?style=flat-square)

Official GKI builds for modern devices with GKI 2.0 support. Latest: v3.2.2

**📥 Download:** [KernelSU Releases](https://github.com/tiann/KernelSU/releases)

</td>
<td width="50%">

**KernelSU-Next**

![Kernel](https://img.shields.io/badge/Kernel-4.4--6.6-blue?style=flat-square)
![Android](https://img.shields.io/badge/Android-9+-green?style=flat-square)

Enhanced builds with extended kernel support and extra features

**📥 Download:** [KernelSU-Next Releases](https://github.com/KernelSU-Next/KernelSU-Next/releases)

</td>
</tr>
<tr>
<td width="50%">

**Wild KSU**

![Kernel](https://img.shields.io/badge/Kernel-4.4--6.6-blue?style=flat-square)
![Android](https://img.shields.io/badge/Android-9+-green?style=flat-square)

Customization and root hiding focused builds with SUSFS integration

**📥 Download:** [Wild KSU Releases](https://github.com/WildKernels/Wild_KSU/releases)

</td>
<td width="50%">

**SukiSU-Ultra**

![Kernel](https://img.shields.io/badge/Kernel-3.4--6.6+-blue?style=flat-square)
![Android](https://img.shields.io/badge/Android-7+-green?style=flat-square)

GKI + non-GKI support with KPM and built-in SUSFS

**📥 Download:** [SukiSU-Ultra Releases](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)

</td>
</tr>
</table>

---

### WildKernels (Multi-Device)

Premium quality kernels with KernelSU and SUSFS integration for multiple device families.

| Kernel Series | Target Devices | Features | Repository |
|---------------|----------------|----------|------------|
| **Wild KSU** | All supported devices | Wild KSU + SUSFS + multi-manager support | [![GitHub](https://img.shields.io/badge/View-Repository-blue?style=flat-square&logo=github)](https://github.com/WildKernels/Wild_KSU) |
| **GKI Series** | Modern GKI Devices | Wild KSU + SUSFS v1.5.12 + GKI 2.0 + BBG | [![GitHub](https://img.shields.io/badge/View-Repository-blue?style=flat-square&logo=github)](https://github.com/WildKernels/GKI_KernelSU_SUSFS) |
| **Sultan Series** | Google Pixel Devices | KernelSU + SUSFS + Pixel Optimizations | [![GitHub](https://img.shields.io/badge/View-Repository-blue?style=flat-square&logo=github)](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) |
| **OnePlus Series** | OnePlus Devices | KernelSU + SUSFS + OxygenOS Tuned | [![GitHub](https://img.shields.io/badge/View-Repository-blue?style=flat-square&logo=github)](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) |

---

### Xiaomi Devices

<details>
<summary><b>🔽 Click to expand Xiaomi device kernels</b></summary>

<br>

#### Redmi Series

| Device Model | Codename | Kernel | Features | Links |
|--------------|----------|---------|----------|-------|
| **Redmi 9** | lancelot | 4.14 | KernelSU Next, SukiSU Ultra, SUSFS, MT6768 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/Edhic1/kernel_KSu_Next_Lancelot) |
| **Redmi Note 12 4G** | topaz/tapas | 5.15 | Smooth optimization, Custom ROM support | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/chickendrop89/device_xiaomi_gemstones-kernel) |
| **Redmi Note 13 4G** | sapphire/sapphiren | 5.15 | Smooth optimization, Custom ROM support | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/chickendrop89/device_xiaomi_gemstones-kernel) |
| **Redmi Note 12/13 4G** | topaz/sapphire | 5.15 | SukiSU Ultra, KPM, SUSFS v1.5.11, Baseband-guard | [![GitHub](https://img.shields.io/badge/Download-ZEPHARO-blue?style=flat-square&logo=github)](https://github.com/topnotchfreaks/kernel_msm-5.15/releases/tag/ZEPHARO) |
| **Redmi Note 12/13 4G** | topaz/sapphire | 5.15 | SukiSU Ultra, KPM, SUSFS, LTO | [![GitHub](https://img.shields.io/badge/Download-YASK-blue?style=flat-square&logo=github)](https://github.com/topnotchfreaks/kernel_msm-5.15/releases/tag/YASK) |
| **Redmi Pad SE** | xun | 5.15 | SukiSU Ultra, KPM, SUSFS, LTO | [![GitHub](https://img.shields.io/badge/Download-YASK-blue?style=flat-square&logo=github)](https://github.com/topnotchfreaks/kernel_msm-5.15/releases/tag/YASK) |
| **Redmi 15 / POCO M7 4G** | creek | 5.15 | SukiSU Ultra, KPM, SUSFS, LTO | [![GitHub](https://img.shields.io/badge/Download-YASK-blue?style=flat-square&logo=github)](https://github.com/topnotchfreaks/kernel_msm-5.15/releases/tag/YASK) |
| **Redmi 4X** | santoni | 4.9 | KernelSU, AOSP Compatible | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/zeta96/L_soul_santoni_msm4.9) |
| **Redmi Note 12 5G / POCO X5** | stone | 5.4 | KernelSU, APatch compatible | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/gawasvedraj/KernelOwO) |

</details>

---

### Samsung Devices

<details>
<summary><b>🔽 Click to expand Samsung device kernels</b></summary>

<br>

#### Galaxy S Series

| Device Model | Codename | Kernel | Features | Links |
|--------------|----------|---------|----------|-------|
| **Galaxy S25** | S93XX (sm8750) | 6.6 | KernelSU, MKSU, SukiSU-Ultra, LKM mode | [![GitHub](https://img.shields.io/badge/Download-Kokuban-blue?style=flat-square&logo=github)](https://github.com/YuzakiKokuban/android_kernel_samsung_sm8750) |
| **Galaxy S25** | S93XX (sm8750) | 6.6 | KernelSU LKM compatible | [![GitHub](https://img.shields.io/badge/Download-GKI-blue?style=flat-square&logo=github)](https://github.com/fei-ke/android_kernel_samsung_sm8750) |
| **Galaxy S24** | S92XX (sm8650) | 6.1 | KernelSU, MKSU, SukiSU-Ultra, LKM mode | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/YuzakiKokuban/android_kernel_samsung_sm8650) |
| **Galaxy S23** | S91XX (sm8550) | 5.15 | KernelSU, MKSU, SukiSU-Ultra, LKM mode | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/YuzakiKokuban/android_kernel_samsung_sm8550_S23) |
| **Galaxy S20** | x1q/y2q/z3q (sm8250) | 4.19 | KernelSU-Next, SuSFS v1.5.9 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/GoRhanHee/kernel_samsung_sm8250) |
| **Galaxy S10 / Note 10** | Exynos 9820 | 4.14 | KernelSU-Next v3.0.0, SuSFS v1.5.11, Ramdisk support | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/GoRhanHee/exynos9820_samsung_Kernel) |

#### Galaxy A Series

| Device Model | Codename | Kernel | Features | Links |
|--------------|----------|---------|----------|-------|
| **Galaxy A32 4G** | A325F | 4.14 | SukiSU-Ultra v3.1.8, SuSFS v1.5.5, Android 15/16, OneUI 7 | [![XDA](https://img.shields.io/badge/Download-XDA-orange?style=flat-square&logo=xda-developers)](https://xdaforums.com/t/closed-kernel-sukisu-ultra-for-galaxy-a32-4g-a325x-unofficial.4754691/) |
| **Galaxy A15 4G** | SM-A155F | 5.10 | KernelSU-Next, SuSFS 1.5.9 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/ReeViiS69/sm155f) |
| **Galaxy A12** | SM-A127F | 4.14 | KernelSU-Next, SUSFS v1.5.7, Wireguard, SELinux toggle | [![XDA](https://img.shields.io/badge/Download-XDA-orange?style=flat-square&logo=xda-developers)](https://xdaforums.com/t/kernel-a127f-project-xed-kernelsu-next-susfs.4735546/) |

#### Galaxy M Series & Tablets

| Device Model | Codename | Kernel | Features | Links |
|--------------|----------|---------|----------|-------|
| **Galaxy Tab S10 Series** | SM-X82XX/X92XX (mt6989) | 6.1 | KernelSU, MKSU, SukiSU-Ultra, LKM variants | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/YuzakiKokuban/android_kernel_samsung_mt6989_TabS10) [![XDA](https://img.shields.io/badge/XDA-Thread-orange?style=flat-square&logo=xda-developers)](https://xdaforums.com/t/kernel-root-oneui8-0-tab-s10-series-kernel-with-kernelsu.4739268/) |
| **Galaxy M30s** | M307F | 4.9 | KernelSU 0.9.5 (Non-GKI) | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/JuiIm/M30s-custom-kernel-M307f---KernelSU-support) |

</details>

---

### OnePlus Devices

<details>
<summary><b>🔽 Click to expand OnePlus device kernels</b></summary>

<br>

| Device Model | Codename | Kernel | Features | ROM Support | Links |
|--------------|----------|---------|----------|-------------|-------|
| **OnePlus 13** | - | Latest | KernelSU-Next, SUSFS | OxygenOS | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/FerGus786/OnePlus_13_KernelSU_SUSFS) |
| **OnePlus 12** | - | 6.1 | KernelSU LKM mode, SukiSU Ultra + SUSFS | OxygenOS/ColorOS 14 | [![GitHub](https://img.shields.io/badge/Download-LKM-blue?style=flat-square&logo=github)](https://github.com/snowwolf725/KernelSU_LKM_For_Oneplus12) |
| **OnePlus 7 Pro** | guacamole | Latest | KernelSU v0.9.5, Full system flash required | LineageOS 21 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/surfaceocean/kernelsu_oneplus_7_pro_lineageos_guacamole) |
| **OnePlus Nord N200 5G** | dre | 5.4 | SukiSU Ultra | LineageOS 22+ | [![XDA](https://img.shields.io/badge/Download-XDA-orange?style=flat-square&logo=xda-developers)](https://xdaforums.com/t/kernel-aosp-lineageos-kernel-kernelsu-included.4749302/) |

> [!NOTE]
> OnePlus devices generally do not support the generic GKI build and require custom kernel builds. Use [WildKernels/OnePlus_KernelSU_SUSFS](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) or manufacturer-specific builds.

</details>

---

### Motorola Devices

<details>
<summary><b>🔽 Click to expand Motorola device kernels</b></summary>

<br>

| Device Model | Codename | Kernel | Features | ROM Support | Links |
|--------------|----------|---------|----------|-------------|-------|
| **Moto G20** | java | 4.14 | KernelSU 0.9.5, KernelSU-Next, SukiSU Ultra | Stock, AOSP | [![XDA](https://img.shields.io/badge/Download-XDA-orange?style=flat-square&logo=xda-developers)](https://xdaforums.com/t/kernel-custom-kernels-with-su-kernelsu-kernelsu-next-and-sukisu-ultra-for-motorola-g20-java.4711782/) |

</details>

---

### Google Pixel Devices

<details>
<summary><b>🔽 Click to expand Google Pixel device kernels</b></summary>

<br>

| Device Model | Codename | Kernel | Features | ROM Support | Links |
|--------------|----------|---------|----------|-------------|-------|
| **Pixel 8a** | GKI | 6.1 | KernelSU-Next, SuSFS, Hide patches | Android 14 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/TheRetikGM/gki-kernelsunext-susfs) |
| **Pixel 7 / 7 Pro** | gs201 | 5.10 | KernelSU-Next, SuSFS v1.5.8, Additional patches | Custom ROMs | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/wspyams/android_kernel_google_gs201) |

> [!TIP]
> For Pixel devices, also check [WildKernels/Sultan_KernelSU_SUSFS](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) for Sultan kernel builds with SUSFS integration.

</details>

---

### Huawei Devices

<details>
<summary><b>🔽 Click to expand Huawei device kernels</b></summary>

<br>

| Device Model | Codename | Kernel | Features | ROM Support | Links |
|--------------|----------|---------|----------|-------------|-------|
| **Huawei Nova 2** | - | 4.4 | KernelSU | LineageOS | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/CoolestEnoch/kernel-su-huawei-nova2) |

</details>

---

### LG Devices

<details>
<summary><b>🔽 Click to expand LG device kernels</b></summary>

<br>

| Device Model | Codename | Kernel | Features | ROM Support | Links |
|--------------|----------|---------|----------|-------------|-------|
| **LG G7** | judyln | 4.9 | KernelSU-Next, SuSFS | LineageOS 22.1 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/No-22-Github/LG-G7-LineageOS-22.1-KernelSU-Next-SuSFS-Kernel) |

</details>

---

### Kernel Selection Guide

**Consider these factors when choosing a kernel:**

| Factor | What to Check |
|--------|---------------|
| **Device Match** | Exact device model and variant (not just similar models) |
| **Android Version** | Kernel must match your current Android version |
| **Security Patch** | Anti-rollback protection - never flash a kernel older than your current security patch level |
| **Features** | KernelSU version, SUSFS support, additional optimizations |
| **Maintenance** | Regular updates and active development |
| **Community** | User feedback on XDA, GitHub issues, Telegram |
| **Documentation** | Clear installation instructions and support |

> [!WARNING]
> **Before Flashing:** Always backup your current boot image. Keep a copy of stock boot.img for emergency recovery. Test with `fastboot boot kernel.img` first if possible. On devices with anti-rollback protection (e.g., Xiaomi, OnePlus), flashing a kernel with an older security patch level can permanently brick your device.

### Need Help?

- **Build your own:** See [Building from Source](#️-building-from-source) section


<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## 🔧 Installation

**Multiple installation methods to suit your needs and technical comfort level.**

### ✅ Pre-Installation Checklist

Before proceeding, ensure you have:

- [x] **Unlocked bootloader** (essential!)
- [x] **Complete device backup**
- [x] **ADB & Fastboot** installed ([Download Platform Tools](https://developer.android.com/studio/releases/platform-tools))
- [x] **USB Debugging** enabled (Settings → Developer Options)
- [x] **Stock boot image** backup (for emergency recovery)
- [x] **Charged device** (at least 50% battery)

> [!WARNING]
> **Backup First!** Installation errors can cause data loss or bootloops. Always have a recovery plan.

> [!TIP]
> **Need help unlocking your bootloader?** Visit [Awesome-Android-Root Guide](https://awesome-android-root.pages.dev/android-root-guides/how-to-unlock-bootloader)

---

### 🚀 Installation Methods Overview

| Method | Difficulty | Best For | Requirements | Time |
|--------|-----------|----------|--------------|------|
| [**GKI Mode**](#method-1-gki-mode) | Easy | Modern devices (5.10+) | Fastboot, unlocked bootloader | 5–10 min |
| [**LKM Mode**](#method-2-lkm-mode) | Easy | Preserving stock kernel | Unlocked bootloader | 5–10 min |
| [**Manager Patching**](#method-3-manager-patching) | Easy | One-click solution | Unlocked bootloader | 10–15 min |
| [**Custom Kernel**](#method-4-custom-kernels) | Medium | Device-specific optimization | TWRP or fastboot | 10–20 min |
| [**Manual Building**](#method-5-manual-building) | Hard | Full customization | Build environment, expertise | 1–3 hours |

---

### Method 1: GKI Mode

**Best for:** Modern devices with GKI 2.0 support (kernel 5.10+)

<details open>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ Strong universality for modern devices
- ✅ Official support and regular updates
- ✅ Clean installation with minimal configuration

**Step-by-Step:**

```bash
# 1. Download boot.img from releases
# Visit: https://github.com/tiann/KernelSU/releases/latest

# 2. Boot device to fastboot mode
adb reboot bootloader

# 3. Flash the kernel
fastboot flash boot boot.img

# 4. Reboot device
fastboot reboot

# 5. Install KernelSU Manager APK after boot

# 6. IMPORTANT: Install a metamodule for module support
# Download meta-overlayfs and install via KernelSU Manager
```

> **More Details**: [GKI Installation Guide](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#method-1-pre-built-gki-kernel-easiest)

</details>

---

### Method 2: LKM Mode

**Best for:** Users wanting to keep original kernel intact and get easy updates

<details>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ Preserves original kernel and manufacturer optimizations
- ✅ Less intrusive modification
- ✅ Easier to revert to stock
- ✅ OTA-friendly (install to inactive slot)
- ✅ Easy in-app updates
- ✅ No AVB/dm-verity issues

**Requirements:**
- Stock/official firmware
- Compatible kernel version

**Step-by-Step:**

1. Install KernelSU Manager APK on device
2. Grant necessary permissions
3. In Manager, select "Install" → "Select and Patch a File"
4. Choose your stock boot.img file
5. Manager will patch it with KernelSU (LKM mode)
6. Flash patched boot via fastboot:

```bash
# Transfer patched boot to PC
adb pull /sdcard/Download/kernelsu_patched_xxxxx.img

# Boot to fastboot
adb reboot bootloader

# Flash patched image
fastboot flash boot kernelsu_patched_xxxxx.img

# Reboot
fastboot reboot
```

7. **Install metamodule** after first boot for module support

> **Complete Guide**: [LKM Mode Installation](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#method-2-boot-image-patching-lkm-mode)

</details>

---

### Method 3: Manager Patching

**Best for:** Users preferring one-click solutions with boot image patching

<details>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ User-friendly, minimal PC usage
- ✅ Automatic patching process
- ✅ Simplest for non-technical users
- ✅ Supports both GKI and LKM modes

**Step-by-Step:**

1. Extract boot.img from your device firmware
2. Install KernelSU Manager APK on device
3. Grant necessary permissions
4. Select "Install" → "Select and Patch a File"
5. Choose your boot.img file
6. Manager patches boot image automatically
7. Flash patched boot via fastboot or custom recovery

```bash
# Flash patched boot via fastboot
adb pull /sdcard/Download/kernelsu_patched_*.img
adb reboot bootloader
fastboot flash boot kernelsu_patched_*.img
fastboot reboot
```

8. **Install metamodule** after first boot for module support

> **Detailed Tutorial**: [Manager Patching Guide](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#method-2-boot-image-patching-lkm-mode)

</details>

---

### Method 4: Custom Kernels

**Best for:** Device-specific optimization and features

<details>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ Device-optimized performance
- ✅ Pre-tested stability
- ✅ Additional features (SUSFS, optimizations)
- ✅ No compilation required

**Step-by-Step:**

1. Find your device in [Prebuilt Kernels](#prebuilt-kernels) section
2. Download appropriate kernel zip
3. Flash via TWRP or fastboot:

**Via TWRP:**
```
1. Boot to TWRP recovery
2. Install → Select kernel zip
3. Swipe to flash
4. Reboot system
```

**Via Fastboot:**
```bash
adb reboot bootloader
fastboot flash boot kernel.img
fastboot reboot
```

4. Install KernelSU Manager APK
5. Verify installation in Manager

</details>

---

### Method 5: Manual Building

**Best for:** Developers and advanced users

<details>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ Full customization control
- ✅ Latest features and patches
- ✅ Learn kernel development

**Requirements:**
- Linux build environment (Ubuntu 20.04+ recommended)
- Kernel source code for your device
- Cross-compiler toolchain
- Build dependencies (see [Building from Source](#️-building-from-source))

**Quick Overview:**
1. Setup Linux build environment
2. Clone kernel source and KernelSU repository
3. Apply KernelSU patches
4. Configure kernel (enable CONFIG_KSU)
5. Compile kernel
6. Package with AnyKernel3
7. Flash to device

**Full guide:** See [Building from Source](#️-building-from-source) section

</details>

---

### Compatibility Check

**Check your kernel version:**
```bash
# Via ADB
adb shell uname -r

# Or on device terminal
uname -r
```

**Compatibility Matrix:**

| Kernel Version | Official KernelSU | KernelSU-Next | Wild KSU | SukiSU-Ultra | Recommended Method |
|----------------|-------------------|---------------|----------|--------------|-------------------|
| 5.10+ (GKI 2.0) | ✅ Full Support | ✅ Full Support | ✅ Full Support | ✅ Full Support | GKI Mode / Manager Patching |
| 4.14–5.9 | ⚠️ Manual Build Only | ✅ Full Support | ✅ Full Support | ✅ Full Support | Custom Kernel / LKM |
| 4.4–4.13 | ❌ Not Supported | ✅ Full Support | ✅ Full Support | ✅ Full Support | Custom Kernel |
| 3.4–4.3 | ❌ Not Supported | ❌ Not Supported | ❌ Not Supported | ⚠️ Experimental | Custom Kernel |

---

### ✨ Post-Installation Setup

> [!IMPORTANT]
> Complete these essential steps to ensure proper functionality and security.

**1. Verify Installation**

```bash
# Check KernelSU version
su -c "kernelsu --version"

# Verify root access
su -c "id"

# Check kernel version
cat /proc/version | grep KernelSU

# Check installation mode
# Look for LKM or GKI indicators in kernel version
```

**2. Install Manager**
- Download appropriate Manager APK
- Grant all required permissions
- Confirm root access in app

**3. Install Metamodule (CRITICAL for KernelSU 3.0+)**
- Download [meta-overlayfs](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) (recommended)
- Install via KernelSU Manager > Modules
- Reboot device
- See [Understanding Metamodules](#understanding-metamodules) for details

**4. Configure App Profiles**
- Set restrictive defaults
- Grant root only to trusted apps
- Configure time-based restrictions

**5. Install Essential Modules**
- Module manager (MMRL recommended)
- SuSFS for root hiding (if needed)
- Performance optimizations (optional)

> [!WARNING]
> Only install modules from trusted sources

**6. Setup Safety Features**
- Backup patched boot image
- Configure module backups
- Test Play Integrity
- Document your setup

> **Complete Setup Guide**: [Post-Installation Setup](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide#post-installation-setup)


---

### Verification Commands

```bash
# Comprehensive verification script
# Check if KernelSU is loaded
cat /proc/version | grep KernelSU

# Test root access
su -c "whoami"
su -c "id"

# Check module directory
ls -la /data/adb/modules/

# View KernelSU logs
dmesg | grep kernelsu

# Check SELinux status
getenforce

# Verify module mounting
mount | grep overlay
```

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## 📚 Documentation

**Comprehensive guides and resources to master KernelSU.**

### 📖 Core Documentation

**Getting Started**
- [What is KernelSU?](https://kernelsu.org/guide/what-is-kernelsu.html)
- [Installation Guide](https://kernelsu.org/guide/installation.html)
- [App Profile System](https://kernelsu.org/guide/app-profile.html)
- [Module System](https://kernelsu.org/guide/module.html)
- [Official Module Repository](https://modules.kernelsu.org)
- [API Documentation](https://kernelsu.org/guide/module.html#kernelsu-modules)

**Advanced Topics**
- [Security Model](https://kernelsu.org/guide/security.html)
- [OverlayFS System](https://kernelsu.org/guide/overlayfs.html)
- [SELinux Configuration](https://kernelsu.org/guide/selinux.html)
- [Debugging Guide](https://kernelsu.org/guide/debug.html)
- [Migration from Magisk](https://kernelsu.org/guide/migration.html)

### 🔨 Integration & Building

- [**Non-GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - For custom kernels 4.14 and earlier
- [**GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-gki.html) - Generic Kernel Image integration
- [**Building from Source**](https://kernelsu.org/guide/how-to-build.html) - Complete compilation guide
- [**Kernel Requirements**](https://kernelsu.org/guide/installation.html#requirements) - Prerequisites and compatibility
- [**Unofficially Supported Devices**](https://kernelsu.org/guide/unofficially-support-devices.html) - Manual compilation for older kernels

### 📦 Module Development

- [**Module Development Guide**](https://kernelsu.org/guide/module.html) - Creating KernelSU modules
- [**Module WebUI Guide**](https://kernelsu.org/guide/module-webui.html) - Building web interfaces
- [**Module Examples**](https://github.com/topics/kernelsu-module) - Community examples on GitHub

### 🆘 Recovery & Troubleshooting

- [**FAQ**](https://kernelsu.org/guide/faq.html) - Frequently asked questions
- [**Bootloop Recovery**](https://kernelsu.org/guide/rescue-from-bootloop.html) - Emergency recovery procedures

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## Modules and Tools

**Essential modules and tools to enhance your KernelSU experience.**

> [!IMPORTANT]
> **KernelSU 3.0+ Requirement**: You must first install a [metamodule](#understanding-metamodules) before regular modules will work. Fresh installations require this step!

### Metamodules (Required for Module Support)

> **First-Time Users**: Start with **meta-overlayfs** for the best balance of compatibility and ease of use.

| Metamodule | Purpose | Download |
|------------|---------|----------|
| [**meta-overlayfs**](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) | Official reference implementation using OverlayFS - **recommended for most users** | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/KernelSU-Modules-Repo/meta-overlayfs/releases) |
| [**mountify**](https://github.com/backslashxx/mountify) | OverlayFS with tmpfs/ext4 sparse support, works on APatch/Magisk too | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/backslashxx/mountify/releases) |
| [**meta-hybrid_mount**](https://github.com/YuzakiKokuban/meta-hybrid_mount) | Dual engine (OverlayFS + Magic Mount) with conflict monitor, diagnostics & auto-fallback | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/YuzakiKokuban/meta-hybrid_mount/releases) |

---

### Root Management & Hiding

| Module | Purpose | Key Features |
|--------|---------|--------------|
| [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module) | Advanced root hiding | Customizable profiles, filesystem manipulation, banking app support |


> [!TIP]
> **Discover More Modules:** Explore the extensive collection at **[Awesome Android Root - KernelSU Modules](https://awesome-android-root.pages.dev/android-root-apps/?filters=%5BK%5D)**

### Framework Modifications

| Framework | Purpose | Features |
|-----------|---------|----------|
| [**LSPosed**](https://github.com/LSPosed/LSPosed) | Xposed framework | Module support via Zygisk integration |
| [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext) | Standalone Zygisk | Independent Zygisk implementation for KernelSU |
| [**ReZygisk**](https://github.com/PerformanC/ReZygisk) | Transparent Zygisk | Improved open-source Zygisk implementation |

---

### 📦 Module Managers

**[MMRL (Modern Module Manager)](https://github.com/MMRLApp/MMRL)**

The all-in-one solution for KernelSU module management.

<details>
<summary><b>🔽 View MMRL Features</b></summary>

**✨ Key Features:**
- ✅ Built-in module repository with 100+ modules
- ✅ Automatic module updates
- ✅ Module backup/restore functionality
- ✅ Dependency management
- ✅ Next-gen WebUI support for advanced modules
- ✅ Material You design language
- ✅ Dark/Light theme support
- ✅ Detailed module information and changelogs

**📥 Download:** [MMRL Latest Release](https://github.com/MMRLApp/MMRL/releases)

</details>

---

### Management Apps

| App | Purpose | Download |
|-----|---------|----------|
| [**KernelSU Manager**](https://github.com/tiann/KernelSU/releases) | Official manager for KernelSU | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/tiann/KernelSU/releases/latest) |
| [**KernelSU-Next Manager**](https://github.com/KernelSU-Next/KernelSU-Next/releases) | Manager for KernelSU-Next | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next/releases/latest) |
| [**Wild KSU Manager**](https://github.com/WildKernels/Wild_KSU/releases) | Manager for Wild KSU | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/WildKernels/Wild_KSU/releases/latest) |
| [**SukiSU Manager**](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) | Manager for SukiSU-Ultra | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases/latest) |
| [**ReSukiSU Manager**](https://github.com/ReSukiSU/ReSukiSU/releases) | Manager for ReSukiSU (multi-manager) | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/ReSukiSU/ReSukiSU/releases/latest) |
| [**Franco Kernel Manager**](https://play.google.com/store/apps/details?id=com.franco.kernel) | Kernel tweaking & monitoring | [![Play Store](https://img.shields.io/badge/Get-Play_Store-green?style=flat-square)](https://play.google.com/store/apps/details?id=com.franco.kernel) |


---

### 🛠️ Development & Debugging

| Tool | Purpose | Use Case |
|------|---------|----------|
| [**Root Checker**](https://play.google.com/store/apps/details?id=com.joeykrim.rootcheck) | Verify root status | Confirm successful installation |
| [**Logcat Reader**](https://github.com/darshanparajuli/LogcatReader) | System log viewer | Debugging and troubleshooting |
| [**Termux**](https://github.com/termux/termux-app) | Terminal emulator | Full Linux environment on Android |


---

## 🛠️ Building from Source

> [!NOTE]
> This section covers building KernelSU from source. For ready-to-use kernels, see the [Prebuilt Kernels](#prebuilt-kernels) section.

### Kernel Source Repositories

- [**KernelSU Source**](https://github.com/tiann/KernelSU) - Official KernelSU source code for integration
- [**KernelSU-Next Source**](https://github.com/KernelSU-Next/KernelSU-Next) - Enhanced fork with extended support
- [**Wild KSU Source**](https://github.com/WildKernels/Wild_KSU) - Customization and root hiding focused fork
- [**SukiSU-Ultra Source**](https://github.com/SukiSU-Ultra/SukiSU-Ultra) - KPM + broad compatibility fork
- [**ReSukiSU Source**](https://github.com/ReSukiSU/ReSukiSU) - SukiSU-Ultra fork with multi-manager support
- [**Ylarod/ddk**](https://github.com/Ylarod/ddk) - Official recommended toolchain for building KernelSU LKM
- [**Kernel Build Action**](https://github.com/dabao1955/kernel_build_action) - Automated building via GitHub Actions

> [!NOTE]
> Since v3.0, official KernelSU **only supports the DDK build environment** and no longer maintains direct kernel integration ("built-in"/GKI image mode) or non-GKI/x86_64 kernels. Third-party kernel maintainers should target the **KernelSU LKM ABI** instead of integrating KernelSU directly. Forks (Next, Wild, SukiSU, ReSukiSU) continue to support direct integration via their own `setup.sh`.

### Device-Specific Kernel Sources

> [!TIP]
> Always use official kernel sources from your device manufacturer for best compatibility.

- [**OnePlus Kernel Sources**](https://github.com/OnePlusOSS) - Official OnePlus kernel sources
- [**Xiaomi Kernel Sources**](https://github.com/MiCode/Xiaomi_Kernel_OpenSource) - Official Xiaomi kernel sources
- [**Google AOSP Kernels**](https://android.googlesource.com/kernel/) - Android Open Source Project kernels
- [**Samsung Opensource**](https://opensource.samsung.com) - Samsung kernel sources

### Building Tools & Scripts

- [**Universal Patcher**](https://github.com/KernelSU-Next/KernelSU-Next/tree/dev/scripts) - Automated kernel patching scripts
- [**KernelSU Builder**](https://github.com/dabao1955/kernel_build_action) - CI/CD building system with GitHub Actions
- [**⭐ AnyKernel3**](https://github.com/osm0sis/AnyKernel3) - Universal kernel flasher and packaging tool
- [**Manual Build Guide**](https://kernelsu.org/guide/how-to-build.html) - Step-by-step building instructions

### Build Environment Setup

<details>
<summary><b>Click to expand: Detailed Build Instructions</b></summary>

> [!IMPORTANT]
> Building kernels requires significant disk space (50GB+) and time. Ensure you have a proper Linux environment.

#### Linux Build Environment

```bash
# Install dependencies (Ubuntu/Debian)
sudo apt update
sudo apt install -y git build-essential kernel-package fakeroot libncurses5-dev \
  libssl-dev ccache bison flex libelf-dev bc python3

# Install cross-compiler
sudo apt install -y gcc-aarch64-linux-gnu gcc-arm-linux-gnueabihf

# Clone KernelSU
git clone https://github.com/tiann/KernelSU
```

> [!TIP]
> Use `ccache` to speed up subsequent builds. Enable it with `export USE_CCACHE=1` and `export CCACHE_DIR=~/.ccache`.

#### Building Process

```bash
# 1. Clone your device kernel source
git clone <kernel_source_url> kernel

# 2. Apply KernelSU patches
cd kernel
curl -LSs "https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh" | bash -

# For KernelSU-Next:
# curl -LSs "https://raw.githubusercontent.com/KernelSU-Next/KernelSU-Next/next/kernel/setup.sh" | bash -

# For Wild KSU:
# curl -LSs "https://raw.githubusercontent.com/WildKernels/Wild_KSU/wild/kernel/setup.sh" | bash -s wild

# For SukiSU-Ultra:
# curl -LSs "https://raw.githubusercontent.com/SukiSU-Ultra/SukiSU-Ultra/main/kernel/setup.sh" | bash -s main      # GKI
# curl -LSs "https://raw.githubusercontent.com/SukiSU-Ultra/SukiSU-Ultra/main/kernel/setup.sh" | bash -s builtin   # non-GKI

# For ReSukiSU:
# curl -LSs "https://raw.githubusercontent.com/ReSukiSU/ReSukiSU/main/kernel/setup.sh" | bash

# 3. Configure kernel
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- <defconfig>

# 4. Enable KernelSU in config
./scripts/config --file .config -e CONFIG_KSU

# For SukiSU-Ultra KPM support:
# ./scripts/config --file .config -e CONFIG_KPM

# 5. Build kernel
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)

# 6. Package with AnyKernel3
# Copy Image.gz-dtb or Image to AnyKernel3 directory
# Zip and flash
```

> [!WARNING]
> Building with wrong toolchain or configuration can produce non-bootable kernels. Always test on non-critical devices first.

#### Supported Architectures

- **arm64-v8a**: Primary support (64-bit ARM) - most modern devices
- **x86_64**: Intel/AMD 64-bit (emulators, some tablets) ⚠️ *Known breaking change on recent kernels for KernelSU/KernelSU-Next*
- **armeabi-v7a**: 32-bit ARM (legacy devices, SukiSU-Ultra only)

#### Continuous Integration

```yaml
name: Build Kernel
on:
  push:
    branches: [ main ]
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Kernel with KernelSU
        uses: dabao1955/kernel_build_action@main
        with:
          kernel-url: <your_kernel_repo>
          branch: <branch_name>
          config: <defconfig_name>
          arch: arm64
```

</details>

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

## 💬 Community

**Connect with thousands of KernelSU users worldwide for support, discussion, and latest updates.**

### Official Communities

**Telegram**

| Channel | Purpose | Link |
|---------|---------|------|
| **KernelSU Channel** | Official announcements | [![Telegram](https://img.shields.io/badge/Join-Channel-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU) |
| **KernelSU Group** | Community support | [![Telegram](https://img.shields.io/badge/Join-Group-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU_group) |
| **KernelSU-Next** | Enhanced variant | [![Telegram](https://img.shields.io/badge/Join-Group-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU_Next) |
| **Wild KSU** | Customization & root hiding fork | [![Telegram](https://img.shields.io/badge/Join-Group-blue?style=flat-square&logo=telegram)](https://t.me/WildKSU) |
| **SukiSU** | KPM & legacy devices | [![Telegram](https://img.shields.io/badge/Join-Group-blue?style=flat-square&logo=telegram)](https://t.me/Sukiksu) |

**GitHub**

| Platform | Purpose | Link |
|----------|---------|------|
| **Discussions** | Technical Q&A | [![GitHub](https://img.shields.io/badge/Join-Discussions-black?style=flat-square&logo=github)](https://github.com/tiann/KernelSU/discussions) |
| **Issues** | Bug reports | [![GitHub](https://img.shields.io/badge/Report-Issues-black?style=flat-square&logo=github)](https://github.com/tiann/KernelSU/issues) |
| **Wild KSU Issues** | Customization fork | [![GitHub](https://img.shields.io/badge/View-Issues-black?style=flat-square&logo=github)](https://github.com/WildKernels/Wild_KSU/issues) |


---

### 🌐 Forums & Platforms

| Platform | Description | Members | Link |
|----------|-------------|---------|------|
| **XDA Developers** | Main discussion & device-specific threads | 10,000+ | [![XDA](https://img.shields.io/badge/Visit-XDA-orange?style=flat-square&logo=xda-developers)](https://forum.xda-developers.com/t/kernelsu-a-kernel-based-root-solution-for-android.4511259/) |
| **Reddit r/KernelSU** | Community discussions & support | Growing | [![Reddit](https://img.shields.io/badge/Join-r%2FKernelSU-red?style=flat-square&logo=reddit)](https://www.reddit.com/r/KernelSU/) |
| **4PDA Forum** | Russian-language community | Active | [![4PDA](https://img.shields.io/badge/Visit-4PDA-blue?style=flat-square)](https://4pda.to/forum/index.php?showtopic=1020374) |

---

## 🔧 Troubleshooting

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

## ❓ FAQ

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

---

### Development

<details>
<summary><b>How do I build KernelSU for my device?</b></summary>

**Quick steps:**

1. Setup Linux build environment
2. Clone kernel source
3. Apply KernelSU patches (use the setup.sh for your chosen variant)
4. Configure kernel (enable CONFIG_KSU; CONFIG_KPM for SukiSU-Ultra)
5. Compile kernel
6. Package with AnyKernel3

See [Building from Source](#️-building-from-source) for detailed guide.

</details>

<details>
<summary><b>Can I contribute to KernelSU?</b></summary>

**Absolutely! Contributions welcome:**

- 🐛 Report bugs on GitHub
- 💻 Submit pull requests
- 📦 Create and share modules
- 📚 Improve documentation
- 💬 Help in community support
- 🧪 Test beta versions

</details>

---

### 💡 More Questions?

- 📚 [**Complete KernelSU Installation Guide**](https://awesome-android-root.pages.dev/rooting-guides/kernelsu-guide) - Comprehensive tutorial with detailed explanations
- 📖 [Official FAQ](https://kernelsu.org/guide/faq.html) - Official documentation
- 💬 [Telegram Community](https://t.me/KernelSU_group) - Real-time support
- 🐙 [GitHub Discussions](https://github.com/tiann/KernelSU/discussions) - Technical discussions
- 🌐 [XDA Forums](https://forum.xda-developers.com/t/kernelsu-a-kernel-based-root-solution-for-android.4511259/) - Community forum

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## 🤝 Contributing

**Help make this the most comprehensive KernelSU resource! All contributions are welcome.**

### Quick Start

**How to Contribute:**

1. Fork this repository
2. Add or update resources
3. Follow formatting standards
4. Test all links
5. Submit pull request

**What We Need:**

- New tools & modules
- Device-specific kernels
- Documentation improvements
- Translations
- Bug fixes & updates
- Tutorials & guides

**📖 See [CONTRIBUTING.md](CONTRIBUTING.md)**

---

### Need Help?

- Check existing [issues](https://github.com/fynks/awesome-kernelsu/issues) and [PRs](https://github.com/fynks/awesome-kernelsu/pulls)
- Open a [discussion](https://github.com/fynks/awesome-kernelsu/discussions)

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## Disclaimer

**Important legal information - Please read carefully before proceeding.**

> [!CAUTION]
> **Proceed at Your Own Risk:** Rooting and kernel modification can void warranties, brick devices, and expose security vulnerabilities. Users assume all risks and responsibilities.

---

### ⚠️ Legal & Safety Information

**Educational Purpose Only**

This documentation is provided for **educational and informational purposes only**. Users are solely responsible for:

- Understanding and complying with local laws
- Following device warranty terms
- Maintaining device security
- Device modifications and consequences

**No Warranty or Liability**

Contributors and maintainers are **NOT liable** for:

- ❌ Device damage or bricking
- ❌ Data loss or corruption
- ❌ Warranty violations
- ❌ Legal consequences
- ❌ Security vulnerabilities

---

### ✅ Safety Best Practices

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

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

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

<div align="center">

[![Star History Chart](https://api.star-history.com/svg?repos=fynks/awesome-kernelsu&type=Date)](https://star-history.com/#fynks/awesome-kernelsu&Date)

---

**Made with ❤️ by the KernelSU Community**

<sub>Last Updated: June 2026 | Maintained by [Fynks](https://github.com/fynks)</sub>

<br>

**[⬆ Back to Top](#awesome-kernelsu)**

</div>
