---
keyword: [Alibaba Cloud, data encryption, security compliance, ECS]
---

# Encrypt a data disk

This topic describes how to encrypt a data disk. After you enable encryption for a data disk, both data in transit and data at rest on the disk are encrypted.

## Encrypt a data disk while you are creating an instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  On the **Instances** page, click **Create Instance**.

4.  In the **Basic Configurations** step, find the **Storage** section and perform the following steps.

    **Note:** This procedure describes only how to configure the encryption settings while you are creating an instance. For information about other configurations of the instance, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    1.  Click **Add Disk**.

    2.  Specify the category and capacity of the data disk.

    3.  Select **Disk Encryption** and then select a key from the drop-down list.

        ![Encrypt a data disk while you are creating an instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0082909951/p76508.png)

        After the encryption is complete, the KMS key that is used to encrypt the disk is automatically assigned with a fixed tag. The key of the tag is `acs:ecs:disk-encryption`, and the value of the tag is `true`. You can view the tag of the KMS key in the KMS console.


## Encrypt a data disk while you are creating the disk

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the upper-right corner of the Disks page, click **Create Disk**.

4.  Specify the category and capacity of the disk.

    **Note:** This procedure describes only how to configure the encryption settings while you are creating a disk. For information about other configurations of the disk, see [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md).

5.  In the **Storage** section, select **Disk Encryption** and then select a key from the drop-down list.

    ![Create a pay-as-you-go data disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8745721061/p4412.png)

    After the encryption is complete, the KMS key that is used to encrypt the disk is automatically assigned with a fixed tag. The key of the tag is `acs:ecs:disk-encryption`, and the value of the tag is `true`. You can view the tag of the KMS key in the KMS console.


## Change the encryption state

After a data disk is created, you cannot directly its encryption state. You can perform the operations described in the following table to change the encryption state of data.

|State change|Operation|Windows Server|Linux|
|:-----------|---------|:-------------|:----|
|From unencrypted to encrypted|1.  Log on to the operating system of the instance.
2.  Manually copy data on the unencrypted disk to a new encrypted disk.

|Run the robocopy command on the command line.|Run the rsync shell command.|
|From encrypted to unencrypted|1.  Log on to the operating system of the instance.
2.  Manually copy data on the encrypted disk to a new unencrypted disk. |

**Related topics**  


[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

[CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md)

