# AMD-SATA-Controller-Ryzentosh

Patched version of SATA-unsupported.kext to allow macOS to detect AMD SATA controller and disks connected to it. Use recommended only if your computer can't read internal disks when in macOS.

Known working in:
11.x Big Sur - 13.x Ventura

May be working in:
10.13 High Sierra, 10.14 Mojave, 10.15 Catalina, 14.x Sonoma

# HOW TO USE
* OpenCore
1. Download kext
2. Copy it to /EFI/OC/Kexts
3. Open config.plist and perform OC Clean Snapshot
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
9. Change the value of the string called 0. Between "pci" and the comma put what comes between VEN_ and the &, and after the comma put what comes after DEV_.
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
