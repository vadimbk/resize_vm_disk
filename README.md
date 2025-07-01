# expand-lvm-disk

A minimalistic script to automatically expand the root LVM volume in a Debian/Ubuntu virtual machine after increasing the virtual disk size.

## Description

This script resizes the last partition on `/dev/sda`, updates the partition table, resizes the LVM physical volume, extends the root logical volume, and grows the filesystem (ext4 or xfs). It also reduces the reserved space on ext4 filesystems to 1% for maximum usable capacity.

## Prerequisites

- Debian 10/11/12 or Ubuntu 18.04+.
- The root filesystem must reside on LVM in the last partition of `/dev/sda`.
- Root privileges.

## Usage

1. Increase the size of your VM disk in your hypervisor (e.g., Proxmox, VMware, VirtualBox).
2. Copy the script to your VM:
    ```bash
    chmod +x expand-lvm-disk.sh
    sudo ./expand-lvm-disk.sh
    ```
3. The script will:
    - Resize the last partition to use the full disk size.
    - Update the kernel partition table.
    - Resize the LVM physical volume.
    - Extend the root logical volume to use all available space.
    - Resize the root filesystem.

4. Verify the new available space:
    ```bash
    df -h
    ```

## Limitations

- The script only supports VMs using `/dev/sda` with root on LVM in the last partition.
- It does not support complex setups with multiple disks, encrypted partitions, or separate /boot partitions outside of the LVM.
- Always back up important data before resizing disks.

## Disclaimer

Use at your own risk. The author assumes no responsibility for data loss or system issues resulting from the use of this script.
