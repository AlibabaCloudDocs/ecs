# Prepare user data

User data allows you to customize the startup behaviors of ECS instances and pass data into instances.

Both Windows and Linux instances support the user data feature. You can use the feature in the following ways:

-   Run user data scripts upon instance startup.
-   Pass user data as common data into an ECS instance for future reference.

## Prepare the user data of a Linux instance

You can configure the user data of a Linux instance by using multiple types of scripts such as the user-data script, cloud-config script, include file, gzip-compressed script, and upstart job script. User data of Linux instances adopts the open source cloud-init architecture and takes metadata of instances as data sources to automatically configure attributes of Linux instances. For more information, visit [User-Data Formats](http://cloudinit.readthedocs.io/en/latest/topics/format.html) in the cloud-init documentation.

To create an include file or gzip-compressed script, you must upload script files to available storage services, obtain the links, and set the validity period for the links. We recommend that you use Alibaba Cloud OSS to create links. For more information, see [Upload objects](/intl.en-US/Quick Start/OSS console/Upload objects.md) and [Configure lifecycle rules](/intl.en-US/Console User Guide/Manage buckets/Basic settings/Configure lifecycle rules.md) in the OSS documentation.

To prepare the user data of a Linux instance, perform the following operations:

1.  Use an editor to create a text file, such as Notepad++.

2.  Edit the script that is related to the user data in the text file.

    The first line of a script must meet the format requirements of this script type. The following section describes the format requirements of different scripts and the format examples:

    -   User-data script

        User-data scripts can be shell scripts. The following section describes the characteristics of a user-data script:

        -   The first line must start with `#!`, such as `#! /bin/sh`.
        -   The script size cannot exceed 16 KB before the script is encoded in Base64.
        -   The script is run only when the instance is started for the first time.
        User-data script example:

        ```
        #! /bin/sh
        echo "Hello World. The time is now $(date -R)!" | tee /root/output10.txt
        service httpd start
        chkconfig httpd on
        ```

        After the instance is created, start and connect to the instance. Run the `cat [file]` command to check the execution result of the script.

        ```
        [root@XXXXX2z ~]# cat output10.txt
        Hello World. The time is now Mon, 24 Jul 2017 13:03:19 +0800!
        ```

    -   Cloud-config script

        The cloud-config script is a user-friendly and efficient way to implement user data. You can use cloud-config scripts to configure services such as updating YUM sources, importing SSH keys, and installing dependency packages. The following section describes the characteristics of a cloud-config script:

        -   The first line must start with `#cloud-config`, and the header cannot have spaces.
        -   The script must be a valid YAML file.
        -   The script size cannot exceed 16 KB before the script is encoded in Base64.
        -   The running frequency of the user data varies based on the service that you configured.
        Cloud-config script example:

        ```
        #cloud-config
        apt:
        primary:
        - arches: [default]
        uri: http://us.archive.ubuntu.com/ubuntu/
        bootcmd:
        - echo 192.168.1.130 us.archive.ubuntu.com >> /etc/hosts
        ```

        After the instance is created, start and connect to the instance. Check the execution result of the script.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8101359951/p5487.png)

    -   Include file

        An include file consists of script links. Each line consists of a link. When an ECS instance is started, cloud-init reads user data from script links of the include file. If an error occurs on a line, the instance stops reading the user data. The following section describes the characteristics of an include file:

        -   The first line must start with `#include`, and the header cannot have spaces.
        -   The file size cannot exceed 16 KB before the file is encoded in Base64.
        -   The running frequency of the user data varies based on the type of the script that is configured in the include file.
        Include file example:

        ```
        #include
        http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/UserData/myscript.sh
        ```

        After the instance is created, start and connect to the instance. Check the execution result of the script.

    -   gzip-compressed script

        When you use the user-data script, cloud-config script, or include file, make sure that the script size is no more than 16 KB before the script is encoded in Base64. If your script size may exceed 16 KB, you can use the gzip utility to compress the script. Compress the script files into script links. The script links constitute an include file. The following section describes the characteristics of a gzip-compressed script:

        -   The first line must start with `#include`, and the header cannot start with spaces.
        -   The running frequency of the user data varies based on the script type.
        gzip-compressed script example:

        ```
        #include
        http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/userdata/config.gz
        ```

        To make a gzip-compressed script file, you must compress the script file into the `.gz` format.

    -   Upstart Job

        To use an upstart job script, you must install the upstart service as the init system. The upstart service uses the CentOS 6, Ubuntu 10/12/14, or Debian 6/7 operating system. Upstart job scripts put your user data in the /etc/init directory. The following section describes the characteristics of an upstart job script:

        -   The first line must start with `#upstart-job`, and the header cannot start with spaces.
        -   The script is run every time the instance is started.
        Upstart job script example:

        ```
        #upstart-job
        description "upstart test"
        start on runlevel [2345]
        stop on runlevel [! 2345]
        exec echo "Hello World. The time is now $(date -R)!" | tee /root/output.txt
        ```

3.  Debug the script to ensure that the user data is correct.


## Prepare the user data of a Windows instance

User data is a feature developed by Alibaba Cloud and enables Windows instances to run initialized scripts. You can use the batch and PowerShell scripts to configure the user data of a Windows instance.

To prepare the user data of a Windows instance, perform the following operations:

1.  Use an editor to create a text file, such as Notepad++.

2.  Edit the script that is related to the user data in the text file.

    The first line of a script must meet the format requirements of this script type. The following section describes the format requirements of different scripts and the format examples:

    -   The following section describes the characteristics of a batch script:

        -   The first line must start with `[bat]`, and the header cannot start with spaces.
        -   The script size cannot exceed 16 KB before the script is encoded in Base64.
        -   Only half-width letters can be entered, and no additional characters are allowed.
        Batch script example:

        ```
        [bat]
        echo "bat test" > c:\1.txt
        ```

        After the instance is created, start and connect to the instance. Check the execution result of the script. You can find that the 1.txt text file is added to the C:\\ drive.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8101359951/p5488.png)

    -   The following section describes the characteristics of a PowerShell script:

        -   The first line must start with `[powershell]`, and the header cannot start with spaces.
        -   The script size cannot exceed 16 KB before the script is encoded in Base64.
        -   Only half-width letters can be entered, and no additional characters are allowed.
        PowerShell script example:

        ```
        [powershell]
        write-output "Powershell Test" | Out-File C:\2.txt
        ```

3.  Debug the script to ensure that the user data is correct.


After the script is prepared, you can use the script to configure the user data. For more information, see [Configure user data](/intl.en-US/Instance/Manage instances/User data/Configure user data.md).

