<div align="center">

<img src="./media/kernelsu-logo.svg" alt="KernelSU Logo" width="200"/>
<br>

# Awesome KernelSU

**A comprehensive curated list of KernelSU resources, tools, modules, and documentation**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/fynks/awesome-kernelsu?style=flat-square&logo=github)](https://github.com/fynks/awesome-kernelsu/stargazers)
[![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)


[Intro](#about-kernelsu) &nbsp; • &nbsp; [Comparison](#comparison) &nbsp; • &nbsp; [Docs](#documentation) &nbsp; • &nbsp; [Community](#community)

---

</div>

## About KernelSU

KernelSU is a kernel-based root solution for Android that provides superior security and reliability compared to traditional rooting methods. Operating at the kernel level, it offers enhanced security isolation, system integrity protection, and powerful module management capabilities through OverlayFS.

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

## Quick Start

### Prerequisites

Before installing KernelSU, ensure you have:
- **Unlocked bootloader** (required for all installation methods)
- **Complete data backup** (always backup before modifying your device)
- **ADB and Fastboot tools** installed on your computer
- **Compatible device** (check compatibility below)

> [!TIP]
> You can use **Awesome-Android-Root Guides** for unlocking bootloaders: [Unlock Bootloader Guide](https://awesome-android-root.org/android-root-guides/how-to-unlock-bootloader)

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

The original and official KernelSU implementation, designed for modern Android devices with GKI (Generic Kernel Image) support.

**Key Features:**
- Official GKI 2.0 support (kernel 5.10+)
- Stable and thoroughly tested
- Regular security updates
- Comprehensive official documentation
- Wide device compatibility for modern phones
- Active development and support

**Supported:**
- **Kernel Version**: 5.10+ (GKI 2.0), 4.14+ with manual compilation
- **Android Version**: 12+ (officially), 10+ (unofficially)
- **Architecture**: arm64-v8a, x86_64
- **Devices**: WSA, ChromeOS, container-based Android

**Links:**
- [Official Repository](https://github.com/tiann/KernelSU)
- [Official Website](https://kernelsu.org/)
- [Latest Releases](https://github.com/tiann/KernelSU/releases)
- [Manager APK](https://github.com/tiann/KernelSU/releases/latest)
- [Telegram Channel](https://t.me/KernelSU)

---

### KernelSU-Next

[![GitHub](https://img.shields.io/badge/GitHub-KernelSU--Next-blue?logo=github&style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next)
[![Documentation](https://img.shields.io/badge/Docs-kernelsu--next.github.io-green?style=flat-square)](https://kernelsu-next.github.io/webpage/)
[![Release](https://img.shields.io/github/v/release/KernelSU-Next/KernelSU-Next?style=flat-square)](https://github.com/KernelSU-Next/KernelSU-Next/releases)

An enhanced fork of KernelSU with extended kernel support, additional features, and improved user experience.

**Enhanced Features:**
- Extended kernel support (4.4-6.6, both GKI and non-GKI)
- Dual module system (Magic Mount + OverlayFS with seamless toggle)
- Enhanced Material You UI with dynamic theming
- Advanced module management (backup/restore, bulk operations, dependency handling)
- Automatic update system with rollback capability
- WebUI X framework for advanced module interfaces
- Built-in developer tools (logcat viewer, performance monitor)
- Custom OverlayFS options (configurable image size, compression, mount strategies)

**Supported:**
- **Kernel Version**: 4.4-6.6 (Non-GKI & GKI)
- **Android Version**: 9+
- **Architecture**: arm64-v8a, armeabi-v7a, x86_64
- **Update Frequency**: Very active development

**Links:**
- [Repository](https://github.com/KernelSU-Next/KernelSU-Next)
- [Official Website](https://kernelsu-next.github.io/webpage/)
- [Latest Release](https://github.com/KernelSU-Next/KernelSU-Next/releases)
- [Telegram Community](https://t.me/KernelSU_Next)

---

### SuKiSu-Ultra

[![GitHub](https://img.shields.io/badge/GitHub-SukiSU--Ultra-blue?logo=github&style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
[![Documentation](https://img.shields.io/badge/Docs-sukisu.org-green?style=flat-square)](https://sukisu.org/)
[![Release](https://img.shields.io/github/v/release/SukiSU-Ultra/SukiSU-Ultra?style=flat-square)](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)

A KernelSU fork optimized for legacy devices with advanced root hiding capabilities and broad kernel compatibility.

**Unique Features:**
- Broad legacy kernel compatibility (3.4-5.4+) with extensive backports
- Built on Magic Mount technology from 5ec1cff for enhanced stability
- KPM (Kernel Patch Module) integration for advanced kernel modifications
- SuSFS built-in for advanced root hiding with customizable profiles
- Multi-architecture support including 32-bit ARM
- Enhanced manager with dark/light themes and SuSFS management panel
- Legacy device focus with optimizations for older Android versions
- Extensive device support with community-maintained database

**Supported:**
- **Kernel Version**: 3.4-5.4+ (Non-GKI focused)
- **Android Version**: 7+
- **Architecture**: arm64-v8a, armeabi-v7a, x86_64
- **Update Frequency**: Active community development

**Links:**
- [Repository](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
- [Official Website](httcps://sukisu.org/)
- [Latest Release](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases)
- [Official Telegram Group](https://t.me/SukiKSU)
- [Guide](https://github.com/SukiSU-Ultra/SukiSU-Ultra/blob/main/docs/guide/installation.md)

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

### Compatibility Matrix

| Variant               | Kernel Support  | Android | Architecture       | Primary Use Case                       | Update Frequency |
| --------------------- | --------------- | ------- | ------------------ | -------------------------------------- | ---------------- |
| **KernelSU Official** | 5.10+ (GKI 2.0) | 12+     | arm64, x86_64      | Modern devices, maximum stability      | Regular          |
| **KernelSU-Next**     | 4.4-6.6         | 9+      | arm64, arm, x86_64 | Enhanced features, broad compatibility | Very Active      |
| **SuKiSu-Ultra**      | 3.4-5.4+        | 7+      | arm64, arm, x86_64 | Legacy devices, advanced hiding        | Community Active |

### Selection Guide

**Choose Official KernelSU if:**
- You have a modern device (2021+) with GKI 2.0
- Stability and official support are top priorities
- You prefer established, well-tested solutions
- OTA compatibility is essential

**Choose KernelSU-Next if:**
- You want enhanced features and better UI
- Your device has kernel 4.4-6.6 support
- You value active development and innovation
- Auto-updates and advanced module management appeal to you
- You need both Magic Mount and OverlayFS options

**Choose SuKiSu-Ultra if:**
- You have an older device with kernel 3.x-5.4
- Advanced root hiding is critical (banking apps, etc.)
- You need KPM support for kernel modifications
- Legacy device optimization is important
- You require 32-bit ARM support

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

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


## Premade Kernels

Pre-built kernels with KernelSU integration save you from manual compilation and are optimized for specific devices.

> [!IMPORTANT]
> Always verify kernel compatibility with your specific device model and Android version before flashing. Flashing an incompatible kernel can result in bootloop or device damage.

### Official Builds

- [**KernelSU GKI Kernels**](https://github.com/tiann/KernelSU/releases) - Official GKI builds for modern devices (5.10+)
- [**KernelSU-Next Kernels**](https://github.com/KernelSU-Next/KernelSU-Next/releases) - Enhanced builds with extended kernel support (4.4-6.6)

### Community Kernels

#### WildKernels

High-quality kernels with KernelSU and SUSFS integration for various device families:

| 🚀 **Kernel** | 📱 **Device Support** | 🔗 **Repository** |
|:-------------:|:---------------------:|:-----------------:|
| **GKI** | GKI Devices | [![Repo](https://img.shields.io/badge/GitHub-GKI_KernelSU_SUSFS-blue?style=flat-square&logo=github)](https://github.com/WildKernels/GKI_KernelSU_SUSFS) |
| **Sultan** | Pixel Devices | [![Repo](https://img.shields.io/badge/GitHub-Sultan_KernelSU_SUSFS-blue?style=flat-square&logo=github)](https://github.com/WildKernels/Sultan_KernelSU_SUSFS) |
| **OnePlus** | OnePlus Devices | [![Repo](https://img.shields.io/badge/GitHub-OnePlus_KernelSU_SUSFS-blue?style=flat-square&logo=github)](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS) |

> [!TIP]
> Check each kernel's release page for device-specific builds and installation instructions. Many kernels provide AnyKernel3 flashable zips for easy installation.

> [!WARNING]
> Always backup your current boot image before flashing a new kernel. Keep a copy of your stock boot.img for recovery purposes.

### Choosing a Kernel

**Consider these factors:**
- **Device Compatibility**: Ensure the kernel explicitly supports your device model
- **Android Version**: Verify kernel is built for your Android version
- **Features**: KernelSU version, SUSFS support, additional optimizations
- **Maintenance**: Active development and regular updates
- **Community Feedback**: Check XDA, GitHub, or Telegram for user experiences

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>


## Installation

### Prerequisites

Before installing KernelSU, ensure you have:

> [!IMPORTANT]
> **Unlocked Bootloader** is essential for all installation methods. Check your device manufacturer's instructions for bootloader unlocking.

1. **Unlocked Bootloader**: Required for all installation methods
2. **Complete Backup**: Always backup your data and stock boot image
3. **ADB & Fastboot**: Install [Android SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools)
4. **USB Debugging**: Enable in Developer Options
5. **Custom Recovery** (Optional): TWRP or OrangeFox for some methods
6. **Stock Boot Image**: Keep a copy for recovery purposes

> [!WARNING]
> Backup your data before proceeding. Installation errors can result in data loss or bootloop situations.

> [!TIP]
> Use **Awesome-Android-Root Guides** for detailed bootloader unlocking instructions: [Unlock Bootloader Guide](https://awesome-android-root.org/android-root-guides/how-to-unlock-bootloader)

### Installation Methods

#### Method 1: GKI Mode (Kernel Replacement)

Best for modern devices with GKI support. Replaces the original kernel with KernelSU's generic kernel image.

**Advantages:**
- Strong universality, suitable for most modern devices
- Official support and regular updates
- Clean installation with minimal configuration

**Steps:**
```bash
# 1. Download appropriate boot.img from releases
# 2. Boot to fastboot mode
adb reboot bootloader

# 3. Flash the kernel
fastboot flash boot boot.img

# 4. Reboot device
fastboot reboot
```

---

#### Method 2: LKM Mode (Loadable Kernel Module)

Loads KernelSU as a module into the existing kernel without replacement.

**Advantages:**
- Preserves original kernel
- Less intrusive modification
- Easier to revert

**Steps:**
1. Download LKM package for your kernel version
2. Install via KernelSU Manager app
3. Reboot device to activate

---

#### Method 3: Manager Patching (One-Click)

Direct boot image patching through the KernelSU Manager app.

**Advantages:**
- User-friendly, no PC required after initial setup
- Automatic updates available
- Simplest for non-technical users

**Steps:**
1. Install KernelSU Manager APK
2. Grant necessary permissions
3. Select "Install" and choose patching method
4. Flash the patched boot image via fastboot or custom recovery

---

#### Method 4: Premade Custom Kernels

Using device-specific kernels with KernelSU pre-integrated from the community.

**Advantages:**
- Device-optimized performance
- Pre-tested stability and compatibility
- Additional features (SUSFS, optimizations)
- No compilation required

**Steps:**
1. Visit [Premade Kernels](#premade-kernels) section to find your device kernel
2. Download the appropriate kernel for your device
3. Flash via custom recovery (TWRP) or fastboot
4. Install KernelSU Manager APK
5. Verify installation

> [!TIP]
> Check [WildKernels](#wildkernels) for high-quality premade kernels with KernelSU and SUSFS support for GKI, Pixel, and OnePlus devices.

---

#### Method 5: Manual Building

Compile KernelSU integrated kernel from source.

**Advantages:**
- Full customization control
- Latest features and patches
- Learn kernel development

**Requirements:**
- Linux build environment
- Kernel source code
- Cross-compiler toolchain
- Build dependencies

**Steps:**
1. Setup build environment
2. Clone kernel source and KernelSU repository
3. Apply KernelSU patches
4. Configure kernel (enable CONFIG_KSU)
5. Compile kernel
6. Package with AnyKernel3
7. Flash to device

See [Building from Source](#kernel-sources-and-building) for detailed instructions.

---

### Installation Method Comparison

| Method               | Difficulty | Requirements                   | Device Support        | Pros                        | Cons                    |
| -------------------- | ---------- | ------------------------------ | --------------------- | --------------------------- | ----------------------- |
| **GKI Mode**         | Easy       | Unlocked bootloader, fastboot  | Modern GKI devices    | Official support, simple    | Limited to GKI devices  |
| **LKM Mode**         | Easy       | Root access or custom recovery | Wide compatibility    | Non-invasive                | May have limitations    |
| **Manager Patching** | Easy       | Unlocked bootloader            | Supported devices     | One-click, auto-updates     | Device-specific support |
| **Custom Kernel**    | Medium     | Custom recovery or fastboot    | Device-specific       | Pre-tested, optimized       | Availability varies     |
| **Manual Building**  | Hard       | Build environment, expertise   | Any compatible device | Full control, customization | Time-consuming, complex |

### Device Compatibility Check

**Check Your Kernel Version:**
```bash
# Using ADB
adb shell uname -r

# Or on device terminal
uname -r
```

**Compatibility Status:**

| Kernel Version  | Official KernelSU | KernelSU-Next   | SuKiSu-Ultra | Installation Method |
| --------------- | ----------------- | --------------- | ------------ | ------------------- |
| 5.10+ (GKI 2.0) | ✅ Supported       | ✅ Supported     | ❌ Not needed | GKI Mode / Manager  |
| 4.14-5.9        | ⚠️ Manual build    | ✅ Supported     | ✅ Supported  | Custom Kernel / LKM |
| 4.4-4.13        | ❌ Not supported   | ✅ Supported     | ✅ Supported  | Custom Kernel       |
| 3.4-4.3         | ❌ Not supported   | ❌ Not supported | ✅ Supported  | Custom Kernel       |

### Post-Installation Setup

After successful installation:

> [!IMPORTANT]
> Complete these essential steps to ensure proper KernelSU functionality and security.

1. **Verify Installation**
   ```bash
   # Check KernelSU version
   su -c "kernelsu --version"
   
   # Verify root access
   su -c "id"
   ```

2. **Install KernelSU Manager**
   - Download and install the appropriate manager app
   - Grant all required permissions
   - Confirm root access in manager

3. **Configure App Profiles**
   - Set up granular permissions for apps requiring root
   - Configure default deny policy
   - Setup time-based access restrictions

> [!TIP]
> Use restrictive App Profiles by default. Only grant necessary permissions to trusted applications.

4. **Install Essential Modules**
   - SuSFS for root hiding
   - Shamiko for SafetyNet bypass
   - Performance optimization modules

> [!WARNING]
> Only install modules from trusted sources. Malicious modules can compromise your device security.

5. **Setup Safety Features**
   - Configure module backup/restore
   - Enable automatic updates (if available)
   - Test SafetyNet/Play Integrity status

6. **Create Recovery Backup**
   - Backup patched boot image
   - Save module configurations
   - Document your setup for recovery

### Verification Commands

```bash
# Check if KernelSU is loaded
cat /proc/version | grep KernelSU

# Test root access
su -c "whoami"

# Check module directory
ls -la /data/adb/modules/

# View KernelSU logs
dmesg | grep kernelsu

# Check SELinux status
getenforce
```

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Official Resources

### Main Projects

- [**KernelSU Official Repository**](https://github.com/tiann/KernelSU) - Main KernelSU project repository
- [**Official Website**](https://kernelsu.org/) - Comprehensive documentation, downloads, and guides
- [**Official Telegram Channel**](https://t.me/KernelSU) - Official announcements and updates

### Latest Releases & Downloads

- [**KernelSU Releases**](https://github.com/tiann/KernelSU/releases) - Latest stable releases with changelogs
- [**Manager APK**](https://github.com/tiann/KernelSU/releases/latest) - Official KernelSU Manager application

### Official Tools

- [**KernelSU Flasher**](https://github.com/tiann/KernelSU/releases) - AnyKernel3-based universal flasher
- [**Kernel Patches**](https://github.com/tiann/KernelSU/tree/main/kernel) - Official kernel integration patches
- [**KernelSU Action**](https://github.com/dabao1955/kernel_build_action) - GitHub Actions for automated kernel building

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Documentation

### Core Documentation

- [**What is KernelSU?**](https://kernelsu.org/guide/what-is-kernelsu.html) - Introduction and architectural overview
- [**Installation Guide**](https://kernelsu.org/guide/installation.html) - Complete installation instructions for all methods
- [**App Profile System**](https://kernelsu.org/guide/app-profile.html) - Advanced root permission management
- [**Module System**](https://kernelsu.org/guide/module.html) - Understanding KernelSU modules
- [**API Documentation**](https://kernelsu.org/guide/module.html#kernelsu-modules) - Complete developer API reference

### Integration & Building

- [**Non-GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - Integrating KernelSU into custom kernels
- [**GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-gki.html) - Generic Kernel Image integration guide
- [**Building from Source**](https://kernelsu.org/guide/how-to-build.html) - Compiling KernelSU and kernels from source
- [**Kernel Requirements**](https://kernelsu.org/guide/installation.html#requirements) - Prerequisites and compatibility matrix
- [**Unofficially Supported Devices**](https://kernelsu.org/guide/unofficially-support-devices.html) - Manual compilation for older kernels

### Advanced Topics

- [**Security Model**](https://kernelsu.org/guide/security.html) - Understanding KernelSU's security architecture
- [**OverlayFS System**](https://kernelsu.org/guide/overlayfs.html) - Technical details of the module system
- [**SELinux Configuration**](https://kernelsu.org/guide/selinux.html) - Managing SELinux policies
- [**Debugging Guide**](https://kernelsu.org/guide/debug.html) - Troubleshooting kernel and module issues
- [**Migration from Magisk**](https://kernelsu.org/guide/migration.html) - Moving from Magisk to KernelSU

### Module Development

- [**Module Development Guide**](https://kernelsu.org/guide/module.html) - Creating and distributing KernelSU modules
- [**Module WebUI Guide**](https://kernelsu.org/guide/module-webui.html) - Building web interfaces for modules
- [**Module Examples**](https://github.com/topics/kernelsu-module) - Community module examples

### Recovery & Troubleshooting

- [**FAQ**](https://kernelsu.org/guide/faq.html) - Frequently asked questions and solutions
- [**Bootloop Recovery**](https://kernelsu.org/guide/rescue.html) - Emergency recovery procedures
- [**Rescue from Bootloop**](https://kernelsu.org/guide/rescue-from-bootloop.html) - Additional recovery methods
- [**Log Analysis**](https://kernelsu.org/guide/logs.html) - Understanding and analyzing system logs

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Development

### Module Development

<details>
<summary><b>📦 Click to expand: Module Development Guide</b></summary>

#### Getting Started

- [**Module Template**](https://github.com/tiann/KernelSU/blob/main/docs/module.md) - Official module development template
- [**API Documentation**](https://kernelsu.org/guide/module.html#kernelsu-modules) - Complete KernelSU API reference
- [**WebUI Development**](https://kernelsu.org/guide/module-webui.html) - Creating interactive web interfaces
- [**Module Examples**](https://github.com/topics/kernelsu-module) - Community-contributed examples

#### Module Structure

```
module_name/
├── module.prop          # Module metadata
├── post-fs-data.sh     # Post-fs-data script
├── service.sh          # Late service script
├── uninstall.sh        # Uninstallation script (optional)
├── system/             # System files to overlay
├── webroot/            # WebUI files (optional)
└── ...
```

#### Module Properties (module.prop)

```properties
id=module_id
name=Module Name
version=v1.0
versionCode=1
author=Author Name
description=Module description
updateJson=https://example.com/update.json
```

</details>

### Kernel Development & Integration

<details>
<summary><b>🔧 Click to expand: Kernel Integration & Building</b></summary>

#### Integration Guides

- [**Non-GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - For custom kernels 4.14 and earlier
- [**GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-gki.html) - For Generic Kernel Images
- [**Manual Building**](https://kernelsu.org/guide/how-to-build.html) - Complete build instructions
- [**KernelSU Action**](https://github.com/dabao1955/kernel_build_action) - GitHub Actions for CI/CD
- [**Kernel Build Scripts**](https://github.com/KernelSU-Next/KernelSU-Next/tree/next/scripts) - Universal patcher scripts

#### Integration Process

1. **Environment Setup**: Install required dependencies and cross-compiler
2. **Source Preparation**: Clone kernel sources and KernelSU repository
3. **Apply Patches**: Integrate KernelSU into kernel source
4. **Configuration**: Enable KernelSU in kernel config (CONFIG_KSU)
5. **Compilation**: Build kernel with appropriate toolchain
6. **Packaging**: Create flashable zip with AnyKernel3

</details>

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Modules and Tools

### Essential Modules

#### Root Management & Hiding

- [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module) - Advanced root hiding with customizable profiles and filesystem manipulation
- [**Shamiko**](https://github.com/LSPosed/LSPosed.github.io/releases) - DenyList bypass for enhanced hiding capabilities and SafetyNet/Play Integrity
- [**Tricky Store**](https://github.com/5ec1cff/TrickyStore) - Key attestation bypass for banking and payment apps

#### System Optimization

- [**Universal GMS Doze**](https://github.com/gloeyisk/universal-gms-doze) - Aggressive Google Play Services battery optimization

> [!TIP]
> Explore more modules on the: **[Awesome Android Root](https://awesome-android-root.org/android-root-apps/?filters=%5BK%5D)**

#### Framework Modifications

- [**LSPosed**](https://github.com/LSPosed/LSPosed) - Xposed framework implementation for KernelSU (via Zygisk)
- [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext) - Standalone Zygisk implementation for KernelSU
- [**ReZygisk**](https://github.com/PerformanC/ReZygisk) - Transparent Zygisk implementation

### Module Managers

- [**MMRL (Modern Module Manager)**](https://github.com/MMRLApp/MMRL) - Feature-rich module manager with:
  - Built-in module repository
  - Automatic updates
  - Module backup/restore
  - Dependency management
  - WebUI support
  - Material You design

### Management Apps

- [**KernelSU Manager**](https://github.com/tiann/KernelSU/releases) - Official management app for KernelSU
- [**SukiSU Manager**](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) - Manager for SuKiSu-Ultra variant
- [**Franco Kernel Manager**](https://play.google.com/store/apps/details?id=com.franco.kernel) - Kernel tweaking and monitoring
- [**SmartPack-Kernel Manager**](https://github.com/SmartPack/SmartPack-Kernel-Manager) - Open-source kernel management tool

### Development & Debugging Tools

- [**Root Checker**](https://play.google.com/store/apps/details?id=com.joeykrim.rootcheck) - Verify root status and installation
- [**Logcat Reader**](https://github.com/darshanparajuli/LogcatReader) - System log viewer and analyzer
- [**Terminal Emulator**](https://github.com/termux/termux-app) - Full Linux terminal environment

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Kernel Sources and Building

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
<summary><b>⚙️ Click to expand: Detailed Build Instructions</b></summary>

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

## Community

### Official Communities

#### Telegram
- [**KernelSU Channel**](https://t.me/KernelSU) - Official announcements and updates
- [**KernelSU Group**](https://t.me/KernelSU_group) - Community support and discussion
- [**KernelSU-Next Group**](https://t.me/KernelSU_Next) - KernelSU-Next specific discussions
- [**SuKiSu Group**](https://t.me/Sukiksu) - SuKiSu-Ultra community support

#### GitHub
- [**GitHub Discussions**](https://github.com/tiann/KernelSU/discussions) - Technical discussions and Q&A
- [**GitHub Issues**](https://github.com/tiann/KernelSU/issues) - Bug reports and feature requests
- [**KernelSU-Next Discussions**](https://github.com/KernelSU-Next/KernelSU-Next/discussions) - Enhanced fork discussions

### Forums & Discussion Platforms

- [**XDA Developers**](https://forum.xda-developers.com/t/kernelsu-a-kernel-based-root-solution-for-android.4511259/) - Main discussion thread with device-specific forums
- [**Reddit r/KernelSU**](https://www.reddit.com/r/KernelSU/) - Community discussions and support
- [**4PDA Forum**](https://4pda.to/forum/index.php?showtopic=1020374) - Russian-language community and resources

### International Communities

- **Chinese Community**: Official documentation and support in Chinese at [kernelsu.org](https://kernelsu.org/)
- **Russian Community**: Active discussions on [4PDA](https://4pda.to/)
- **Spanish Community**: Latin American users on XDA and Telegram
- **Indian Community**: Growing Hindi/English community on Telegram

### Community Resources

- **Module Repositories**: Community-maintained collections of KernelSU modules
- **Device Databases**: Lists of tested devices and kernel compatibility
- **Troubleshooting Wikis**: Community-contributed solutions and guides
- **Tutorial Videos**: YouTube channels with installation and usage guides

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Troubleshooting

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

## FAQ

### General Questions

**Q: What is KernelSU and how does it differ from Magisk?**

A: KernelSU is a kernel-based root solution that operates entirely in kernel space, providing superior security and isolation compared to Magisk's userspace approach. Key differences:
- **Architecture**: Kernel-level vs userspace
- **Security**: Better isolation and tamper resistance
- **Compatibility**: Requires compatible kernel vs universal support
- **Module System**: OverlayFS vs Magic Mount
- **Future**: Designed for modern Android security model

**Q: Which KernelSU variant should I use?**

A: Selection guide:
- **Modern devices (Android 12+, kernel 5.10+)**: Official KernelSU
- **Mid-range devices (Android 9-11, kernel 4.4-6.6)**: KernelSU-Next
- **Legacy devices (Android 7-8, kernel 3.4-5.4)**: SuKiSu-Ultra

**Q: Is KernelSU safer than Magisk?**

A: Yes, in several ways:
- Kernel-level operation prevents userspace attacks
- App Profile system offers granular permission control
- Zero system modification maintains integrity
- Hardware security integration (ARM TrustZone)
- Advanced hiding at kernel level

**Q: Can I use Magisk modules with KernelSU?**

A: Compatibility varies:
- **Simple modules**: Many work without modification
- **Complex modules**: May need adaptation for OverlayFS
- **Zygisk modules**: Require ZygiskNext or ReZygisk
- **Hardware-specific**: Usually compatible

**Q: Will KernelSU break OTA updates?**

A: Generally no:
- System partition remains unmodified
- Boot partition modification may need re-patching
- Some variants have automatic OTA survival
- Manual re-installation may be required for major updates

### Installation & Setup

<details>
<summary><b>📥 Click to expand: Installation & Setup FAQs</b></summary>

**Q: How do I check if my device is compatible?**

A: Check your kernel version:
```bash
adb shell uname -r
# or on device
uname -r
```
Then refer to the [compatibility matrix](#compatibility-matrix).

**Q: Do I need to uninstall Magisk before installing KernelSU?**

A: Yes, it's strongly recommended to:
1. Uninstall all Magisk modules
2. Uninstall Magisk completely
3. Flash stock boot image
4. Then install KernelSU

**Q: Can I have both Magisk and KernelSU installed?**

A: Not recommended. They modify the boot process differently and will conflict. Choose one solution.

**Q: How do I backup my current setup before installing?**

A: Create backups:
1. Full TWRP backup (if available)
2. Backup stock boot.img
3. Document installed modules
4. Export app data
5. Save important files to external storage

</details>

### Modules & Features

<details>
<summary><b>🔌 Click to expand: Modules & Features FAQs</b></summary>

**Q: Where can I find KernelSU modules?**

A: Sources:
- [MMRL](https://github.com/MMRLApp/MMRL) - Module manager with repository
- GitHub - Search for "kernelsu module"
- Telegram groups - Community shared modules
- XDA Forums - Device-specific modules

**Q: How do I create my own KernelSU module?**

A: Follow the [module development guide](https://kernelsu.org/guide/module.html):
1. Use the official module template
2. Create module.prop file
3. Add necessary scripts
4. Test thoroughly
5. Package as zip file

**Q: What are App Profiles and how do I use them?**

A: App Profiles allow granular control of root permissions per app:
- Custom UID/GID assignment
- Capability restrictions
- SELinux context customization
- Time-based access control
- Namespace isolation

Configure in KernelSU Manager under each app's settings.

</details>

### Troubleshooting

<details>
<summary><b>🔧 Click to expand: Common Troubleshooting FAQs</b></summary>

**Q: My device is stuck in a bootloop, what do I do?**

A: Emergency recovery:
```bash
# Enter fastboot mode (Power + Volume Down)
# Flash stock boot image
fastboot flash boot stock_boot.img
fastboot reboot
```
Always keep stock boot.img backup!

**Q: Banking apps are not working, how do I fix this?**

A: Root hiding setup:
1. Install Shamiko or SuSFS module
2. Configure DenyList in manager
3. Add banking apps to DenyList
4. Hide KernelSU Manager app
5. Test with SafetyNet checker

**Q: How do I check if KernelSU is working?**

A: Verification:
```bash
# Check kernel version
cat /proc/version | grep KernelSU

# Test root
su -c "id"

# Check manager
# Open KernelSU Manager and verify status
```

**Q: Modules are not loading, what's wrong?**

A: Common causes:
- Incompatible module version
- Insufficient permissions
- Module conflicts
- OverlayFS not supported

Check module logs: `/data/adb/modules/[module]/install.log`

</details>

### Development

<details>
<summary><b>👨‍💻 Click to expand: Development & Debugging FAQs</b></summary>

**Q: How do I build KernelSU for my device?**

A: Follow the [building guide](#kernel-sources-and-building):
1. Setup Linux build environment
2. Clone kernel source
3. Apply KernelSU patches
4. Configure kernel (enable CONFIG_KSU)
5. Compile kernel
6. Package with AnyKernel3

**Q: Can I contribute to KernelSU?**

A: Yes! Contributions welcome:
- Report bugs on GitHub
- Submit pull requests
- Create and share modules
- Improve documentation
- Help in community support
- Test beta versions

**Q: How do I enable debug mode?**

A: Enable debugging:
```bash
# Enable verbose logging
setprop persist.kernelsu.debug 1

# Collect logs
logcat -s "KernelSU" > /sdcard/debug.log
dmesg > /sdcard/kernel.log
```

</details>

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Contributing

We welcome contributions from the community! Help us make this the best KernelSU resource.

### Quick Contribution Guide

**To contribute:**
1. **Fork** this repository
2. **Add/Update** resources following our formatting standards
3. **Test** all links and verify information accuracy
4. **Submit** a pull request with clear description

**What to contribute:**
- New tools, modules, kernels, and resources
- Documentation improvements and translations
- Bug fixes and outdated information updates
- Tutorials, guides, and troubleshooting solutions

**Quality Standards:**
- Link to official/trusted sources
- Provide clear, concise descriptions
- Include version numbers and compatibility info
- Ensure resources are actively maintained
- Follow existing formatting patterns

**Resource Format:**
```markdown
- [**Resource Name**](https://link) - Clear, concise description
```

### Code of Conduct

Be respectful, constructive, and welcoming. Give credit, focus on community benefit, and show empathy.

### Need Help?

- Check existing [issues](https://github.com/fynks/awesome-kernelsu/issues) and [PRs](https://github.com/fynks/awesome-kernelsu/pulls)
- Ask in [Telegram community](https://t.me/KernelSU_group)
- Review [CONTRIBUTING.md](CONTRIBUTING.md) for comprehensive guidelines

**📖 For detailed contribution guidelines, formatting standards, review process, and more, see [CONTRIBUTING.md](CONTRIBUTING.md)**

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

## Disclaimer

> [!CAUTION]
> Rooting and kernel modification can void your warranty, brick your device, and expose security vulnerabilities. Proceed at your own risk.

### ⚠️ Important Legal Information

This documentation is for **educational and informational purposes only**. Users are solely responsible for understanding and complying with local laws regarding device modification.

> [!WARNING]
> **Warranty & Liability:**
> - Rooting typically **voids manufacturer warranty**
> - Contributors/maintainers are **not liable** for: device damage, data loss, warranty violations, legal consequences, or security vulnerabilities

**User Responsibilities:**
- Understand modification risks and create backups before changes
- Comply with local laws and manufacturer warranty terms
- Accept security risks and app compatibility issues

### Best Practices

<details>
<summary><b>Click to expand: Safety Guidelines & Recommendations</b></summary>

**Always:**
- ✅ Create complete backups before modifying device
- ✅ Read and understand documentation thoroughly
- ✅ Test changes on non-critical devices first
- ✅ Keep stock firmware and boot images
- ✅ Research device-specific considerations
- ✅ Understand security implications

**Never:**
- ❌ Proceed without proper backups
- ❌ Grant root access to untrusted apps
- ❌ Install modules from unknown sources
- ❌ Ignore security warnings
- ❌ Modify system without understanding changes

**Security Considerations:**

Root access can bypass Android security, allow malicious apps full system access, expose sensitive data, interfere with security-sensitive apps, and affect device encryption.

**Recommended:**
- Use App Profiles to restrict root access
- Install root hiding for sensitive apps
- Only grant root to trusted applications
- Regularly review app permissions
- Keep KernelSU updated

</details><br>

**Third-Party Content:** External projects have their own licenses (separate from this repository's MIT License). Verify safety before use.

**Updates:** This community-maintained documentation may contain outdated information. Verify against official sources.

**Affiliation:** KernelSU and derivatives are independent, community-driven projects—not affiliated with Google, Android, or device manufacturers.

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

## License

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Copyright (c) 2025 Fynks**

### License Terms

- **Free to Use**: Permission is granted to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
- **Attribution Required**: Copyright notice and permission notice must be included in all copies or substantial portions
- **No Warranty**: The software is provided "as is", without warranty of any kind
- **Liability**: Authors or copyright holders are not liable for any claim, damages or other liability

<div align="right">
<a href="#awesome-kernelsu">⬆ Back to Top</a>
</div><br>

---

## Acknowledgments

### Special Thanks

**Project Creators:**
- [**tiann**](https://github.com/tiann) - Creator of KernelSU, visionary behind kernel-based root
- [**topjohnwu**](https://github.com/topjohnwu) - Magisk creator, inspiration for systemless modifications

**Derivative Maintainers:**
- KernelSU-Next team - Enhanced fork development
- SuKiSu-Ultra team - Legacy device support

**Community Contributors:**
- Module developers creating useful tools
- Documentation translators and writers
- Community moderators and support staff
- Beta testers and bug reporters
- Everyone who shares knowledge

<br>
<div align="center">

[![Star History Chart](https://api.star-history.com/svg?repos=fynks/awesome-kernelsu&type=Date)](https://star-history.com/#fynks/awesome-kernelsu&Date)

---

**Made with ❤️ by the KernelSU Community**

<small>**Last Updated**: October 2025</small>

[⬆ Back to Top](#awesome-kernelsu)

</div>