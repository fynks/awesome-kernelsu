<div align="center">

<img src="./media/kernelsu-logo.svg" alt="KernelSU Logo" width="200"/>
<br>

# Awesome KernelSU

**A comprehensive curated list of KernelSU resources, tools, modules, and documentation**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/fynks/awesome-kernelsu?style=flat-square&logo=github)](https://github.com/fynks/awesome-kernelsu/stargazers)
[![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)
[![Last Updated](https://img.shields.io/badge/Updated-October%202025-brightgreen?style=flat-square)](https://github.com/fynks/awesome-kernelsu)

<br>

[Intro](#what-is-kernelsu) &nbsp; • &nbsp; [Prebuilt Kernels](#prebuilt-kernels) &nbsp; • &nbsp; [Docs](#-documentation) &nbsp; • &nbsp; [Community](#-community)


<br>

</div>


## What is KernelSU?

KernelSU is a **kernel-based root solution** for Android that delivers superior security and reliability compared to traditional rooting methods. By operating at the kernel level, it provides enhanced security isolation, maintains system integrity, and offers powerful module management through modern OverlayFS technology.

### Key Features

- **Zero System Modification**: Maintains system integrity and OTA compatibility by operating entirely within kernel space
- **Advanced Permission Control**: Granular app-level root access management with customizable profiles
- **Enhanced Security Model**: Kernel-level isolation prevents root detection and tampering
- **Modern Module System**: Efficient OverlayFS-based modifications with rollback capability
- **App Profile System**: Customizable groups, capabilities, and SELinux rules for fine-grained root privilege control


## Table of Contents

- [Quick Start](#quick-start)
- [KernelSU Variants](#kernelsu-variants)
- [Comparison](#comparison)
- [Premade Kernels](#premade-kernels)
- [Installation](#installation)
- [Official Resources](#official-resources)
- [Documentation](#documentation)
- [Development](#development)
- [Modules and Tools](#modules-and-tools)
- [Kernel Sources and Building](#kernel-sources-and-building)
- [Community](#community)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)

## Getting Started

### Prerequisites

Before installing KernelSU, ensure you have:
- **Unlocked bootloader** (required for all installation methods)
- **Complete data backup** (always backup before modifying your device)
- **ADB and Fastboot tools** installed on your computer
- **Compatible device** (check compatibility below)

> [!TIP]
> **New to bootloader unlocking?** Check out the comprehensive guide at [Awesome-Android-Root](https://awesome-android-root.org/android-root-guides/how-to-unlock-bootloader)

### New to KernelSU?

1. **Check Compatibility**
   - Kernel 5.10+ for official KernelSU (Android 12+)
   - Kernel 4.4-6.6 for KernelSU-Next (Android 9+)
   - Kernel 3.4-5.4+ for SuKiSu-Ultra (Android 7+)

2. **Download Manager**
   - Get the [official KernelSU Manager](https://github.com/tiann/KernelSU/releases/latest) for your variant

3. **Install KernelSU**
   - Follow the [installation guide](#installation) for your chosen method

4. **Verify Installation**
   - Open KernelSU Manager and confirm root status

### Device Selection Guide

| Device Age | Kernel Version  | Recommended Variant   | Primary Benefits                       |
| ---------- | --------------- | --------------------- | -------------------------------------- |
| 2021+      | 5.10+ (GKI 2.0) | **KernelSU Official** | Maximum stability, official support    |
| 2018-2021  | 4.4-6.6         | **KernelSU-Next**     | Enhanced features, broad compatibility |
| Pre-2018   | 3.4-5.4+        | **SuKiSu-Ultra**      | Legacy support, advanced hiding        |

### Essential First Steps

After successful installation:

1. **Configure App Profiles**: Set up [App Profiles](https://kernelsu.org/guide/app-profile.html) for granular root permission management
2. **Install Module Manager**: Use [MMRL](https://github.com/MMRLApp/MMRL) for easier module management
3. **Setup Root Hiding**: Install *SuSFS* module for banking/payment app compatibility
4. **Join Community**: Connect with [Telegram community](https://t.me/KernelSU_group) for support and updates
5. **Create Backup**: Make a backup of your patched boot image for recovery

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## KernelSU Variants

### Official KernelSU

[![GitHub](https://img.shields.io/badge/GitHub-tiann%2FKernelSU-blue?logo=github&style=flat-square)](https://github.com/tiann/KernelSU)
[![Documentation](https://img.shields.io/badge/Docs-kernelsu.org-green?style=flat-square)](https://kernelsu.org/)
[![Release](https://img.shields.io/github/v/release/tiann/KernelSU?style=flat-square)](https://github.com/tiann/KernelSU/releases)
[![Telegram](https://img.shields.io/badge/Telegram-KernelSU-blue?style=flat-square&logo=telegram)](https://t.me/KernelSU)

> The original and most stable KernelSU implementation for modern Android devices with GKI support.

<details open>
<summary><b>📋 View Details</b></summary>

**Best For:** Modern flagship devices (2021+) prioritizing stability and official support

**✨ Key Features:**
- Official GKI 2.0 support (kernel 5.10+)
- Battle-tested stability
- Regular security updates & maintenance
- Comprehensive official documentation
- Wide device compatibility for modern phones
- Active development by original author

**Technical Specs:**
- **Kernel Support:** 5.10+ (GKI 2.0), 4.14+ with manual compilation
- **Android Version:** 12+ (official), 10+ (community builds)
- **Architecture:** arm64-v8a, x86_64
- **Special Support:** WSA, ChromeOS, container-based Android

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/tiann/KernelSU/releases/latest)
- [📖 Official Documentation](https://kernelsu.org/)
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
- Extended kernel support (4.4-6.6, GKI & non-GKI)
- Dual module system (Magic Mount + OverlayFS with seamless toggle)
- Beautiful Material You UI with dynamic theming
- Advanced module management (backup/restore, bulk ops, dependencies)
- **Automatic update system** with rollback capability
- WebUI X framework for advanced module interfaces
- Built-in developer tools (logcat, performance monitor)
- Configurable OverlayFS options

**Technical Specs:**
- **Kernel Support:** 4.4 - 6.6 (Non-GKI & GKI)
- **Android Version:** 9+
- **Architecture:** arm64-v8a, armeabi-v7a, x86_64
- **Update Frequency:** Very active development with frequent updates

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/KernelSU-Next/KernelSU-Next/releases)
- [📖 Official Website](https://kernelsu-next.github.io/webpage/)
- [💬 Telegram Community](https://t.me/KernelSU_Next)
- [🐛 Report Issues](https://github.com/KernelSU-Next/KernelSU-Next/issues)

</details>

---

### SuKiSu-Ultra

[![GitHub](https://img.shields.io/badge/GitHub-SukiSU--Ultra-blue?logo=github&style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
[![Documentation](https://img.shields.io/badge/Docs-sukisu.org-green?style=flat-square)](https://sukisu.org/)
[![Release](https://img.shields.io/github/v/release/SukiSU-Ultra/SukiSU-Ultra?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
[![Telegram](https://img.shields.io/badge/Telegram-SukiKSU-blue?style=flat-square&logo=telegram)](https://t.me/SukiKSU)


> Specialized fork for legacy devices with advanced root hiding and broad compatibility.

<details>
<summary><b>📋 View Details</b></summary>

**Best For:** Legacy devices and users requiring advanced root hiding for banking apps

**✨ Unique Features:**
- Broad legacy kernel compatibility (3.4-5.4+) with extensive backports
- Built on Magic Mount technology for enhanced stability
- KPM (Kernel Patch Module) integration
- **SuSFS built-in** for superior root hiding
- Multi-architecture including 32-bit ARM support
- Enhanced manager with SuSFS management panel
- Legacy device optimizations
- Community-maintained device database

**Technical Specs:**
- **Kernel Support:** 3.4 - 5.4+ (Non-GKI focused)
- **Android Version:** 7+
- **Architecture:** arm64-v8a, armeabi-v7a, x86_64
- **Update Frequency:** Active community-driven development

**🔗 Resources:**
- [📥 Download Manager APK](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
- [📖 Official Website](https://sukisu.org/)
- [📚 Installation Guide](https://github.com/SukiSU-Ultra/SukiSU-Ultra/blob/main/docs/guide/installation.md)
- [💬 Telegram Group](https://t.me/SukiKSU)

</details>

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

### Compatibility Matrix

| Feature | Official KernelSU | KernelSU-Next | SuKiSu-Ultra |
|---------|-------------------|---------------|--------------|
| **Kernel Support** | 5.10+ (GKI 2.0) | 4.4 - 6.6 | 3.4 - 5.4+ |
| **Android Version** | 12+ | 9+ | 7+ |
| **Architecture** | arm64, x86_64 | arm64, arm, x86_64 | arm64, arm, x86_64 |
| **Module System** | OverlayFS | Dual (Magic Mount + OverlayFS) | Magic Mount + OverlayFS |
| **Auto Updates** | ❌ | ✅ | ❌ |
| **Root Hiding** | Basic | Advanced | SuSFS Built-in |
| **UI/UX** | Standard | Material You | Enhanced |
| **Legacy Support** | ❌ | ⚠️ Limited | ✅ Extensive |
| **Update Frequency** | Regular | Very Active | Community Active |
| **Best For** | Modern devices | Power users | Legacy devices |

### Which Variant Should You Choose?

<table>
<tr>
<td width="33%" valign="top">

**Choose Official KernelSU if:**

✅ Modern device (2021+)<br>
✅ GKI 2.0 support<br>
✅ Want maximum stability<br>
✅ Prefer official support<br>
✅ OTA compatibility priority

</td>
<td width="33%" valign="top">

**Choose KernelSU-Next if:**

✅ Kernel 4.4-6.6<br>
✅ Want latest features<br>
✅ Prefer modern UI<br>
✅ Auto-updates desired<br>
✅ Advanced module mgmt

</td>
<td width="33%" valign="top">

**Choose SuKiSu-Ultra if:**

✅ Legacy device<br>
✅ Kernel 3.x-5.4<br>
✅ Banking app hiding<br>
✅ Need KPM support<br>
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

| Feature                 | KernelSU        | KernelSU-Next           | SuKiSu-Ultra            | Magisk      | APatch       |
| ----------------------- | --------------- | ----------------------- | ----------------------- | ----------- | ------------ |
| **Architecture**        | Kernel-level    | Kernel-level            | Kernel-level            | Userspace   | Kernel-level |
| **Module System**       | OverlayFS       | OverlayFS + Magic Mount | Magic Mount + OverlayFS | Magic Mount | OverlayFS    |
| **Kernel Support**      | 5.10+ (GKI 2.0) | 4.4-6.6                 | 3.4-5.4+                | Any         | 3.18-6.1     |
| **Architecture**        | arm64, x86_64   | arm64, arm, x86_64      | arm64, arm, x86_64      | Universal   | arm64        |
| **Security Model**      | App Profile     | App Profile             | App Profile             | Root Toggle | SuperKey     |
| **Hide Capability**     | Basic           | Advanced                | SuSFS Integrated        | Deprecated  | Kernel-level |
| **Update Method**       | Manual          | Auto-update             | Manual                  | OTA         | Manual       |
| **System Modification** | Zero            | Zero                    | Zero                    | Minimal     | Zero         |
| **OTA Compatibility**   | Excellent       | Excellent               | Good                    | Good        | Excellent    |
| **Development Status**  | Active          | Very Active             | Active                  | Active      | Active       |
| **Learning Curve**      | Medium          | Medium                  | Hard                    | Easy        | Hard         |
| **Community Size**      | Growing         | Medium                  | Small                   | Large       | Small        |

### Advantages of KernelSU Ecosystem

<details>
<summary><b>✨ Click to expand: Detailed Advantages & Benefits</b></summary>

#### Security Benefits

1. **Kernel-Level Isolation**: Root access operates in kernel space, preventing userspace tampering
2. **App Profile System**: Granular per-application permission control with temporal restrictions
3. **Hardware-Level Protection**: Utilizes ARM TrustZone and hardware security features
4. **Verified Boot Compatible**: Maintains system integrity verification where possible
5. **Advanced Hiding**: Kernel-level hiding harder to detect than userspace methods

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
- Learning curve for new concepts
- Some Magisk-specific features unavailable

**Migration Steps:**
1. Backup all data and current setup
2. Document installed modules and configurations
3. Uninstall Magisk completely
4. Flash stock boot image
5. Install KernelSU using preferred method
6. Reinstall compatible modules
7. Configure app profiles

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

### Quick Navigation

**Jump to your device manufacturer:**
- [Official GKI](#-official-gki-builds)
- [WildKernels](#-wildkernels-multi-device)
- [Xiaomi](#-xiaomi-devices)
- [Samsung](#-samsung-devices)
- [OnePlus](#-oneplus-devices)
- [Motorola](#-motorola-devices)
- [Google Pixel](#-google-pixel-devices)
- [Huawei](#-huawei-devices)
- [LG](#-lg-devices)

---

### 🏆 Official GKI Builds

Official kernels from KernelSU project maintainers.

<table>
<tr>
<td width="50%">

**KernelSU Official GKI**

![Kernel](https://img.shields.io/badge/Kernel-5.10+-blue?style=flat-square)
![Android](https://img.shields.io/badge/Android-12+-green?style=flat-square)

Official GKI builds for modern devices with GKI 2.0 support

**📥 Download:** [KernelSU Releases](https://github.com/tiann/KernelSU/releases)

</td>
<td width="50%">

**KernelSU-Next Enhanced**

![Kernel](https://img.shields.io/badge/Kernel-4.4--6.6-blue?style=flat-square)
![Android](https://img.shields.io/badge/Android-9+-green?style=flat-square)

Enhanced builds with extended kernel support and extra features

**📥 Download:** [KernelSU-Next Releases](https://github.com/KernelSU-Next/KernelSU-Next/releases)

</td>
</tr>
</table>

---

### WildKernels (Multi-Device)

Premium quality kernels with KernelSU and SUSFS integration for multiple device families.

| Kernel Series | Target Devices | Features | Repository |
|---------------|----------------|----------|------------|
| **GKI Series** | Modern GKI Devices | KernelSU + SUSFS + GKI 2.0 | [![GitHub](https://img.shields.io/badge/View-Repository-blue?style=flat-square&logo=github)](https://github.com/WildKernels/GKI_KernelSU_SUSFS) |
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
| **Redmi Note 12/13 4G** | topaz/sapphire | 5.15 | SukiSU Ultra v3.2.0, KPM, SUSFS v1.5.11, Baseband-guard | [![GitHub](https://img.shields.io/badge/Download-ZEPHARO-blue?style=flat-square&logo=github)](https://github.com/topnotchfreaks/kernel_msm-5.15/releases/tag/ZEPHARO) |
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
| **Galaxy S10 / Note 10** | Exynos 9820 | 4.14 | KernelSU-Next, SuSFS v1.5.11, Ramdisk support | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/GoRhanHee/exynos9820_samsung_Kernel) |

#### Galaxy A Series

| Device Model | Codename | Kernel | Features | Links |
|--------------|----------|---------|----------|-------|
| **Galaxy A15 4G** | SM-A155F | 5.10 | KernelSU-Next 1.0.9, SuSFS 1.5.9 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/ReeViiS69/sm155f) |
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
| **OnePlus 13** | — | Latest | KernelSU-Next, SUSFS | OxygenOS | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/FerGus786/OnePlus_13_KernelSU_SUSFS) |
| **OnePlus 12** | — | Latest | KernelSU LKM mode | OxygenOS | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/snowwolf725/KernelSU_LKM_For_Oneplus12) |
| **OnePlus 7 Pro** | guacamole | Latest | KernelSU v0.9.5, Full system flash required | LineageOS 21 | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/surfaceocean/kernelsu_oneplus_7_pro_lineageos_guacamole) |
| **OnePlus Nord N200 5G** | dre | 5.4 | SukiSU Ultra | LineageOS 22+ | [![XDA](https://img.shields.io/badge/Download-XDA-orange?style=flat-square&logo=xda-developers)](https://xdaforums.com/t/kernel-aosp-lineageos-kernel-kernelsu-included.4749302/) |

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

</details>

---

### Huawei Devices

<details>
<summary><b>🔽 Click to expand Huawei device kernels</b></summary>

<br>

| Device Model | Codename | Kernel | Features | ROM Support | Links |
|--------------|----------|---------|----------|-------------|-------|
| **Huawei Nova 2** | — | 4.4 | KernelSU | LineageOS | [![GitHub](https://img.shields.io/badge/Download-blue?style=flat-square&logo=github)](https://github.com/CoolestEnoch/kernel-su-huawei-nova2) |

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
| **Features** | KernelSU version, SUSFS support, additional optimizations |
| **Maintenance** | Regular updates and active development |
| **Community** | User feedback on XDA, GitHub issues, Telegram |
| **Documentation** | Clear installation instructions and support |

> [!WARNING]
> **Before Flashing:** Always backup your current boot image. Keep a copy of stock boot.img for emergency recovery. Test with `fastboot boot kernel.img` first if possible.

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
> **Need help unlocking your bootloader?** Visit [Awesome-Android-Root Guide](https://awesome-android-root.org/android-root-guides/how-to-unlock-bootloader)

---

### 🚀 Installation Methods Overview

| Method | Difficulty | Best For | Requirements | Time |
|--------|-----------|----------|--------------|------|
| [**GKI Mode**](#method-1-gki-mode) | Easy | Modern devices (5.10+) | Fastboot, unlocked bootloader | 5-10 min |
| [**LKM Mode**](#method-2-lkm-mode) | Easy | Preserving stock kernel | Root or custom recovery | 5-10 min |
| [**Manager Patching**](#method-3-manager-patching) | Easy | One-click solution | Unlocked bootloader | 10-15 min |
| [**Custom Kernel**](#method-4-custom-kernels) | Medium | Device-specific optimization | TWRP or fastboot | 10-20 min |
| [**Manual Building**](#method-5-manual-building) | Hard | Full customization | Build environment, expertise | 1-3 hours |

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
```

</details>

---

### Method 2: LKM Mode

**Best for:** Users wanting to keep original kernel intact

<details>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ Preserves original kernel
- ✅ Less intrusive modification
- ✅ Easier to revert to stock

**Step-by-Step:**

1. Download LKM package for your kernel version
2. Install KernelSU Manager APK
3. In Manager, select "Install" → "LKM Mode"
4. Reboot device to activate

</details>

---

### Method 3: Manager Patching

**Best for:** Users preferring one-click solutions

<details>
<summary><b>📋 View Installation Steps</b></summary>

**Advantages:**
- ✅ User-friendly, minimal PC usage
- ✅ Automatic updates available
- ✅ Simplest for non-technical users

**Step-by-Step:**

1. Install KernelSU Manager APK on device
2. Grant necessary permissions
3. Select "Install" → Choose boot image or extract from ROM
4. Manager patches boot image automatically
5. Flash patched boot via fastboot or custom recovery

```bash
# Flash patched boot via fastboot
adb reboot bootloader
fastboot flash boot patched_boot.img
fastboot reboot
```

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

1. Find your device in [Prebuilt Kernels](#-prebuilt-kernels) section
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

| Kernel Version | Official KernelSU | KernelSU-Next | SuKiSu-Ultra | Recommended Method |
|----------------|-------------------|---------------|--------------|-------------------|
| 5.10+ (GKI 2.0) | ✅ Full Support | ✅ Full Support | ❌ Not Needed | GKI Mode / Manager Patching |
| 4.14 - 5.9 | ⚠️ Manual Build Only | ✅ Full Support | ✅ Full Support | Custom Kernel / LKM |
| 4.4 - 4.13 | ❌ Not Supported | ✅ Full Support | ✅ Full Support | Custom Kernel |
| 3.4 - 4.3 | ❌ Not Supported | ❌ Not Supported | ✅ Full Support | Custom Kernel |

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
```

**2. Install Manager**
- Download appropriate Manager APK
- Grant all required permissions
- Confirm root access in app

**3. Configure App Profiles**
- Set restrictive defaults
- Grant root only to trusted apps
- Configure time-based restrictions

**4. Install Essential Modules**
- SuSFS for root hiding
- Performance optimizations (optional)

> [!WARNING]
> Only install modules from trusted sources

**5. Setup Safety Features**
- Backup patched boot image
- Configure module backups
- Test SafetyNet/Play Integrity
- Document your setup


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
- [API Documentation](https://kernelsu.org/guide/module.html#kernelsu-modules)

</td>
<td width="50%" valign="top">

**Advanced Topics**
- [Security Model](https://kernelsu.org/guide/security.html)
- [OverlayFS System](https://kernelsu.org/guide/overlayfs.html)
- [SELinux Configuration](https://kernelsu.org/guide/selinux.html)
- [Debugging Guide](https://kernelsu.org/guide/debug.html)
- [Migration from Magisk](https://kernelsu.org/guide/migration.html)

</td>
</tr>
</table>

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
- [**Bootloop Recovery**](https://kernelsu.org/guide/rescue.html) - Emergency recovery procedures
- [**Log Analysis**](https://kernelsu.org/guide/logs.html) - Understanding system logs

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## Modules and Tools

**Essential modules and tools to enhance your KernelSU experience.**

### Root Management & Hiding

| Module | Purpose | Key Features |
|--------|---------|--------------|
| [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module) | Advanced root hiding | Customizable profiles, filesystem manipulation, banking app support |
| [**Shamiko**](https://github.com/LSPosed/LSPosed.github.io/releases) | DenyList bypass | Enhanced hiding, SafetyNet/Play Integrity bypass |
| [**Tricky Store**](https://github.com/5ec1cff/TrickyStore) | Key attestation bypass | Banking and payment app compatibility |

### System Optimization

| Module | Purpose | Benefits |
|--------|---------|----------|
| [**Universal GMS Doze**](https://github.com/gloeyisk/universal-gms-doze) | Battery optimization | Aggressive Google Play Services battery savings |

> [!TIP]
> **Discover More Modules:** Explore the extensive collection at **[Awesome Android Root - KernelSU Modules](https://awesome-android-root.org/android-root-apps/?filters=%5BK%5D)**

### Framework Modifications

| Framework | Purpose | Features |
|-----------|---------|----------|
| [**LSPosed**](https://github.com/LSPosed/LSPosed) | Xposed framework | Module support via Zygisk integration |
| [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext) | Standalone Zygisk | Independent Zygisk implementation |
| [**ReZygisk**](https://github.com/PerformanC/ReZygisk) | Transparent Zygisk | Improved Zygisk implementation |

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
- ✅ WebUI support for advanced modules
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
| [**SukiSU Manager**](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) | Manager for SuKiSu-Ultra | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases/latest) |
| [**Franco Kernel Manager**](https://play.google.com/store/apps/details?id=com.franco.kernel) | Kernel tweaking & monitoring | [![Play Store](https://img.shields.io/badge/Get-Play_Store-green?style=flat-square)](https://play.google.com/store/apps/details?id=com.franco.kernel) |
| [**SmartPack-Kernel Manager**](https://github.com/SmartPack/SmartPack-Kernel-Manager) | Open-source kernel management | [![Download](https://img.shields.io/badge/Download-Latest-blue?style=flat-square)](https://github.com/SmartPack/SmartPack-Kernel-Manager/releases) |

---

### 🛠️ Development & Debugging

| Tool | Purpose | Use Case |
|------|---------|----------|
| [**Root Checker**](https://play.google.com/store/apps/details?id=com.joeykrim.rootcheck) | Verify root status | Confirm successful installation |
| [**Logcat Reader**](https://github.com/darshanparajuli/LogcatReader) | System log viewer | Debugging and troubleshooting |
| [**Termux**](https://github.com/termux/termux-app) | Terminal emulator | Full Linux environment on Android |

<div align="right">

[⬆ Back to Top](#awesome-kernelsu)

</div>

---

## 🛠️ Building from Source

> [!NOTE]
> This section covers building KernelSU from source. For ready-to-use kernels, see the [Premade Kernels](#premade-kernels) section.

### Kernel Source Repositories

- [**KernelSU Source**](https://github.com/tiann/KernelSU) - Official KernelSU source code for integration
- [**KernelSU-Next Source**](https://github.com/KernelSU-Next/KernelSU-Next) - Enhanced fork with extended support
- [**Kernel Build Action**](https://github.com/dabao1955/kernel_build_action) - Automated building via GitHub Actions

### Device-Specific Kernel Sources

> [!TIP]
> Always use official kernel sources from your device manufacturer for best compatibility.

- [**OnePlus Kernel Sources**](https://github.com/OnePlusOSS) - Official OnePlus kernel sources
- [**Xiaomi Kernel Sources**](https://github.com/MiCode/Xiaomi_Kernel_OpenSource) - Official Xiaomi kernel sources
- [**Google AOSP Kernels**](https://android.googlesource.com/kernel/) - Android Open Source Project kernels
- [**Samsung Opensource**](https://opensource.samsung.com) - Samsung kernel sources

### Building Tools & Scripts

- [**Universal Patcher**](https://github.com/KernelSU-Next/KernelSU-Next/tree/next/scripts) - Automated kernel patching scripts
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

# 3. Configure kernel
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- <defconfig>

# 4. Enable KernelSU in config
./scripts/config --file .config -e CONFIG_KSU

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
- **x86_64**: Intel/AMD 64-bit (emulators, some tablets)
- **armeabi-v7a**: 32-bit ARM (legacy devices, SuKiSu-Ultra only)

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
| **SuKiSu** | Legacy devices | [![Telegram](https://img.shields.io/badge/Join-Group-blue?style=flat-square&logo=telegram)](https://t.me/Sukiksu) |

**GitHub**

| Platform | Purpose | Link |
|----------|---------|------|
| **Discussions** | Technical Q&A | [![GitHub](https://img.shields.io/badge/Join-Discussions-black?style=flat-square&logo=github)](https://github.com/tiann/KernelSU/discussions) |
| **Issues** | Bug reports | [![GitHub](https://img.shields.io/badge/Report-Issues-black?style=flat-square&logo=github)](https://github.com/tiann/KernelSU/issues) |
| **KSU-Next Discussions** | Enhanced fork | [![GitHub](https://img.shields.io/badge/Join-Discussions-black?style=flat-square&logo=github)](https://github.com/KernelSU-Next/KernelSU-Next/discussions) |


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
| **Module Not Working**       | Incompatible module version           | Verify module compatibility, check installation logs |
| **Root Not Detected**        | Manager not installed properly        | Reinstall KernelSU Manager, verify kernel version    |
| **SafetyNet Failing**        | Root detection                        | Install Shamiko or SuSFS, configure hiding properly  |
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
- **Color OS Migration**: Recent devices need special handling for OxygenOS vs ColorOS
- **Parallel Apps**: OxygenOS parallel apps may conflict with root
- **Slot System**: A/B partition devices need careful slot management

#### Xiaomi Devices
- **Anti-Rollback**: Be careful with MIUI version downgrades (brick risk)
- **Bootloader Unlock**: Xiaomi requires waiting period (up to 168 hours)
- **MIUI Optimizations**: Some MIUI features conflict with KernelSU
- **Vendor Mismatch**: Ensure kernel matches vendor version

#### Google Pixel Devices
- **Hardware Attestation**: Strong SafetyNet enforcement on newer Pixels
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

**Prevention:**
- Avoid aggressive kernel tweaks
- Monitor temperature during stress tests
- Ensure adequate RAM for modules
- Use stable kernel versions

</details>

### App Compatibility

<details>
<summary><b>🏦 Click to expand: Banking & Gaming App Compatibility</b></summary>

#### Banking/Payment Apps

**Solutions:**
1. **Configure app profiles**: Restrict root access for sensitive apps
2. **Enable advanced hiding**: Install SuSFS or Shamiko modules
3. **Check SafetyNet**: Use YASNAC or Play Integrity API tester
4. **Hardware attestation**: Some devices use hardware-based detection (harder to bypass)

**Recommended Setup:**
```bash
# Install hiding modules
# 1. Install Shamiko module
# 2. Install SuSFS4KSU module
# 3. Configure DenyList in manager
# 4. Reboot device
# 5. Test with SafetyNet checker
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
2. **KernelSU Variant**: Official, Next, or SuKiSu-Ultra + version number
3. **Installation Method**: How you installed KernelSU
4. **Reproduction Steps**: Detailed steps to reproduce the issue
5. **Logs**: Relevant log files (dmesg, logcat, module logs)
6. **Module List**: All installed modules and versions

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
<summary><b>What is KernelSU and how does it differ from Magisk?</b></summary>

KernelSU is a **kernel-based root solution** operating in kernel space, while Magisk operates in userspace.

**Key Differences:**

| Aspect | KernelSU | Magisk |
|--------|----------|--------|
| **Architecture** | Kernel-level | Userspace |
| **Security** | Superior isolation | Good but less isolated |
| **Module System** | OverlayFS | Magic Mount |
| **Compatibility** | Requires compatible kernel | Universal |
| **Future-proof** | Built for modern Android | Legacy support focus |

</details>

<details>
<summary><b>Which KernelSU variant should I use?</b></summary>

**Quick Selection Guide:**

- **Modern devices** (Android 12+, kernel 5.10+) → **Official KernelSU**
- **Mid-range devices** (Android 9-11, kernel 4.4-6.6) → **KernelSU-Next**
- **Legacy devices** (Android 7-8, kernel 3.4-5.4) → **SuKiSu-Ultra**

See [KernelSU Variants](#-kernelsu-variants) for detailed comparison.

</details>

<details>
<summary><b>Is KernelSU safer than Magisk?</b></summary>

**Yes, in several ways:**

- ✅ Kernel-level operation prevents userspace attacks
- ✅ App Profile system for granular permission control
- ✅ Zero system modification maintains integrity
- ✅ Hardware security integration (ARM TrustZone)
- ✅ Advanced kernel-level hiding

However, both are safe when properly configured.

</details>

<details>
<summary><b>Can I use Magisk modules with KernelSU?</b></summary>

**Compatibility varies:**

| Module Type | Compatibility |
|-------------|---------------|
| **Simple modules** | ✅ Most work without changes |
| **Complex modules** | ⚠️ May need OverlayFS adaptation |
| **Zygisk modules** | ⚠️ Require ZygiskNext or ReZygisk |
| **Hardware-specific** | ✅ Usually compatible |

</details>

<details>
<summary><b>Will KernelSU break OTA updates?</b></summary>

**Generally no:**

- ✅ System partition remains unmodified
- ⚠️ Boot partition may need re-patching after OTA
- ✅ Some variants have OTA survival features
- ⚠️ Manual re-installation may be required for major updates

Always keep your patched boot image backup!

</details>

---

### Installation & Setup

<details>
<summary><b>How do I check if my device is compatible?</b></summary>

**Check your kernel version:**

```bash
# Via ADB
adb shell uname -r

# On device terminal
uname -r
```

Then refer to the [Compatibility Matrix](#-comparison-matrix) to find the right variant.

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
- [**Awesome Android Root**](https://awesome-android-root.org/android-root-apps/?filters=%5BK%5D) - Curated collection
- **GitHub** - Search "kernelsu module"
- **Telegram** - Community-shared modules
- **XDA Forums** - Device-specific modules

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
5. Test with SafetyNet checker

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

<details>
<summary><b>Modules aren't loading, what's wrong?</b></summary>

**Common causes:**

- ❌ Incompatible module version
- ❌ Insufficient permissions
- ❌ Module conflicts
- ❌ OverlayFS not supported

**Check logs:** `/data/adb/modules/[module]/install.log`

</details>

---

### Development

<details>
<summary><b>How do I build KernelSU for my device?</b></summary>

**Quick steps:**

1. Setup Linux build environment
2. Clone kernel source
3. Apply KernelSU patches
4. Configure kernel (enable CONFIG_KSU)
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

- 📚 [Official FAQ](https://kernelsu.org/guide/faq.html)
- 💬 [Telegram Community](https://t.me/KernelSU_group)
- 🐙 [GitHub Discussions](https://github.com/tiann/KernelSU/discussions)
- 🌐 [XDA Forums](https://forum.xda-developers.com/t/kernelsu-a-kernel-based-root-solution-for-android.4511259/)

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
- **SuKiSu-Ultra Team** - Legacy device support and compatibility


**Community Contributors**

- Module developers creating useful tools
- Documentation translators and writers
- Community moderators and support staff
- Everyone who shares knowledge

**Special Recognition**

- All kernel developers maintaining device-specific builds
- Community members providing support
- Contributors to this awesome list

</td>
</tr>
</table>

---

<div align="center">

[![Star History Chart](https://api.star-history.com/svg?repos=fynks/awesome-kernelsu&type=Date)](https://star-history.com/#fynks/awesome-kernelsu&Date)

---

**Made with ❤️ by the KernelSU Community**

<sub>Last Updated: October 2025 | Maintained by [Fynks](https://github.com/fynks)</sub>

<br>

**[⬆ Back to Top](#awesome-kernelsu)**

</div>