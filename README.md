# unsigned code loader for Amlogic bootrom

* https://github.com/frederic/amlogic-usbdl.git
* https://github.com/Raxone/amlogic-usbdl_s905x3.git

## Changes 
* 14.09.2024
* add gxlimg
* fix some script 

## Disclaimer
You will be solely responsible for any damage caused to your hardware/software/warranty/data/cat/etc...

## Description
Amlogic bootrom supports booting from USB. This method of boot requires an USB host to send a signed bootloader to the bootrom via USB port.

This tool exploits a [vulnerability](https://fredericb.info/2021/02/amlogic-usbdl-unsigned-code-loader-for-amlogic-bootrom.html) in the USB download mode to load and run unsigned code in Secure World.

## Supported targets
* X88proX3
* Work with all s905x3 box if usb is not locked or need password.

## Scripts
* all.sh		
* Dump bootloader+dtb+boot
* Convert dtb to dts
* Dump efuse extract bl2 asekey and iv 
* Decrypt bootloader
* Extract u-boot
* Decrypt u-boot
* Decrypt boot 
* Extract bl3xaeskey+kernelaeskes
* Extract asc.bin
* Extract bl33.bin (u-boot_LZ4)
* All files be in dump_all dir.

## Usage
Box must be in usbdl mod.
To put box to usbdl mod with toopick in AV hole on box push button and connect box with USB-A to USB-A cable with PC, keep button pushed (10sec) after connect usb cable with pc.

* git clone https://github.com/Raxone/amlogic-usbdl_s905x3.git

* If board usb password protect, put password file in password folder,and rename to password.bin

* cd amlogic-usbdl_s905x3

* ./scripts/all.sh

* All files be in dump_all dir.

* If board in nonsecured mode

* Only dump boot.bin dtb.bin bootloader.bin efuse.bin and extract dtb.bin to dts.


* If board in secured mode  

* bl2aeskey -Bootloader(BL2) aeskey used for decrypt bootloader.
* bl2aesiv  -Bootloader(BL2) initialization vector(IV)used for decrypt bootloader.bin.
* bl3xaeskey -U-boot aeskey
* kernelaeskey - Kernel aeskey
* bootloader.bin -Dumped main bootloader from box(BL2,FIP,BL3.1,BL33(U-boot)).
* bootloader_dec.bin -Decrypted bootloader.bin
* Extract -u-boot
* Decrypt -u-boot
* Decrypt -boot/kernel
* dtb.bin  -Device tree blob binary 
* dtb_dts  -Device tree blob txt
* root_rsa_keys.sha -sha256 of rootkeys used for encrypt bootloader.
* pattern.secureboot.efuse -pattern burned in efuse from manufacturer to enable secureboot

```
./amlogic-usbdl <input_file> [<output_file>]
	input_file: payload binary to load and execute (max size 65280 bytes)
	output_file: file to write data returned by payload
```

## Payloads
Payloads are raw binary AArch64 executables. Some are provided in directory **payloads/**.

## License
Please see [LICENSE](/LICENSE).
