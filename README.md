i.MX95 Venus OS build (Yocto-based)

Custom Embedded Linux build for i.MX95 with Venus OS.
Includes BSP integration, dependency fixes and bootable image.
i.MX95 Venus OS Build
Custom Yocto-based Embedded Linux build for NXP i.MX95 with Venus OS integration.
Overview
This project contains a working Yocto build environment for the UCM-iMX95 platform with Venus OS layers
integrated.
The build includes:
• 
• 
• 
• 
• 
• 
NXP i.MX95 BSP integration
Venus OS layers
Bootable WIC image generation
Debian package management support
Root filesystem fixes
BSP bring-up and dependency fixes
Hardware
Tested platform:
• 
• 
• 
UCM-iMX95
i.MX95 19x19 LPDDR5 EVK configuration
CompuLab evaluation carrier board
Build Environment
Host OS:
• 
Ubuntu Linux (VirtualBox)
Main tools:
• 
• 
• 
• 
Yocto Project
BitBake
NXP BSP
Venus OS meta-layers
1
Repository Structure
conf/                    
meta-victronenergy/      
README.md                -> Yocto configuration-> Venus OS layers-> Project documentation
Main Build Configuration
Machine:
MACHINE ??= "imx95-19x19-lpddr5-evk"
Distribution:
DISTRO ?= "fsl-imx-wayland"
Build threading:
BB_NUMBER_THREADS = "2"
PARALLEL_MAKE = "-j2"
Enter Build Environment
cd ~/imx95-yocto
source sources/poky/oe-init-build-env build-imx95
Build Image
bitbake imx95-venus-minimal-image
2
Output Image Location
Generated images are located in:
build-imx95/tmp/deploy/images/imx95-19x19-lpddr5-evk/
Main output files:
imx95-venus-minimal-image-imx95-19x19-lpddr5-evk.rootfs-*.wic.zst
imx95-venus-minimal-image-imx95-19x19-lpddr5-evk.rootfs-*.wic.bmap
Flashing SD Card
Linux
Decompress image:
unzstd image.wic.zst
Flash using dd:
sudo dd if=image.wic of=/dev/sdX bs=4M status=progress
sync
Windows
The image can be flashed using:
• 
• 
Balena Etcher
Rufus
GitHub Release
Release artifacts are available in:
3
Releases -> v1.0
Included:
• 
• 
bootable .wic.zst image
.wic.bmap metadata file
Known Issues
Current LVDS display bring-up is still under investigation.
Observed:
• 
• 
• 
DRM devices not fully enumerated
No framebuffer device
LVDS pipeline inactive
Camera and Linux system functionality are operational.
Current Status
Working:
• 
• 
• 
• 
• 
Yocto build
BSP integration
Bootable image generation
Camera pipeline
GitHub release workflow
In progress:
• 
• 
LVDS display bring-up
GPU/NPU acceleration validation
License
Internal engineering/integration project
