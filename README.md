# Solution to fix boot error after enabling VMD

If you are not able to boot after enabling VMD in BIOS, this is due to VMD driver not being included in the boot image and not loaded upon boot.
This results the system cannot recognize the boot drive and causing the blue screen of not finding boot drive.
The solution is to inject the VMD driver into our original boot image to achieve the same purpose as in https://www.intel.com/content/www/us/en/support/articles/000058724/memory-and-storage/intel-optane-memory.html

1. grab a f6vmdflpy-x64 from the computer manufacturer e.g. https://download.msi.com/nb_drivers/imsm/F6_RST_PV_19.5.1.1040.3_SV2_SV1_Win10_19.5.1.1040_0x21dc22f8.zip
2. copy the F6_RST_PV_19.5.1.1040.3_SV2_SV1_Win10_19.5.1.1040 folder for example to a USB and plug in during next boot
3. boot into recovery screen and choose to use command prompt
4. follow the answer in https://superuser.com/questions/1117591/access-entire-c-drive-from-x-source-boot to locate:
    a) The drive letter of your original C: Windows partition (e.g. E:)
    b) The drive letter of your USB loaded with the driver (e.g. D:)
5. once we know the drive letters in the current command prompt session, use the following command:
       DISM /Image:E:\ /Add-Driver /driver:D:\F6_RST_PV_19.5.1.1040.3_SV2_SV1_Win10\ /recurse
6. wait for indication of completion and reboot

references:
https://gist.github.com/TomCan/9644966
https://learn.microsoft.com/en-us/answers/questions/1151478/install-intel-vmd-driver-into-windows-10-system-af
