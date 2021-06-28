# Use Alibaba Cloud Linux 3 images in an on-premises environment

Alibaba Cloud Linux 3 images are available in various formats and have cloud-init built in. This topic describes how to use Alibaba Cloud Linux 3 images in an on-premises environment.

Alibaba Cloud Linux 3 images can be run only on kernel-based virtual machines \(KVMs\). Alibaba Cloud Linux 3 images cannot directly start KVMs. You must configure a boot image.

For example, in this topic, the on-premises operating system is CentOS. Alibaba Cloud Linux 3 is used to create a KVM, and cloud-init is used to initialize the system settings of the KVM. The NoCloud data source is used to create on-premises configuration files. After the configuration files are attached to the KVM as virtual disks, the KVM can be started. For more information about cloud-init, see [Alibaba Cloud \(AliYun\) data source on the official cloud-init website](https://cloudinit.readthedocs.io/en/latest/topics/datasources/aliyun.html?spm=a2c4g.11186623.2.24.1bec3fcaonbql3).

## Step 1: Download an Alibaba Cloud Linux 3 image to your computer

You can download an Alibaba Cloud Linux 3 image to your computer from the [Alibaba Cloud Linux 3 On-premise Image](http://mirrors.aliyun.com/alinux/3/image/) page. Alibaba Cloud Linux 3 images are available in the VHD or qcow2 format.

## Step 2: Obtain the seed.img boot image from your computer

You must configure the network, account, and YUM repository for the boot image. In most cases, the image is named seed.img. You can change the name of the image, but we recommend that you do not.

**Note:** The seed.img image contains only the configuration files that are required to start cloud-init. The image does not contain Alibaba Cloud Linux 3 system files.

You can use one of the following methods to obtain the seed.img image:

-   Go to the [Alibaba Cloud Linux 3 On-premise Image](http://mirrors.aliyun.com/alinux/3/image/) page and click seed.img to download the seed.img image.

    The configuration information in this image cannot be modified, which makes it less ideal for some scenarios. Make sure that you are familiar with the image before you use it.

-   Perform the following operations to manually generate the seed.img image based on the NoCloud data source:

1.  In an on-premises directory, create two configuration files named `meta-data` and `user-data`.

    1.  Create a directory named `seed` and go to the directory.

        ```
        mkdir seed
        cd seed/
        ```

    2.  Create the `meta-data` configuration file.

        The following example shows the content of the configuration file. You can modify the content.

        ```
        #cloud-config
        #vim:syntax=yaml
        
        local-hostname: alinux-host                 
        ```

    3.  Create the `user-data` configuration file.

        The following example shows the content of the configuration file. You can modify the content.

        ```
        #cloud-config
        #vim:syntax=yaml
        
        # Create a user named alinux who is authorized to run sudo commands. 
        users:
          - default
          - name: alinux
            sudo: ['ALL=(ALL)   ALL']
            plain_text_passwd: aliyun
            lock_passwd: false
        
        # Create a YUM repository for Alibaba Cloud Linux 3. 
        yum_repos:
            alinux3-module:
                name: alinux3-module
                baseurl: https://mirrors.aliyun.com/alinux/$releasever/module/$basearch/
                enabled: 1
                gpgcheck: 1
                gpgkey: https://mirrors.aliyun.com/alinux/$releasever/RPM-GPG-KEY-ALINUX-3
            alinux3-updates:
                name: alinux3-updates
                baseurl: https://mirrors.aliyun.com/alinux/$releasever/updates/$basearch/
                enabled: 1
                gpgcheck: 1
                gpgkey: https://mirrors.aliyun.com/alinux/$releasever/RPM-GPG-KEY-ALINUX-3
            alinux3-plus:
                name: alinux3-plus
                baseurl: https://mirrors.aliyun.com/alinux/$releasever/plus/$basearch/
                enabled: 1
                gpgcheck: 1
                gpgkey: https://mirrors.aliyun.com/alinux/$releasever/RPM-GPG-KEY-ALINUX-3
            alinux3-powertools:
                name: alinux3-powertools
                baseurl: https://mirrors.aliyun.com/alinux/$releasever/powertools/$basearch/
                gpgcheck: 1
                enabled: 1
                gpgkey: https://mirrors.aliyun.com/alinux/$releasever/RPM-GPG-KEY-ALINUX-3
            alinux3-os:
                name: alinux3-os
                baseurl: https://mirrors.aliyun.com/alinux/$releasever/os/$basearch/
                gpgcheck: 1
                enabled: 1
                gpgkey: https://mirrors.aliyun.com/alinux/$releasever/RPM-GPG-KEY-ALINUX-3
        ```

2.  Install the `cloud-utils` software package on your on-premises computer.

    ```
    yum install -y cloud-utils
    ```

3.  In the `seed` directory, run the following command to generate the `seed.img` image:

    ```
    cloud-localds seed.img user-data meta-data
    ```


## Step 3: Start the KVM

Start the KVM and use the account information in the `user-data` configuration file to log on to the KVM.

-   Use libvirt to start the KVM.
    1.  Create a configuration file in the XML format on your computer. The sample file is named `alinux3.xml` and contains the following content. You can modify this file based on your requirements.

        ```
        <domain type='kvm'>
            <name>alinux3</name>
            <memory>1048576</memory> <!-- 1 GB of memory -->
            <vcpu>1</vcpu>
            <os>
                <type arch='x86_64'>hvm</type>
                <boot dev='hd'/>
            </os>
            <clock sync="localtime"/>
            <on_poweroff>destroy</on_poweroff>
            <on_reboot>restart</on_reboot>
            <on_crash>restart</on_crash>
            <devices>
                <emulator>/usr/bin/qemu-kvm</emulator><!-- Configure a KVM path based on the operating system. For example, the KVM path for Ubuntu is /usr/bin/kvm. -->
                <disk type='file' device='disk'><!-- Specify the type parameter based on the image format. Set type to qcow2 if the image is in the QCOW2 format, or to vhd if the image is in the VHD format. -->
                    <driver name='qemu' type='qcow2' cache='none' dataplane='on' io='native'/> <!-- If you want to create a snapshot in the qcow2 format, you must disable dataplane. -->
                    <source file='path'/> <!-- Enter the absolute path of the Alibaba Cloud Linux 3 image. -->
                    <target dev='vda' bus='virtio'/>
                </disk>
                <!-- Add the information of seed.img. -->
                <disk type='file' device='disk'>
                    <driver name='qemu' type='raw'/>
                    <source file='/path/to/your/seed.img'/> <!-- Enter the absolute path of seed.img. -->.
                    <target dev='vdb' bus='virtio'/>
                </disk>
                <interface type='network'>
                    <source network='default'/>
                    <model type='virtio'/>
                </interface>
                <console type='pty'>
                    <target type='virtio' port='0'/>
                </console>
                <video>
                    <model type='cirrus' vram='9216' heads='1'/>
                    <alias name='video0'/>
                </video>
                <input type='tablet' bus='usb'/>
                <input type='mouse' bus='ps2'/>
                <graphics type='vnc' port='-1' autoport='yes'/>
            </devices>
        </domain>
        ```

    2.  Run the `virsh` command to start the KVM. Sample command:

        **Note:** By default, libvirt is started by a common user. Make sure that common users have the permissions to manage image files and their paths.

        ```
        virsh define alinux3.xml
        virsh start KVMName    # Enter the actual name of the KVM. 
        ```

-   Run the `qemu-kvm` command to start the KVM. You must append the following parameter information to the command. Set the `file` parameter to the actual absolute path of the seed.img image.

    ```
    -drive file=/path/to/your/seed.img,if=virtio,format=raw
    ```

    For more information about how to configure and manage virtualization, see [Configuring and managing virtualization](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_virtualization/index).

-   Use the graphical interface \(virt-manager\) to start the KVM. Before you start the KVM, find the configuration file of the KVM on your on-premises computer and add the absolute path of the seed.img image to the configuration file.

