# Create a security-enhanced instance

When you create a security-enhanced instance, you must obtain corresponding permissions and select a specific operating system. This topic describes how to create a security-enhanced instance in the ECS console.

When you create an instance in the ECS console, you are prompted to enable the following permissions:

-   Key Management Service \(KMS\). After KMS is enabled, a service key is automatically created. You do not need to pay for this key.

    **Note:** If you call an API operation to create a security-enhanced instance, you must first enable KMS. Otherwise, the instance cannot be created. For more information, see [Activate KMS](/intl.en-US/Quick Start/Activate KMS.md).

-   Create a RAM role and grant permissions to the role. Alibaba Cloud provides you with system policies for trusted services. You can follow the wizard to create an instance.

## Create an instance

The procedure for creating a security-enhanced instance is similar to that for creating a non-security-enhanced instance. However, you must pay attention to specific options when you create a security-enhanced instance. This procedure describes the specific configurations to be made when you create an instance of the c6t instance family. For other general configurations, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Click **Create Instance**.

4.  Configure the settings in the Basic Configurations step.

    Take note of the following items:

    ![Basic configurations](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231806.png)

    -   **Instance Type**: You can filter and select a c6t instance type.
    -   **Image**: You can select **Alibaba Cloud Linux 2.1903 64-bit \(Trusted\)** or **CentOS 7.8 64-bit \(Trusted\)**.

        **Note:** When you purchase a security-enhanced instance, **Trusted System** is automatically selected. The Alibaba Cloud trusted system verifies the instance when the instance starts. If you want to build a self-managed trusted service system, you can clear **Trusted System**.

5.  Click **Next: Networking**. If the **Enable Key Management Service \(KMS\)** dialog box appears, click **Enable**.

    KMS must be enabled. Otherwise, the security-enhanced instance cannot be created. If you have enabled KMS, the dialog box does not appear. Proceed with the next step.

6.  Configure the settings in the Networking step.

7.  In the System Configurations step, specify **RAM Role**.

    If **Trusted System** is enabled for your instance, you must specify a RAM role for the instance. The RAM role must be granted permissions to access the trusted services. Alibaba Cloud provides you with the corresponding **AliyunECSInstanceForYundunSysTrustRole** service role. We recommend that you configure and select the role by performing the following steps:

    **Note:** If you need more precise or customized configurations, create a role and grant it permissions based on your needs. For more information, see [Create and authorize an instance RAM role](#section_y82_9i9_35k).

    1.  Authorize the role first. ****

        ![Authorize](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231953.png)

    2.  In the **Cloud Resource Access Authorization** dialog box, click **Confirm Authorization Policy**.

    3.  In the dialog box that appears, click **Confirm Authorization**.

    4.  Click **Authorized**.

        ![Confirm Authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231920.png)

    5.  Select **AliyunECSInstanceForYundunSysTrustRole** as the RAM role.

        ![Set RAM Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231921.png)

    **Note:** You can also skip the authorization step and grant permissions after the instance is created. For specific steps, see the [Create and authorize a RAM role](#section_y82_9i9_35k) section.

8.  Follow the wizard to create an instance.


## Create and authorize an instance RAM role

If you have bound an instance RAM role to the instance when you create the instance, skip this section. If you created a security-enhanced instance by calling an API operation, or if you created the instance in the ECS console but did not specify an instance RAM role, you must bind an instance RAM role to the instance. The following section describes the procedure:

-   To bind a RAM role to an instance in the console, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).
-   To create and bind a RAM role to an instance by calling API operations, see [Use an instance RAM role by calling API operations](/intl.en-US/Security/Instance RAM roles/Use an instance RAM role by calling API operations.md).

We recommend that you create a custom permission policy that contains the least required permissions. Then, you can attach the policy to the RAM role. You can select **System Policy** \(**AliyunSysTrustFullAccess**\) corresponding to the trusted service as the permission type. You can also select **Custom Policy** as the permission type for precise authorization. The following section shows the precise policy for accessing the trusted service:

**Note:** You can select a system policy with higher permissions, such as AdministratorAccess. However, RAM permissions are related to information security risks. We strongly recommend that you assign the least required permissions to a policy based on your needs and do not grant excessive permissions to a role. For more information, see [What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md).

```
{
    "Statement": [
        {
            "Action": [
                "yundun-systrust:GenerateNonce",
                "yundun-systrust:GenerateAikcert",
                "yundun-systrust:RegisterMessage",
                "yundun-systrust:PutMessage"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ],
    "Version": "1"
}
```

![Custom policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p232021.tif)

