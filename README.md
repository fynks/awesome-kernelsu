<div align="center">

<img src="./media/kernelsu-logo.svg" alt="KernelSU Logo" width="128"/>

# Awesome KernelSU

**A curated list of KernelSU resources: official documentation, variants, modules, tools, and device kernels.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)

</div>

## Contents

- [What is KernelSU?](#what-is-kernelsu)
- [Quick Start](#quick-start)
- [Installation Modes](#installation-modes)
- [Metamodules](#metamodules)
- [Official Resources](#official-resources)
- [KernelSU Variants](#kernelsu-variants)
- [Modules & Tools](#modules--tools)
- [Device Kernels](#device-kernels)
- [Building from Source](#building-from-source)
- [Documentation](#documentation)
- [Community](#community)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)
- [License](#license)

## What is KernelSU?

**KernelSU** is a kernel-based root solution for Android. Unlike userspace tools such as Magisk, it runs inside the Linux kernel and grants root access to apps directly in kernel space.

Core concepts:

- **Kernel-based `su`** — only permitted apps can access or even see `su`; all other apps remain unaware of it.
- **App Profiles** — lock root privileges in a cage: customize a granted app's uid, gid, groups, capabilities, and SELinux rules.
- **Metamodule system** — a pluggable module infrastructure that handles systemless `/system` modifications (see [Metamodules](#metamodules)).

> Official KernelSU targets Android **GKI 2.0** devices (kernel 5.10+). Compatibility ultimately depends on the device's **KMI**, not just the kernel version — see the [installation guide](https://kernelsu.org/guide/installation.html).

**Learn more:** [Official website](https://kernelsu.org/) · [GitHub](https://github.com/tiann/KernelSU) · [Module repository](https://modules.kernelsu.org/)

## Quick Start

1. **Check compatibility** — install the [KernelSU Manager](https://github.com/tiann/KernelSU/releases/latest) and open it:
   - `Not installed` → officially supported.
   - `Unsupported` → you must build a kernel yourself (see [Unofficially supported devices](https://kernelsu.org/guide/unofficially-support-devices.html) and [Device Kernels](#device-kernels)).
2. **Install KernelSU** — see [Installation Modes](#installation-modes) and the official [installation guide](https://kernelsu.org/guide/installation.html).
3. **Install a metamodule** — required only if you use modules that modify `/system` files (e.g. `meta-overlayfs`). See [Metamodules](#metamodules).
4. **Verify** — open the Manager and confirm root status.

> **Prerequisites:** unlocked bootloader, a backup of your stock `boot.img`, and ADB/fastboot. Never skip the boot image backup — it is your recovery path.

## Installation Modes

On GKI devices KernelSU historically supports two modes. The official guide recommends:

- **LKM** — for phones.
- **GKI** — for emulators, WSA, and Waydroid.

### LKM (Loadable Kernel Module)

Loads KernelSU as a kernel module without replacing the original kernel.

- Keeps the stock kernel and manufacturer optimizations.
- Updates and OTA can be done in-app (including "install to inactive slot").
- Does not replace the boot partition, so it does not trigger AVB.
- Can be temporarily uninstalled without a reboot.
- Patches the **ramdisk** — on Android 13+ devices this means the **`init_boot`** partition, not `boot`.

### GKI (Generic Kernel Image)

Replaces the original kernel with a GKI image.

- Works without official firmware, as long as the **KMI** matches.
- Useful for devices where LKM cannot work (e.g. Samsung devices with KNOX enabled).

> [!NOTE]
> Since v3.0, official KernelSU has **dropped GKI image builds** (the [build guide](https://kernelsu.org/guide/how-to-build.html) is now archival) and recommends building the LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk). Official releases ship LKM modules and the Manager, not `boot.img` files. Forks (KernelSU-Next, SukiSU-Ultra, etc.) still provide GKI builds.

**Full instructions:** [Official installation guide](https://kernelsu.org/guide/installation.html) — including KMI and security-patch-level explanations.

## Metamodules

A **metamodule** is a special module that provides the module *mounting* infrastructure. Since v3.0, official KernelSU no longer mounts modules itself — it delegates mounting to a metamodule.

> [!IMPORTANT]
> A metamodule is needed **only for modules that modify `/system` files** (the `system` directory). Modules that only use scripts, `sepolicy`, or `system.prop` work without one. Only **one** metamodule can be installed at a time.

Note the scope: metamodule-based mounting applies to **official KernelSU** (v3.0+) and **ReSukiSU**. **KernelSU-Next** and **SukiSU-Ultra** still ship built-in mounting (Magic Mount / OverlayFS).

### Available metamodules

| Metamodule | Mounting | Notes |
|------------|----------|-------|
| [**meta-overlayfs**](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) | OverlayFS | **Official reference implementation** — recommended starting point. Also on the [official module repository](https://modules.kernelsu.org/module/meta-overlayfs). |
| [**mountify**](https://github.com/backslashxx/mountify) | OverlayFS | Third-party; supports APatch/Magisk too. |
| [**meta-hybrid_mount**](https://github.com/Hybrid-Mount/meta-hybrid_mount) | OverlayFS + Magic Mount | Third-party; dual-engine with auto-fallback ("Hybrid Mount"). |

Browse the full, current list of metamodules and modules at the **[official module repository](https://modules.kernelsu.org/)**.

**Details & switching procedure:** [Official metamodule guide](https://kernelsu.org/guide/metamodule.html)

## Official Resources

| Resource | Link |
|----------|------|
| Website & documentation | [kernelsu.org](https://kernelsu.org/) |
| Source code | [tiann/KernelSU](https://github.com/tiann/KernelSU) |
| Manager APK & LKM releases | [Releases](https://github.com/tiann/KernelSU/releases) ![Release](https://img.shields.io/github/v/release/tiann/KernelSU?style=flat-square&label=) |
| Module repository | [modules.kernelsu.org](https://modules.kernelsu.org/) |
| Announcements | [Telegram @KernelSU](https://t.me/KernelSU) |

## KernelSU Variants

> [!WARNING]
> Everything below **Official KernelSU** is a **community fork/derivative**, not an official project. Features of one variant do not apply to the others.

### Official KernelSU

The original implementation, by the KernelSU project (author [tiann](https://github.com/tiann)).

- **Target:** GKI 2.0 devices (kernel 5.10+). WSA, ChromeOS, and container-based Android are supported.
- **Architectures:** `arm64-v8a` and `x86_64`.
- **Module mounting:** metamodule-based (v3.0+).
- **Non-GKI:** dropped since v1.0 (last version `v0.9.5`); the [integration guide](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) is archival.
- **Notable changes:** seccomp+ioctl supercall (v2.0), `selinux hide` (v3.2.x), optional "jailbreak" mode via Magica (v3.2+).

> [!CAUTION]
> Recent kernel versions introduced a breaking change that can make KernelSU fail or **kernel-panic on `x86_64`**. Check the [official repository](https://github.com/tiann/KernelSU) for current status.

### KernelSU-Next

Enhanced fork with broader compatibility. [![GitHub](https://img.shields.io/badge/GitHub-KernelSU--Next-blue?style=flat-square&logo=github)](https://github.com/KernelSU-Next/KernelSU-Next) [![Release](https://img.shields.io/github/v/release/KernelSU-Next/KernelSU-Next?style=flat-square&label=)](https://github.com/KernelSU-Next/KernelSU-Next/releases) · [Website](https://kernelsu-next.github.io/webpage/)

- **Kernel support:** 4.4–6.6 (non-GKI 4.x–5.4 LTS; GKI 5.10–6.6; 6.6+ experimental).
- **Module mounting:** built-in **Magic Mount + OverlayFS**, switchable from settings.
- **Features:** module backup & restore, auto-updates, bulk install, hide hosts (unmount), SuSFS controls, SU-allowlist backup.
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86_64` (same `x86_64` panic caveat as upstream).
- **Community device list:** [Unofficially supported devices](https://kernelsu-next.github.io/webpage/pages/devices.html)

### SukiSU-Ultra

Fork focused on legacy devices, KPM, and built-in SUSFS management. [![GitHub](https://img.shields.io/badge/GitHub-SukiSU--Ultra-blue?style=flat-square&logo=github)](https://github.com/SukiSU-Ultra/SukiSU-Ultra) [![Release](https://img.shields.io/github/v/release/SukiSU-Ultra/SukiSU-Ultra?style=flat-square&label=)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) · [Website](https://sukisu.org/)

- **Kernel support:** non-GKI 4.4+; GKI 5.10+; 3.x (3.4–3.18) experimental.
- **Module mounting:** built-in **Magic Mount**.
- **KPM** (Kernel Patch Module) support — run code in kernel space (based on KernelPatch).
- **SUSFS** management built into the Manager (the kernel still needs SUSFS patches).
- **Architectures:** `arm64-v8a`, `armeabi-v7a` (bare), `x86_64` (some).

### ReSukiSU

Newer fork of SukiSU-Ultra. [![GitHub](https://img.shields.io/badge/GitHub-ReSukiSU-blue?style=flat-square&logo=github)](https://github.com/ReSukiSU/ReSukiSU) · [Website](https://resukisu.github.io/)

- **Module mounting:** metamodule-based.
- **Multi-manager:** works with the KernelSU, MKSU, RKSU, and SukiSU managers.
- **Kernel support:** GKI 2.0 (5.10+); 3.4+ with manual build.
- **Releases:** pre-release/CI builds so far (latest tag `v4.2.0-rc1`) — check the repository.

### Wild KSU — archived

> [!NOTE]
> The **Wild KSU** fork ([WildKernels/Wild_KSU](https://github.com/WildKernels/Wild_KSU)) is **archived** (last release v3.1.2). It is no longer maintained as a root variant. The **WildKernels** team still ships KernelSU/SUSFS device kernels — see [Device Kernels](#device-kernels).

### Comparison

| Feature | Official KernelSU | KernelSU-Next | SukiSU-Ultra | ReSukiSU |
|---|---|---|---|---|
| **Status** | Official, active | Active fork | Active fork | Active fork |
| **Kernel support** | GKI 2.0 (5.10+) | 4.4–6.6 | 4.4+ non-GKI; GKI 5.10+; 3.x exp. | 5.10+; 3.4+ manual |
| **Module mounting** | Metamodule | Magic Mount + OverlayFS | Magic Mount | Metamodule |
| **KPM** | ✗ | ✗ | ✓ | ✓ |
| **SUSFS** | via kernel patch | via kernel patch | built-in management | built-in management |
| **Multi-manager** | ✗ | ✗ | ✗ | ✓ |
| **Architectures** | arm64, x86_64 | arm64, arm, x86_64 | arm64, arm, x86_64 (some) | arm64, arm, x86_64 |

> SUSFS is a **separate** kernel-patch addon ([gitlab.com/simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu)) — it is not part of KernelSU itself. "Built-in management" means the Manager can control SUSFS on a SUSFS-patched kernel; it does not bundle the kernel patches.

### Which variant should I use?

- **Modern GKI 2.0 device (kernel 5.10+), stability first** → **Official KernelSU**.
- **Older kernel (4.4–6.6) or want extra module-management features** → **KernelSU-Next**.
- **Legacy/non-GKI device or need KPM** → **SukiSU-Ultra**.
- **Want metamodule architecture + multi-manager in the SukiSU family** → **ReSukiSU**.

## Modules & Tools

> The primary source for modules is the **[official module repository](https://modules.kernelsu.org/)**.

### Zygisk & frameworks

KernelSU has no built-in Zygisk; use a standalone implementation for Zygisk modules.

- [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext) — standalone Zygisk implementation.
- [**ReZygisk**](https://github.com/PerformanC/ReZygisk) — open-source, transparent Zygisk implementation.
- [**LSPosed**](https://github.com/LSPosed/LSPosed) — Xposed framework (requires Zygisk).

### Module managers

- [**MMRL**](https://github.com/MMRLApp/MMRL) — modern module manager with a built-in repository, updates, backup/restore, and WebUI support.

### Root hiding

- [**SUSFS**](https://gitlab.com/simonpunk/susfs4ksu) — kernel patches + userspace addon providing root-hiding mechanisms (experimental; requires a SUSFS-patched kernel).
- [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module) — addon root-hiding service for KernelSU.

> [!WARNING]
> These provide *root-hiding mechanisms* and **may improve** compatibility with apps that perform root checks. They do **not** guarantee passing Play Integrity or bypassing any given banking app, and often require additional configuration.

### Managers by variant

- [KernelSU Manager](https://github.com/tiann/KernelSU/releases) — official.
- [KernelSU-Next Manager](https://github.com/KernelSU-Next/KernelSU-Next/releases)
- [SukiSU Manager](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
- [ReSukiSU Manager](https://github.com/ReSukiSU/ReSukiSU)

## Device Kernels

Prebuilt kernels save you from compiling. **Always verify the exact device model, Android version, kernel version, and security-patch level before flashing.**

> For anything not listed here, check the maintained community list of [KernelSU-Next unofficially supported devices](https://kernelsu-next.github.io/webpage/pages/devices.html), the [XDA KernelSU tag](https://xdaforums.com/tags/ksu/), or GitHub topic/search results.

| Project | Devices | Notes |
|---------|---------|-------|
| [WildKernels — GKI](https://github.com/WildKernels/GKI_KernelSU_SUSFS) | GKI 2.0 (5.10+) devices | KernelSU + SUSFS; active |
| [WildKernels — Sultan](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) | Google Pixel | Sultan base + SUSFS; active |
| [WildKernels — OnePlus](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) | OnePlus devices | KernelSU + SUSFS; active |
| [WildKernels — Samsung](https://github.com/WildKernels/Samsung_KernelSU_SUSFS) | Samsung devices | KernelSU + SUSFS; active |
| [YuzakiKokuban — Samsung](https://github.com/YuzakiKokuban) | Galaxy S23/S24/S25, Tab S10 | KernelSU kernel sources (`sm8550`, `sm8650`, `sm8750`, `mt6989`); active |
| [KernelSU LKM — OnePlus 12](https://github.com/snowwolf725/KernelSU_LKM_For_Oneplus12) | OnePlus 12 | LKM for OxygenOS/ColorOS; active |
| [topnotchfreaks — msm-5.15](https://github.com/topnotchfreaks/kernel_msm-5.15) | Redmi Note 12/13 4G, Redmi Pad SE, Redmi 15/POCO M7 | SukiSU-Ultra + KPM + SUSFS variants; active |

**Kernel selection checklist:** exact device match · matching Android/kernel version · security-patch level (anti-rollback can brick on older patches) · active maintenance · a copy of your stock `boot.img` for recovery.

## Building from Source

- **Official KernelSU:** build the LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk) (recommended since v3.0). The GKI and non-GKI build guides are archival — [How to build](https://kernelsu.org/guide/how-to-build.html) · [Integrate for non-GKI](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html).
- **Forks** (KernelSU-Next, SukiSU-Ultra, ReSukiSU) still support direct kernel integration — see each repository's `kernel/setup.sh`.
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

- [@KernelSU](https://t.me/KernelSU) — official announcements channel.
- [@KernelSU_group](https://t.me/KernelSU_group) — official community group.
- [@Sukiksu](https://t.me/Sukiksu) — SukiSU community.
- [@ReSukiSU](https://t.me/ReSukiSU) — ReSukiSU community.

**Other**

- [GitHub Discussions](https://github.com/tiann/KernelSU/discussions) · [Issue tracker](https://github.com/tiann/KernelSU/issues)
- [r/KernelSU](https://www.reddit.com/r/KernelSU/) on Reddit
- [XDA Developers — KernelSU tag](https://xdaforums.com/tags/ksu/)

## Troubleshooting

| Issue | Likely cause | Fix |
|-------|--------------|-----|
| **Bootloop** | Incompatible kernel/image | Flash your stock `boot.img` via fastboot; see [rescue guide](https://kernelsu.org/guide/rescue-from-bootloop.html) |
| **Modules not mounted** | No metamodule installed (official KSU 3.0+) | Install [meta-overlayfs](https://github.com/KernelSU-Modules-Repo/meta-overlayfs) and reboot |
| **Root not detected** | Manager/install issue | Reinstall the Manager; check `su` from a terminal |
| **App detects root** | Root-visible to app | Configure App Profiles; see [Root hiding](#root-hiding) |

Before any change, keep a backup of your stock `boot.img`. When asking for help, include device model, Android/kernel version, variant + version, installation method, and which metamodule (if any) is installed.

## Contributing

Contributions are welcome — new tools, modules, maintained device kernels, and documentation fixes. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Disclaimer

Rooting and kernel modification can void warranties, brick devices, and expose security vulnerabilities. This list is provided for **educational and informational purposes only** — you assume all risks.

KernelSU and its derivatives are independent, community-driven projects. They are not affiliated with or endorsed by Google, Android, or any device manufacturer.

## License

[MIT](LICENSE) © Fynks
