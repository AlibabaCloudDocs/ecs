---
keyword: [LVM, LV, dynamic management, volume]
---

# Resize an LV

This topic describes how to use Logical Volume Manager \(LVM\) to resize a logical volume \(LV\) on a Linux ECS instance.

-   An LV is created. For more information, see [Create an LV](/intl.en-US/Best Practices/Block Storage/Use LVs for Linux/Create an LV.md).
-   A cloud disk is resized in the console. For more information, see [Step 2: Resize the disk in the ECS console](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md). In this example, /dev/vdf is resized by 500 GiB.

## Procedure

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to view information about the LV that is created on the ECS instance:

    ```
    lvdisplay
    ```

    The following command output shows that the /dev/lvm\_01/lv01 LV is created and has a physical capacity of 5 TiB.

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

3.  Run the following command to resize the PV. Replace /dev/vdf with the name of the cloud disk that you want to resize.

    ```
    pvresize /dev/vdf
    ```

    The following command output shows that the /dev/vdf PV is resized:

    ```
    root@lvs06:~# pvresize /dev/vdf
      Physical volume "/dev/vdf" changed
      1 physical volume(s) resized or updated / 0 physical volume(s) not resized
    ```

4.  Run the following command to view the PV usage:

    ```
    pvs
    ```

    The following command output shows that the /dev/vdf PV has a free space of 500 GiB:

    ```
    root@lvs06:~# pvs
      PV         VG     Fmt  Attr PSize     PFree
      /dev/vdb   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdc   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdd   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vde   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdf   lvm_01 lvm2 a--  <1024.00g <523.98g
    ```

5.  Run the following command to resize the LV:

    ```
    lvextend -L +500GB /dev/lvm_01/lv01
    ```

    The following section describes the variables in this example. You must modify the variables based on your actual needs.

    -   `+500GB`: increases or decreases the capacity. You can resize the LV only when the VG has remaining capacity.
    -   `/dev/lvm_01/lv01`: the name of the LV.
    The following command output shows that the /dev/lvm\_01/lv01 LV is resized by a physical capacity of 500 GiB.

    ```
    root@lvs06:~# lvextend -L +500GB /dev/lvm\_01/lv01
    Size of logical volume lvm_01/lv01 changed from5.00 TiB (1310720 extents) to <5.49 TiB (1438720 extents).
    Logical volume lvm_01/lv01 successfully resized.
    ```

6.  Run the following command to resize the file system of the LV:

    ```
    resize2fs /dev/lvm_01/lv01
    ```

    A command output similar to the following one is displayed:

    ```
    root@lvs06:~# resize2fs /dev/lvm\_01/lv01
    resize2fs 1.44.1 (24-Mar-2018)
    Filesystem at /dev/lvm_01/lv01 is mounted on /media/lv01; on-line resizing required
    old_desc_blocks = 640, new_desc_blocks = 703
    The filesystem on /dev/lvm_01/lv01 is now 1473249280 (4k) blocks long.
    ```

7.  Run the following command to check whether the file system is resized:

    ```
    df -h
    ```

    The following command output shows that the total capacity of the LV is 5.5 TiB, which indicates that the file system is resized.

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
    /dev/mapper/lvm_01-lv01  5.5T   83M  5.2T   1% /media/lv01
    ```


**Related topics**  


[Create an LV](/intl.en-US/Best Practices/Block Storage/Use LVs for Linux/Create an LV.md)

