<div align="center">

<img src="./media/kernelsu-logo.svg" alt="KernelSU Logo" width="128"/>

# Awesome KernelSU

**A curated list of KernelSU resources: official documentation, variants, metamodules, modules, tools, and device kernels.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/fynks/awesome-kernelsu?style=flat-square&logo=github)](https://github.com/fynks/awesome-kernelsu)
[![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)

</div>

## Contents

- [What is KernelSU?](#what-is-kernelsu)
- [Getting Started](#getting-started)
- [Installation Modes](#installation-modes)
- [Metamodules](#metamodules)
- [KernelSU Variants](#kernelsu-variants)
- [Modules & Tools](#modules--tools)
- [Device Kernels](#device-kernels)
- [Building from Source](#building-from-source)
- [Documentation](#documentation)
- [Community](#community)
- [Troubleshooting](#troubleshooting)
- [FAQs](#faqs)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## What is KernelSU?

**KernelSU** is a kernel-based root solution for Android. The `su` binary, the root allowlist, and the permission checks live in the Linux kernel, so nothing in the system partition has to be modified to grant root.

### Key Features

- **Root access control** — root is granted per UID/package. Apps without a grant never see `su`.
- **Kernel-level isolation** — the manager talks to the kernel over a small IOCTL interface, so a userspace app cannot rewrite the rules it is judged by.
- **Metamodule system** — module mounting is delegated to a pluggable metamodule instead of living in the core.
- **App Profile** — per-app UID, GID, supplementary groups, Linux capabilities, SELinux domain, and mount namespace.
- **Module configuration store** — modules read and write persistent or per-boot key-value settings through `ksud module config`.
- **Late-load mode** — the kernel module can be loaded after boot instead of at init, for use cases that need the stock boot path.
- **Native module blacklist** — other kernel modules can be blocked at boot from the Manager.
- **ADB root** — an optional `adb root` shell, optionally restricted to live adb sessions with `shell_su_adb_only`.
- **SELinux hide** — optional kernel-side hiding of the SELinux mode and attribute state.
- **Magica jailbreak mode** — root escalation on a boot that comes up with permissive SELinux.
- **x86_64 support** — LKM builds for x86_64 cover emulators, WSA, Waydroid, and ChromeOS containers.

> [!NOTE]
> Official KernelSU targets Android **GKI 2.0** devices (kernel 5.10+). Compatibility ultimately depends on the device's **KMI**, not just the kernel version — see the [installation guide](https://kernelsu.org/guide/installation.html).

<br>

> **Read next:** [KernelSU rooting guide](https://awesome-android-root.xyz/rooting-guides/kernelsu-guide) · [Official documentation](https://kernelsu.org/) · [Official module registry](https://modules.kernelsu.org)

## Getting Started

### Prerequisites

- **Unlocked bootloader** — required for every installation method.
- **Stock boot image backup** — your only way out of a bootloop.
- **ADB and fastboot** on your computer.
- **A compatible device** — check with the Manager before anything else.

> [!TIP]
> Bootloader unlocking is device-specific and often gated. [Awesome Android Root](https://awesome-android-root.xyz/rooting-guides/how-to-unlock-bootloader) walks through the process.

### Steps

1. **Check compatibility.** Install the [KernelSU Manager](https://github.com/tiann/KernelSU/releases/latest) and open it:
   - `Not installed` → the device is officially supported.
   - `Unsupported` → you need to build the kernel yourself. See [Device Kernels](#device-kernels) and the [non-GKI integration guide](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html).
2. **Choose an installation mode** — [LKM](#lkm-loadable-kernel-module) or [GKI](#gki-generic-kernel-image).
3. **Install KernelSU** following the [installation guide](https://kernelsu.org/guide/installation.html).
4. **Install a metamodule** if you use modules that ship a `system/` directory. See [Metamodules](#metamodules).
5. **Verify** that the Manager reports an installed kernel with a matching version.

## Installation Modes

Two installation modes are documented. The official recommendation: **LKM for phones, GKI for emulators, WSA, and Waydroid.**

### LKM (Loadable Kernel Module)

Loads KernelSU as a kernel module instead of replacing the kernel.

- Keeps the stock kernel and vendor tuning.
- Upgrades in the Manager, including "install to inactive slot" after an OTA.
- Patches the ramdisk, not the boot image, so AVB is not tripped.
- Can be removed temporarily and re-enabled on the next reboot.
- On Android 13+ the patched partition is **`init_boot`**, not `boot`.

### GKI (Generic Kernel Image)

Replaces the device kernel with a generic image.

- Works on any device with a matching KMI, with or without official firmware.
- The option for Knox-locked Samsung devices, where LKM cannot run.

> [!NOTE]
> Since the 3.0 line, official KernelSU no longer publishes GKI images — the build guide is archival and [Ylarod/ddk](https://github.com/Ylarod/ddk) is the recommended way to produce an LKM. Forks (KernelSU-Next, SukiSU-Ultra, BakaSU) and community builders still ship GKI images.

<details>
<summary>Quick comparison</summary>

| GKI mode | LKM mode |
| --- | --- |
| Universal GKI compatibility | Preserves the original kernel and tuning |
| Works on Knox-locked devices | In-app updates, OTA-friendly |
| Independent of firmware updates | No AVB or dm-verity issues |
| Better on heavily modified devices | Can be disabled without a reboot |
| Loses manufacturer kernel tuning | Needs matching official firmware |
| Requires manual fastboot flashing | May not work on modified firmware |
| Must be reflashed after major updates | |

</details><br>

> [!TIP]
> Full instructions, KMI matching, and security-patch-level rules: [official installation guide](https://kernelsu.org/guide/installation.html).

## Metamodules

A **metamodule** provides the module *mounting* infrastructure. Since the 3.0 line, official KernelSU does not mount modules itself — a metamodule does.

> [!IMPORTANT]
> A metamodule is required only for modules that ship a `system/` directory. Script-only, `sepolicy.rule`, and `system.prop` modules work without one. Only one metamodule can be active at a time.

This applies to official KernelSU, BakaSU, YukiSU, and FinaSU. KernelSU-Next and SukiSU-Ultra still carry their own mounting engines.

<img src="./media/metamodule-flow.svg" alt="A module's system directory is read by the metamodule at boot, which routes it to OverlayFS, Magic Mount, or VFS injection, then applies it to the live filesystem" width="760">

*How a module's `system/` directory reaches the live filesystem.*

### Available metamodules

| Metamodule | Mounting | Requirements | Notes |
|---|---|---|---|
| [**meta-hybrid_mount**](https://github.com/Hybrid-Mount/meta-hybrid_mount) | OverlayFS + Magic Mount | OverlayFS-capable kernel; an ext4 staging partition is used | Listed in the [official registry](https://modules.kernelsu.org/). Picks the engine per module and per path, with automatic fallback. |
| [**mountify**](https://github.com/backslashxx/mountify) | OverlayFS | OverlayFS-capable kernel | Global mount mode, works with Magisk and APatch too. |
| [**meta-magic_mount-rs**](https://github.com/Tools-cx-app/meta-magic_mount-rs) | Magic Mount | None beyond a supported KernelSU build | Rust rewrite of the Magic Mount metamodule, based on MKSU. |
| [**meta-magic_mount**](https://github.com/backslashxx/meta-magic_mount) | Magic Mount | None beyond a supported KernelSU build | Original Magic Mount metamodule, for modules that need Magisk-identical mounts. |
| [**NoMount**](https://github.com/maxsteeel/nomount) | VFS injection | Kernel must allow inode-operation interception; the bundled LKM covers most GKI kernels without a custom kernel | Mountless: paths are redirected in the VFS instead of mounted, so nothing reaches the mount table. Works with KernelSU and APatch, ships a WebUI and an `nm` CLI. |
| [**Meta-Overlayfsx**](https://github.com/RipperHybrid/Meta-Overlayfsx) | OverlayFS | OverlayFS-capable kernel; slow storage adds I/O overhead | Continuation of the original `meta-overlayfs` with a WebUI and a live mount inspector. |
| [**MyOverlayFs**](https://github.com/MySU-org/meta-overlayfs) | OverlayFS | OverlayFS-capable kernel; writes to an ext4 image, with a repair pass on boot | Another continuation of the original `meta-overlayfs`. |

> [!WARNING]
> `NoMount` and `meta-hybrid_mount` both hijack inode operations and register different key types, so they cannot coexist on one kernel. hybrid_mount refuses to install into a tree that already integrates NoMount. Pick one.

> [!TIP]
> Unsure which engine you need? A mountless metamodule (NoMount) avoids the I/O overhead of OverlayFS entirely; Magic Mount is the safest match for modules ported from Magisk. When in doubt, `meta-hybrid_mount` routes per module and falls back automatically.

### Installing a metamodule

1. Download the metamodule ZIP from its GitHub releases.
2. Open the Manager → **Modules**.
3. Tap the **➕** button and pick the ZIP.
4. Reboot.

The active metamodule is marked in the module list.

> [!TIP]
> The full list of metamodules and modules: [modules.kernelsu.org](https://modules.kernelsu.org/). Details on switching: [metamodule guide](https://kernelsu.org/guide/metamodule.html).

## KernelSU Variants

> [!WARNING]
> Everything below official KernelSU is a community fork. Features do not carry over between them, and a fork can add detection vectors or stop being maintained.

### Picking a variant

Start from your situation:

| Situation | Pick |
|---|---|
| Stock-ish GKI phone, firmware updates matter | Official KernelSU, LKM mode |
| Kernel outside 5.10–6.18, or you want SUSFS without rebuilding | KernelSU-Next |
| You need KPM modules or a very old kernel | SukiSU-Ultra |
| You want the official Manager on a non-upstream kernel, or manual hooks down to 3.4 | BakaSU |
| You want Zygisk bundled with the Manager | YukiSU or FinaSU |
| Knox-locked Samsung, or an emulator image | GKI mode, from a fork or a community builder |

Then compare the details:

| Variant | Kernel support | Mounting | KPM | Multi-manager | Manager highlights | Best for |
|---|---|---|---|---|---|---|
| **Official KernelSU** | GKI 2.0 (5.10+), LKM to Android 17 / 6.18 | Metamodule | — | — | App profiles, module config, `adb root`, Magica, SELinux hide | Stability and OTA survival |
| **KernelSU-Next** | Non-GKI 4.x–5.4 LTS, GKI 5.10+ | Magic Mount + OverlayFS toggle | — | — | Module/allowlist backup, prebuilt SUSFS LKM, bulk install | Wide kernel range without compiling |
| **SukiSU-Ultra** | Non-GKI 4.x–5.4 LTS (3.x experimental), GKI 5.10+ | Built-in Magic Mount | ✅ | — | SUSFS controls, WebUI X, jailbreak mode | KPM and legacy devices |
| **BakaSU** | GKI 2.0, 3.4+ manual | Metamodule | — | ✅ | Minimal hooks, built-in SUSFS management | Old kernels and a second Manager |
| **YukiSU** | ARM64 GKI 2.0 | Metamodule | — | — | Built-in YukiZygisk, C++ userspace, temporary jailbreak mode | A self-contained Zygisk |
| **FinaSU** | GKI 5.10+, 4.14+ manual | Metamodule | — | — | FolkZygisk, theme store | Customization |
| **KOWSU** | GKI 2.0, 4.14+ manual | Metamodule | — | ✅ | Material theming, many translations | Upstream look with a different theme |
| **Wild KSU** | Archived | — | — | — | — | Historic reference only |

> [!NOTE]
> SUSFS is a separate kernel-side project ([susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu)), not part of KernelSU. "Built-in management" means the Manager can drive SUSFS on a SUSFS-capable kernel; the patches or the LKM loader are still required.

> [!NOTE]
> KPM is a SukiSU-Ultra feature. [KPatch-Next](https://github.com/KernelSU-Next/KPatch-Next) ports it to Magisk and KernelSU, so a KPM module can be used on a plain KernelSU build.

### Official KernelSU

[![GitHub](https://img.shields.io/badge/GitHub-tiann%2FKernelSU-blue?logo=github&style=flat-square)](https://github.com/tiann/KernelSU)
[![Release](https://img.shields.io/github/v/release/tiann/KernelSU?style=flat-square)](https://github.com/tiann/KernelSU/releases)
[![Stars](https://img.shields.io/github/stars/tiann/KernelSU?style=flat-square)](https://github.com/tiann/KernelSU)
[![Docs](https://img.shields.io/badge/Docs-kernelsu.org-green?style=flat-square)](https://kernelsu.org/)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU)

> The original implementation, and the reference for everything else.

<details open>
<summary><b>View details</b></summary>

- **Target:** GKI 2.0 (kernel 5.10+), including WSA, ChromeOS, and container-based Android.
- **Architectures:** `arm64-v8a`, `x86_64`; `riscv64` `ksud`/`ksuinit` artifacts.
- **Kernel coverage in releases:** Android 12 / 5.10 through Android 17 / 6.18.
- **Mounting:** metamodule-based.
- **Manager:** Material 3 and MIUI-style themes, app profiles, module config, `adb root`, Magica jailbreak mode, optional SELinux hiding, native module blacklist, late-load mode, `boot-patch-v2`, and a kernel-side `sulog` view.
- **Not supported:** non-GKI kernels were dropped after the 1.0 line; the [integration guide](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) is archival.

**Resources:** [Manager APK](https://github.com/tiann/KernelSU/releases/latest) · [Documentation](https://kernelsu.org/) · [Module registry](https://modules.kernelsu.org/) · [Telegram channel](https://t.me/KernelSU) · [Issue tracker](https://github.com/tiann/KernelSU/issues)

</details>

### KernelSU-Next

[![GitHub](https://img.shields.io/badge/GitHub-KernelSU--Next-blue?logo=github&style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next)
[![Release](https://img.shields.io/github/v/release/KernelSU-Next/KernelSU-Next?style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next/releases)
[![Stars](https://img.shields.io/github/stars/KernelSU-Next/KernelSU-Next?style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next)
[![Docs](https://img.shields.io/badge/Docs-kernelsu--next.github.io-green?style=flat-square)](https://kernelsu-next.github.io/webpage/)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU--Next-blue?style=flat-square&logo=telegram)](https://t.me/ksunext)

> Wide kernel coverage, module backup, and prebuilt SUSFS loaders.

<details>
<summary><b>View details</b></summary>

- **Kernel support:** non-GKI 4.x–5.4 in LTS mode, GKI 5.10 upward; released LKM artifacts cover Android 12 / 5.10 through Android 17 / 6.18.
- **Mounting:** built-in Magic Mount and OverlayFS, switchable from settings.
- **SUSFS:** ships `susfs_guard_lkm.ko` per KMI, with KPROBES hiding controls in the Manager.
- **Manager:** module backup and restore, SU allowlist backup, bulk install, auto-updates, hide-hosts via app-profile unmount, spoofed-package Manager builds, native kernel-module blocking, `shell_su_adb_only`.
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86_64`.
- **Device list:** [unofficially supported devices](https://kernelsu-next.github.io/webpage/pages/devices.html).

**Resources:** [Manager APK](https://github.com/KernelSU-Next/KernelSU-Next/releases) · [Website](https://kernelsu-next.github.io/webpage/) · [Telegram group](https://t.me/ksunext) · [CI channel](https://t.me/ksunext_ci) · [Issue tracker](https://github.com/KernelSU-Next/KernelSU-Next/issues)

</details>

### SukiSU-Ultra

[![GitHub](https://img.shields.io/badge/GitHub-SukiSU--Ultra-blue?logo=github&style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
[![Release](https://img.shields.io/github/v/release/SukiSU-Ultra/SukiSU-Ultra?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
[![Stars](https://img.shields.io/github/stars/SukiSU-Ultra/SukiSU-Ultra?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
[![Docs](https://img.shields.io/badge/Docs-sukisu.org-green?style=flat-square)](https://sukisu.org/)
[![Telegram](https://img.shields.io/badge/Telegram-SukiKSU-blue?style=flat-square&logo=telegram)](https://t.me/Sukiksu)

> The variant with KPM, built-in Magic Mount, and the deepest legacy device coverage.

<details>
<summary><b>View details</b></summary>

- **Kernel support:** non-GKI 4.x–5.4 in LTS mode (3.x experimental), GKI 5.10 upward, with LKM, GKI, and built-in integration paths.
- **Mounting:** built-in Magic Mount.
- **KPM:** KernelPatch-style kernel modules, ported from APatch, with inline and syscall-table hooks.
- **Manager:** built-in SUSFS management, Magica jailbreak mode, WebUI X, MIUI and Material themes, in-app language switcher, Zygisk implementation detection, multi-manager signature authorization, Android 8–11 support.
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86_64`.

**Resources:** [Manager APK](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) · [Website](https://sukisu.org/) · [Installation guide](https://sukisu.org/guide/installation) · [Telegram](https://t.me/Sukiksu)

</details>

### BakaSU

[![GitHub](https://img.shields.io/badge/GitHub-Baka--SU%2FBakaSU-blue?logo=github&style=flat-square)](https://github.com/Baka-SU/BakaSU)
[![Pre-release](https://img.shields.io/github/v/pre-release/Baka-SU/BakaSU?style=flat-square)](https://github.com/Baka-SU/BakaSU/releases)
[![Stars](https://img.shields.io/github/stars/Baka-SU/BakaSU?style=flat-square)](https://github.com/Baka-SU/BakaSU)
[![Docs](https://img.shields.io/badge/Docs-bakasu.org-green?style=flat-square)](https://bakasu.org/)
[![Telegram](https://img.shields.io/badge/Telegram-BakaSU-blue?style=flat-square&logo=telegram)](https://t.me/BAKASU_grp)

> Formerly **ReSukiSU**. A downstream of KernelSU through the SukiSU branch, with minimal hooks and multi-manager support.

<details>
<summary><b>View details</b></summary>

- **Mounting:** metamodule-based.
- **Multi-manager:** the official KernelSU Manager and the KOWSU Manager both work with a BakaSU kernel.
- **Hook modes:** tracepoint syscall redirect (GKI 2.0), manual hook (Linux 3.4 to 6.18), and SUSFS inline hook.
- **Kernel support:** GKI 2.0 (5.10+); older kernels down to 3.4 with a manual build.
- **SUSFS:** built-in management, with the SUSFS backport limited to kernel 4.3+.
- **Architectures:** `arm64-v8a`, `armeabi-v7a`, `x86_64`.
- **Releases:** tagged as pre-releases, so watch the releases page rather than the "latest release" badge.

**Resources:** [Manager APK](https://github.com/Baka-SU/BakaSU/releases) · [Website](https://bakasu.org/) · [Telegram group](https://t.me/BAKASU_grp) · [Telegram channel](https://t.me/BakaSU_Grp)

</details>

### YukiSU

[![GitHub](https://img.shields.io/badge/GitHub-Anatdx%2FYukiSU-blue?logo=github&style=flat-square)](https://github.com/Anatdx/YukiSU)
[![Release](https://img.shields.io/github/v/release/Anatdx/YukiSU?style=flat-square)](https://github.com/Anatdx/YukiSU/releases)
[![Stars](https://img.shields.io/github/stars/Anatdx/YukiSU?style=flat-square)](https://github.com/Anatdx/YukiSU)
[![Docs](https://img.shields.io/badge/Docs-yukisu.anatdx.com-green?style=flat-square)](https://yukisu.anatdx.com/)
[![Telegram](https://img.shields.io/badge/Telegram-YukiSU-blue?style=flat-square&logo=telegram)](https://t.me/YukiSU)

> A KernelSU fork with a rewritten C++ userspace and its own kernel-level Zygisk implementation.

<details>
<summary><b>View details</b></summary>

- **Scope:** ARM64 GKI 2.0 with LKM, and nothing else — the project keeps a deliberately narrow target.
- **Userspace:** `ksud`, `ksuinit`, and `su` are rewritten in C++ rather than wrapping upstream binaries.
- **Zygisk:** [YukiZygisk](https://github.com/Anatdx/YukiZygisk) is built in and managed from the Manager, so no separate Zygisk module is needed.
- **Jailbreak mode:** the LKM can be loaded temporarily without touching the boot image; the root does not survive a reboot.
- **Authentication:** the official Manager authenticates by signature; a SuperKey is available for private deployments.
- **Mounting:** metamodule-based, following upstream.

**Resources:** [Manager APK](https://github.com/Anatdx/YukiSU/releases) · [Website](https://yukisu.anatdx.com/) · [Telegram](https://t.me/YukiSU)

</details>

### FinaSU

[![GitHub](https://img.shields.io/badge/GitHub-LyraVoid%2FFinaSU-blue?logo=github&style=flat-square)](https://github.com/LyraVoid/FinaSU)
[![Release](https://img.shields.io/github/v/release/LyraVoid/FinaSU?style=flat-square)](https://github.com/LyraVoid/FinaSU/releases)
[![Stars](https://img.shields.io/github/stars/LyraVoid/FinaSU?style=flat-square)](https://github.com/LyraVoid/FinaSU)
[![Telegram](https://img.shields.io/badge/Telegram-FinaSU-blue?style=flat-square&logo=telegram)](https://t.me/FinaSU)

> A KernelSU fork with a built-in Zygisk engine, SUSFS support, and a theme store.

<details>
<summary><b>View details</b></summary>

- **Zygisk:** the built-in FolkZygisk engine, with Manager controls.
- **Hiding:** mount hiding, SELinux hiding, AVC log spoofing, unmount policy, and SUSFS support gated on kernel capability.
- **Manager:** `.fpt` themes with a theme store, multi-page wallpapers, module repository browsing, in-app language picker.
- **Kernel support:** GKI 5.10+; 4.14+ with a manual build.
- **Architectures:** `arm64-v8a` first, with `x86_64` and `riscv64` hooks present.

**Resources:** [Manager APK](https://github.com/LyraVoid/FinaSU/releases) · [Telegram](https://t.me/FinaSU)

</details>

### KOWSU

[![GitHub](https://img.shields.io/badge/GitHub-KOWX712%2FKernelSU-blue?logo=github&style=flat-square)](https://github.com/KOWX712/KernelSU)
[![Last commit](https://img.shields.io/github/last-commit/KOWX712/KernelSU?style=flat-square)](https://github.com/KOWX712/KernelSU)
[![Stars](https://img.shields.io/github/stars/KOWX712/KernelSU?style=flat-square)](https://github.com/KOWX712/KernelSU)
[![Telegram](https://img.shields.io/badge/Telegram-KOWSU-blue?style=flat-square&logo=telegram)](https://t.me/kowsu_build)

> A personal upstream fork focused on Material theming and translation coverage.

No tagged releases — the Manager APK comes from the project's build channel. Kernel support follows upstream: GKI 2.0, with 4.14+ through manual integration. The channel also runs a [discussion group](https://t.me/kowchannelchat).

### Wild KSU — archived

> [!NOTE]
> [Wild KSU](https://github.com/WildKernels/Wild_KSU) is archived and no longer maintained as a root variant. The **WildKernels** organisation still publishes KernelSU and SUSFS device kernels — see [Device Kernels](#device-kernels).

## Modules & Tools

> The primary source for modules is the [official registry](https://modules.kernelsu.org/). It indexes modules that live in their authors' own repositories, published as immutable GitHub releases.

### Publishing a module

- [**KernelSU Modules registry**](https://modules.kernelsu.org/) — the catalog the Manager reads.
- [**Developer portal**](https://developers.kernelsu.org/) — sign in with GitHub and submit a repository.
- [**Developer documentation**](https://developers.kernelsu.org/docs/) — `module.yaml` reference, release action, closed-source distribution, check codes.
- [**Example module**](https://github.com/KernelSU-Modules/example-module) — a minimal working layout.

### Zygisk implementations

KernelSU has no built-in Zygisk. Pick one of these and install it as a module.

| Implementation | Notes | Release |
|---|---|---|
| [**ZygiskNext**](https://github.com/LSPosed/ZygiskNext) | The long-standing standalone implementation, now hosted by the LSPosed organisation. The original repository is [Dr-TSNG/ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext). | [![Release](https://img.shields.io/github/v/release/LSPosed/ZygiskNext?style=flat-square)](https://github.com/LSPosed/ZygiskNext/releases) |
| [**ReZygisk**](https://github.com/PerformanC/ReZygisk) | Transparent implementation, written to be auditable. | [![Release](https://img.shields.io/github/v/release/PerformanC/ReZygisk?style=flat-square)](https://github.com/PerformanC/ReZygisk/releases) |
| [**NeoZygisk**](https://github.com/JingMatrix/NeoZygisk) | ptrace-based zygote injection. | [![Release](https://img.shields.io/github/v/release/JingMatrix/NeoZygisk?style=flat-square)](https://github.com/JingMatrix/NeoZygisk/releases) |
| [**ZygiskNextNext**](https://github.com/VeryBaaad/ZygiskNextNext) | A from-scratch implementation, listed in the official registry. | [![Release](https://img.shields.io/github/v/release/VeryBaaad/ZygiskNextNext?style=flat-square)](https://github.com/VeryBaaad/ZygiskNextNext/releases) |
| [**YukiZygisk**](https://github.com/Anatdx/YukiZygisk) | Kernel-level Zygisk, bundled with YukiSU. | [![Release](https://img.shields.io/github/v/release/Anatdx/YukiZygisk?style=flat-square)](https://github.com/Anatdx/YukiZygisk/releases) |
| [**VexZygisk**](https://github.com/Lxiaoyao077/VexZygisk) | Kernel-level Zygisk; submitted to the official registry. | [![Release](https://img.shields.io/github/v/release/Lxiaoyao077/VexZygisk?style=flat-square)](https://github.com/Lxiaoyao077/VexZygisk/releases) |

For the Xposed layer on top of Zygisk: [**LSPosed**](https://github.com/LSPosed/LSPosed).

### Module managers

- [**MMRL**](https://github.com/MMRLApp/MMRL) — module manager with a built-in repository, updates, backup and restore, and the WebUI X runtime. Community repositories: [ZGUATION-PROJECTS/ZG-R](https://github.com/ZGUATION-PROJECTS/ZG-R) · [Yukari0201/mmrl-repo](https://github.com/Yukari0201/mmrl-repo).

### Root hiding and attestation

| Project | What it does | Release |
|---|---|---|
| [**SUSFS**](https://gitlab.com/simonpunk/susfs4ksu) | Upstream kernel patches and userspace tool for hiding root files and mounts. The `master` branch is frozen; per-kernel-version branches carry the current code. | [![Last commit](https://img.shields.io/gitlab/last-commit/simonpunk/susfs4ksu?style=flat-square)](https://gitlab.com/simonpunk/susfs4ksu) |
| [**susfs4ksu**](https://github.com/ShirkNeko/susfs4ksu) | Actively maintained SUSFS tree. | [![Last commit](https://img.shields.io/github/last-commit/ShirkNeko/susfs4ksu?style=flat-square)](https://github.com/ShirkNeko/susfs4ksu) |
| [**susfs4ksu-lkm**](https://github.com/inforcqb/susfs4ksu-lkm) | SUSFS ported to a loadable kernel module, loaded through `ksud`. Releases also ship a flashable KernelSU module that picks the matching `.ko` for the device kernel and loads it at boot, so no kernel rebuild or manual loading is needed. | [![Release](https://img.shields.io/github/v/release/inforcqb/susfs4ksu-lkm?style=flat-square)](https://github.com/inforcqb/susfs4ksu-lkm/releases) |
| [**susfs-lkm-module**](https://github.com/matsuzaka-yuki/susfs-lkm-module) | KernelSU-compatible ZIP wrapper around the pinned SUSFS LKM. | [![Release](https://img.shields.io/github/v/release/matsuzaka-yuki/susfs-lkm-module?style=flat-square)](https://github.com/matsuzaka-yuki/susfs-lkm-module/releases) |
| [**susfs4ksu-module**](https://github.com/sidex15/susfs4ksu-module) | Userspace addon service for SUSFS. | [![Release](https://img.shields.io/github/v/release/sidex15/susfs4ksu-module?style=flat-square)](https://github.com/sidex15/susfs4ksu-module/releases) |
| [**ReSuSFS**](https://github.com/ahmed-alnassif/ReSuSFS) | Packaged SUSFS experience: strong hiding by default, built-in spoofing, config files, script manager. Listed in the official registry. | [![Release](https://img.shields.io/github/v/release/ahmed-alnassif/ReSuSFS?style=flat-square)](https://github.com/ahmed-alnassif/ReSuSFS/releases) |
| [**Zygisk Assistant**](https://github.com/snake-4/Zygisk-Assistant) | Zygisk module that hides root for KernelSU, Magisk, and APatch. | [![Release](https://img.shields.io/github/v/release/snake-4/Zygisk-Assistant?style=flat-square)](https://github.com/snake-4/Zygisk-Assistant/releases) |
| [**Integrity-Box**](https://github.com/MeowDump/Integrity-Box) | Toolset for Play Integrity and system environment management. | [![Release](https://img.shields.io/github/v/release/MeowDump/Integrity-Box?style=flat-square)](https://github.com/MeowDump/Integrity-Box/releases) |
| [**Play Integrity Fix**](https://github.com/KOWX712/PlayIntegrityFix) | Universal Play Integrity fix, now maintained here. Listed in the official registry. | [![Release](https://img.shields.io/github/v/release/KOWX712/PlayIntegrityFix?style=flat-square)](https://github.com/KOWX712/PlayIntegrityFix/releases) |
| [**TrickyStore**](https://github.com/5ec1cff/TrickyStore) | Spoofs the TEE/keystore attestation chain. Closed source. | [![Release](https://img.shields.io/github/v/release/5ec1cff/TrickyStore?style=flat-square)](https://github.com/5ec1cff/TrickyStore/releases) |
| [**TrickyStoreOSS**](https://github.com/beakthoven/TrickyStoreOSS) | Open-source alternative to TrickyStore. | [![Release](https://img.shields.io/github/v/release/beakthoven/TrickyStoreOSS?style=flat-square)](https://github.com/beakthoven/TrickyStoreOSS/releases) |
| [**Oh My Keymint**](https://github.com/qwq233/OhMyKeymint) | Custom keystore implementation for Android keystore spoofing. | [![Release](https://img.shields.io/github/v/release/qwq233/OhMyKeymint?style=flat-square)](https://github.com/qwq233/OhMyKeymint/releases) |
| [**Duck ToolBox**](https://github.com/eltavine/Duck-ToolBox) | Attestation workbench: Tricky Store, TEESimulator, OhMyKeymint, and RKP tooling in one WebUI. | [![Release](https://img.shields.io/github/v/release/eltavine/Duck-ToolBox?style=flat-square)](https://github.com/eltavine/Duck-ToolBox/releases) |

> [!WARNING]
> These provide *root-hiding mechanisms*. They may improve compatibility with apps that check for root, but they do **not** guarantee a passing Play Integrity verdict or a working banking app, and most need a matching kernel and a correct configuration. Any paid "keybox" offer is a scam.

> [!NOTE]
> Shamiko was part of this stack and is no longer maintained — the LSPosed repositories that hosted it are archived. Zygisk Assistant and the SUSFS LKM path cover the same ground.

### Kernel-side tooling

- [**KPatch-Next**](https://github.com/KernelSU-Next/KPatch-Next) — standalone KPM implementation for Magisk and KernelSU, with an installer module in [KPatch-Next-Module](https://github.com/KernelSU-Next/KPatch-Next-Module). This is what makes KPM usable outside SukiSU-Ultra.
- [**Ylarod/ddk**](https://github.com/Ylarod/ddk) — kernel driver development kit, the recommended way to build an LKM for a custom kernel.
- [**AnyKernel3**](https://github.com/osm0sis/AnyKernel3) — packaging and flashing for kernel ZIPs.
- [**kernel_build_action**](https://github.com/dabao1955/kernel_build_action) — GitHub Actions workflow that builds a kernel with KernelSU in CI.
- [**KernelSU_Action**](https://github.com/xiaoleGun/KernelSU_Action) — another CI action for integrating KernelSU into a kernel tree.
- [**KernelSU_General_porting_guide**](https://github.com/dabao1955/KernelSU_General_porting_guide) — Chinese-language guide to porting KernelSU to a non-GKI kernel.
- [**kernelsu-coccinelle**](https://github.com/devnoname120/kernelsu-coccinelle) — automatic KernelSU patches for non-GKI kernels using Coccinelle.
- [**KernelSU-Style-UI-Kit**](https://github.com/chenaizhang/KernelSU-Style-UI-Kit) — UI templates extracted from the KernelSU Manager, for building a custom manager.

### Other projects

- [**systemless-hosts**](https://github.com/symbuzzer/systemless-hosts-KernelSU-module) — hosts-file blocking as a systemless module.
- [**KernelSUGrantToast**](https://github.com/NativeStar/KernelSUGrantToast) — show a Magisk-style toast when root is granted.
- [**Nethunter for KernelSU**](https://github.com/SherlockChiang/Nethunter_for_KernelSU) — the NetHunter toolkit as a KernelSU module.
- [**Droidspaces**](https://github.com/ravindu644/Droidspaces-OSS) — lightweight container runtime for rooted Android.
- [**HyperUnlocked**](https://github.com/ukriu/HyperUnlocked) — unlock high-end Xiaomi features on more devices.
- [**BRENE**](https://github.com/rrr333nnn333/BRENE) — KernelSU module bundling SUSFS support and other tweaks.
- [**Awesome Android Root**](https://github.com/awesome-android-root/awesome-android-root) — the sibling list: root apps, modules, and guides across the whole scene. Worth a look if you root for reasons other than KernelSU.

## Device Kernels

Prebuilt kernels save you from compiling. **Verify the exact model, Android version, kernel version, and security-patch level before flashing.**

> For anything not listed here, check the maintained community list of [KernelSU-Next unofficially supported devices](https://kernelsu-next.github.io/webpage/pages/devices.html), the [XDA KSU tag](https://xdaforums.com/tags/ksu/), or GitHub topic search.

| Project | Devices | Notes | Release |
|---|---|---|---|
| [WildKernels GKI](https://github.com/WildKernels/GKI_KernelSU_SUSFS) | GKI 2.0 (5.10+) | KernelSU + SUSFS | [![Release](https://img.shields.io/github/v/release/WildKernels/GKI_KernelSU_SUSFS?style=flat-square)](https://github.com/WildKernels/GKI_KernelSU_SUSFS/releases) |
| [WildKernels OnePlus](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) | OnePlus | KernelSU + SUSFS | [![Release](https://img.shields.io/github/v/release/WildKernels/OnePlus_KernelSU_SUSFS?style=flat-square)](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS/releases) |
| [WildKernels Samsung](https://github.com/WildKernels/Samsung_KernelSU_SUSFS) | Samsung | KernelSU + SUSFS | [![Release](https://img.shields.io/github/v/release/WildKernels/Samsung_KernelSU_SUSFS?style=flat-square)](https://github.com/WildKernels/Samsung_KernelSU_SUSFS/releases) |
| [WildKernels Sultan](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) | Google Pixel | Sultan base + SUSFS | [![Release](https://img.shields.io/github/v/release/WildKernels/Sultan_KernelSU_SUSFS?style=flat-square)](https://github.com/WildKernels/Sultan_KernelSU_SUSFS/releases) |
| [Action-Build](https://github.com/Numbersf/Action-Build) | OnePlus, QCOM and MTK | CI builds for SukiSU-Ultra, KernelSU, KernelSU-Next, and BakaSU | [![Release](https://img.shields.io/github/v/release/Numbersf/Action-Build?style=flat-square)](https://github.com/Numbersf/Action-Build/releases) |
| [NonGKI_Kernel_Build_2nd](https://github.com/JackA1ltman/NonGKI_Kernel_Build_2nd) | Non-GKI devices | Non-GKI kernels with KSU and SUSFS | [![Release](https://img.shields.io/github/v/release/JackA1ltman/NonGKI_Kernel_Build_2nd?style=flat-square)](https://github.com/JackA1ltman/NonGKI_Kernel_Build_2nd/releases) |
| [GKID-Kernels](https://github.com/ahmed-alnassif/GKID-Kernels) | GKI 2.0 | KernelSU/ReSukiSU + SUSFS, baseband guard | [![Release](https://img.shields.io/github/v/release/ahmed-alnassif/GKID-Kernels?style=flat-square)](https://github.com/ahmed-alnassif/GKID-Kernels/releases) |
| [YuzakiKokuban](https://github.com/YuzakiKokuban) | Galaxy S23 / S24 / S25, Tab S10, Xiaomi | Samsung kernel sources built from Samsung's open source, with KernelSU + hybrid mount + SUSFS | [![Last commit](https://img.shields.io/github/last-commit/YuzakiKokuban/android_kernel_samsung_sm8750?style=flat-square)](https://github.com/YuzakiKokuban/android_kernel_samsung_sm8750) |
| [kernel_msm-5.15](https://github.com/topnotchfreaks/kernel_msm-5.15) | Redmi Note 12/13 4G, Redmi Pad SE | SukiSU-Ultra, KPM, and SUSFS variants | [![Release](https://img.shields.io/github/v/release/topnotchfreaks/kernel_msm-5.15?style=flat-square)](https://github.com/topnotchfreaks/kernel_msm-5.15/releases) |
| [KernelSU_LKM_For_Oneplus12](https://github.com/snowwolf725/KernelSU_LKM_For_Oneplus12) | OnePlus 12 | LKM for OxygenOS/ColorOS | [![Release](https://img.shields.io/github/v/release/snowwolf725/KernelSU_LKM_For_Oneplus12?style=flat-square)](https://github.com/snowwolf725/KernelSU_LKM_For_Oneplus12/releases) |
| [s10plus-snapdragon-droidspaces-kernel](https://github.com/tingao/s10plus-snapdragon-droidspaces-kernel) | Galaxy S10+ Snapdragon (SM-G9750) | Non-GKI 4.14 with KernelSU-Next built in (manual hooks) and Droidspaces container support | [![Release](https://img.shields.io/github/v/release/tingao/s10plus-snapdragon-droidspaces-kernel?style=flat-square)](https://github.com/tingao/s10plus-snapdragon-droidspaces-kernel/releases) |
| [saipan-droidspaces-kernel](https://github.com/tingao/saipan-droidspaces-kernel) | moto g(50) 5G (XT2149-1) | Non-GKI 4.14 with KernelSU-Next (legacy branch), vendor-module CRC tolerance, and Droidspaces container support | [![Release](https://img.shields.io/github/v/release/tingao/saipan-droidspaces-kernel?style=flat-square)](https://github.com/tingao/saipan-droidspaces-kernel/releases) |
| [galaxy-s21-kernel-droidspaces](https://github.com/tingao/galaxy-s21-kernel-droidspaces) | Galaxy S21 5G (SM-G9910) | Non-GKI 5.4 with KernelSU-Next (legacy branch) and Droidspaces container support | [![Last commit](https://img.shields.io/github/last-commit/tingao/galaxy-s21-kernel-droidspaces?style=flat-square)](https://github.com/tingao/galaxy-s21-kernel-droidspaces) |

**Kernel selection checklist:** exact device match · matching Android and kernel version · security-patch level (anti-rollback can brick on an older patch) · active maintenance · a copy of your stock `boot.img` for recovery.

## Building from Source

- **Official KernelSU:** build an LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk). The GKI and non-GKI build guides are archival — [How to build](https://kernelsu.org/guide/how-to-build.html) · [Integrate for non-GKI](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html).
- **Forks** (KernelSU-Next, SukiSU-Ultra, BakaSU) still support direct kernel integration — see each repository's `kernel/setup.sh`.
- **Packaging and CI:** [AnyKernel3](https://github.com/osm0sis/AnyKernel3) · [kernel_build_action](https://github.com/dabao1955/kernel_build_action) · [KernelSU_Action](https://github.com/xiaoleGun/KernelSU_Action).
- **Vendor kernel sources:** [Google](https://android.googlesource.com/kernel/) · [Xiaomi](https://github.com/MiCode/Xiaomi_Kernel_OpenSource) · [OnePlus](https://github.com/OnePlusOSS) · [Motorola](https://github.com/MotorolaMobilityLLC) · [Samsung](https://opensource.samsung.com).
- **Writing a module:** [Module guide](https://kernelsu.org/guide/module.html) · [WebUI](https://kernelsu.org/guide/module-webui.html) · [configuration API](https://kernelsu.org/guide/module-config.html) · [Difference with Magisk](https://kernelsu.org/guide/difference-with-magisk.html).

## Documentation

- [What is KernelSU?](https://kernelsu.org/guide/what-is-kernelsu.html)
- [Installation](https://kernelsu.org/guide/installation.html)
- [Metamodules](https://kernelsu.org/guide/metamodule.html)
- [Module guide](https://kernelsu.org/guide/module.html) · [Module WebUI](https://kernelsu.org/guide/module-webui.html) · [Module configuration](https://kernelsu.org/guide/module-config.html)
- [App Profile](https://kernelsu.org/guide/app-profile.html)
- [Difference with Magisk](https://kernelsu.org/guide/difference-with-magisk.html)
- [Unofficially supported devices](https://kernelsu.org/guide/unofficially-support-devices.html)
- [FAQ](https://kernelsu.org/guide/faq.html) · [Rescue from bootloop](https://kernelsu.org/guide/rescue-from-bootloop.html)
- [KernelSU Modules developer docs](https://developers.kernelsu.org/docs/)
- [Awesome Android Root guides](https://awesome-android-root.xyz/rooting-guides/) — the sibling site's rooting guides, including [KernelSU](https://awesome-android-root.xyz/rooting-guides/kernelsu-guide), [SUSFS](https://awesome-android-root.xyz/rooting-guides/susfs-guide), and [root framework comparison](https://awesome-android-root.xyz/rooting-guides/root-framework-comparison)

## Community

**Telegram**

- [@KernelSU](https://t.me/KernelSU) — official announcements channel.
- [@KernelSU_group](https://t.me/KernelSU_group) — official community group.
- [@Sukiksu](https://t.me/Sukiksu) — SukiSU-Ultra channel.
- [@BAKASU_grp](https://t.me/BAKASU_grp) — BakaSU group (the former ReSukiSU group).
- [@YukiSU](https://t.me/YukiSU) — YukiSU contact channel.
- [@ksunext](https://t.me/ksunext) — KernelSU-Next community group.
- [@ksunext_ci](https://t.me/ksunext_ci) — KernelSU-Next CI and build announcements channel.

> [!NOTE]
> KOWSU publishes through GitHub and its own build channel rather than a Telegram group.

**Other**

- [GitHub Discussions](https://github.com/tiann/KernelSU/discussions) · [Issue tracker](https://github.com/tiann/KernelSU/issues)
- [r/KernelSU](https://www.reddit.com/r/KernelSU/) on Reddit
- [XDA Developers — KernelSU tag](https://xdaforums.com/tags/ksu/)

## Troubleshooting

> [!NOTE]
> Keep a stock boot image backup before you start. It is the only reliable way back from a bootloop.

### Common issues

| Issue | Likely cause | Fix |
|---|---|---|
| **Bootloop** | Incompatible kernel or module | Flash the stock `boot.img`; disable modules through safe mode |
| **App crashes** | SELinux policy conflict | Adjust the app profile's SELinux rules |
| **Module not working** | No metamodule installed on a 3.0+ install | Install a metamodule and reboot |
| **Root not detected** | Manager not installed, or version mismatch | Reinstall the Manager, check the reported kernel version |
| **Play Integrity failing** | Root detected | SUSFS plus a hiding module, and verify the verdict with a tester |
| **Update failed** | Storage space or a corrupt download | Clear the cache and re-download |
| **Banking app broken** | Root detected | Tighten the app profile and configure hiding |
| **System unstable** | Conflicting modules | Disable modules one at a time |

### Emergency recovery

> [!WARNING]
> If the device is in a bootloop, restore it immediately.

<details>
<summary><b>Bootloop recovery</b></summary>

```bash
# 1. Enter fastboot (Power + Volume Down), then connect the device
# 2. Flash the stock boot image
fastboot flash boot stock_boot.img

# 3. If needed, clear the cache
fastboot erase cache

# 4. Reboot
fastboot reboot
```

**From recovery:** boot TWRP or another custom recovery, flash the stock boot image, wipe cache and Dalvik, reboot.

**KernelSU's own safe mode:** press Volume Down three times (press-release, press-release, press-release) after the first boot screen. All modules are disabled, and you can still uninstall them from the Manager.

**From ADB, with a root shell:**

```bash
ksud module list
ksud module disable <id>
ksud module uninstall <id>
reboot
```

**If nothing boots:** boot a recovery, mount `data`, remove `/data/adb/ksud`, and remove `/metadata/ksu/modules.rc` and `/metadata/watchdog/ksu/modules.rc`. KernelSU then loads no modules at all.

**Prevention:** always keep the stock boot image, test with `fastboot boot test_boot.img` first, and make a TWRP backup before large changes.

</details>

### Debugging commands

<details>
<summary><b>Diagnostics</b></summary>

```bash
# KernelSU status
cat /proc/version | grep -i kernelsu
su -c "ksud --version"

# Kernel and SELinux
uname -r
getenforce
cat /proc/filesystems | grep overlay

# Module state
su -c "ksud module list"
ls -la /data/adb/modules/
cat /data/adb/modules/*/module.prop
cat /data/adb/modules/*/install.log

# Mount points
mount | grep overlay
mount | grep -E "/system|/product"

# Logs
dmesg > /sdcard/dmesg.log
logcat -s KernelSU > /sdcard/kernelsu.log
cat /proc/last_kmsg > /sdcard/last_kmsg.log

# Verify root
su -c "id"
```

</details>

### Device-specific notes

<details>
<summary><b>Samsung</b></summary>

- Unlocking the bootloader trips the Knox warranty bit permanently.
- LKM cannot run on Knox-locked devices — GKI mode is the only route.
- Some kernels are incompatible with Samsung's encryption; keep the stock image close.
- OEM unlocking must be enabled in Developer Options.

</details>

<details>
<summary><b>OnePlus</b></summary>

- Unlock with `fastboot oem unlock`.
- OnePlus devices generally do not boot generic GKI images — use a device-specific kernel.
- Anti-rollback makes older security-patch kernels a brick risk.
- A/B slot devices need deliberate slot handling, especially with OTA updates.

</details>

<details>
<summary><b>Xiaomi</b></summary>

- Mi Unlock requires an account and a waiting period.
- HyperOS/MIUI features sometimes conflict with KernelSU.
- Downgrading MIUI versions risks a brick.
- The vendor version must match the kernel you flash.

</details>

<details>
<summary><b>Google Pixel</b></summary>

- Titan M and hardware attestation make root hiding harder on recent Pixels.
- An orange verified-boot state after flashing is expected.
- KernelSU re-roots cleanly after an OTA with LKM.

</details>

### Performance and app compatibility

<details>
<summary><b>Performance</b></summary>

**System feels slow**

1. Disable modules one at a time to find the culprit.
2. Check thermal throttling and CPU frequency scaling.
3. OverlayFS on slow storage adds I/O overhead; a mountless metamodule avoids it.
4. Read `dmesg` and `logcat` for kernel errors.

```bash
top -m 10
iostat -x 1 10
cat /sys/class/thermal/thermal_zone*/temp
dmesg | grep -i error
```

**Random reboots**

1. Read `dmesg` and `/proc/last_kmsg`.
2. Look for the OOM killer in the logs.
3. Stress-test the hardware without KernelSU loaded.
4. Test with no modules installed.

</details>

<details>
<summary><b>Banking and gaming</b></summary>

**Banking and payment apps**

1. Restrict root per app with app profiles.
2. Install a hiding stack: SUSFS (LKM or patched kernel) plus Zygisk Assistant.
3. Check the verdict with a Play Integrity tester rather than assuming.
4. Remember that hardware attestation cannot be spoofed by any module.

```bash
# 1. Install the hiding modules
# 2. Configure the app profile to deny root
# 3. Reboot and test
```

**Games with anti-cheat**

- Some titles detect root and ban accounts.
- Deny root to the game through its app profile, and keep the game out of any hiding exceptions.
- Use a separate profile or a non-rooted device for competitive play.

</details>

### Getting help

<details>
<summary><b>What to include in a report</b></summary>

1. **Device**: model, Android version, kernel version.
2. **Variant and version**: which fork, and which release.
3. **Installation method**: LKM or GKI, and which partition was patched.
4. **Metamodule**: which one is installed.
5. **Reproduction**: exact steps.
6. **Logs**: `dmesg`, `logcat`, and module install logs.
7. **Module list**: every installed module with its version.

```bash
#!/system/bin/sh
# Collect logs for a bug report

LOGDIR="/sdcard/ksu_logs_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$LOGDIR"

getprop > "$LOGDIR/system_props.txt"
uname -a > "$LOGDIR/kernel_info.txt"
cat /proc/version > "$LOGDIR/kernel_version.txt"

su -c "ksud --version" > "$LOGDIR/ksud_version.txt" 2>&1

dmesg > "$LOGDIR/dmesg.log"
logcat -d > "$LOGDIR/logcat.log"
cat /proc/last_kmsg > "$LOGDIR/last_kmsg.log" 2>/dev/null

ls -laR /data/adb/modules > "$LOGDIR/modules_list.txt"
cat /data/adb/modules/*/module.prop > "$LOGDIR/modules_props.txt" 2>/dev/null

mount > "$LOGDIR/mount_points.txt"
df -h > "$LOGDIR/disk_usage.txt"

echo "Logs collected in: $LOGDIR"
```

</details>

#### Where to ask

1. [kernelsu.org FAQ](https://kernelsu.org/guide/faq.html) and the official docs.
2. GitHub Discussions and the issue tracker of your variant.
3. The Telegram group for your variant.
4. [XDA forums](https://xdaforums.com/tags/ksu/) for device-specific threads.
5. [r/KernelSU](https://www.reddit.com/r/KernelSU/) for general questions.
6. [Awesome Android Root](https://awesome-android-root.xyz/) if the question is about rooting in general rather than KernelSU specifically.

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

## FAQs

### General

<details open>
<summary><b>What is a metamodule and why do I need one?</b></summary>

Since the 3.0 line, the built-in module mounting system was removed and a metamodule provides the mounting infrastructure instead.

**Why the change**

- **Less to detect** — KernelSU itself performs no mounts, so it exposes fewer signatures.
- **Choice** — the mounting strategy becomes a module you can replace.
- **Stability** — the core stays stable while mount implementations evolve.

**Quick start**

1. Download a metamodule ZIP — `meta-hybrid_mount` is listed in the [official registry](https://modules.kernelsu.org/), and the OverlayFS forks are linked above.
2. Install it from the Manager → Modules.
3. Reboot.

See [Metamodules](#metamodules).

</details>

<details>
<summary><b>How does KernelSU differ from Magisk?</b></summary>

| Aspect | KernelSU | Magisk |
|---|---|---|
| **Architecture** | Kernel-level | Userspace, ramdisk-based |
| **Root control** | Per-app profiles with UID, GID, capabilities, SELinux domain | DenyList |
| **Module system** | Metamodule-based (3.0+) | Magic Mount, built in |
| **Installation** | LKM or GKI | Boot image patching |
| **Compatibility** | Needs a matching kernel | Broad |
| **Zygisk** | External implementation required | Built in |

</details>

<details>
<summary><b>LKM or GKI?</b></summary>

**LKM** — keeps the stock kernel, upgrades in the app, survives OTA, touches only the ramdisk. Use it on phones.

**GKI** — universal across GKI devices, works on Knox-locked Samsung, independent of firmware. Use it on emulators, WSA, and Waydroid, or when a device-specific GKI image exists.

Official releases no longer ship GKI images, so a GKI install comes from a fork or a community builder.

</details>

<details>
<summary><b>Which variant should I use?</b></summary>

- **GKI device, modern phone, stability first** → official KernelSU
- **Kernel outside 5.10–6.18, or you want SUSFS without rebuilding** → KernelSU-Next
- **KPM modules, or a very old kernel** → SukiSU-Ultra
- **Manual hooks down to 3.4, or a second Manager** → BakaSU
- **Bundled Zygisk** → YukiSU or FinaSU

See [KernelSU Variants](#kernelsu-variants).

</details>

<details>
<summary><b>Is KernelSU safer than Magisk?</b></summary>

In several respects, yes:

- Root checks run in the kernel, so a userspace app cannot rewrite them.
- The app profile system grants partial root instead of all-or-nothing.
- The system partition stays untouched.
- seccomp and ioctl hooks shrink the detection surface.
- The metamodule architecture keeps mounting out of the core.

Both are safe when configured properly. Neither is invisible to a determined detector.

</details>

<details>
<summary><b>Can I use Magisk modules with KernelSU?</b></summary>

| Module type | Compatibility |
|---|---|
| **Simple modules** | Usually work unchanged, once a metamodule is installed |
| **Complex modules** | May need adaptation for the metamodule system |
| **Zygisk modules** | Need ZygiskNext, ReZygisk, or a similar implementation |
| **Hardware-specific** | Usually work |

KernelSU does not support Magisk's `.replace` mechanism. Delete a file with `mknod filename c 0 0` instead, or use the `REMOVE` and `REPLACE` variables. The `KSU=true` environment variable distinguishes the two environments in module scripts.

</details>

<details>
<summary><b>Will KernelSU break OTA updates?</b></summary>

Usually not. The system partition is untouched, and in LKM mode the Manager can install to the inactive slot before you reboot. A major Android upgrade sometimes needs a re-patch. Keep a backup of the patched image.

</details>

### Installation and setup

<details>
<summary><b>What changed in the 3.0 line?</b></summary>

1. **Module mounting left the core** — fresh installs need a metamodule, and existing installs have to reinstall their modules after upgrading.
2. **Official GKI image builds were dropped** — build an LKM with [Ylarod/ddk](https://github.com/Ylarod/ddk) instead. The GKI build guide is archival; forks still publish GKI images.
3. **An official module registry** — reviewed modules at [modules.kernelsu.org](https://modules.kernelsu.org/), now backed by the KernelSU Modules API.
4. **Magica jailbreak mode** — optional root escalation on a permissive-SELinux boot.
5. **More hiding** — SELinux hiding, a native kernel-module blacklist, and `shell_su_adb_only` for ADB-only shell root.

</details>

<details>
<summary><b>How do I check whether my device is supported?</b></summary>

```bash
adb shell uname -r
```

Then read the KMI out of the kernel string. `5.10.101-android12-9-...` means KMI `5.10-android12-9`; the sublevel is not part of the KMI. The Manager also tells you directly: `Not installed` means supported, `Unsupported` means you need to build the kernel.

</details>

<details>
<summary><b>Do I have to uninstall Magisk first?</b></summary>

Yes. Remove every Magisk module, uninstall Magisk, flash the stock boot image, then install KernelSU. The two patch the boot process differently and conflict.

</details>

<details>
<summary><b>What should I back up?</b></summary>

1. A full TWRP backup, if your device has a recovery.
2. The stock `boot.img` — and `init_boot.img` on Android 13+.
3. The list of your current modules.
4. App data, exported to local storage.

</details>

### Modules and features

<details>
<summary><b>Where do I find modules?</b></summary>

- [**Official registry**](https://modules.kernelsu.org/) — reviewed, and the one the Manager reads.
- [**MMRL**](https://github.com/MMRLApp/MMRL) and its repository collections.
- [**Awesome Android Root**](https://awesome-android-root.xyz/apps-and-modules/) — the wider scene.
- GitHub search, Telegram, and XDA for device-specific builds.

Fresh 3.0+ installs need a metamodule before any of them mount.

</details>

<details>
<summary><b>My modules stopped working after updating to 3.0+</b></summary>

Install a metamodule. The 3.0 release notes call it out explicitly: after upgrading, modules have to be reinstalled once a metamodule is present. See [Metamodules](#metamodules).

</details>

<details>
<summary><b>Can I switch metamodules?</b></summary>

Yes, one at a time:

1. Uninstall the regular modules.
2. Uninstall the current metamodule.
3. Reboot.
4. Install the new metamodule.
5. Reboot again.
6. Reinstall the regular modules.

</details>

<details>
<summary><b>What are app profiles?</b></summary>

App profiles define the root policy for a single app:

- Custom UID and GID, and supplementary groups
- Capability restrictions
- SELinux context and rules
- Mount namespace and unmount behaviour
- Reusable templates

Configure them per app in the Manager. Full details: [App Profile](https://kernelsu.org/guide/app-profile.html).

</details>

<details>
<summary><b>What is KPM?</b></summary>

KPM — Kernel Patch Module — runs code in kernel space with inline hooks and syscall-table hooks. It started in APatch and was ported to KernelSU by SukiSU-Ultra. It is no longer exclusive to SukiSU: [KPatch-Next](https://github.com/KernelSU-Next/KPatch-Next) provides a standalone implementation for Magisk and KernelSU.

</details>

<details>
<summary><b>Do I need to keep the kernel and Manager versions in sync?</b></summary>

Yes. The kernel and the Manager share an interface version, and a mismatched pair produces warnings and unstable behaviour. The Manager in the official release page matches the kernel in the same release.

</details>

### Troubleshooting

<details>
<summary><b>My device is in a bootloop</b></summary>

```bash
# 1. Enter fastboot (Power + Volume Down) and connect the device
# 2. Flash the stock boot image
fastboot flash boot stock_boot.img

# 3. Reboot
fastboot reboot
```

This is why the stock `boot.img` backup is not optional. Full procedures: [Rescue from bootloop](https://kernelsu.org/guide/rescue-from-bootloop.html).

</details>

<details>
<summary><b>Banking apps do not work</b></summary>

1. Install the hiding stack: SUSFS (LKM or patched kernel) and Zygisk Assistant.
2. Deny root to the banking app in its app profile.
3. Hide the Manager app.
4. Verify with a Play Integrity tester.

No module guarantees a passing verdict on hardware-attested devices.

</details>

<details>
<summary><b>How do I confirm KernelSU is working?</b></summary>

```bash
# Check the kernel
cat /proc/version | grep -i kernelsu

# Test root
su -c "id"
```

The Manager should also report an installed kernel and a matching version.

</details>

---

## Contributing

Contributions are welcome — new tools, modules, maintained device kernels, and documentation fixes. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Disclaimer

Rooting and kernel modification can void warranties, brick devices, and expose security vulnerabilities. This list is provided for **educational and informational purposes only** — you assume all risks.

KernelSU and its derivatives are independent, community-driven projects. They are not affiliated with or endorsed by Google, Android, or any device manufacturer.

### Legal and safety information

**Educational purpose only.** Users are solely responsible for understanding and complying with local laws, following device warranty terms, maintaining device security, and understanding the consequences of modifying a device.

**No warranty or liability.** Contributors and maintainers are **not liable** for device damage or bricking, data loss or corruption, warranty violations, legal consequences, or security vulnerabilities.

### Safety best practices

<details>
<summary><b>Guidelines</b></summary>

**Always do**

| Action | Why it matters |
|---|---|
| ✅ **Create complete backups** | Essential for recovery |
| ✅ **Read the documentation thoroughly** | Understand before acting |
| ✅ **Test on a device you can replace** | Avoid daily-driver risk |
| ✅ **Keep stock firmware** | Emergency recovery option |
| ✅ **Check device-specific issues** | Know your device's limits |
| ✅ **Understand the security implications** | Protect your data |

**Never do**

| Action | Risk |
|---|---|
| ❌ **Proceed without backups** | Irreversible data loss |
| ❌ **Grant root to untrusted apps** | Security compromise |
| ❌ **Install unknown modules** | Malware or instability |
| ❌ **Ignore security warnings** | Serious vulnerabilities |
| ❌ **Modify without understanding** | System damage |

</details><br>

> [!IMPORTANT]
> KernelSU and its derivatives are **independent, community-driven projects**. They are not affiliated with, endorsed by, or connected to Google, Android, device manufacturers, or any other commercial entity.

---

## License

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

**This project is licensed under the [MIT License](LICENSE).**

---

## Acknowledgments

**Special thanks to everyone who made KernelSU possible.**

**Project creators**

- [**tiann**](https://github.com/tiann) — creator of KernelSU, and the reason kernel-based root is practical on modern Android.
- [**topjohnwu**](https://github.com/topjohnwu) — Magisk creator, whose systemless model KernelSU inherits.

**Derivative maintainers**

- **KernelSU-Next** — wider kernel coverage, module backup, prebuilt SUSFS loaders.
- **SukiSU-Ultra** — KPM integration, legacy device support, and the deepest Manager feature set.
- **BakaSU** — minimal hooks and multi-manager support.
- **YukiSU and FinaSU** — bundled Zygisk engines and a different Manager direction.
- **KOWSU** — Material theming and translation coverage on top of upstream.
- **WildKernels** — the device kernel projects that continue after Wild KSU was archived.

**Community contributors**

- Module developers building the modules, metamodules, and hiding tools in the registry.
- Kernel maintainers shipping device-specific builds.
- Documentation translators and writers.
- Community moderators and support staff.
- Everyone who shares knowledge.

---

**Made with ❤️ by the KernelSU community**

<sub>Maintained by [Fynks](https://github.com/fynks)</sub>

<br>

**[⬆ Back to Top](#awesome-kernelsu)**

</div>
