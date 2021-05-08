---
keyword: [lvm, 逻辑卷, 动态管理, 数据库, volume]
---

# 创建LVM逻辑卷

本文介绍了如何使用多块云盘创建一个逻辑卷管理LVM（Logical Volume Manager），适用于Linux系统ECS实例。

您已经创建并挂载了多块云盘，具体操作请参见[创建云盘](/intl.zh-CN/块存储/云盘/创建云盘/创建云盘.md)和[挂载数据盘](/intl.zh-CN/块存储/云盘/挂载数据盘.md)。

LVM是Linux系统ECS实例的一种管理硬盘分区机制，最大的特点是可以动态管理硬盘。LVM在硬盘和分区之上建立一个逻辑层，提高了硬盘分区管理的灵活性。 逻辑卷的大小可以动态调整，而且不会丢失现有数据。即使您新增了数据盘，也不会改变现有的逻辑卷。

**说明：** 快照只能备份单块云盘数据，使用LVM后，回滚云盘时会造成数据差异。

本文中，LVM配置示意图如下所示。

![lvm和云盘](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8640770061/p169254.png)

## 步骤一：创建物理卷

1.  以root权限远程连接ECS实例。连接方式请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  使用以下命令查看ECS实例上所有云盘信息。

    ```
    lsblk
    ```

    回显信息如下所示，则您可以使用五块云盘通过LVM创建弹性可扩展的逻辑卷。

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

3.  使用以下命令创建物理卷PV（Physical Volume）。

    ```
    pvcreate <数据盘设备名称1> ... <数据盘设备名称N>
    ```

    如果您需要添加多块数据盘，则可以添加多个数据盘设备名称，设备名称之间以空格间隔。

    ```
    root@lvs06:~# pvcreate /dev/vdb /dev/vdc /dev/vdd /dev/vde /dev/vdf
      Physical volume "/dev/vdb" successfully created.
      Physical volume "/dev/vdc" successfully created.
      Physical volume "/dev/vdd" successfully created.
      Physical volume "/dev/vde" successfully created.
      Physical volume "/dev/vdf" successfully created.
    ```

4.  使用以下命令查看ECS实例已经创建的物理卷（PV）信息。

    ```
    lvmdiskscan
    ```

    执行结果如下所示。

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


## 步骤二：创建卷组

1.  使用以下命令创建卷组VG（Volume Group）。

    ```
    vgcreate <卷组名> <物理卷名称1>……<物理卷名称N>
    ```

    如果您需要添加多块物理卷，则可以添加多个物理卷名称，名称之间以空格间隔。卷组名由您自定义名称，假设为lvm\_01。

    ```
    root@lvs06:~# vgcreate lvm\_01 /dev/vdb /dev/vdc /dev/vdd /dev/vde /dev/vdf
      Volume group "lvm_01" successfully created
    ```

2.  使用以下命令向卷组中添加物理卷。

    ```
    vgextend 卷组名称  <物理卷名称1>……<物理卷名称N>
    ```

    例如向卷组lvm\_01中添加新的物理卷，执行结果如下所示。

    ```
    root@lvs06:~# vgextend lvm\_01 /dev/vdb /dev/vdc /dev/vdd /dev/vde /dev/vdf
      Volume group "lvm_01" successfully extended
    ```

3.  使用以下命令查看卷组信息。

    ```
    vgs
    ```

    执行结果如下所示。

    ```
    root@lvs06:~# vgs
      VG     #PV #LV #SN Attr   VSize  VFree
      lvm_01   600 wz--n- <6.00t <6.00t
    ```


## 步骤三：创建逻辑卷

1.  使用以下命令创建逻辑卷LV（Logical Volume）。

    ```
    lvcreate [-L <逻辑卷大小>][ -n <逻辑卷名称>] <卷组名称>
    ```

    **说明：**

    -   逻辑卷大小：逻辑卷的大小应小于卷组（VG）剩余可用空间，容量单位支持M、G或者T。
    -   逻辑卷名称：由您自定义。
    -   卷组名称：已经创建的卷组的名称。
    例如创建一个5 TiB的逻辑卷（LV），执行结果如下所示。

    ```
    root@lvs06:~# lvcreate -L 5T -n lv01 lvm\_01
      Logical volume "lv01" created.
    ```

2.  使用以下命令查看逻辑卷详细信息。

    ```
    lvdisplay
    ```

    执行结果如下所示。

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


## 步骤四：创建并挂载文件系统

1.  使用以下命令在逻辑卷（LV）上创建文件系统。

    ```
    mkfs.<文件系统格式> <逻辑卷路径>
    ```

    例如创建一个ext4文件系统，执行结果如下所示。

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

2.  创建挂载点，例如/media/lv01。

    您也可以将云盘挂载到已有目录下。

    ```
    mkdir /media/lv01
    ```

3.  使用以下命令挂载文件系统。

    本示例中，逻辑卷路径为/dev/lvm\_01/lv01，挂载点为/media/lv01，您需要根据实际情况修改。

    ```
    mount /dev/lvm_01/lv01 /media/lv01
    ```

4.  使用以下命令查看逻辑卷的挂载信息。

    ```
    df -h
    ```

    执行结果如下所示。

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


**相关文档**  


[扩容LVM逻辑卷](/intl.zh-CN/最佳实践/块存储/使用逻辑卷（Linux）/扩容LVM逻辑卷.md)

