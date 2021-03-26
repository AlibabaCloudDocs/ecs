# Hibernate an instance

If you do not require the use of an ECS instance for a period of time, but you still want to retain the instance without performing operations such as configuration upgrade or downgrade on the instance, we recommend that you hibernate the instance. A hibernated instance is different from a stopped instance. A hibernated instance automatically restores the applications on the instance to the status before hibernation when the instance is waked. This allows the instance to resume providing services in a short of time.

When you hibernate an instance, the operating system of the instance saves data from the memory to the system disk of the instance. The saved data includes the applications that run in the operating system and the usage status of the applications. When you wake the instance, the operating system reads the data saved in the system disk, automatically restores the applications to the status before hibernation, and resumes the running state of the instance. In comparison, when you stop and restart an instance, the operating system restarts the backend services and applications.

**Note:** If the instance fails to be hibernated, the instance is automatically shut down. Data in the memory is not saved to the system disk. When the instance is started again, the operating system of the instance restarts the backend services and applications. The operating system cannot restore the applications to the status before hibernation.

Hibernation has different impacts on the billing of instances that use different billing methods:

-   Subscription instance: The expiration time and billing of the hibernated instance are not affected.
-   Pay-as-you-go instance: Whether the billing of the hibernated instance is affected is based on whether you select the **No Fees for Hibernated Instances** option when you hibernate the instance. The following table describes the billing details of resources.

|Resource|No Fees for Hibernated Instances|Retain Instance and Continue Charging After Instance Is Hibernated|
|--------|--------------------------------|------------------------------------------------------------------|
|Computing resource \(vCPUs and memory\)|Release and stop billing|Retain and continue billing|
|Disk \(system disk and data disk\)|Retain and continue billing|Retain and continue billing|
|Internal IP address|Retain and stop billing|Retain and stop billing|
|Public IP address|Release and stop billing. After the instance is started, a new public IP address is obtained.|Retain and stop billing|
|EIP|Retain and continue billing|Retain and continue billing|
|Bandwidth|Continue billing|Continue billing|

## Limits

-   You can enable the instance hibernation feature only when you create an ECS instance. Then, you can hibernate the instance based on your requirements. The instance hibernation feature cannot be disabled after it is enabled. If you do not enable the instance hibernation feature when you create an instance, you cannot hibernate the instance.
-   You can enable the instance hibernation feature only when you create an ECS instance by using an encrypted custom image. The following image versions are supported:
    -   Windows Server 2016 or later
    -   Ubuntu 18 or later
    -   CentOS 7 or later
-   If the instance hibernation feature is enabled for an ECS instance when the instance is created, you cannot perform the following operations on the instance:
    -   Create images.
    -   Create snapshots.
    -   Change the instance type.
    -   Change the CPU and memory sizes.
    -   Replace the system disk.
-   If the instance hibernation feature is enabled for a preemptible instance, you can select the No Fees for Hibernated Instances option when you hibernate the instance.
-   You cannot hibernate ECS instances in scaling groups.

## Step 1: Enable the instance hibernation feature

You must enable the instance hibernation feature when you create an ECS instance. Otherwise, you cannot hibernate the instance. When you create the instance, you must use an encrypted image.

1.  Obtain an encrypted custom image.

    You can use one of the following methods to obtain an encrypted custom image:

    -   Create an encrypted custom image that meets the hibernation requirements.
    -   Copy an image and encrypt it at the same time. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
    **Note:** For more information about the limits on images, see [Limits](#section_55c_coc_sg1).

2.  Create an ECS instance and enable the instance hibernation feature when you create the instance.

    For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). Take note of the parameters described in the following table.

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |Instance|    -   Instance Type: Select an I/O optimized instance type, except ECS Bare Metal Instance.
    -   Memory:
        -   Windows: Set the memory size to a value less than 16 GiB.
        -   Linux: Set the memory size to a value less than 150 GiB.
|ecs.g6e.large|
    |Image|    -   Select the encrypted custom image created in the previous step or an existing encrypted custom image that meets the hibernation requirements.
    -   Select **Instance Hibernation** to enable the instance hibernation feature.
|    -   encrypted.windows2016
    -   Select **Instance Hibernation**. |
    |Disk|    -   System Disk: required. The system disk must meet the following requirements:
        -   Category: ultra disk, standard SSD, or enhanced SSD \(ESSD\).
        -   Capacity: The system disk capacity must be sufficient. We recommend that you set the system disk capacity to at least twice the memory size. This is because when the instance hibernation feature is enabled, the system disk reserves some space to store memory data. Therefore, the system disk capacity must be sufficient to ensure normal running of the operating system and applications when the system disk stores the memory data.
        -   Encryption: By default, the system disk is encrypted if an encrypted image is used.
    -   Data Disk: optional. To create data disks for an instance when you create the instance, you must select the disk categories and specify the sizes and quantity of the disks. You must also determine whether to encrypt the disks.
|    -   System Disk: Select Enhanced SSD \(ESSD\), set Disk Capacity to 60 GiB, select Disk Encryption, and then select **Default Service CMK** from the drop-down list.
    -   Data Disk: Select Enhanced SSD \(ESSD\), set Disk Capacity to 40 GiB, and do not select Disk Encryption. |
    |Network|Select a virtual private cloud \(VPC\). **Note:** ECS instances in the classic network do not support the instance hibernation feature.

|\[Default\]vpc-bp1opxu1zkhn00g\*\*\*\*|


## Step 2: Hibernate the instance

If the instance hibernation feature is enabled for an instance and the instance is in the Running state, you can perform the following operations to hibernate the instance. You are unable to connect to the instance when the instance is hibernated.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance that you want to hibernate and choose **More** \> **Instance Status** \> **Stop** in the **Actions** column.

5.  In the Stop Instance dialog box, configure the parameters.

    1.  Set **Stop By** to **Hibernate**.
    2.  Set **Stop Mode** to **Retain Instance and Continue Charging After Instance Is Hibernated** or **No Fees for Hibernated Instances** based on the billing method of the instance.

        -   You are charged for subscription instances even after the instances are hibernated. Select **Retain Instance and Continue Charging After Instance Is Hibernated**.
        -   For pay-as-you-go instances, you can select **Retain Instance and Continue Charging After Instance Is Hibernated** or **No Fees for Hibernated Instances**.

            **Note:** For preemptible instances, select **No Fees for Hibernated Instances**.

        For more information about the difference between **Retain Instance and Continue Charging After Instance Is Hibernated** and **No Fees for Hibernated Instances**, see [Table 1](#table_82t_3jc_tg6) in this topic.

    3.  Click **OK**.

        **Note:** The instance is stopped and enters the **Stopped** state. To start the instance, see [Start or stop an instance](/intl.en-US/Instance/Manage instances/Start ECS instances.md).


