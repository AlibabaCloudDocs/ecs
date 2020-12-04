# Bind an instance RAM role

This topic describes how to create, authorize, and bind an instance RAM role in the RAM and ECS consoles.

-   The RAM service is activated. For more information, see [Activate RAM](/intl.en-US/Pricing/Billing.md).
-   The network type of the ECS instance to which you want to bind a RAM role is VPC.
-   A RAM user is authorized to use the instance RAM role if you use the RAM user to perform operations in this topic. For more information, see [Authorize a RAM user to manage an instance RAM role](/intl.en-US/Security/Instance RAM roles/Manage an instance RAM role/Authorize a RAM user to manage an instance RAM role.md).

-   A RAM role can be bound to one instance at a time.
-   If you want to access the APIs of other Alibaba Cloud services from applications within an ECS instance that is bound with an instance RAM role, you must obtain a temporary authorization token for the instance RAM role by using the instance metadata. For more information, see [Obtain a temporary authorization token](/intl.en-US/Security/Instance RAM roles/Manage an instance RAM role/Obtain a temporary authorization token.md).

## Procedure

An Alibaba Cloud account is used in the following example to create an instance RAM role and bind the role to an ECS instance in the RAM console:

1.  [Step 1: Create an instance RAM role](#section_s9s_ayg_45l)
2.  [Step 2: Authorize the instance RAM role](#section_dpz_sjj_rbj)
3.  [Step 3: Bind the instance RAM role](#section_xb2_v3o_mtj)

## Step 1: Create an instance RAM role

Perform the following operations to create an instance RAM role in the RAM console:

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  In the left-side navigation pane, click **RAM Roles**.

3.  On the **RAM Roles** page, click **Create RAM Role**.

4.  In the Create RAM Role panel, select **Alibaba Cloud Service** for the Trusted entity type parameter and click **Next**.

    **Alibaba Cloud Service** is used to authorize ECS instances to access or manage your cloud resources. After you select **Alibaba Cloud Service** for the RAM role, you can bind the RAM role to ECS instances.

    ![Select Alibaba Cloud Service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6602507061/p183974.png)

    **Note:**

    If you select **Alibaba Cloud Account**for a RAM role, you must click **Edit Trust Policy** on the **Trust Policy Management** tab to manually add the following permission policy for ECS after the RAM role is created:

    ```
    "Service": [
        "ecs.aliyuncs.com"
    ]
    ```

5.  Select **Normal Service Role** for the **Role Type** parameter.

6.  Specify the **RAM Role Name** and **Note** parameters.

7.  Select **Elastic Compute Service** as the trusted service.

8.  Click **OK**.


After the RAM role is created, check whether the RAM role include the following permission policy for ECS on the **Trust Policy Management** tab.

![ECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6602507061/p183955.png)

## Step 2: Authorize the instance RAM role

Perform the following operations to attach a system policy or custom policy to the instance RAM role in the RAM console:

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  \(Optional\) Create a custom policy if you do not want to use a system policy. For more information, see [Implement access control by using RAM](/intl.en-US/Security/Implement access control by using RAM.md).

3.  In the left-side navigation pane, click **RAM Roles**.

4.  In the **RAM Role Name** column, click the name of the target RAM role.

5.  On the **Permissions** tab, click **Input and Attach**.

6.  Select **System Policy** or **Custom Policy**.

7.  Enter the policy name.

8.  Click **OK**.

9.  Click **Close**.


## Step 3: Bind the instance RAM role

Perform the following operations to bind the instance RAM role to an ECS instance in the ECS console:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the ECS instance and choose **More** \> **Instance Settings** \> **Bind/Unbind RAM Role**.

5.  In the Bind/Unbind RAM Role dialog box, select the created instance RAM role from the RAM Role drop-down list and click **OK**.


Alternatively, you can select the created instance RAM role from the **RAM Role** drop-down list in the **System Configurations** step when you create an ECS instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

**Related topics**  


[CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md)

[CreatePolicy](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/CreatePolicy.md)

[AttachPolicyToRole](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/AttachPolicyToRole.md)

[AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md)

