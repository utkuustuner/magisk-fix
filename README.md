## Magisk Channels
I created this repo because magisk deprecated recovery method for huawei devices. I know, both magisk and huawei is irrelevant to developers at this point. But still, I want to dictate when my device dies not someone else. I make use of custom channel url feature in magisk manager to select which version to patch boot/recovery image with. If you want to use these channels get the raw .json url and paste it into custom channel url section in magisk manager settings. After refreshing main page it'll fetch the version written inside the .json. Channels with "official" prefix gets original files and hashes from [topjohnwu/Magisk](https://github.com/topjohnwu/Magisk). "a10" and "debug" prefixed ones have modified versions (hosted in this repo) so use them on your own discretion. 

**For A11 I recommend trying these versions in order**

latest official → official-channel-21.2 → debug-channel-21.1

**For A10 I recommend trying these versions in order**

latest official → official-channel-20.4 → a10-channel-20.2 → a10-channel-20.3

**Keep these version limits in mind**
- 22.0 = end of official huawei support (refer to [Magisk-Phh/Releases](https://github.com/Magisk-Phh/Releases) for future a-only builds)
- 21.0 is minimum for Magisk Manager v8.0.7 (use v7.5.1 for anything below)
- 21.0 is minimum for android 11
- 19.4 is minimum for android 10 on a-only devices,
- 19.0 is minimum for android 10,
- 18.1 is minimum for huawei devices running emui 9

As a side note, versions after 21.2 have some changes that makes apps recognize device arch as **armvl8** instead of **aarch64**. You'll care about this if you're running a chroot environment inside android.


As official huawei section got removed from magisk's install documentation, I'll leave the updated version of it down below.

## Huawei
Magisk no longer officially support modern Huawei devices as the bootloader on their devices are not unlockable, and more importantly they do not follow standard Android partitioning schemes. The following are just some general guidance.

Huawei devices using Kirin processors have a different partitioning method from most common devices. Magisk is usually installed to the `boot` partition of the device, however Huawei devices do not have this partition. To install it anyway:

- After downloading your firmware zip (you may find a lot in [Huawei Firmware Database](http://pro-teammt.ru/firmware-database/) and [AndroidHost.ru](https://androidhost.ru/search.html)), you have to extract images from `UPDATE.APP` in the zip with [Huawei Update Extractor](https://forum.xda-developers.com/showthread.php?t=2433454) (Windows only!)
  - If you device is EMUI9 then you can use TWRP image instead of stock `RECOVERY_RAMDIS.img`
- Regarding patching images:
  - If your device is EMUI8 then it does have boot ramdisk, patch `RAMDISK.img` instead of `boot.img` *(Do **NOT** tick recovery mode!)*
  - If your device is EMUI9 then it does **NOT** have boot ramdisk, patch `RECOVERY_RAMDIS.img` (this is not a typo) instead of `recovery.img` *(Tick recovery mode!)*
- Regarding flashing the image back with `fastboot`
  - If you patched `RAMDISK.img`, flash with command `fastboot flash ramdisk magisk_patched.img`
  - If you patched `RECOVERY_RAMDIS.img`, flash with command `fastboot flash recovery_ramdisk magisk_patched.img`
- Special Case for EMUI 9
  - (Normal Boot) → (System without Magisk)
  - (Recovery Key Combo) → (Splash screen) → (Release all buttons) → (System with Magisk)
  - (Recovery Key Combo) → (Splash screen) → (Keep pressing volume up) → (Recovery Mode) *Might not work on some devices*
