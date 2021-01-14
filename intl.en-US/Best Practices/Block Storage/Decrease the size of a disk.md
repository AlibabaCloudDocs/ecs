# Decrease the size of a disk

You can use the Alibaba Cloud Migration tool to decrease the size of a disk. Currently, you cannot decrease the size of system or data disks that are attached to ECS instances.

Before you decrease the size of a disk, make sure that the following requirements are met:

-   The remote data synchronization tool rsync is installed in the instance when the disk is attached to a Linux instance. To install rsync, use one of the following commands based on the operating system:
    -   CentOS: Run the `yum install rsync -y` command.
    -   Ubuntu: Run the `apt-get install rsync -y` command.
    -   Debian: Run the `apt-get install rsync -y` command.
    -   Other distributions: For information about the installation, visit the official website.
-   An AccessKey pair to be exported into the user\_config.json configuration file is created in the console. For more information, see [Create an AccessKey]().

    **Note:** To avoid disclosing the AccessKey pair of your Alibaba Cloud account, we recommend that you create a RAM user and use the credentials of the RAM user to create an AccessKey pair. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md) and [Create an AccessKey]().

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   Other prerequisites and requirements are met. For more information, see [Migrate your server to Alibaba Cloud by using the Cloud Migration tool]().

The Cloud Migration tool is designed to balance the cloud-based and offline workloads of Alibaba Cloud users.

The Cloud Migration tool allows you to create a custom image from an ECS instance. During the process of creating a custom image, you can reset the size of a disk to decrease its size. The target object for which we want to decrease the disk size is an ECS instance. You can use the Cloud Migration tool with the same procedure and limits for disk size decreasing and data migration. Data migration between ECS instances is more efficient and has a lower error rate.

However, this method causes some attributes of the original ECS instance to change, such as the instance ID \(`InstanceId`\) and public IP address. If your instance is in a VPC, you can retain the public IP address by changing it to an Elastic IP address \(EIP\). We recommend that you use this method when instances are associated with EIPs, or when you are less dependent on public IP addresses.

**Note:**

The Cloud Migration tool is upgraded to Server Migration Center \(SMC\). Alibaba Cloud no longer provides version updates and technical support to the Cloud Migration tool. We recommend that you use SMC for a better cloud migration experience. SMC provides services, which include full migration, incremental migration, batch migration, and VPC-connected migration. For more information, see [Server Migration Center](/intl.en-US/Product Introduction/What is SMC?.md).

1.  Connect to the target ECS instance by using the administrator or root account. For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a username and password.md).

2.  Download the [ZIP file of Alibaba Cloud Migration Tool](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip?spm=5176.7765564.2.3.6SzsdG&file=Alibaba_Cloud_Migration_Tool.zip).

3.  Decompress the ZIP file, access the client file directory of the corresponding operating system and version, and find the user\_config.json configuration file.

4.  Complete the configuration. For more information, see [t9833.md\#section\_p5x\_xzz\_jfb]().

    The following figure shows the configuration file of a Linux instance.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5314488951/p11775.png)

    When you decrease the size of a disk, take note of the following parameters:

    -   [`system_disk_size`](): Set this parameter to the expected size of the system disk in GB. The value cannot be less than the actual size of the system disk.
    -   [`data_disks`](): Set this parameter to the expected size of the data disk in GB. The value cannot be less than the actual size of the data disk.
    **Note:**

    -   If a Linux instance is attached with a data disk, the data\_disks parameter is required even if you do not want to decrease the size of the data disk.
    -   If a Windows instance is attached with a data disk, the data\_disks parameter is optional if you do not want to decrease the size of the data disk.
5.  Run the go2aliyun\_client.exe program.

    -   Windows instance: Right-click go2aliyun\_client.exe, and then select **Run as administrator**.
    -   Linux instance:
        1.  Run `chmod +x go2aliyun_client` to grant execute permissions to the client.
        2.  Run `./ go2aliyun_client` to run the client.
6.  Wait for the operation results.

    -   If `Goto Aliyun Finished!` is displayed, go to the [Images page in the ECS console](https://ecs.console.aliyun.com/#/image/region/cn-hangzhou/imageList) to view the custom image after the disk size is decreased. If the custom image is generated, you can release the original ECS instance and create an ECS instance from the generated custom image. After the instance is created, the new instance will have a reduced disk size. For more information, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).
    -   If `Goto Aliyun Not Finished!` is displayed, check the files in the Logs folder of the same directory for troubleshooting. For more information, see [Troubleshooting]().

        After the problems are solved, run the Cloud Migration tool again to resume the process to decrease the disk size.


**Related topics**  


[Overview of the Cloud Migration tool]()

[Migrate a server to Alibaba Cloud by using the Cloud Migration tool]()

