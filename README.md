# How to compile kernel for Redmi Note 9 Pro (joyeuse)
## Intro
This source code already contains WiFi and Audio drivers that were not included in the original Xiaomi code.
Also, added [AOSP Device Tree Compiler (DTC)](https://android.googlesource.com/platform/external/dtc/+/refs/heads/android10-release) 
to compile DTB and DTBO trees.
### Features
Differences from stock are minimal:
* Removed incompatible architectures
* TTL target support
* Some TCP congestion-avoidance algorithms
* CPU frequency statistics for the schedutil governor
* Various minor changes

## 1. Downloading
Create a working folder, for example `kernel`:
```bash
mkdir kernel
cd kernel
```
Download kernel source:
```bash
git clone --depth=1 https://github.com/tifictive/kernel_joyeuse.git kernel_joyeuse
```
Download a compatible GCC toolchain. I used AOSP GCC 4.9 for 
[arm64](https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/+/refs/heads/android10-release).
```bash
git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 aarch64-linux-android
```
Download Clang toolchain. 
I used [Proton Clang](https://github.com/kdrag0n/proton-clang), you can use another suitable one, for example AOSP Clang.
```bash
git clone https://github.com/kdrag0n/proton-clang.git proton-clang
```
## 2. Building the kernel
Move to the kernel folder:
```bash
cd kernel_joyeuse
```
Setup default config:
```bash
./build.sh custj_defconfig
```
**Note**: `build.sh` - a simple script that sets up environment variables and starts the compilation process.

**Optional**. You can tweak some kernel parameters:
```bash
./build.sh menuconfig
```

Compiling:
```bash
./build.sh
```
## 3. Flashing
If the compilation passed without errors, then in the `arch/arm64/boot` folder you will see the following files:
* `Image.gz` - kernel image
* `dtbo.img` - board-specific device tree overlay
* `dtb` - SoC device tree blob

### Preparation
These files must be flashed into the `boot` section of the phone. To do this, we will use the [AnyKernel3](https://github.com/osm0sis/AnyKernel3) utility.

Download AnyKernel3.zip, unpack and change the following lines in `anykernel.sh` file as shown below:
```
kernel.string=Kernel for Joyeuse
do.devicecheck=1
do.modules=0
do.systemless=1
do.cleanup=1
do.cleanuponabort=0
device.name1=joyeuse

# remove others lines like "device.name*"!

block=/dev/block/bootdevice/by-name/boot;
```
Also remove the lines from `# begin ramdisk changes` to `# end ramdisk changes`.

Place the files `Image.gz`, `dtbo.img` and `dtb` where the script is located and repack all the contents of the folder into a zip archive.

### Flashing
Reboot into recovery mode, backup the `boot` and `dtbo` partitions. Then install our zip archive. Reboot into the system.
