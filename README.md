# Redmi Note 9 Pro
## NetHunter Kernel by Naster17
### ⚠️ Warning! ⚠️
#### The author is not responsible for your actions! <br>
CAN interface: Regardless of which solution you choose, it is important to keep safety in mind when working with automotive systems. <br>
Make sure you understand all the risks and associated precautions when working with automotive systems.

## 👾 Features 👾
### NetHunter:
  * Fxation TTL
  * Zram & Zswap
  * HackRF, Ubertooth
  * CAN interface [ [What is](https://medium.com/@yogeshojha/car-hacking-101-practical-guide-to-exploiting-can-bus-using-instrument-cluster-simulator-part-i-cd88d3eb4a53) ]
  * Built-in wifi [ monitor, ~~frame~~ ]
  * Work built-in bluetooth [ hci0 ]
  * Added interfaces [ ip_vti0, sit0, ip6tnl0 ]
  * HID functions [ hid, mass_storage, rndis, ... ] 
  * Support RTL8150, RTL8152, RTL8192CU, RTL2830, RTL8192EU, RTL8188EUS, RTL8187[+LEDS], RTL2832[+SDR] <br>
  Compatible: [ [Firmware](https://github.com/rithvikvibhu/nh-magisk-wifi-firmware) ] 
  * Support common bluetooth adapters
  * External drivers supports [ insmod_drivers.zip ]
  * All possible NetHunter functions [ [More](https://www.kali.org/docs/nethunter/) ]

### System:
* CPU governor seted "schedutil" [ default is performance ]
* Added all posible CPU governors [performance, powersave, ondemand, ... ]
* EXT4 and F2FS 
* Disabled logging to reduce performance impact and leaks

<br>

# How to compile kernel for Redmi Note 9 Pro (joyeuse)

## 1. Downloading
Create a working folder, for example `kernel`:
```bash
mkdir kernel
cd kernel
```
Download kernel source:
```bash
git clone --depth=1 https://github.com/Naster17/NetHunter-Kernels/ kernel_joyeuse
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

All config path: arch/arm64/configs/

Setup default config:
```bash
./build.sh custj_defconfig
```
Setup nethunter config: 
```bash
./build.sh nethunter_defconfig
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

Compiling modules (insmod drivers):
```bash
./build_modules.sh
```
After you will see the archive with external drivers. [ InsmodDrivers.zip ]
<br>
Make AnyKernel3.zip:
```bash
./MakeAnyKernel3.sh
```
After you will see the archive. [ NasterKernel.zip ]
<br>
## And now you can flash it via TWRP! 😁
