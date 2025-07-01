# expand-lvm-disk

This script automatically expands the root LVM disk in a Debian/Ubuntu virtual machine **after increasing the disk size in your hypervisor or control panel**.

## Description

expand-lvm-disk resizes the last partition on `/dev/sda`, updates the partition table, resizes the LVM physical volume, extends the root logical volume, and grows the filesystem (ext4 or xfs). It also reduces reserved blocks on ext4 filesystems to 1% to maximize usable disk space.

## Prerequisites

- Debian 10/11/12 or Ubuntu 18.04 or later.
- Root filesystem on LVM in the last partition of `/dev/sda`.
- Root privileges.

## Usage

1. **Increase the size of your VM disk in your hypervisor/control panel.**
2. Upload the script to your VM.
3. Make it executable:
    ```bash
    chmod +x expand-lvm-disk
    ```
4. Run the script as root:
    ```bash
    sudo ./expand-lvm-disk
    ```
5. Verify the new disk space:
    ```bash
    df -h
    ```

## Limitations

- Only works with `/dev/sda` where the root filesystem resides on LVM in the last partition.
- Does not support complex partition layouts, multiple disks, encrypted volumes, or separate non-LVM root filesystems.
- Always create a backup before modifying disk partitions.

## Disclaimer

Use this script at your own risk. The author assumes no responsibility for data loss or system issues resulting from its use.
