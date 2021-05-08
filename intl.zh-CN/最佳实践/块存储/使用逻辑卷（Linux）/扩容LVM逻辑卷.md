---
keyword: [lvm, 逻辑卷, 动态管理, volume]
---

# 扩容LVM逻辑卷

本文介绍了如何通过LVM（Logical Volume Manager）扩容一个逻辑卷LV（Logical Volume），适用于Linux系统ECS实例。

-   您已经创建了一个逻辑卷。详细步骤请参见[创建LVM逻辑卷](/intl.zh-CN/最佳实践/块存储/使用逻辑卷（Linux）/创建LVM逻辑卷.md)。
-   云盘已经在控制台完成扩容，详情请参见[步骤二：在控制台扩容云盘容量](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Linux系统）.md)。本文示例为/dev/vdf扩容了500 GiB。

## 在原云盘上扩容

1.  以root权限远程连接ECS实例。连接方式请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  使用以下命令查看ECS实例中已经创建的逻辑卷LV信息。

    ```
    lvdisplay
    ```

    执行结果如下，表示已经创建了/dev/lvm\_01/lv01逻辑卷，拥有5 TiB物理空间。

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

3.  使用以下命令扩容物理卷PV（Physical Volume），注意将/dev/vdf修改为你要扩容的云盘名称。

    ```
    pvresize /dev/vdf
    ```

    执行结果如下，表示成功扩容物理卷/dev/vdf。

    ```
    root@lvs06:~# pvresize /dev/vdf
      Physical volume "/dev/vdf" changed
      1 physical volume(s) resized or updated / 0 physical volume(s) not resized
    ```

4.  使用以下命令查看物理卷（PV）使用情况。

    ```
    pvs
    ```

    执行结果如下，表示物理卷/dev/vdf已有500 GiB待分配空间。

    ```
    root@lvs06:~# pvs
      PV         VG     Fmt  Attr PSize     PFree
      /dev/vdb   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdc   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdd   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vde   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdf   lvm_01 lvm2 a--  <1024.00g <523.98g
    ```

5.  使用以下命令扩容逻辑卷。

    ```
    lvextend -L +500GB /dev/lvm_01/lv01
    ```

    本示例中变量说明如下，您需要根据实际情况修改。

    -   `+500GB`：增减容量，卷组VG（Volume Group）必须有剩余容量时才可以执行扩容逻辑卷操作。
    -   `/dev/lvm_01/lv01`：逻辑卷名称。
    执行结果如下，表示您为逻辑卷/dev/lvm\_01/lv01扩容了500 GiB物理空间。

    ```
    root@lvs06:~# lvextend -L +500GB /dev/lvm\_01/lv01
    Size of logical volume lvm_01/lv01 changed from5.00 TiB (1310720 extents) to <5.49 TiB (1438720 extents).
    Logical volume lvm_01/lv01 successfully resized.
    ```

6.  使用以下命令扩容逻辑卷文件系统。

    ```
    resize2fs /dev/lvm_01/lv01
    ```

    执行结果如下。

    ```
    root@lvs06:~# resize2fs /dev/lvm\_01/lv01
    resize2fs 1.44.1 (24-Mar-2018)
    Filesystem at /dev/lvm_01/lv01 is mounted on /media/lv01; on-line resizing required
    old_desc_blocks = 640, new_desc_blocks = 703
    The filesystem on /dev/lvm_01/lv01 is now 1473249280 (4k) blocks long.
    ```

7.  使用以下命令查看文件系统扩容结果。

    ```
    df -h
    ```

    执行结果如下，显示逻辑卷的总容量为5.5 TiB，表示扩容成功。

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


**相关文档**  


[创建LVM逻辑卷](/intl.zh-CN/最佳实践/块存储/使用逻辑卷（Linux）/创建LVM逻辑卷.md)

