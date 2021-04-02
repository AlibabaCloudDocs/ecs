# Decrease the size of a disk

You cannot decrease the sizes of system or data disks in Elastic Compute Service \(ECS\). You can use Alibaba Cloud Server Migration Center \(SMC\) to decrease the sizes of disks.

The preparations for the migration are completed. For more information, see [Before you begin](/intl.en-US/User Guide/Before you begin.md).

SMC is designed to balance the cloud-based and offline workloads of Alibaba Cloud users. You can also use SMC to decrease the sizes of ECS disks.

SMC allows you to create a custom image from an ECS instance. When you create the custom image, you can reset the size of a disk to a smaller value. The same procedure and limits apply when you use SMC to decrease the size of a disk and migrate data. However, when you decrease the size of a disk, the associated ECS instance is used as the migration source. When you decrease the size of a disk, data is migrated between ECS instances. Data migration between ECS instances is more efficient and has a lower error rate.

Take note that when you use SMC to decrease the size of a disk, some attributes of the ECS instance used as the migration source are changed, such as the instance ID \(`InstanceId`\) and public IP address. If your instance resides in a VPC, you can change the public IP address to an elastic IP address \(EIP\). This way, you can retain the public IP address. We recommend that you use SMC to decrease the size of a disk when instances are associated with EIPs, or when you are less dependent on public IP addresses.

1.  Connect to the ECS instance for which you want to decrease the size of a disk.

    For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

2.  Download the [SMC client](https://p2v-tools.oss-cn-hangzhou.aliyuncs.com/smc/Alibaba_Cloud_Migration_Tool.zip?file=Alibaba_Cloud_Migration_Tool.zip).

3.  Decompress the SMC client package.

    The SMC client is available for both 32-bit \(i386\) and 64-bit \(x86\_64\) versions of Windows and Linux. Select the version that is compatible with the migration source.

4.  Import the migration source. For more information, see [Step 1: Import the information of a migration source](/intl.en-US/User Guide/Step 1: Import the information of a migration source.md).

5.  Create and start a migration task.

    When you migrate data from a source disk to a specified disk of the destination instance, decrease the size of the disk of the instance that is used as the migration source. For more information, see [Migrate servers to ECS instances](/intl.en-US/Best Practices/Migrate servers to ECS instances.md).

    When you create a migration task, configure the **System Disk** and **Data Disk** parameters in the **Target Disk Size** section. The values of these parameters cannot be less than the actual used space of the source disk.

6.  Wait until the migration task is complete.

    -   If the migration task is in the **Finished** state, the task is complete and you can view the destination ECS instance.
    -   If the migration task is in the **InError** state, the task failed. You can check the logs to troubleshoot the failure. Then, restart the migration task. For information about common errors and solutions, see [SMC FAQ](/intl.en-US/FAQ/SMC FAQ.md).

