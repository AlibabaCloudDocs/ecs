# 在本地使用Alibaba Cloud Linux 3镜像

Alibaba Cloud Linux 3提供了多种格式的本地镜像，并内置cloud-init。本文介绍如何在本地使用Alibaba Cloud Linux 3镜像。

Alibaba Cloud Linux 3镜像目前只支持KVM虚拟机。镜像本身不可直接启动虚拟机，需要配置引导镜像。

例如，本文示例中，本地环境为CentOS操作系统，使用Alibaba Cloud Linux 3镜像创建了KVM虚拟机，使用cloud-init初始化虚拟机系统设置，然后使用NoCloud数据源在本地建立相关配置文件，以虚拟磁盘的形式挂载到KVM虚拟机中进行设置，并启动虚拟机。cloud-init的相关信息请参见[cloud-init官网 - 阿里云数据源说明文档](https://cloudinit.readthedocs.io/en/latest/topics/datasources/aliyun.html?spm=a2c4g.11186623.2.24.1bec3fcaonbql3)。

## 步骤一：本地下载Alibaba Cloud Linux 3镜像

在本地下载Alibaba Cloud Linux 3镜像，下载地址为[Alibaba Cloud Linux 3 On-premise Image](http://mirrors.aliyun.com/alinux/3/image/)，目前提供vhd与qcow2格式的本地镜像。

## 步骤二：本地生成seed.img引导镜像

该镜像为引导镜像，需要配置网络、账号、YUM源等信息。通常情况下该镜像的名称设置为seed.img，您可以使用其他名称，但不建议您这样做。

**说明：** seed.img镜像只包含cloud-init启动所需要的配置文件，不包含Alibaba Cloud Linux 3系统文件。

您可以通过以下两种方式生成seed.img镜像。

-   Alibaba Cloud Linux 3预先提供了seed.img镜像文件，下载地址为[Alibaba Cloud Linux 3 On-premise Image](http://mirrors.aliyun.com/alinux/3/image/)，在页面列表选择seed.img下载镜像。

    该引导镜像中的配置信息是不可修改的，因此不适用于所有场景。在使用之前请确保您已了解镜像文件的内容。

-   使用NoCloud数据源手动生成seed.img镜像，操作步骤如下。

1.  在本地同一级目录下，创建`meta-data`和`user-data`两个配置文件。

    1.  新建名为`seed`的目录，并进入该目录。

        ```
        mkdir seed
        cd seed/
        ```

    2.  创建`meta-data`配置文件。

        文件内容示例如下，您可以根据需要修改相关配置信息。

        ```
        #cloud-config
        #vim:syntax=yaml
        
        local-hostname: alinux-host                 
        ```

    3.  创建`user-data`配置文件。

        文件内容示例如下，您可以根据需要修改相关配置信息。

        ```
        #cloud-config
        #vim:syntax=yaml
        
        # 添加一个名为alinux的账号，并且可以执行sudo命令。
        users:
          - default
          - name: alinux
            sudo: ['ALL=(ALL)   ALL']
            plain_text_passwd: aliyun
            lock_passwd: false
        
        # 添加Alibaba Cloud Linux 3的YUM源。
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

2.  本地安装`cloud-utils`软件包。

    ```
    yum install -y cloud-utils
    ```

3.  在`seed`目录下，执行以下命令生成`seed.img`镜像。

    ```
    cloud-localds seed.img user-data meta-data
    ```


## 步骤三：启动虚拟机

您可以使用以下任一方式启动KVM虚拟机，成功启动后，使用`user-data`配置文件中的账号信息登录虚拟机。

-   使用libvirt工具启动KVM虚拟机。
    1.  在本地创建一个xml配置文件。示例文件的名称为`alinux3.xml`，内容如下。 您可以依据需求修改xml配置文件。

        ```
        <domain type='kvm'>
            <name>alinux3</name>
            <memory>1048576</memory> <!-- 1 GB内存。 -->
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
                <emulator>/usr/bin/qemu-kvm</emulator><!-- 请根据不同的操作系统设置对应的kvm路径。例如：Ubuntu对应的kvm路径是/usr/bin/kvm -->
                <disk type='file' device='disk'><!-- 请根据镜像格式设置下面的type参数：qcow2对应type='qcow2'、vhd对应type='vpc'。 -->
                    <driver name='qemu' type='qcow2' cache='none' dataplane='on' io='native'/> <!-- 如果要创建qcow2快照，需要关闭dataplane。 -->
                    <source file='path'/> <!-- 填写Alibaba Cloud Linux 3镜像的绝对路径。 -->
                    <target dev='vda' bus='virtio'/>
                </disk>
                <!-- 加入seed.img的信息。 -->
                <disk type='file' device='disk'>
                    <driver name='qemu' type='raw'/>
                    <source file='/path/to/your/seed.img'/> <!-- 填写seed镜像的绝对路径。 -->
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

    2.  使用`virsh`命令启动虚拟机，命令示例如下。

        **说明：** libvirt工具默认使用普通用户启动，请确认镜像文件及所在路径对普通用户是否具有相应的操作权限。

        ```
        virsh define alinux3.xml
        virsh start KVMName    # 请修改为KVM虚拟机的真实名称。
        ```

-   使用`qemu-kvm`命令行启动KVM虚拟机。您需要在命令行中追加如下参数信息，其中`file`参数信息修改为seed.img镜像真实的绝对路径。

    ```
    -drive file=/path/to/your/seed.img,if=virtio,format=raw
    ```

    关于虚拟化配置的更多信息，请参见[Red Hat官方说明](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_virtualization/index)。

-   使用图形界面（virt-manager）启动KVM虚拟机。在启动虚拟机之前，您需要在本地找到KVM虚拟机的配置文件，在文件内添加seed.img镜像文件的绝对路径。

