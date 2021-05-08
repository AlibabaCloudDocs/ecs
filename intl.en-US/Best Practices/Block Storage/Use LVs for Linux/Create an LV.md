---
keyword: [LVM, LV, dynamic management, database, volume]
---

# Create an LV

This topic describes how to use multiple cloud disks to create a logical volume \(LV\) on a Linux ECS instance.

Multiple cloud disks are created and attached to an ECS instance. For more information, see [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md) and [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

Logical Volume Manager \(LVM\) is a disk partition management mechanism for Linux ECS instances and features dynamic management of hard disks. In this mechanism, a logical layer is created on hard disks and partitions to help you manage hard disks and partitions in a more flexible manner. You can dynamically adjust the LV size without losing existing data. The existing LV remains unchanged even if you add new data disks.

**Note:** A snapshot backs up only the data of a single cloud disk. When LVM is used, data differences may occur when you roll back cloud disks.

## Step 1: Create a PV

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to view information about all cloud disks on the ECS instance:

    ```
    lsblk
    ```

    If the following information is displayed, you can use five cloud disks to create a resizable LV by using LVM.

    ```
    root@lvs06:~# lsblk
    NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    vda    252:0040G  0 disk
    └─vda1 252:1040G  0 part /
    vdb    252:1601T  0 disk
    vdc    252:3201T  0 disk
    vdd    252:4801T  0 disk
    vde    252:6401T  0 disk
    vdf    252:8001T  0 disk
    ```

3.  Run the following command to create a physical volume \(PV\):

    ```
    pvcreate <Device name of data disk 1> ... <Device name of data disk N>
    ```

    If you want to add multiple data disks, you can add multiple device names. Separate multiple names with spaces.

    ```
    root@lvs06:~# pvcreate /dev/vdb /dev/vdc /dev/vdd /dev/vde /dev/vdf
      Physical volume "/dev/vdb" successfully created.
      Physical volume "/dev/vdc" successfully created.
      Physical volume "/dev/vdd" successfully created.
      Physical volume "/dev/vde" successfully created.
      Physical volume "/dev/vdf" successfully created.
    ```

4.  Run the following command to view information about the created PV on the ECS instance:

    ```
    lvmdiskscan
    ```

    A command output similar to the following one is displayed:

    ```
    root@lvs06:~# lvmdiskscan \| grep LVM
      /dev/vdb  [       1.00 TiB] LVM physical volume
      /dev/vdc  [       1.00 TiB] LVM physical volume
      /dev/vdd  [       1.00 TiB] LVM physical volume
      /dev/vde  [       1.00 TiB] LVM physical volume
      /dev/vdf  [       1.00 TiB] LVM physical volume
      5 LVM physical volume whole disks
      0 LVM physical volumes
    ```


## Step 2: Create a VG

1.  Run the following command to create a volume group \(VG\):

    ```
    vgcreate <VG name> <Name of PV 1> ...... <Name of PV N>
    ```

    If you want to add multiple PVs, you can add multiple PV names. Separate multiple names with spaces. You can customize the VG name. Example: lvm\_01.

    ```
    root@lvs06:~# vgcreate lvm\_01 /dev/vdb /dev/vdc /dev/vdd /dev/vde /dev/vdf
      Volume group "lvm_01" successfully created
    ```

2.  Run the following command to add a PV to the VG:

    ```
    vgextend VG name  <Name of PV 1> ...... <Name of PV N>
    ```

    The following command output shows that a PV is added to the lvm\_01 VG:

    ```
    root@lvs06:~# vgextend lvm\_01 /dev/vdb /dev/vdc /dev/vdd /dev/vde /dev/vdf
      Volume group "lvm_01" successfully extended
    ```

3.  Run the following command to view the VG information:

    ```
    vgs
    ```

    A command output similar to the following one is displayed:

    ```
    root@lvs06:~# vgs
      VG     #PV #LV #SN Attr   VSize  VFree
      lvm_01   600 wz--n- <6.00t <6.00t
    ```


## Step 3: Create an LV

1.  Run the following command to create an LV:

    ```
    lvcreate [-L <LV size>][ -n <LV name>] <VG name>
    ```

    **Note:**

    -   LV size: The LV size must be smaller than the free space of the VG. The unit can be MiB, GiB, or TiB.
    -   LV name: You can customize the name.
    -   VG name: the name of an existing VG.
    The following command output shows that a 5 TiB LV is created:

    ```
    root@lvs06:~# lvcreate -L 5T -n lv01 lvm\_01
      Logical volume "lv01" created.
    ```

2.  Run the following command to view the LV details:

    ```
    lvdisplay
    ```

    A command output similar to the following one is displayed:

    ```
    root@lvs06:~# lvdisplay
      --- Logical volume ---
      LV Path                /dev/lvm_01/lv01
      LV Name                lv01
      VG Name                lvm_01
      LV UUID                svB00x-l6Ke-ES6M-ctsE-9P6d-dVj2-o0h***
      LV Write Access        read/write
      LV Creation host, time lvs06, 2019-06-0615:27:19 +0800
      LV Status              available
      # open                 0
      LV Size                5.00 TiB
      Current LE             1310720
      Segments               6
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     256
      Block device           253:0
    ```


## Step 4: Create and mount a file system

1.  Run the following command to create a file system on the LV:

    ```
    mkfs. <File system format> <LV path>
    ```

    The following command output shows that an ext4 file system is created:

    ```
    root@lvs06:~# mkfs.ext4 /dev/lvm\_01/lv01
    mke2fs 1.44.1 (24-Mar-2018)
    Creating filesystem with13421772804k blocks and 167772160 inodes
    Filesystem UUID: 2529002f-9209-4b6a-9501-106c1145c***
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
            102400000, 214990848, 512000000, 550731776, 644972544
    
    Allocating group tables: done
    Writing inode tables: done
    Creating journal (262144 blocks): done
    Writing superblocks and filesystem accounting information:
    done
    ```

2.  Create a mount point. Example: /media/lv01.

    You can also use an existing mount point.

    ```
    mkdir /media/lv01
    ```

3.  Run the following command to mount the file system:

    In this example, the LV path is /dev/lvm\_01/lv01, and the mount point is /media /lv01. You can modify the LV path and mount point based on your actual needs.

    ```
    mount /dev/lvm_01/lv01 /media/lv01
    ```

4.  Run the following command to check whether the file system is mounted on the LV:

    ```
    df -h
    ```

    A command output similar to the following one is displayed:

    ```
    root@lvs06:~# df -h
    Filesystem               Size  Used Avail Use% Mounted on
    udev                      12G     012G   0% /dev
    tmpfs                    2.4G  3.7M  2.4G   1% /run
    /dev/vda1                 40G  3.6G   34G  10% /
    tmpfs                     12G     0   12G   0% /dev/shm
    tmpfs                    5.0M     05.0M   0% /run/lock
    tmpfs                     12G     012G   0% /sys/fs/cgroup
    tmpfs                    2.4G     02.4G   0% /run/user/0
    /dev/mapper/lvm_01-lv01  5.0T   89M  4.8T   1% /media/lv01
    ```


**Related topics**  


[Resize an LV](/intl.en-US/Best Practices/Block Storage/Use LVs for Linux/Resize an LV.md)

