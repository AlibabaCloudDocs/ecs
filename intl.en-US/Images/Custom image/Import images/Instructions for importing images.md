---
keyword: [cloud migration, impotImage, ECS, Alibaba Cloud, import an image]
---

# Instructions for importing images

Before you import an image, we recommend that you read the following instructions to improve the efficiency of importing images and the availability of imported images.

## Windows Server images

Precautions:

-   Verify the integrity of the file system.
-   Do not modify critical system files.
-   Make sure that the system disk has sufficient free space.
-   Configure the system disk size based on the virtual disk size rather than the image size. The system disk size can be 40 GiB to 500 GiB.
-   Disable the firewall.
-   Allow traffic on RDP port 3389.
-   Make sure that the logon password for the administrator account meets the password complexity requirements. The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /`. The password cannot start with a forward slash \(/\).

Items not supported:

-   ISO images. Before you import ISO images to ECS, use tools such as VirtualBox installed on premises to convert the images to the RAW, VHD, or QCOW2 format.
-   Installation of qemu-ga in images. If qemu-ga is installed, some of the services that ECS requires may be unavailable.
-   Images that run the following operating system versions:
    -   Windows XP
    -   Windows 7
    -   Windows 8
    -   Windows 8.1
    -   Windows 10
-   Installation of a Community Edition virtio driver in Windows Server operating systems. If a Community Edition virtio driver is installed, remove the read-only property of the following files:
    -   C:\\Windows\\System32\\drivers\\netkvm.sys
    -   C:\\Windows\\System32\\drivers\\balloon.sys
    -   C:\\Windows\\System32\\drivers\\vioser.sys
    -   C:\\Windows\\System32\\drivers\\viostor.sys
    -   C:\\Windows\\System32\\drivers\\pvpanic.sys

Items supported:

-   Multi-partition system disks.
-   NTFS file systems, and MBR and GPT partitions.
-   Images in the RAW, QCOW2, or VHD format. If the image to be imported is not in the preceding formats, convert the image to a supported format before you import the image. For more information, see [Convert the image file format](/intl.en-US/Images/Custom image/Import images/Convert the image file format.md).
-   Images that run the following operating system versions:
    -   Microsoft Windows Server 2019
    -   Microsoft Windows Server 2016
    -   Microsoft Windows Server 2012 R2
    -   Microsoft Windows Server 2012
    -   Microsoft Windows Server 2008 R2
    -   Microsoft Windows Server 2008
    -   Windows Server 2003 Service Pack 1 or later

## Linux images

Precautions:

-   Verify the integrity of the file system.
-   Do not modify critical system files such as /sbin, /bin, and /lib\*.
    -   Do not modify /etc/issue\*. Otherwise, the system distribution cannot be identified by ECS, and the system fails to be created.
    -   Do not modify /boot/grub/menu.lst. Otherwise, the ECS instance cannot be started.
    -   Do not modify /etc/fstab. Otherwise, the exception partition cannot be loaded and ECS instances cannot be started.
    -   Do not set /etc/shadow to **read-only**. Otherwise, the password file cannot be modified, and the system fails to be created.
    -   Do not modify /etc/selinux/config to enable SELinux. Otherwise, the system cannot be started. If you must enable SELinux, see [Enable or disable SELinux](/intl.en-US/Best Practices/Security/Enable or disable SELinux.md).
-   Make sure that the system disk has sufficient free space.
-   Disable the firewall.
-   Allow traffic on SSH port 22.
-   Enable Dynamic Host Configuration Protocol \(DHCP\).
-   Install XEN or KVM virtualization drivers. For more information, see [Install a virtio driver](/intl.en-US/Images/Custom image/Import images/Install a virtio driver.md).
-   Install cloud-init to configure the hostname, NTP source, and YUM source. For more information, see [Install cloud-init](/intl.en-US/Images/Custom image/Import images/Install cloud-init.md).
-   Make sure that the logon password for the root account meets the password complexity requirements. The password must be 8 to 30 characters in length and must contain three of the following character types: lowercase letters, uppercase letters, digits, and special characters. Special characters include `( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /`.

Items not supported:

-   ISO images. Before you import ISO images to ECS, use tools such as VirtualBox installed on premises to convert the images to the RAW, VHD, or QCOW2 format.
-   Multiple network interfaces.
-   IPv6 addresses.
-   Adjustment of system disk partitions. Only disks with a single root partition are supported.
-   Installation of qemu-ga in images. If qemu-ga is installed, some of the services that ECS requires may be unavailable.

Items supported:

-   Images in the RAW, QCOW2, or VHD format. If the image to be imported is not in the preceding formats, convert the image to a supported format before you import the image. For more information, see [Convert the image file format](/intl.en-US/Images/Custom image/Import images/Convert the image file format.md).
-   MBR and GPT partitions as well as XFS, ext3, and ext4 file systems.
-   However, the ext4 file system cannot contain the `64bit` feature, and the `project` and `quota` features cannot be used together. You can run the following command to view the list of features contained in the ext4 file system:

    ```
    tune2fs -l <ext4 file system disk directory\> | grep features
    ```

-   Images that run the following operating system versions:
    -   Alibaba Cloud Linux
    -   CentOS 5/6/7/8
    -   Debian 6/7/8/9/10
    -   FreeBSD
    -   OpenSUSE 13/42/15
    -   RedHat
    -   Red Hat Enterprise Linux \(RHEL\)
    -   SUSE Linux 10/11/12/15
    -   Ubuntu 10/12/13/14/16/18/20
    -   CoreOS 681.2.0+

## Non-standard Linux images

Linux images that are not listed as ECS public images are considered non-standard images. Non-standard images are developed on a standard OS platform, but none of their critical system configuration files, basic system environments, or applications comply with ECS requirements for a standard operating system. If you want to use a non-standard image, select one of the following image types and perform corresponding operations:

-   Others Linux: ECS identifies all images of this type as other Linux systems. If you import an Others Linux image and then use it to create instances, ECS does not process the created instances. If DHCP is disabled in the Others Linux image, you must connect to the instances by using the remote connection feature in the ECS console, and then manually configure IP addresses, routes, and passwords for the instances. If DHCP is enabled in the Others Linux image, networks are automatically configured for the instances when you log on to the instances.
-   Customized Linux: After a customized Linux image is imported, you can create instances from this image and configure networks and passwords for the instances in the same way as you do with instances created from standard ECS images. For more information, see [Customize Linux images](/intl.en-US/Images/Custom image/Import images/Customize Linux images.md).

