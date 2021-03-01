---
keyword: [Cloud Assistant, remote command, O&M plug-in, Alibaba Cloud, ECS]
---

# Install the Cloud Assistant client

The Cloud Assistant client is used to run Cloud Assistant commands on ECS instances. This topic describes how to install the Cloud Assistant client.

-   You must use the account of an administrator to install and use the Cloud Assistant client. The administrator username is root for Linux instances, and system for Windows instances.
-   Before you install the Cloud Assistant client, make sure that your instance type and operating system support Cloud Assistant. For more information, see the "Limits" section of the [Overview](/intl.en-US/Deployment & Maintenance/Cloud assistant/Overview.md) topic.

By default, ECS instances created by using public images on and after December 1, 2017 are pre-installed with the Cloud Assistant client. For ECS instances created before December 1, 2017, you must manually install the Cloud Assistant client.

The following table describes the methods of how to install the Cloud Assistant client on instances of different operating systems.

|Operating system|Installation method|
|----------------|-------------------|
|Windows|-   [Install the client on Windows instances](#section_e5n_k2x_ydb)
-   [Install the client on Windows or Linux instances by using Alibaba Cloud CLI](#section_qkk_yt2_ngb) |
|Linux operating systems such as Alibaba Cloud Linux, CentOS, Red Hat Enterprise Linux \(RHEL\), and SUSE Linux|-   [Install the client on Linux instances by using the RPM package](#section_lnz_vm0_zad)
-   [Install the client on Linux instances by using source code](#section_anv_mzg_1zr)
-   [Install the client on Windows or Linux instances by using Alibaba Cloud CLI](#section_qkk_yt2_ngb)

**Note:** You cannot install the Cloud Assistant client on instances that run RHEL by using Alibaba Cloud CLI. |
|Linux operating systems such as Debian and Ubuntu|-   [Install the client on Linux instances by using the Debian package](#section_hpe_zlj_a6g)
-   [Install the client on Linux instances by using source code](#section_anv_mzg_1zr)
-   [Install the client on Windows or Linux instances by using Alibaba Cloud CLI](#section_qkk_yt2_ngb) |
|Other Linux operating systems|-   [Install the client on Linux instances by using source code](#section_anv_mzg_1zr)
-   [Install the client on Windows or Linux instances by using Alibaba Cloud CLI](#section_qkk_yt2_ngb) |

## Install the client on Windows instances

1.  Connect to an ECS instance as the administrator. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Download the Cloud Assistant client installation file.

    You can download the installation file for a specific version of the Cloud Assistant client from one of the following links:

    -   Public link for the latest version: [latest version of the Cloud Assistant client](https://aliyun-client-assist.oss-accelerate.aliyuncs.com/windows/aliyun_agent_latest_setup.exe)
    -   Public link for a specific version:

        ```
        https://aliyun-client-assist.oss-accelerate.aliyuncs.com/windows/aliyun_agent_\{version\}_setup.exe
        ```

    -   Internal link for the latest version:

        ```
        https://aliyun-client-assist-\{regionId\}.oss-\{regionId\}-internal.aliyuncs.com/windows/aliyun_agent_latest_setup.exe
        ```

    -   Internal link for a specific version:

        ```
        https://aliyun-client-assist-\{regionId\}.oss-\{regionId\}-internal.aliyuncs.com/windows/aliyun_agent_\{version\}_setup.exe
        ```

    **Note:**

    -   \{version\} indicates the version number of the Cloud Assistant client.
    -   \{regionId\} indicates the **region ID** of your instance.
    For example, you can download the installation file for the 1.0.0.128 version of the Cloud Assistant client from the following link:

    ```
    https://aliyun-client-assist-cn-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/windows/aliyun_agent_1.0.0.128_setup.exe
    ```

3.  Double-click the installation file and install the client as instructed.

    The default installation path is C:\\ProgramData\\aliyun\\assist\\ for Windows instances.

4.  If the instance is in the classic network, perform the following steps:

    1.  In the installation directory of the Cloud Assistant client, create a file named region-id. Do not add extensions such as .txt or .conf.

    2.  In the region-id file, enter the region ID of the instance. Example: cn-hangzhou.

    **Note:** In Windows, you must clear the Hide extensions for known file types option to check whether the region-id file has an extension.


## Install the client on Linux instances by using the RPM package

This method is applicable to operating systems such as Alibaba Cloud Linux, CentOS, RHEL, and SUSE Linux.

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Download the RPM package for a specific version of the Cloud Assistant client from one of the following links:

    -   Public link for the latest version:

        ```
        wget "https://aliyun-client-assist.oss-accelerate.aliyuncs.com/linux/aliyun_assist_latest.rpm"
        ```

    -   Public link for a specific version:

        ```
        wget "https://aliyun-client-assist.oss-accelerate.aliyuncs.com/linux/aliyun_assist_\{version\}.rpm"
        ```

    -   Internal link for the latest version:

        ```
        wget "https://aliyun-client-assist-\{regionId\}.oss-\{regionId\}-internal.aliyuncs.com/linux/aliyun_assist_latest.rpm"
        ```

    -   Internal link for a specific version:

        ```
        wget "https://aliyun-client-assist-\{regionId\}.oss-\{regionId\}-internal.aliyuncs.com/linux/aliyun_assist_\{version\}.rpm"
        ```

    **Note:**

    -   \{version\} indicates the version number of the Cloud Assistant client.
    -   \{regionId\} indicates the **region ID** of your instance.
    For example, you can download the RPM package for the 1.0.2.458 version of the Cloud Assistant client from the following link:

    ```
    wget "https://aliyun-client-assist-cn-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/linux/aliyun_assist_1.0.2.458.rpm"
    ```

3.  Install the Cloud Assistant client.

    In this example, the latest version of the Cloud Assistant client is installed.

    ```
    rpm -ivh --force aliyun_assist_latest.rpm
    ```

4.  If the operating system of the instance is Red Hat, perform the following steps:

    1.  Stop the qemu-ga service.

        ```
        systemctl stop qemu-guest-agent
        systemctl disable qemu-guest-agent
        ```

    2.  Restart Cloud Assistant.

        ```
        systemctl restart aliyun.service
        ```

5.  If the instance is in the classic network, perform the following steps:

    1.  In the installation directory of the Cloud Assistant client, create a file named region-id. Do not add extensions such as .txt or .conf.

    2.  In the region-id file, enter the region ID of the instance. Example: cn-hangzhou.


If you select the default installation directories, the Cloud Assistant client is installed in one of the following directories on Linux instances:

-   CoreOS: /opt/local/share/aliyun-assist/.
-   Other operating systems: /usr/local/share/aliyun-assist/. Other operating systems include Alibaba Cloud Linux, Ubuntu, Debian, Red Hat, SUSE Linux Enterprise Server, and openSUSE.

## Install the client on Linux instances by using the Debian package

This method is applicable to operating systems such as Debian and Ubuntu.

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Download the Debian package for a specific version of the Cloud Assistant client from one of the following links:

    -   Public link for the latest version:

        ```
        wget "https://aliyun-client-assist.oss-accelerate.aliyuncs.com/linux/aliyun_assist_latest.deb"
        ```

    -   Public link for a specific version:

        ```
        wget "https://aliyun-client-assist.oss-accelerate.aliyuncs.com/linux/aliyun_assist_\{version\}.deb"
        ```

    -   Internal link for the latest version:

        ```
        wget "https://aliyun-client-assist-\{regionId\}.oss-\{regionId\}-internal.aliyuncs.com/linux/aliyun_assist_latest.deb"
        ```

    -   Internal link for a specific version:

        ```
        wget "https://aliyun-client-assist-\{regionId\}.oss-\{regionId\}-internal.aliyuncs.com/linux/aliyun_assist_\{version\}.deb"
        ```

    **Note:**

    -   \{version\} indicates the version number of the Cloud Assistant client.
    -   \{regionId\} indicates the **region ID** of your instance.
    For example, you can download the Debian package for the 1.0.2.458 version of the Cloud Assistant client from the following link:

    ```
    wget "https://aliyun-client-assist-cn-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/linux/aliyun_assist_1.0.2.458.deb"
    ```

3.  If an earlier version of the Cloud Assistant client is installed on the instance, uninstall the earlier version.

    ```
    dpkg -r aliyun-assist
    ```

4.  Install the Cloud Assistant client.

    In this example, the latest version of the Cloud Assistant client is installed.

    ```
    dpkg -i aliyun_assist_latest.deb
    ```

5.  If the instance is in the classic network, perform the following steps:

    1.  In the installation directory of the Cloud Assistant client, create a file named region-id. Do not add extensions such as .txt or .conf.

    2.  In the region-id file, enter the region ID of the instance. Example: cn-hangzhou.


If you select the default installation directories, the Cloud Assistant client is installed in one of the following directories on Linux instances:

-   CoreOS: /opt/local/share/aliyun-assist/.
-   Other operating systems: /usr/local/share/aliyun-assist/. Other operating systems include Alibaba Cloud Linux, Ubuntu, Debian, Red Hat, SUSE Linux Enterprise Server, and openSUSE.

## Install the client on Linux instances by using source code

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Install necessary software such as Git and Go.

    YUM is used in this example. If you use other versions of Linux, use the corresponding package manager.

    -   Install Git.

        ```
        yum install git -y
        ```

    -   Install Go.

        ```
        yum install go -y
        ```

3.  Download the source code of the Cloud Assistant client.

    ```
    git clone https://github.com/aliyun/aliyun_assist_client
    ```

4.  Access the source code directory.

    ```
    cd ./aliyun_assist_client
    ```

5.  Compile the source code.

    ```
    go build
    ```

    If no error message is returned, the client is installed.

6.  If the instance is in the classic network, perform the following steps:

    1.  In the installation directory of the Cloud Assistant client, create a file named region-id. Do not add extensions such as .txt or .conf.

    2.  In the region-id file, enter the region ID of the instance. Example: cn-hangzhou.

7.  Run the Cloud Assistant client.

    ```
    aliyun-service -d
    ```


## Install the client on Windows or Linux instances by using Alibaba Cloud CLI

To use this method, you do not need to connect to the instance but you must install Alibaba Cloud CLI first. For more information about how to install Alibaba Cloud CLI in different operating systems, see the following topics:

-   [Windows]()
-   [Linux]()
-   [MacOS]()

**Note:** You cannot install the Cloud Assistant client on instances that run RHEL by using Alibaba Cloud CLI.

1.  Call the [DescribeCloudAssistantStatus](/intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md) operation to check whether the Cloud Assistant client is installed on your ECS instance.

    ```
    aliyun ecs DescribeCloudAssistantStatus --RegionId TheRegionId --InstanceId.1 i-bp1g6zv0ce8og\*\*\*\*\*\*p --output cols=CloudAssistantStatus rows=InstanceCloudAssistantStatusSet.InstanceCloudAssistantStatus[]
    ```

    If the value of `CloudAssistantStatus` is true in the response, the Cloud Assistant client is installed on the instance. Otherwise, proceed to the next step.

2.  Call the [InstallCloudAssistant](/intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md) operation to install the Cloud Assistant client.

    ```
    aliyun ecs InstallCloudAssistant --RegionId TheRegionId --InstanceId.1 i-bp1g6zv0ce8og\*\*\*\*\*\*p
    ```

3.  Call the [RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md) operation to restart the ECS instance.

    ```
    aliyun ecs RebootInstance --InstanceId i-bp1g6zv0ce8og\*\*\*\*\*\*p
    ```

4.  If the instance is in the classic network, add a region declaration within the instance.

    1.  Connect to the ECS instance as the administrator. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

    2.  View the version of Cloud Assistant.

        -   For Linux instances, run the following command:

            ```
            aliyun-service -v
            ```

        -   For Windows instances, see [Update or disable updates for the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Update or disable updates for the Cloud Assistant client.md).
        If the version of the Cloud Assistant client is later than 1.0.1.400, the Cloud Assistant client is installed. Otherwise, proceed to the next step.

    3.  In the installation directory of the Cloud Assistant client, create a file named region-id. Do not add extensions such as .txt or .conf.

    4.  In the region-id file, enter the region ID of the instance. Example: cn-hangzhou.

    **Note:** In Windows, you must clear the Hide extensions for known file types option to check whether the region-id file has an extension.


**References**  


[InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md)

[DescribeCloudAssistantStatus](/intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md)

[InstallCloudAssistant](/intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md)

[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)

[Regions and zones]()

[Alibaba Cloud GitHub repository](https://github.com/aliyun/aliyun_assist_client)

