---
keyword: [virtio, import a custom image, manually install a virtio driver, custom image]
---

# Install a virtio driver

In some scenarios, you may want to use the operating system data of a source server such as a server, virtual machine, or cloud web host to create a custom image, and import the custom image to Alibaba Cloud to create an ECS instance. If the source server is not installed with a virtio driver, the created ECS instance may be unable to be started. To avoid this problem, you must check whether a virtio driver is installed in the source server before you import a custom image to Alibaba Cloud.

You can determine whether to manually install a virtio driver based on the operating system of your source server.

|Operating system|Description|
|----------------|-----------|
|-   Windows Server 2008
-   Windows Server 2012
-   Windows Server 2016
-   Windows Server Version \*\*\*\* \(Semi-Annual Channel\)
-   Windows Server 2019 and later
-   CentOS 6, CentOS 7, CentOS 8, and later
-   Ubuntu 12, Ubuntu 14, Ubuntu 16, Ubuntu 18, and later
-   Debian 7, Debian 8, Debian 9, Debian 10, and later
-   SUSE 11, SUSE 12, SUSE 15, and later

|If the source server runs one of the operating systems listed on the left, when you import a custom image to Alibaba Cloud, Alibaba Cloud automatically adds a virtio driver to the server. You do not need to manually install a virtio driver on the source server before you create the custom image. You must fix the temporary file systems of the servers that are pre-installed with a virtio driver when the temporary file system does not contain the configuration description of the driver. For more information, see [Step 2: Fix the temporary file system](#RecoverTheInitramfs). |
|Other operating systems|If your source server runs a Linux-like operating system that is not included in the preceding list, perform the following steps to install the virtio driver: 1.  [Step 1: Check whether the operating system kernel supports the virtio driver](#Sample)
2.  [Step 2: Fix the temporary file system](#RecoverTheInitramfs)
3.  [Step 3: Download the kernel installation package](#compile)
4.  [Step 4: Compile the kernel](#section_e71_j5s_8ud) |

## Step 1: Check whether the operating system kernel supports the virtio driver

1.  Run the `grep -i virtio /boot/config-$(uname -r)` command to check whether the kernel of the current operating system supports the virtio driver.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4963559951/p4632.png)

    Check the CONFIG\_VIRTIO\_BLK and CONFIG\_VIRTIO\_NET parameters.

    |Check result|Description|
    |------------|-----------|
    |The two parameters do not exist.|The virtio driver is not installed on the operating system and a custom image cannot be directly imported to Alibaba Cloud. You must compile the kernel and install the virtio driver for the source server. For more information, see [Step 3: Download the kernel installation package](#compile) and [Step 4: Compile the kernel](#section_e71_j5s_8ud).|
    |The parameter values are both **m**.|Go to the next step.|
    |The parameter values are both **y**.|The virtio driver is installed on the operating system and a custom image can be directly imported to Alibaba Cloud. For more information, see [Instructions for importing images](/intl.en-US/Images/Custom image/Import images/Instructions for importing images.md) and [Import custom images](/intl.en-US/Images/Custom image/Import images/Import custom images.md).|

2.  Run the `lsinitrd /boot/initramfs-$(uname -r).img | grep virtio` command to check whether the virtio driver is included in the initramfs or initrd temporary file system.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4963559951/p4633.png)

    **Note:**

    -   The preceding figure shows that initramfs contains the virtio\_blk installation file, and the virtio.ko, virtio\_pci.ko, and virtio\_ring.ko dependencies. Therefore, you can directly import your custom images to Alibaba Cloud. For more information, see [Instructions for importing images](/intl.en-US/Images/Custom image/Import images/Instructions for importing images.md) and [Import custom images](/intl.en-US/Images/Custom image/Import images/Import custom images.md).
    -   If initramfs does not contain the virtio\_blk installation file, you must fix the temporary file system before you import custom images to Alibaba Cloud.

## Step 2: Fix the temporary file system

If the check result shows that the kernel of the operating system supports virtio drivers but the initramfs or initrd temporary file system does not contain the virtio\_blk installation file, you must fix the temporary file system. Operating systems such as CentOS are used in the following examples:

-   CentOS/RedHat 5

    ```
    mkinitrd -f --allow-missing \
                --with=xen-vbd  --preload=xen-vbd \
                --with=xen-platform-pci --preload=xen-platform-pci \
                --with=virtio_blk --preload=virtio_blk \
                --with=virtio_pci --preload=virtio_pci \
                --with=virtio_console --preload=virtio_console \
    ```

-   CentOS/RedHat 6/7

    ```
    mkinitrd -f --allow-missing \
                --with=xen-blkfront --preload=xen-blkfront \
                --with=virtio_blk --preload=virtio_blk \
                --with=virtio_pci --preload=virtio_pci \
                --with=virtio_console --preload=virtio_console \
                /boot/initramfs-$(uname -r).img $(uname -r)
    ```

-   Debian/Ubuntu

    ```
    echo -e 'xen-blkfront\nvirtio_blk\nvirtio_pci\nvirtio_console' >> \
    /etc/initramfs-tools/modules
    mkinitramfs -o /boot/initrd.img-$(uname -r)"
    ```


## Step 3: Download the kernel installation package

**Note:** The linux-4.4.24.tar.gz kernel version is used in the following example. You must modify the commands based on the kernel version of your operating system.

1.  Run the `yum install -y ncurses-devel gcc make wget` command to install required components for compiling the kernel.

2.  Run the `uname -r` command to query the kernel version of your operating system. In this example, the kernel version is 4.4.24-2.a17.x86\_64.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4963559951/p4634.png)

3.  Go to the [Index of pub/lunix/kernel/](https://www.kernel.org/pub/linux/kernel/) page to query the download link of the kernel version source code.

    The download link of linux-4.4.24.tar.gz is `https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.4.24.tar.gz` as shown in the following figure.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4963559951/p4638.png)

4.  Run the `cd /usr/src/` command to switch the directory.

5.  Run the `wget https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.4.24.tar.gz` command to download the installation package.

6.  Run the `tar -xzf linux-4.4.24.tar.gz` command to decompress the installation package.

7.  Run the `ln -s linux-4.4.24 linux` command to build a link.

8.  Run the `cd /usr/src/linux` command to switch the directory.


## Step 4: Compile the kernel

1.  Run the following commands in sequence to compile the kernel:

    ```
    make mrproper
    symvers_path=$(find /usr/src/ -name "Module.symvers")
    test -f $symvers_path && cp $symvers_path .
    cp /boot/config-$(uname -r) . /.config
    make menuconfig
    ```

2.  Start to perform virtio-related configurations when the following page is displayed:

    **Note:** If you select the configurations that have the asterisks \(\*\), the virtio driver is directly compiled into the kernel. If you select configurations that have m, the virtio driver is compiled into a module, and then the module is inserted into the kernel when the driver is to start.

    1.  Select Virtualization.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4963559951/p4639.png)

        Select the Kernel-based Virtual Machine \(KVM\) support option.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5963559951/p4640.png)

        ```
        Processor type and features  --->
           [*] Paravirtualized guest support  --->
             --- Paravirtualized guest support
         (128)   Maximum allowed size of a domain in gigabytes
         [*]   KVM paravirtualized clock
         [*]   KVM Guest support
        ```

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5963559951/p4641.png)

        ```
        Device Drivers  --->
          [*] Block devices  --->
         <M>   Virtio block driver (EXPERIMENTAL)
         -*- Network device support  --->
             <M>   Virtio network driver (EXPERIMENTAL)
        ```

    2.  Press the Esc key to exit the kernel configuration window and save the .config file.

    3.  Check whether virtio-related configurations are complete. For more information, see [Step 1: Check whether the operating system kernel supports the virtio driver](#Sample).

    4.  If virtio-related configurations are not complete, run the following commands to manually edit the .config file.

        ```
        make oldconfig
        make prepare
        make scripts
        make
        make install
        ```

    5.  Run the following commands to check the installation status of the virtio driver:

        ```
        find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
        grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
        ```

        If one of the command outputs contains virtio-related files such as virtio\_blk and virtio\_pci.virtio\_console, the virtio driver is installed.


After you install the virtio driver, you can perform the following operations:

-   [Migrate servers](/intl.en-US/Migration Service/Migrate servers.md)
-   [Import custom images](/intl.en-US/Images/Custom image/Import images/Import custom images.md)

