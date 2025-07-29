# Awesome KernelSU [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A comprehensive curated list of KernelSU resources, tools, modules, derivatives, and documentation for Android kernel-based root management

KernelSU is a revolutionary kernel-based root solution for Android that provides superior security and reliability compared to traditional rooting methods. Operating at the kernel level, it offers enhanced security isolation, system integrity protection, and powerful module management capabilities through OverlayFS.

## Contents

- [Official Resources](#-official-resources)
- [Documentation](#-documentation)
- [KernelSU Derivatives](#-kernelsu-derivatives)
- [Installation & Setup](#-installation--setup)
- [Kernel Sources & Building](#-kernel-sources--building)
- [Development](#️-development)
- [Modules & Tools](#-modules--tools)
- [Community](#-community)
- [Tutorials & Guides](#-tutorials--guides)
- [Related Projects](#-related-projects)
- [Comparison](#-comparison)
- [FAQ & Troubleshooting](#-faq--troubleshooting)

## Official Resources

### Main Projects
- [**KernelSU Official Repository**](https://github.com/tiann/KernelSU) - Main KernelSU project repository
- [**Official Website**](https://kernelsu.org/) - Official documentation, downloads, and guides
- [**Official Telegram Channel**](https://t.me/KernelSU) - Official announcements and updates

### Latest Releases
- [**KernelSU Releases**](https://github.com/tiann/KernelSU/releases) - Latest stable releases
- [**Manager APK**](https://github.com/tiann/KernelSU/releases/latest) - Official KernelSU Manager application

## Documentation

### Core Documentation
- [**What is KernelSU?**](https://kernelsu.org/guide/what-is-kernelsu.html) - Introduction and overview
- [**Installation Guide**](https://kernelsu.org/guide/installation.html) - Complete installation instructions
- [**Module Development Guide**](https://kernelsu.org/guide/module.html) - Creating KernelSU modules
- [**Module WebUI Guide**](https://kernelsu.org/guide/module-webui.html) - Web interface for modules
- [**App Profile System**](https://kernelsu.org/guide/app-profile.html) - Root permission management
- [**API Documentation**](https://kernelsu.org/guide/module.html#kernelsu-modules) - Complete API reference

### Integration Guides
- [**Non-GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - Custom kernel integration
- [**GKI Integration**](https://kernelsu.org/guide/how-to-integrate-for-gki.html) - GKI kernel integration
- [**Building Guide**](https://kernelsu.org/guide/how-to-build.html) - Compiling from source
- [**FAQ**](https://kernelsu.org/guide/faq.html) - Frequently asked questions

## KernelSU Derivatives

### KernelSU-Next (Enhanced Fork)
- [**Repository**](https://github.com/KernelSU-Next/KernelSU-Next) - Advanced kernel-based root solution
- [**Official Website**](https://kernelsu-next.github.io/webpage/) - Documentation and downloads
- [**Latest Release**](https://github.com/KernelSU-Next/KernelSU-Next/releases)
- [**Nightly Builds**](https://nightly.link/KernelSU-Next/KernelSU-Next/workflows/build-manager-ci/next/Manager)

#### KernelSU-Next Features
- **Extended Kernel Support**: 4.4-6.6 kernels (Non-GKI & GKI)
- **Dual Module System**: Magic Mount + OverlayFS with toggle switching
- **Enhanced UI**: Redesigned manager with Material You design
- **Module Management**: Backup/restore functionality for modules
- **Auto-Updates**: Automatic manager updates
- **Advanced Features**: Custom OverlayFS image size, bulk module installation
- **WebUI X**: Enhanced WebUI system with system-level APIs

### SuKiSu-Ultra (Non-GKI Focused)
- [**Repository**](https://github.com/SukiSU-Ultra/SukiSU-Ultra) - KernelSU fork for older devices
- [**Official Website**](https://sukisu.org/) - Project homepage
- [**Latest Release**](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) - Download latest release of SukiSU-Ultra
- [**Official Telegram Group**](https://t.me/SukiKSU) - Official group of SukiSU-Ultra on Telegram

#### SuKiSu-Ultra Features
- **Broad Compatibility**: Supports kernels 3.4-5.4+ with backports
- **KPM Support**: Kernel Patch Module integration
- **SuSFS Integration**: Advanced root hiding capabilities
- **Architecture Support**: arm64-v8a, armeabi-v7a, x86_64
- **Enhanced Manager**: Improved theme and built-in SuSFS management

#### Compatibility Matrix
| Derivative | Kernel Support | Architecture | Special Features |
|------------|---------------|-------------|-----------------|
| **KernelSU** | 5.10+ (GKI 2.0) | arm64, x86_64 | Official, Stable |
| **KernelSU-Next** | 4.4-6.6 | arm64, arm, x86_64 | Magic Mount, WebUI X |
| **SuKiSu-Ultra** | 3.4-5.4+ | arm64, arm, x86_64 | KPM, Non-GKI focus |

## Installation & Setup

### Boot Image Patching Tools
- [**KernelSU Manager**](https://github.com/tiann/KernelSU/releases) - Official app for patching boot images
- [**Kernel Flasher**](https://github.com/tiann/KernelSU/releases) - Alternative flashing method
- [**KernelSU Action**](https://github.com/dabao1955/kernel_build_action) - GitHub Actions for automated builds

### Pre-built Images
- [**AnyKernel3 Flasher**](https://github.com/tiann/KernelSU/releases) - Universal flashable zip
- [**GKI Boot Images**](https://github.com/tiann/KernelSU/releases) - Ready-to-flash GKI kernels

### Installation Methods
1. **Manager Method**: Patch boot image with official manager
2. **Custom Kernel**: Flash pre-built kernel with KernelSU integrated
3. **Manual Building**: Compile kernel with KernelSU patches

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

## Development

### Module Development
- [**Module Template**](https://github.com/tiann/KernelSU/blob/main/docs/module.md) - Basic module structure
- [**API Documentation**](https://kernelsu.org/guide/module.html#kernelsu-modules) - Complete API reference
- [**WebUI Development**](https://kernelsu.org/guide/module-webui.html) - Creating web interfaces
- [**Module Examples**](https://github.com/topics/kernelsu-module) - Community modules

### Kernel Development
- [**Integration Guide**](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) - Adding KernelSU to kernels
- [**KernelSU Source**](https://github.com/tiann/KernelSU/tree/main/kernel) - Kernel driver code
- [**Patches Repository**](https://github.com/tiann/KernelSU/tree/main/kernel) - Required patches

### Building Environment
- **Supported Kernels**: 4.14+ (3.18+ experimental)
- **Required Configs**: `CONFIG_KALLSYMS=y`, `CONFIG_KALLSYMS_ALL=y`
- **Build Tools**: Clang, GCC cross-compiler, AnyKernel3

## Modules & Tools

### Popular KernelSU Modules
- [**SuSFS4KSU**](https://github.com/sidex15/susfs4ksu-module) - Root hiding service
- [**MAGNETAR**](https://github.com/Kyliekyler/MAGNETAR) - Device performance optimizer

### Module Managers
- [**MMRL**](https://github.com/MMRLApp/MMRL) - Modern module manager with repository support
- [**MMRL CLI**](https://github.com/MMRLApp/MMRL-CLI) - Command-line module management

### System Tools
- [**Systemless Hosts**](https://github.com/symbuzzer/systemless-hosts-KernelSU-module) - AdAway compatibility
- [**BindHosts**](https://github.com/bindhosts/bindhosts) - Advanced hosts management

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

### Video Tutorials (Community)
- [**XDA Portal Articles**](https://www.xda-developers.com/tag/kernelsu/) - Installation guides
- [**YouTube Tutorials**](https://www.youtube.com/results?search_query=kernelsu+installation) - Visual guides
- [**Kernel Building Videos**](https://www.youtube.com/results?search_query=kernelsu+kernel+build) - Compilation tutorials

## Related Projects

### Alternative Root Solutions
- [**Magisk**](https://github.com/topjohnwu/Magisk) - Traditional systemless root (54.5k+ ⭐)
- [**APatch**](https://github.com/bmax121/APatch) - KernelPatch-based root solution (6k+ ⭐)
- [**KernelPatch**](https://github.com/bmax121/KernelPatch) - Kernel patching framework

### Compatibility Layers
- [**ZygiskNext**](https://github.com/Dr-TSNG/ZygiskNext) - Standalone Zygisk implementation
- [**ReZygisk**](https://github.com/PerformanC/ReZygisk) - Transparent Zygisk implementation
- [**Shamiko**](https://github.com/LSPosed/LSPosed.github.io/releases) - Magisk hide successor

### Root Detection & Hiding
- [**SuSFS**](https://gitlab.com/simonpunk/susfs4ksu) - Advanced root hiding kernel patches
- [**Tricky Store**](https://github.com/5ec1cff/TrickyStore) - Key attestation bypass

### Development Tools
- [**WSA Builds**](https://github.com/MustardChef/WSABuilds) - Windows Subsystem for Android with root
- [**Android Subsystem for Linux**](https://github.com/RuriOSS/asl) - Linux container on Android
- [**Kernel Assisted Superuser**](https://git.zx2c4.com/kernel-assisted-superuser/about/) - Original concept

## Comparison

### KernelSU vs Alternatives

| Feature | KernelSU | KernelSU-Next | SuKiSu-Ultra | Magisk | APatch |
|---------|----------|---------------|--------------|---------|---------|
| **Kernel Level** | ✅ | ✅ | ✅ | ❌ | ✅ |
| **Module System** | OverlayFS | OverlayFS + Magic Mount | Magic Mount + OverlayFS | Magic Mount | OverlayFS |
| **Kernel Support** | 5.10+ | 4.4-6.6 | 3.4-5.4+ | Any | 3.18-6.1 |
| **Architecture** | arm64, x86_64 | arm64, arm, x86_64 | arm64, arm, x86_64 | All | arm64 |
| **Security Model** | App Profile | App Profile | App Profile | Root Toggle | SuperKey |
| **Hide Capability** | Basic | Advanced | SuSFS | MagiskHide | Kernel-level |
| **Update Method** | Manual | Auto-update | Manual | OTA | Manual |
| **Development** | Active | Active | Active | Active | Active |

### Advantages of KernelSU
- **Superior Security**: Kernel-level operation provides better isolation
- **System Integrity**: Less system modification compared to traditional methods  
- **App Profile System**: Granular permission control per application
- **OverlayFS**: More efficient than bind mounting
- **Future-Proof**: Designed for modern Android security models

## FAQ & Troubleshooting

### Common Questions

**Q: What's the difference between KernelSU and its derivatives?**
- **KernelSU**: Official version, GKI 2.0+ focus, OverlayFS modules
- **KernelSU-Next**: Enhanced fork with broader kernel support and Magic Mount
- **SuKiSu-Ultra**: Non-GKI focused with KPM support and advanced features

**Q: Which version should I choose?**
- **New devices (5.10+ kernel)**: KernelSU official
- **Older devices (4.4-5.4 kernel)**: KernelSU-Next or SuKiSu-Ultra  
- **Legacy devices (3.x kernel)**: SuKiSu-Ultra only

**Q: Is KernelSU safer than Magisk?**
- Yes, kernel-level operation provides better security isolation
- App Profile system offers granular permission control
- Less system modification reduces attack surface

### Troubleshooting

**Bootloop Issues:**
1. Flash stock kernel to recover
2. Check kernel compatibility
3. Verify proper installation method

**Manager Not Working:**
1. Ensure KernelSU is properly installed in kernel
2. Check app signature verification
3. Grant necessary permissions

**Module Issues:**
1. Verify module compatibility
2. Check OverlayFS support
3. Review module logs

**Root Detection:**
1. Use SuSFS modules for advanced hiding
2. Configure App Profile properly
3. Consider hardware attestation bypass

### Getting Help
- Check [official FAQ](https://kernelsu.org/guide/faq.html) first
- Search [GitHub discussions](https://github.com/tiann/KernelSU/discussions)
- Ask in [Telegram group](https://t.me/KernelSU_group)
- Report bugs with debug builds only

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

---

**Made with ❤️ by the KernelSU community**
