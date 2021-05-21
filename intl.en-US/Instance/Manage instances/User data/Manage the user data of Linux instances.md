# Manage the user data of Linux instances

This topic describes how to prepare user data for Linux instances and how to pass in user data and verify the result of running the user data.

If you want to modify the user data of an instance, the instance is in the **Stopped** state.

The user data feature for Linux instances uses the open source cloud-init architecture. After you pass user data into an instance by using the console or by calling an API operation, you can view the user data content by using the metadata of the instance. Metadata is also used for cloud-init to automatically configure Linux instances. When an instance starts, the system uses the administrator or root permissions to run user data.

The following limits apply to user data:

-   The user data feature is supported only for instances that reside in virtual private clouds \(VPCs\).
-   The instances must be created from the following public images or custom images derived from public images:
    -   Alibaba Cloud Linux, CentOS, Ubuntu, SUSE Linux Enterprise, OpenSUSE, and Debian
    -   Windows Server 2008 R2 and later
-   The user data feature is supported for all available instance types. For retired instance types, the user data feature is supported only for I/O-optimized instances. For more information, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).
-   The user data that you want to run must be encoded in Base64. The size of the user data cannot exceed 16 KB before it is encoded.

    **Note:** You can enter the user data that has not been encoded in Base64 in the console. The console automatically encodes the user data in Base64. If you do not want to enter the user data in the console, you must encode it in Base64 on your own.


## Procedure

