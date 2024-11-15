# Resizing Disk Space for Kali Linux on a Dual Boot Laptop

This guide details how I resized the disk space of my Kali Linux installation on a dual-boot system with Windows, using an Ubuntu Live USB to manage the partitioning process. This solution is useful for users running out of space on their Kali Linux partition, particularly in dual-boot scenarios where Windows and Linux share the same disk.

## Repository Description

**Name**: kali-linux-disk-resize

**Short Description**: A detailed guide on resizing the disk space for Kali Linux in a dual-boot setup with Windows, using GParted on an Ubuntu Live USB. Includes steps for creating unallocated space in Windows, booting via a live USB, and extending the Linux partition.

## Prerequisites

- A USB flash drive (at least 8 GB).
- **Rufus** (for creating a bootable USB from an ISO image).
- An **Ubuntu ISO** image.
- Access to **Disk Management** in Windows.
- Basic knowledge of using terminal commands and partition management.

---

## Steps to Resize Disk Space

### 1. Create Unallocated Space in Windows

The first step involves creating unallocated space that will later be used to extend the Kali Linux partition. Follow these steps:

1. **Open Disk Management** in Windows:
   - Press `Win + R`, type `diskmgmt.msc`, and press `Enter`.
2. **Shrink a Volume** to create unallocated space:
   - Identify a partition with sufficient free space (e.g., `E:\` drive).
   - Right-click on the partition and select **Shrink Volume**.
   - Enter the amount of space to shrink. This space will be made available as unallocated space.
3. **Apply** the changes.

### 2. Prepare a Bootable Live USB with Ubuntu

You will need an Ubuntu live environment to use GParted for resizing partitions. Use the following steps to create a bootable USB with Ubuntu:

1. **Download Ubuntu ISO** from [Ubuntu's official website](https://ubuntu.com/download/desktop).
2. **Create a bootable USB** with Rufus:
   - Insert your USB drive.
   - Open **Rufus** and select the Ubuntu ISO you downloaded.
   - Set the **Partition scheme** to `GPT` (depending on your system).
   - Click **Start** to create the bootable USB.

### 3. Boot from the Live USB

1. **Restart your laptop** and enter the BIOS/boot menu:
   - Typically, you can press `F2`, `F12`, `Esc`, or `Del` while the computer boots (this varies by manufacturer).
2. **Select the USB drive** to boot from it.
3. When prompted, select **Try Ubuntu** to run Ubuntu in live mode without installing it on your system.

### 4. Use GParted to Resize the Partition

After booting into Ubuntu, you can use GParted to manage the partitions:

1. **Open a terminal** and install GParted (if it is not already installed):
   ```bash
   sudo apt update
   sudo apt install gparted -y
   ```
2. **Launch GParted**:
   ```bash
   sudo gparted
   ```
3. **Identify the Partitions**:
   - In GParted, you will see a graphical representation of your disk.
   - Locate the unallocated space that you created earlier in Windows.
   - Also, locate the Kali Linux partition that you wish to extend (typically an `ext4` partition).

4. **Move the Unallocated Space**:
   - To extend the Linux partition, the unallocated space must be next to it.
   - If there are partitions between the unallocated space and your Linux partition, right-click and select **Resize/Move** to move them until the unallocated space is adjacent to the Linux partition.

5. **Resize the Linux Partition**:
   - Right-click on the Linux partition (`ext4`) and select **Resize/Move**.
   - Drag the slider or enter the new size to extend the partition into the unallocated space.
   - Click **Resize/Move** and then **Apply** to make the changes.

### 5. Apply Changes and Reboot

1. **Apply the changes** in GParted by clicking the checkmark button.
2. Once the process is complete, **close GParted** and shut down Ubuntu.
3. **Remove the USB** drive and reboot your system.
4. Boot into Kali Linux and verify that the partition has been extended:
   ```bash
   df -h
   ```
   This command will show the updated partition size.

---

## Notes and Precautions

- **Backup Important Data**: Before making any partition changes, ensure all important data is backed up.
- **Use GParted Carefully**: Partitioning errors can lead to data loss or an unbootable system. Double-check all actions before applying changes.
- **Disk Management**: Ensure you understand your disk layout before proceeding to avoid accidental data loss.

---

## Tools Used

- **Windows Disk Management**: To create unallocated space from an existing Windows partition.
- **Rufus**: To create a bootable USB drive with the Ubuntu ISO.
- **Ubuntu Live USB**: Used to run GParted without installing a new OS.
- **GParted**: To manage and resize disk partitions.

## Summary

By following this guide, I successfully resized the Kali Linux partition on my dual-boot system, allowing for more storage space to be allocated to Linux. This process involved creating unallocated space in Windows, booting into a live Ubuntu environment, and using GParted to extend the desired partition.

Feel free to use this guide if you encounter similar storage limitations on your dual-boot setup. Contributions and suggestions are always welcome!

### [Repository Link](#) (Link to be updated once the repository is created)

