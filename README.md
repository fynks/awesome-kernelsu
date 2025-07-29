# Awesome KernelSU 
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![GitHub stars](https://img.shields.io/github/stars/fynks/awesome-kernelsu?style=flat-square)](https://github.com/fynks/awesome-kernelsu/stargazers) [![License](https://img.shields.io/github/license/fynks/awesome-kernelsu?style=flat-square)](LICENSE)

> A comprehensive curated list of KernelSU resources, tools, modules, derivatives, and documentation for Android kernel-based root management

![KernelSU Banner](https://kernelsu.org/logo.png)

KernelSU is a revolutionary kernel-based root solution for Android that provides superior security and reliability compared to traditional rooting methods. Operating at the kernel level, it offers enhanced security isolation, system integrity protection, and powerful module management capabilities through OverlayFS.

Unlike traditional rooting methods that modify system partitions, KernelSU operates entirely within the kernel space, providing:
- **Zero system partition modification** - maintains system integrity and OTA compatibility
- **Advanced permission control** - granular app-level root access management
- **Enhanced security model** - kernel-level isolation prevents root detection and tampering
- **Modern module system** - efficient OverlayFS-based modifications with rollback capability

## Contents

- [🚀 Quick Start](#quick-start)
- [📚 Official Resources](#official-resources)
- [📖 Documentation](#documentation)
- [🔀 KernelSU Derivatives](#kernelsu-derivatives)
- [⚙️ Installation & Setup](#️installation--setup)
- [📦 Modules & Tools](#modules--tools)
- [👥 Community](#community)
- [📝 Tutorials & Guides](#tutorials--guides)
- [🔗 Related Projects](#related-projects)
- [📊 Comparison](#comparison)
- [❓ FAQ & Troubleshooting](#faq--troubleshooting)

## Quick Start

### New to KernelSU?
1. **Check compatibility**: Ensure your device has kernel 5.10+ (for official KernelSU)
2. **Download manager**: Get the [official KernelSU Manager](https://github.com/tiann/KernelSU/releases/latest)
3. **Install**: Follow the [installation guide](https://kernelsu.org/guide/installation.html)
4. **Verify**: Confirm installation through the manager app

### For Older Devices
- **Kernel 4.4-5.4**: Use [KernelSU-Next](https://github.com/KernelSU-Next/KernelSU-Next)
- **Kernel 3.x-5.4**: Use [SuKiSu-Ultra](https://github.com/SukiSU-Ultra/SukiSU-Ultra)

### Essential First Steps
- Configure [App Profiles](https://kernelsu.org/guide/app-profile.html) for root permission management
- Install [MMRL](https://github.com/MMRLApp/MMRL) for module management
- Join the [Telegram community](https://t.me/KernelSU_group) for support

## Official Resources

### Main Projects
- [**KernelSU Official Repository**](https://github.com/tiann/KernelSU) - Main KernelSU project repository
- [**Official Website**](https://kernelsu.org/) - Comprehensive documentation, downloads, and guides
- [**Official Telegram Channel**](https://t.me/KernelSU) - Official announcements and updates

### Latest Releases & Downloads
- [**KernelSU Releases**](https://github.com/tiann/KernelSU/releases) - Latest stable releases with changelogs
- [**Manager APK**](https://github.com/tiann/KernelSU/releases/latest) - Official KernelSU Manager application
- [**CI Builds**](https://github.com/tiann/KernelSU/actions) - Development builds and automated testing

### Official Tools
- [**KernelSU Flasher**](https://github.com/tiann/KernelSU/releases) - AnyKernel3-based universal flasher
- [**Kernel Patches**](https://github.com/tiann/KernelSU/tree/main/kernel) - Official kernel integration patches

[↑ Back to top](#contents)

## Documentation

### Core Documentation
- [**What is KernelSU?**](https://kernelsu.org/guide/what-is-kernelsu.html) - Introduction and architectural overview
- [**Installation Guide**](https://kernelsu.org/guide/installation.html) - Complete installation instructions for all methods
- [**Module Development Guide**](https://kernelsu.org/guide/module.html) - Creating and distributing KernelSU modules
- [**Module WebUI Guide**](https://kernelsu.org/guide/module-webui.html) - Building web interfaces for modules
- [**App Profile System**](https://kernelsu.org/guide/app-profile.html) - Advanced root permission management
- [**API Documentation**](https://kernelsu.org/guide/module.html#kernelsu-modules) - Complete developer API reference

### Integration & Building Guides
- [**Non-GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - Integrating KernelSU into custom kernels
- [**GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-gki.html) - Generic Kernel Image integration guide
- [**Building from Source**](https://kernelsu.org/guide/how-to-build.html) - Compiling KernelSU and kernels from source
- [**Kernel Requirements**](https://kernelsu.org/guide/installation.html#requirements) - Prerequisites and compatibility matrix

### Advanced Topics
- [**Security Model**](https://kernelsu.org/guide/security.html) - Understanding KernelSU's security architecture
- [**OverlayFS Deep Dive**](https://kernelsu.org/guide/overlayfs.html) - Technical details of the module system
- [**Debugging Guide**](https://kernelsu.org/guide/debug.html) - Troubleshooting kernel and module issues
- [**Migration Guide**](https://kernelsu.org/guide/migration.html) - Moving from Magisk to KernelSU

### Troubleshooting Resources
- [**Common Issues**](https://kernelsu.org/guide/faq.html) - Frequently asked questions and solutions
- [**Bootloop Recovery**](https://kernelsu.org/guide/rescue.html) - Emergency recovery procedures
- [**Log Analysis**](https://kernelsu.org/guide/logs.html) - Understanding and analyzing system logs

[↑ Back to top](#contents)

## KernelSU Derivatives

### KernelSU-Next (Enhanced Fork)
- [**Repository**](https://github.com/KernelSU-Next/KernelSU-Next) - Advanced kernel-based root solution
- [**Official Website**](https://kernelsu-next.github.io/webpage/) - Documentation and comprehensive guides
- [**Latest Release**](https://github.com/KernelSU-Next/KernelSU-Next/releases) - Stable releases with enhanced features
- [**Nightly Builds**](https://nightly.link/KernelSU-Next/KernelSU-Next/workflows/build-manager-ci/next/Manager) - Development builds with latest features
- [**Telegram Community**](https://t.me/KernelSU_Next) - Official support and discussion group

#### KernelSU-Next Features
- **Extended Kernel Support**: 4.4-6.6 kernels (Non-GKI & GKI) with wide device compatibility
- **Dual Module System**: Magic Mount + OverlayFS with seamless toggle switching
- **Enhanced Material You UI**: Redesigned manager with dynamic theming and improved UX
- **Advanced Module Management**: Backup/restore functionality, bulk operations, and dependency handling
- **Auto-Update System**: Automatic manager updates with rollback capability
- **WebUI X Framework**: Enhanced WebUI system with system-level APIs and React support
- **Developer Tools**: Built-in logcat viewer, performance monitor, and debugging utilities
- **Custom OverlayFS Options**: Configurable image size, compression, and mount strategies

### SuKiSu-Ultra (Non-GKI Specialized)
- [**Repository**](https://github.com/SukiSU-Ultra/SukiSU-Ultra) - KernelSU fork optimized for legacy devices
- [**Official Website**](https://sukisu.org/) - Project homepage with detailed documentation
- [**Latest Release**](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) - Download latest stable release
- [**Official Telegram Group**](https://t.me/SukiKSU) - Community support and announcements
- [**Wiki & Guides**](https://github.com/SukiSU-Ultra/SukiSU-Ultra/wiki) - Comprehensive setup and troubleshooting guides

#### SuKiSu-Ultra Features
- **Broad Kernel Compatibility**: Supports kernels 3.4-5.4+ with extensive backports
- **KPM Integration**: Kernel Patch Module support for advanced kernel modifications
- **SuSFS Built-in**: Advanced root hiding capabilities with customizable profiles  
- **Multi-Architecture**: arm64-v8a, armeabi-v7a, x86_64 with optimized builds
- **Enhanced Manager**: Refined UI with dark/light themes and SuSFS management panel
- **Legacy Device Focus**: Optimizations for older Android versions and hardware
- **Extensive Device Support**: Community-maintained device database and kernel sources

### Compatibility & Selection Matrix

| Derivative | Kernel Support | Android Version | Architecture | Primary Use Case | Update Frequency |
|------------|---------------|-----------------|-------------|------------------|------------------|
| **KernelSU Official** | 5.10+ (GKI 2.0) | 12+ | arm64, x86_64 | Modern devices, stability | Regular |
| **KernelSU-Next** | 4.4-6.6 | 9+ | arm64, arm, x86_64 | Enhanced features, broad support | Active |
| **SuKiSu-Ultra** | 3.4-5.4+ | 7+ | arm64, arm, x86_64 | Legacy devices, advanced hiding | Community |

### Choosing the Right Derivative

#### Recommended for New Devices (2021+)
- **Primary**: KernelSU Official for maximum stability and official support
- **Alternative**: KernelSU-Next for additional features and enhanced UI

#### Recommended for Mid-range Devices (2018-2021)  
- **Primary**: KernelSU-Next for optimal balance of features and compatibility
- **Alternative**: SuKiSu-Ultra if advanced root hiding is required

#### Recommended for Legacy Devices (Pre-2018)
- **Primary**: SuKiSu-Ultra for comprehensive legacy support
- **Fallback**: KernelSU-Next if kernel 4.4+ is available

[↑ Back to top](#contents)

## Installation & Setup

### Boot Image Patching Tools
- [**KernelSU Manager**](https://github.com/tiann/KernelSU/releases) - Official app for patching boot images with one-click installation
- [**Kernel Flasher**](https://github.com/tiann/KernelSU/releases) - AnyKernel3-based universal flasher for custom recovery
- [**KernelSU Action**](https://github.com/dabao1955/kernel_build_action) - GitHub Actions for automated kernel building and CI/CD

### Pre-built Images & Kernels
- [**GKI Boot Images**](https://github.com/tiann/KernelSU/releases) - Ready-to-flash Generic Kernel Images
- [**Device-Specific Kernels**](https://github.com/search?q=kernelsu%20kernel&type=repositories) - Community-built kernels for specific devices

### Installation Methods Comparison

| Method | Difficulty | Requirements | Pros | Cons |
|--------|------------|-------------|------|------|
| **Manager Patching** | Easy | Unlocked bootloader | One-click process, automatic updates | Limited to supported devices |
| **Custom Kernel** | Medium | Custom recovery/fastboot | Pre-tested stability | Device-specific availability |
| **Manual Building** | Hard | Build environment | Full customization | Time-consuming, requires expertise |
| **Recovery Flash** | Easy | Custom recovery | Works offline | Requires recovery access |

### Installation Prerequisites
- **Unlocked Bootloader**: Essential for all installation methods
- **Root/ADB Access**: Required for manager-based patching  
- **Custom Recovery**: Needed for flashable zip installation
- **Backup Tools**: Create full system backup before installation

### Post-Installation Setup
1. **Verify Installation**: Check KernelSU status in manager app
2. **Configure App Profiles**: Set up granular root permissions
3. **Install Essential Modules**: SuSFS for hiding, performance tweaks
4. **Setup Module Manager**: Install MMRL for easier module management
5. **Create Safety Net**: Configure hiding for banking/payment apps

[↑ Back to top](#contents)

## Kernel Sources & Building

### Official Kernels & Sources
- [**KernelSU GKI Kernels**](https://github.com/tiann/KernelSU/releases) - Official GKI builds
- [**KernelSU-Next Kernels**](https://github.com/KernelSU-Next/KernelSU-Next/releases) - Enhanced builds
- [**Kernel Build Action**](https://github.com/dabao1955/kernel_build_action) - Automated building

### Device-Specific Resources
- [**OnePlus Sources**](https://github.com/OnePlusOSS) - OnePlus kernel sources
- [**Xiaomi Sources**](https://github.com/MiCode/Xiaomi_Kernel_OpenSource) - Xiaomi kernel sources
- [**Google Sources**](https://android.googlesource.com/kernel/) - AOSP kernel sources

### Building Tools & Scripts
- [**Universal Patcher**](https://github.com/KernelSU-Next/KernelSU-Next/tree/next/scripts) - Kernel patching scripts
- [**KernelSU Builder**](https://github.com/dabao1955/kernel_build_action) - CI/CD building system
- [**Manual Build Guide**](https://kernelsu.org/guide/how-to-build.html) - Step-by-step building

### Supported Architectures
- **arm64-v8a** - Primary support (64-bit ARM)
- **x86_64** - Intel/AMD 64-bit (limited device support)
- **armeabi-v7a** - 32-bit ARM (SuKiSu-Ultra only)

[↑ Back to top](#contents)

## Development

### Module Development

#### Getting Started
- [**Module Template**](https://github.com/tiann/KernelSU/blob/main/docs/module.md) - Official module development template with examples
- [**API Documentation**](https://kernelsu.org/guide/module.html#kernelsu-modules) - Complete KernelSU API reference and usage guide
- [**WebUI Development Guide**](https://kernelsu.org/guide/module-webui.html) - Creating interactive web interfaces for modules
- [**Module Examples Repository**](https://github.com/topics/kernelsu-module) - Community-contributed example modules

#### Advanced Module Development
- [**OverlayFS Integration**](https://kernelsu.org/guide/overlayfs-advanced.html) - Deep dive into OverlayFS module system
- [**Native Library Support**](https://kernelsu.org/guide/native-modules.html) - Integrating C/C++ components in modules
- [**SELinux Policy Handling**](https://kernelsu.org/guide/selinux-modules.html) - Working with SELinux in KernelSU modules
- [**Module Security Guidelines**](https://kernelsu.org/guide/module-security.html) - Best practices for secure module development


### Kernel Development & Integration

#### Integration Guides
- [**Non-GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - Comprehensive guide for custom kernel integration


### Building & Compilation

#### Automated Building Systems
- [**KernelSU Action**](https://github.com/dabao1955/kernel_build_action) - GitHub Actions for automated kernel building

#### Manual Building Procedures
1. **Environment Setup**: Install required dependencies and tools
2. **Source Preparation**: Clone kernel sources and apply KernelSU patches
3. **Configuration**: Set up kernel config with KernelSU requirements
4. **Compilation**: Build kernel with appropriate cross-compiler
5. **Packaging**: Create flashable zip with AnyKernel3 or similar

#### Cross-Platform Development
- **Android Studio Integration**: Plugin for KernelSU module development
- **VS Code Extensions**: Syntax highlighting and debugging support
- **Docker Containers**: Standardized development environments
- **Remote Development**: Cloud-based building and testing systems

[↑ Back to top](#contents)

## Modules & Tools

### Essential KernelSU Modules

#### Root Management & Hiding
- [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module) - Advanced root hiding with customizable profiles
- [**Shamiko**](https://github.com/LSPosed/LSPosed.github.io/releases) - DenyList bypass for enhanced hiding capabilities

#### Performance & System Optimization
- [**MAGNETAR**](https://github.com/Kyliekyler/MAGNETAR) - Comprehensive device performance optimizer

#### System Customization
- [**SystemUI Tuner**](https://github.com/Magisk-Modules-Repo/systemui-tuner) - Advanced SystemUI customization
- [**AdAway**](https://github.com/AdAway/AdAway) - System-wide ad blocking

### Module Manager

#### Modern Module Managers
- [**MMRL (Modern Module Manager)**](https://github.com/MMRLApp/MMRL) - Feature-rich module manager with repository support

[↑ Back to top](#contents)

## Community

### Official Communities
- [**Telegram Channel**](https://t.me/KernelSU) - Official announcements
- [**GitHub Discussions**](https://github.com/tiann/KernelSU/discussions) - Technical discussions
- [**Telegram Group**](https://t.me/KernelSU_group) - Community chat

### Derivative Communities
- [**KernelSU-Next Telegram**](https://t.me/KernelSU_Next) - KernelSU-Next discussions
- [**SuKiSu Telegram**](https://t.me/Sukiksu) - SuKiSu-Ultra community

### Forums & Discussion Platforms
- [**XDA Developers Thread**](https://forum.xda-developers.com/t/kernelsu-a-kernel-based-root-solution-for-android.4511259/) - Main discussion
- [**Reddit Community**](https://www.reddit.com/r/KernelSU/) - Community discussions
- [**4PDA Forum**](https://4pda.to/forum/index.php?showtopic=1020374) - Russian community

[↑ Back to top](#contents)

## Tutorials & Guides

### Beginner Guides
- [**What is KernelSU?**](https://kernelsu.org/guide/what-is-kernelsu.html) - Complete introduction
- [**First Installation**](https://kernelsu.org/guide/installation.html) - Step-by-step setup
- [**Manager App Guide**](https://kernelsu.org/guide/installation.html#verify-installation) - Using the manager
- [**App Profile Setup**](https://kernelsu.org/guide/app-profile.html) - Managing app permissions

### Advanced Guides
- [**Custom Kernel Building**](https://kernelsu.org/guide/how-to-build.html) - Compile your own kernel
- [**Module Development**](https://kernelsu.org/guide/module.html) - Create custom modules
- [**WebUI Development**](https://kernelsu.org/guide/module-webui.html) - Advanced module interfaces
- [**Troubleshooting Guide**](https://kernelsu.org/guide/faq.html) - Common issues and solutions

[↑ Back to top](#contents)

## Related Projects

### Alternative Root Solutions
- [**Magisk**](https://github.com/topjohnwu/Magisk) - Traditional systemless root
- [**APatch**](https://github.com/bmax121/APatch) - KernelPatch-based root solution
- [**KernelPatch**](https://github.com/bmax121/KernelPatch) - Kernel patching framework

### Compatibility Layers
- [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext) - Standalone Zygisk implementation
- [**ReZygisk**](https://github.com/PerformanC/ReZygisk) - Transparent Zygisk implementation
- [**Shamiko**](https://github.com/LSPosed/LSPosed.github.io/releases) - Magisk hide successor

### Root Detection & Hiding
- [**SuSFS**](https://gitlab.com/simonpunk/susfs4ksu) - Advanced root hiding kernel patches
- [**Tricky Store**](https://github.com/5ec1cff/TrickyStore) - Key attestation bypass

[↑ Back to top](#contents)

## Comparison

### KernelSU vs Alternative Root Solutions
| Feature | KernelSU | KernelSU-Next | SuKiSu-Ultra | Magisk | APatch |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Architecture** | Kernel-level | Kernel-level | Kernel-level | Userspace | Kernel-level |
| **Module System** | OverlayFS | OverlayFS + Magic Mount | Magic Mount + OverlayFS | Magic Mount | OverlayFS |
| **Kernel Support** | 5.10+ (GKI 2.0) | 4.4-6.6 | 3.4-5.4+ | Any | 3.18-6.1 |
| **Architecture** | arm64, x86_64 | arm64, arm, x86_64 | arm64, arm, x86_64 | Universal | arm64 |
| **Security Model** | App Profile | App Profile | App Profile | Root Toggle | SuperKey |
| **Hide Capability** | Basic | Advanced | SuSFS Integrated | MagiskHide (deprecated) | Kernel-level |
| **Update Method** | Manual | Auto-update | Manual | OTA | Manual |
| **System Modification** | Zero | Zero | Zero | Minimal | Zero |
| **OTA Compatibility** | Excellent | Excellent | Good | Good | Excellent |
| **Development Status** | Active | Very Active | Active | Active | Active |
| **Learning Curve** | Medium | Medium | Hard | Easy | Hard |
| **Community Size** | Growing | Medium | Small | Large | Small |

### Technical Architecture Comparison

#### Security Models
- **KernelSU Family**: Kernel-level operation provides superior isolation and tamper resistance
- **Magisk**: Userspace operation with systemless modifications, easier detection
- **APatch**: Kernel patching with advanced hiding but complex setup
- **SuperSU**: Traditional system modification, highest detectability

#### Module Systems Performance
- **OverlayFS (KernelSU)**: Efficient copy-on-write, minimal performance impact
- **Magic Mount (Magisk)**: Bind mounting, higher overhead but broader compatibility  
- **Hybrid Systems**: Best of both worlds but increased complexity

### Advantages of KernelSU Ecosystem

#### Security Benefits
- **Kernel-Level Isolation**: Root access operates in kernel space, preventing userspace tampering
- **App Profile System**: Granular per-application permission control with temporal restrictions
- **Hardware-Level Protection**: Utilizes ARM TrustZone and other hardware security features
- **Verified Boot Compatibility**: Maintains system integrity verification where possible

#### Technical Advantages  
- **Zero System Modification**: No changes to system partitions, preserving OTA capabilities
- **OverlayFS Efficiency**: More efficient than bind mounting with better performance characteristics
- **Future-Proof Design**: Built for modern Android security models and requirements
- **Developer-Friendly**: Clean APIs and comprehensive documentation

#### Ecosystem Maturity
- **Multiple Derivatives**: Options for different use cases and device compatibility
- **Active Development**: Regular updates and feature additions across all derivatives
- **Growing Module Repository**: Expanding collection of high-quality modules
- **Community Support**: Knowledgeable community with expert developers

### Migration Considerations

#### From Magisk to KernelSU
**Pros:**
- Enhanced security and hiding capabilities
- Better performance with OverlayFS
- Future-proof architecture
- Maintained OTA compatibility

**Considerations:**
- Module compatibility may require updates
- Different app profile management
- Learning curve for new concepts

#### From SuperSU/Other Legacy Solutions
**Pros:**
- Dramatically improved security
- Modern Android compatibility  
- Systemless approach
- Active development and support

**Essential:**
- Complete system restoration recommended
- Fresh start with modern practices
- Understanding of new security model

### Use Case Recommendations

#### Choose KernelSU Official If:
- You have a modern device (2021+) with GKI 2.0
- Stability and official support are priorities  
- You prefer established, well-tested solutions
- OTA compatibility is essential

#### Choose KernelSU-Next If:
- You want enhanced features and better UI
- Your device has kernel 4.4-6.6 support
- You value active development and innovation
- Auto-updates and advanced module management appeal to you

#### Choose SuKiSu-Ultra If:
- You have an older device with kernel 3.x-5.4
- Advanced root hiding is critical (banking apps, etc.)
- You need KPM support for kernel modifications
- Legacy device optimization is important

#### Stick with Magisk If:
- You have very old hardware not supported by KernelSU derivatives
- You rely heavily on Xposed or other Magisk-specific modules
- You're satisfied with current functionality and stability
- Migration effort outweighs potential benefits

## FAQ & Troubleshooting

### Frequently Asked Questions

#### **Q: What's the difference between KernelSU and its derivatives?**
**A: Each derivative targets different use cases:**
- **KernelSU Official**: Best for modern devices (5.10+ kernels), maximum stability, official support
- **KernelSU-Next**: Enhanced features, broader compatibility (4.4-6.6 kernels), automatic updates, advanced UI
- **SuKiSu-Ultra**: Legacy device focus (3.x-5.4 kernels), advanced hiding (SuSFS), KPM support

#### **Q: Which version should I choose for my device?**
**A: Selection guide:**
- **Android 12+ devices**: KernelSU Official → KernelSU-Next (if you want extra features)
- **Android 9-11 devices**: KernelSU-Next → SuKiSu-Ultra (if kernel too old)
- **Android 7-8 devices**: SuKiSu-Ultra (only option for legacy kernels)

#### **Q: Is KernelSU safer than Magisk?**
**A: Yes, in several ways:**
- **Kernel-level operation** provides superior isolation from userspace attacks
- **App Profile system** offers granular, time-based permission control
- **Zero system modification** maintains system integrity and OTA compatibility  
- **Hardware security integration** utilizes ARM TrustZone and secure boot when available
- **Advanced hiding** at kernel level is harder to detect than userspace methods

#### **Q: Can I use Magisk modules with KernelSU?**
**A: Compatibility varies:**
- **Simple modules**: Many work without modification
- **Complex modules**: May require adaptation for OverlayFS
- **Zygisk modules**: Need ZygiskNext or ReZygisk for KernelSU
- **Hardware-specific**: Usually compatible across root solutions

#### **Q: Will KernelSU break OTA updates?**
**A: Generally no:**
- **KernelSU preserves** system partition integrity
- **Boot partition modification** may need re-patching after OTA
- **Automatic tools** in some derivatives handle OTA survival
- **Manual re-installation** may be required for major Android updates

[↑ Back to top](#contents)

### Advanced Troubleshooting

#### **Bootloop Recovery Procedures**

**Immediate Steps:**
1. **Power + Volume Down** to enter fastboot mode
2. **Flash stock boot image**: `fastboot flash boot stock_boot.img`
3. **Clear cache partition** if available in recovery
4. **Factory reset** only as last resort (data loss)

**Prevention:**
- Always keep stock boot image backup
- Test kernels with temporary boot before permanent flash
- Use TWRP/recovery with restore capabilities
- Keep emergency download mode access available

#### **Manager App Issues**

**App Won't Open:**
1. Check KernelSU kernel installation: `su -c "kernelsu --version"`
2. Verify app signature and install from official sources
3. Clear app data and cache, reinstall if necessary  
4. Check for conflicting security apps or policies

**Root Permission Denied:**
1. Verify KernelSU service is running: `ps aux | grep kernelsu`
2. Check app profile configuration in manager
3. Ensure SELinux policies allow KernelSU operation
4. Debug with: `dmesg | grep kernelsu`

**Module Installation Failures:**
1. Verify OverlayFS support: `mount | grep overlay`
2. Check available storage space in data partition  
3. Validate module format and compatibility
4. Review module logs: `/data/adb/modules/[module]/install.log`

#### **Performance and Stability Issues**

**System Slowdown:**
1. **Identify problematic modules**: Disable modules one by one
2. **Check CPU throttling**: Monitor thermals and frequency scaling
3. **Review I/O performance**: OverlayFS overhead on slow storage
4. **Analyze system logs**: Look for kernel errors or warnings

**Random Reboots:**
1. **Check kernel logs**: `dmesg` and `/proc/last_kmsg`
2. **Monitor memory usage**: OOM killer activity
3. **Verify hardware stability**: Stress test without KernelSU
4. **Test minimal configuration**: Remove all modules temporarily

**App Compatibility Problems:**
1. **Configure app profiles**: Restrict root access for sensitive apps
2. **Enable advanced hiding**: Install SuSFS or similar modules
3. **Check SafetyNet status**: Use apps like YASNAC or SafetyNet Test
4. **Review detection methods**: Banking apps may use hardware attestation

[↑ Back to top](#contents)

### Device-Specific Troubleshooting

#### **Samsung Devices**
- **Knox triggered**: Some Samsung devices may trip Knox warranty bit
- **Secure boot issues**: Disable secure boot verification if possible
- **Encryption problems**: Some kernels may have issues with Samsung encryption

#### **OnePlus Devices**  
- **Fastboot mode**: Use `fastboot oem unlock` for bootloader unlocking
- **Color OS migration**: Recent devices may need special handling
- **Parallel app conflicts**: OxygenOS parallel apps may conflict with root

#### **Xiaomi Devices**
- **Anti-rollback protection**: Be careful with MIUI version downgrades
- **Bootloader unlock delay**: Xiaomi requires waiting period for unlock
- **MIUI optimizations**: Some MIUI features may conflict with KernelSU

#### **Google Pixel Devices**
- **Hardware attestation**: Strong SafetyNet enforcement on newer Pixels
- **Verified boot warnings**: May show orange state warning on boot
- **Titan M security**: Hardware security module may affect root hiding

[↑ Back to top](#contents)

### Community Support Resources

#### **Getting Help Priority Order**
1. **Official Documentation**: Check kernelsu.org FAQ and troubleshooting guides
2. **GitHub Discussions**: Search existing issues and discussions on official repo
3. **Telegram Groups**: Ask in appropriate group (official/derivative-specific)
4. **XDA Forums**: Post in device-specific or general KernelSU threads
5. **Reddit Communities**: r/KernelSU for general discussion and support

#### **Effective Bug Reporting**
**Include in bug reports:**
- Device model, Android version, kernel version
- KernelSU derivative and version  
- Steps to reproduce the issue
- Full logs: `dmesg`, manager logs, module logs
- Module list and configuration

**Log Collection Commands:**
```bash
# Kernel logs
dmesg > /sdcard/dmesg.log

# KernelSU specific logs  
logcat -s "KernelSU" > /sdcard/kernelsu.log

# Module installation logs
cat /data/adb/modules/*/install.log > /sdcard/module_logs.log
```

#### **Contributing to Solutions**
- **Document solutions**: Add working fixes to community wikis
- **Test beta versions**: Help with testing new releases and features
- **Contribute modules**: Create and maintain useful modules
- **Support others**: Answer questions in community forums
- **Improve documentation**: Submit PR for documentation improvements

[↑ Back to top](#contents)

---

## Contributing

Contributions are welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

### How to Contribute
1. **Fork** this repository
2. **Add** your resource to the appropriate section
3. **Ensure** the resource is actively maintained and relevant
4. **Test** all links and verify information accuracy
5. **Submit** a pull request with a clear description

### Resource Guidelines
- Should provide clear value to the KernelSU community
- Links must be working and lead to official sources
- Include relevant metrics (stars, downloads) where available
- Maintain alphabetical order within sections

### Quality Standards
- All information must be accurate and up-to-date
- Links should be to official repositories or trusted sources
- Descriptions should be clear and concise
- Include version numbers and compatibility information

### Legal & Disclaimer
This documentation is provided for educational purposes. Users are responsible for understanding their local laws regarding device modification. The contributors and maintainers of this list are not responsible for any damage to devices or violation of warranties. Always create backups before modifying your device.

*KernelSU and its derivatives are independent projects not affiliated with Google, Android, or device manufacturers.*

[↑ Back to top](#contents)

---
<div style="text-align:center">

**Made with ❤️ by the KernelSU community**

</div>