1.  Prepare user data.

    You can run various scripts to prepare user data of Linux instances. For more information about the characteristics of different scripts and their examples, see the following sections:

    -   [User-data scripts](#section_lu5_puw_zsj)
    -   [Cloud-config data](#section_7gb_rtg_ouq)
    -   [Include files](#section_t34_b33_6gz)
    -   [Gzip compressed content](#section_esq_lq8_ra7)
    -   [Upstart job scripts](#section_7ug_631_wrv)
    **Note:** If you want to use include files or gzip compressed content, you must upload script files to available storage services, obtain the links, and set the validity period for the links. We recommend that you use Alibaba Cloud Object Storage Service \(OSS\). For more information, see [Upload objects](/intl.en-US/Quick Start/OSS console/Upload objects.md) and [Configure lifecycle rules](/intl.en-US/Console User Guide/Manage buckets/Basic settings/Configure lifecycle rules.md). You can also learn more about the ways to prepare user data from the cloud-init documentation. For more information, see [User-Data Formats](http://cloudinit.readthedocs.io/en/latest/topics/format.html).

2.  Pass the user data into the instance.

    -   Pass in the user data when you create the instance: In the **System Configurations \(Optional\)** step, click **Advanced** to show the parameters and enter the user data in the **User Data** section. If the user data is encoded in Base64, select **Enter Base64 Encoded Information**.

        The following figure shows an example on how to write the system time to a specified file when the instance starts for the first time.

        ![createinstance-userdata](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7276941261/p271700.png)

    -   Modify the user data of an existing instance: On the **Instances** page, find the instance for which you want to modify the user data and choose **More** \> **Instance Settings** \> **Set User Data**. In the Set User Data dialog box, enter new user data in the **User Data** section.

        **Note:** If you want to start a pay-as-you-go instance immediately after you modify the user data of the instance, we recommend that you set the stop mode of the instance to **Keep Instances and Continue Billing**.

        The following figure shows an example on how to write the system time to a specified file on each instance startup.

        ![modifyinstance-userdata](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8276941261/p271925.png)

        After the user data is modified for a Linux instance, whether new user data is run when the instance is started depends on the type of the script and the type of the module. Examples:

        -   User-data scripts are not run.
        -   Cloud-config data is not run if modules such as Byobu and Set Passwords are configured.
        -   Cloud-config data is run if modules such as Bootcmd, Update Etc Hosts, and Yum Add Repo are configured.
        For information about the characteristics of the modules, see the module frequency line of each module in [Modules](http://cloudinit.readthedocs.io/en/latest/topics/modules.html)

3.  View the content passed into the instance and the result of running the script.

    1.  Connect to the instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

    2.  View the content by using the metadata of the instance.

        ```
        curl http://100.100.100.200/latest/user-data
        ```

        In this example, the user data that is passed in in [Step 2](#step_7v1_zjw_1b8) is used as an example. If the user data is included in the output, the user data is passed in, as shown in the following figure.

        ![view-user-data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8276941261/p272240.png)

    3.  View the running result.

        The result of running a script is related to its content. The following figure shows an example of the result of writing content to the specified file.

        ![view-result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8276941261/p272241.png)


## User-data scripts

User-data scripts are directly executed as shell scripts after they are passed into Linux instances. User-data scripts have the following characteristics:

-   The first line starts with `#!`.
-   User-data scripts are run once only when the instance starts for the first time.

Example:

```
#!/bin/sh
echo "Hello World. The time is now $(date -R)!" | tee /root/userdata_test.txt
```

The example user-data script can be run to write the system time to the userdata\_test.txt file when the instance starts for the first time.

## Cloud-config data

Cloud-config data is a convenient way to configure services such as YUM source update, SSH key import, and instance dependency installation. Cloud-config data has the following characteristics:

-   The first line starts with `#cloud-config`, and the header cannot have spaces.
-   The script must follow the YAML syntax.
-   The running frequency of the user data varies based on the modules that you configure. For example, if you configure the Apt Configure module, the user data is run only once for each instance. If you configure the Bootcmd module, the user data is run each time the instance starts.

Example:

```
#cloud-config
apt:
primary:
- arches: [default]
uri: http://us.archive.ubuntu.com/ubuntu/
bootcmd:
- echo "Hello World. The time is now $(date -R)!" | tee /root/userdata_test.txt
```

The example cloud-config data can be run to modify the default software source and write the latest system time to the userdata\_test.txt file each time the instance starts.

## Include files

An include file contains one or more script links, one per line. When the instance starts, cloud-init reads each script link and its content. If an error occurs while a script is being read, the remaining scripts are not read. Include files have the following characteristics:

-   The first line starts with `#include`, and the header cannot have spaces.
-   The size of each script cannot exceed 16 KB before it is encoded in Base64.
-   The running frequency of the user data varies based on the types of scripts and modules.

Example:

```
#include
http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/userdata/myscript.sh
```

The example include file contains a script link. The running frequency is determined by the type of the script. For example, if the script is a user-data script, the script is run once only when the instance starts for the first time.

## Gzip compressed content

If the size of your user-data script, cloud-config data, or include file may exceed 16 KB, you can use gzip compressed content in the `.gz` format to compress the script into a link. Then, you can pass in the link as an include file. cloud-init automatically decompresses the gzip compressed content. The result of running the decompressed content shows no difference from that of running a script that is directly passed in. Gzip compressed content has the following characteristics:

-   The first line starts with `#include`, and the header cannot have spaces.
-   The size of the gzip compressed content cannot exceed 16 KB before it is encoded in Base64.
-   The running frequency of the user data varies based on the types of scripts and modules.

Example:

```
#include
http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/userdata/myscript.gz
```

The example include file contains a link to gzip compressed content. cloud-init reads the gzip compressed content and automatically decompresses and runs it. The running frequency is determined by the type of the script. For example, if the gzip compressed content is obtained by compressing a user-data script, the gzip compressed content is run once only when the instance starts for the first time.

## Upstart job scripts

The content of upstart job scripts is placed into a file in the /etc/init directory. Upstart job scripts have the following characteristics:

-   The first line starts with `#upstart-job`, and the header cannot have spaces.
-   Upstart job scripts are run each time the instance starts.

**Note:** To use upstart job scripts, you must install the upstart service for the instance. The upstart service is supported for instances that run the CentOS 6, Ubuntu 10, Ubuntu 12, Ubuntu 14, Debian 6, or Debian 7 operating system.

Example:

```
#upstart-job
description "upstart test"
start on runlevel [2345] #Starts at run levels 2, 3, 4, and 5.
stop on runlevel [!2345] #Stops at a run level that is not 2, 3, 4, or 5.
exec echo "Hello World. The time is now $(date -R)!" | tee /root/output.txt
```

## Example 1: Use user-data scripts to customize YUM sources and the NTP and DNS services

When an instance starts, the system configures the default YUM source and Network Time Protocol \(NTP\) and Domain Name System \(DNS\) services. You can use the user data of the instance to change the default YUM source and NTP and DNS services that are configured. Take note of the following items:

-   If you customize a YUM source, Alibaba Cloud stops providing YUM source support.
-   If you customize the NTP service, Alibaba Cloud stops providing time synchronization services.

The following code provides an example of a user-data script that can be run on an instance that runs the CentOS 7.2 operating system:

```
#!/bin/sh
# Modify DNS
echo "nameserver 8.8.8.8" | tee /etc/resolv.conf
# Modify yum repo and update
rm -rf /etc/yum.repos.d/*
touch myrepo.repo
echo "[base]" | tee /etc/yum.repos.d/myrepo.repo
echo "name=myrepo" | tee -a /etc/yum.repos.d/myrepo.repo
echo "baseurl=http://mirror.centos.org/centos" | tee -a /etc/yum.repos.d/myrepo.repo
echo "gpgcheck=0" | tee -a /etc/yum.repos.d/myrepo.repo
echo "enabled=1" | tee -a /etc/yum.repos.d/myrepo.repo
yum update -y
# Modify NTP Server
echo "server ntp1.aliyun.com" | tee /etc/ntp.conf
systemctl restart ntpd.service
```

**Note:**

-   In the preceding example, the URL is for reference only. You can replace it to suit your needs.
-   You can also use cloud-config data to change the YUM source. However, cloud-config data is not as flexible and is not applicable to scenarios where Alibaba Cloud pre-configures some YUM sources. We recommend that you use user-data scripts.

Pass in the user data when you create the instance. After the instance starts, log on to the instance to view the running result. Check whether the configurations of the YUM source and NTP and DNS services are as expected, as shown in the following figure.

![custom-yum-dns-ntp](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8276941261/p272130.png)

## Example 2: Use user-data scripts to customize the administrator account

By default, Linux instances use the root user as the administrator. You can use the user data of an instance to configure another user as the administrator.

The following code provides an example of a user-data script that can be run on an instance that runs the CentOS 7.2 operating system:

```
#!/bin/sh
useradd test
echo "test   ALL=(ALL)        NOPASSWD:ALL" | tee -a /etc/sudoers
mkdir /home/test/.ssh
touch /home/test/.ssh/authorized_keys
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCRnnUveAis****" | tee -a /home/test/.ssh/authorized_keys
```

**Note:** Replace ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCRnnUveAis\*\*\*\* in the preceding example with your public key.

The example user-data script can be run to obtain the following results:

-   A user named test is created and used as the administrator account.
-   The user can use only Secure Shell \(SSH\) key pairs to log on to the instance and cannot use passwords for logon.
-   If the user wants to perform operations that require the administrator permissions, the user needs only to run the sudo command, without the need to enter the password.

Pass in the user data when you create the instance. After the instance starts, log on to the instance by using the test user and the SSH key pair. An error is reported if you attempt to use the password for logon. After you connect to the instance, you can run the sudo command to perform operations that require the administrator permissions, as shown in the following figure.

![test-admin-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8276941261/p272158.png)

