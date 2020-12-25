# Configure user data

This topic describes how to configure user data by using the console.

When you configure user data, take note of the following items:

-   You can configure user data only for VPC-type instances.
-   If an instance is of a retired instance type, the instance must be I/O optimized. This limit does not apply to instance types that are not retired. For more information, see [Retired instance types](/intl.en-US/Instance/Retired instance types.md) and [Instance families](/intl.en-US/Instance/Instance families.md).
-   The size of user data cannot exceed 16 KB before it is encoded in Base64.

    **Note:** The user data must be Base64-encoded before it can be configured. If you do not use the Base64 encoding service provided by the ECS console, you must manually convert the user data to Base64-encoded data before you configure it.

-   The instance must use a public image or a custom image derived from a public image. The following table lists the operating systems that are supported.

    |Platform|Operating system|
    |:-------|:---------------|
    |Windows|Windows Server 2008 R2 and later|
    |Linux|    -   CentOS
    -   Ubuntu
    -   SUSE Linux Enterprise
    -   OpenSUSE
    -   Debian
    -   Alibaba Cloud Linux |


1.  Create a Linux instance. For more information, see [Create an instance by using the provided wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    When you create the instance, enter user data in the **User Data** field of the **Advanced \(based on instance RAM roles or cloud-init\)** section. If your user data is already Base64-encoded, select **Enter Based64 Encoded Information**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8101359951/p33312.png)

2.  After the instance is started, connect to the instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

    When the instance is in the **Running** state, the system runs the user data by using the root permission. Then the system runs the initialization scripts in the `/etc/init` folder.

3.  View execution results based on your configured user data.

    If a failure occurs, you must check the relevant log files. The following figure shows an example result generated from user data configured by using the upstart job script on a CentOS instance.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9101359951/p5485.png)

    In the preceding output, the part-001.conf startup job file is generated in the /etc/init folder.


