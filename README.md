# AMDSata

Patched version of SATA-unsupported.kext to allow macOS to detect SATA controllers used by AMD PCs. Use recommended only if your computer can't read all or some internal disks in macOS.

Known working in:
11.x Big Sur - 15.x Sequoia

May be working in:
10.15 Catalina and older

This kext has no executable, it just consists of an Info.plist file that adds the missing entries for the AMD SATA controller device ID to the macOS AppleAHCIPort driver.

# HOW TO USE
* OpenCore
1. Download the source code by clicking Code and then Download ZIP. You will find the kext in its folder.
2. Copy it to /EFI/OC/Kexts
3. Open config.plist and perform OC Snapshot
4. Save config.plist and close it
5. Boot macOS and the disk should be found

# IF YOUR DISK STILL ISN'T VISIBLE
1. Boot into Windows
2. Open devmgmt.msc
3. Expand "IDE ATA/ATAPI controllers" and open "Standard AHCI SATA controller"
4. Go to the Details tab
5. From the dropdown menu, select Hardware IDs.
6. In the box underneath, you will find a string starting with PCI\VEN_####&DEV_####.
7. Open the kext's Info.plist file and go to the AMD-AHCI-unsupported section under IOKitPersonalities.
8. In this section, open the sub-section called IONameMatch.
9. Change the value of the string called 0. Between "pci" and the comma put the 4 characters that come between VEN_ and the &, and after the comma put the 4 characters that come after DEV_.
10. Save the file and reboot
11. It should work now!

OR
1. On macOS, download Hackintool and open it.
2. Go to the PCIe menu
3. Find the SATA controller. You should be able to find it by the "Device Name" and "Subclass" columns.
4. From the "IOReg IOName" column, copy the value related to the SATA controller.
5. Now open the kext's Info.plist file, and open IOKitPersonalities, then AMD-AHCI-unsupported and finally IONameMatch.
6. Paste the value copied from Hackintool into the "0" string.
7. Save the file and reboot
8. It should work now!

Based on RehabMan's SATA-unsupported.kext.

Note: Create an issue if your controller isn't supported. It'll be very pleasant for me, and I'll add your controller right away!
