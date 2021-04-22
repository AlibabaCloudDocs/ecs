# Run Cloud Assistant commands as a regular user

The best practice in permission management is to run commands based on the least privilege principle. We recommend that you run Cloud Assistant commands as a regular user. This topic describes how to configure access control for RAM users to run Cloud Assistant commands as regular users.

Regular users are created for the ECS instance. In this topic, regular users user01 and user02 are used.

When you run a Cloud Assistant command, the command is run based on the highest level of permissions on the ECS instance if you do not configure the specified permission. For example, Cloud Assistant commands are run by the root user on Linux instances and by the system user on Windows instances.

For information security, you may need to forbid the use of the root or system user in ECS instances. In this case, you can use a RAM user and configure a permission policy to forbid the root or system user to run Cloud Assistant commands on ECS instances, and allow a specific user \(such as user01 and user02\) to run the Cloud Assistant commands on the ECS instances.

## Run Cloud Assistant commands on Linux instances as a regular user

To run Cloud Assistant commands only on Linux instances, you can perform the following operations to limit a RAM user from running Cloud Assistant commands as the root user.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using your Alibaba Cloud account.

2.  Create a RAM user. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md).

    The following table shows a configuration example.

    |Parameter|Example|
    |---------|-------|
    |**Logon Name**|commandUser|
    |**Display Name**|commandUser|
    |**Access Mode**|You can use Cloud Assistant by using the Alibaba Cloud Management Console or by calling API operations. In this example, select **Console Access** and **Programmatic Access**.**Note:** You can select an access mode based on your actual usage to implement least privilege-based management. |
    |**Console Password**|Select **Automatically Generate Default Password**.|
    |**Password Reset**|Select **Required at Next Logon**.|
    |**Multi-factor Authentication**|Select **Not Required**.|

    After you have created the RAM user, you must keep the username, password, and AccessKey pair of the RAM user.

3.  Create a Cloud Assistant permission policy. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

    ![RAM user permission settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4157898161/p238462.png)

    Create a commandUserPolicy policy to limit users from running Cloud Assistant commands on the ECS instance. The following section shows the example policies. You can modify them based on your needs.

    -   RAM permission policy that allows some regular users \(such as user01 and user02\) to run Cloud Assistant commands on the ECS instance:

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "ecs:DescribeInstances",
                        "ecs:DescribeTagKeys",
                        "ecs:DescribeTags",
                        "ecs:CreateCommand",
                        "ecs:DescribeCommands",
                        "ecs:InvokeCommand",
                        "ecs:RunCommand",
                        "ecs:DeleteCommand",
                        "ecs:DescribeInvocations",
                        "ecs:DescribeInvocationResults",
                        "ecs:StopInvocation",
                        "ecs:DescribeCloudAssistantStatus",
                        "ecs:InstallCloudAssistant"
                    ],
                    "Resource": [
                        "acs:ecs:*:*:instance/*",
                        "acs:ecs:*:*:command/*"
                    ],
                    "Condition": {
                        "StringEquals": {
                            "ecs:CommandRunAs": [
                                "user01",
                                "user02"
                            ]
                        }
                    }
                }
            ],
            "Version": "1"
        }
        ```

        **Note:** If you want to allow other users, you can modify the username or add usernames in the Condition parameter.

    -   RAM permission policy that forbids some users \(such as the root or system user\) to run Cloud Assistant commands on the ECS instance:

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "ecs:DescribeInstances",
                        "ecs:DescribeTagKeys",
                        "ecs:DescribeTags",
                        "ecs:CreateCommand",
                        "ecs:DescribeCommands",
                        "ecs:InvokeCommand",
                        "ecs:RunCommand",
                        "ecs:DeleteCommand",
                        "ecs:DescribeInvocations",
                        "ecs:DescribeInvocationResults",
                        "ecs:StopInvocation",
                        "ecs:DescribeCloudAssistantStatus",
                        "ecs:InstallCloudAssistant"
                    ],
                    "Resource": [
                        "acs:ecs:*:*:instance/*",
                        "acs:ecs:*:*:command/*"
                    ],
                    "Condition": {
                        "StringNotEqualsIgnoreCase": {
                            "ecs:CommandRunAs": [
                                "system",
                                "root"
                            ]
                        }
                    }
                }
            ],
            "Version": "1"
        }
        ```

        **Note:** If you want to forbid other users, you can modify the username or add usernames in the Condition parameter.

4.  Grant the ECS read-only and Cloud Assistant permissions to the RAM user. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).

    ![Add Permissions pane](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4157898161/p238554.png)

    -   Grant the ECS read-only permission: On the **System Policy** tab, select **AliyunECSReadOnlyAccess**.
    -   Grant the Cloud Assistant permission: On the **Custom Policy** tab, select **commandUserPolicy** that you created in the previous step.
5.  Log on to the [Alibaba Cloud Management Console](https://ram.console.aliyun.com) as the RAM user.

6.  Run a Cloud Assistant command and verify the result. For more information, see [Immediate execution](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Immediate execution.md).

    -   The following figure shows the procedure by using the ECS console. You must set the Execution user parameter.

        ![Remote command](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5157898161/p240464.png)

        user01 is able to run the Cloud Assistant command, but an error is reported when the root user runs the command.

    -   The following figure shows the procedure by using the CLI. user01 is able to run the Cloud Assistant command, but an error is reported when the root user runs the command.

        ![CLI result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5157898161/p240630.png)


## Run Cloud Assistant commands on Windows instances as a regular user

To run Cloud Assistant commands on Windows instances, you must provide the username and password. For data security, you must host your logon password in Operation Orchestration Service \(OOS\) and perform encryption by using Key Management Service \(KMS\). For more information, see [Introduction to OOS](https://www.alibabacloud.com/help/doc-detail/120556.htm) and [What is Key Management Service?](/intl.en-US/Product Introduction/What is Key Management Service?.md)

You can perform the following operations to limit a RAM user from running Cloud Assistant commands as the root or system user.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using your Alibaba Cloud account.

2.  Create a RAM user. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md).

    The following table shows a configuration example.

    |Parameter|Example|
    |---------|-------|
    |**Logon Name**|commandUser|
    |**Display Name**|commandUser|
    |**Access Mode**|You can use Cloud Assistant by using the Alibaba Cloud Management Console or by calling API operations. In this example, select **Console Access** and **Programmatic Access**.**Note:** You can select an access mode based on your actual usage to implement least privilege-based management. |
    |**Console Password**|Select **Automatically Generate Default Password**.|
    |**Password Reset**|Select **Required at Next Logon**.|
    |**Multi-factor Authentication**|Select **Not Required**.|

    After you have created the RAM user, you must keep the username, password, and AccessKey pair of the RAM user.

3.  Create Cloud Assistant and KMS permission policies. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

    -   Cloud Assistant permission policy:

        Create a commandUserPolicy policy to limit users from running Cloud Assistant commands on the ECS instance. The following section shows the example policies. You can modify them based on your needs.

        -   RAM permission policy that allows some regular users \(such as user01 and user02\) to run Cloud Assistant commands on the ECS instance:

            ```
            {
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Action": [
                            "ecs:DescribeInstances",
                            "ecs:DescribeTagKeys",
                            "ecs:DescribeTags",
                            "ecs:CreateCommand",
                            "ecs:DescribeCommands",
                            "ecs:InvokeCommand",
                            "ecs:RunCommand",
                            "ecs:DeleteCommand",
                            "ecs:DescribeInvocations",
                            "ecs:DescribeInvocationResults",
                            "ecs:StopInvocation",
                            "ecs:DescribeCloudAssistantStatus",
                            "ecs:InstallCloudAssistant"
                        ],
                        "Resource": [
                            "acs:ecs:*:*:instance/*",
                            "acs:ecs:*:*:command/*"
                        ],
                        "Condition": {
                            "StringEquals": {
                                "ecs:CommandRunAs": [
                                    "user01",
                                    "user02"
                                ]
                            }
                        }
                    }
                ],
                "Version": "1"
            }
            ```

            **Note:** If you want to allow other users, you can modify the username or add usernames in the Condition parameter.

        -   RAM permission policy that forbids some users \(such as the root or system user\) to run Cloud Assistant commands on the ECS instance:

            ```
            {
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Action": [
                            "ecs:DescribeInstances",
                            "ecs:DescribeTagKeys",
                            "ecs:DescribeTags",
                            "ecs:CreateCommand",
                            "ecs:DescribeCommands",
                            "ecs:InvokeCommand",
                            "ecs:RunCommand",
                            "ecs:DeleteCommand",
                            "ecs:DescribeInvocations",
                            "ecs:DescribeInvocationResults",
                            "ecs:StopInvocation",
                            "ecs:DescribeCloudAssistantStatus",
                            "ecs:InstallCloudAssistant"
                        ],
                        "Resource": [
                            "acs:ecs:*:*:instance/*",
                            "acs:ecs:*:*:command/*"
                        ],
                        "Condition": {
                            "StringNotEqualsIgnoreCase": {
                                "ecs:CommandRunAs": [
                                    "system",
                                    "root"
                                ]
                            }
                        }
                    }
                ],
                "Version": "1"
            }
            ```

            **Note:** If you want to forbid other users, you can modify the username or add usernames in the Condition parameter.

    -   KMS permission policy:

        Create a kmsPolicy policy, as shown in the following example. For more information, see [RAM policy examples](/intl.en-US/Access Control and Audit/Use RAM to control access to resources.md).

        ```
        {
          "Version": "1",
          "Statement": [
            {
              "Effect": "Allow",
              "Action": [
                "kms:List*", "kms:Describe*",
                "kms:Encrypt", "kms:Decrypt", "kms:GenerateDataKey"
              ],
              "Resource": [
                "*"
              ]
            }
          ]
        }             
        ```

4.  Grant ECS, OOS, Cloud Assistant, and KMS permissions to the RAM user. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).

    ![Grant permissions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5157898161/p240583.png)

    -   Grant the ECS read-only permission: On the **System Policy** tab, select **AliyunECSReadOnlyAccess**.
    -   Grant the OOS read-only permission: On the **System Policy** tab, select **AliyunOOSReadOnlyAccess**.
    -   Grant the Cloud Assistant permission: On the **Custom Policy** tab, select **commandUserPolicy** that you created in the previous step.
    -   Grant the KMS permission: On the **Custom Policy** tab, select **kmsPolicy** that you created in the previous step.
5.  Configure a RAM role for the Windows instance.

    1.  Create a RAM policy. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

        Example:

        ```
        {
            "Version": "1",
            "Statement": [
                {
                    "Action": [
                        "kms:GetSecretValue"
                    ],
                    "Resource": "*",
                    "Effect": "Allow"
                },
                {
                    "Action": [
                        "oos:GetSecretParameter"
                    ],
                    "Effect": "Allow",
                    "Resource": "*"
                }
            ]
        }
        ```

    2.  Create a RAM role. For more information, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md).

        The following table shows a configuration example.

        |Parameter|Example|
        |---------|-------|
        |**Trusted entity type**|Select **Alibaba Cloud Service**.|
        |**Role Type**|Select **Normal Service Role**.|
        |**RAM Role Name**|AxtSecretRamRole|
        |**Select Trusted Service**|Select **Elastic Compute Service** from the drop-down list.|

    3.  Grant permissions to the RAM role. For more information, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).

    4.  Configure the RAM role for the ECS instance. For more information, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).

6.  Create encryption parameters in OOS to manage the logon passwords for Windows instances.

    **Note:** The encryption parameters must be located within the same region as the ECS instance. Otherwise, the logon password of the ECS instance cannot be hosted in OOS.

    The following table shows an example of configuring the password of user01.

    |Parameter|Example|
    |---------|-------|
    |**Parameter Name**|axtSecretPassword|
    |**KMS Key ID**|Select **Default Service CMK**.|
    |**Value**|The logon password of the Windows instance. In this example, enter the logon password of user01.|

7.  Log on to the [Alibaba Cloud Management Console](https://ram.console.aliyun.com) as the RAM user.

8.  Run a Cloud Assistant command and verify the result. For more information, see [Immediate execution](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Immediate execution.md).

    Run the Cloud Assistant command on the Windows instance and verify whether the permission settings have taken effect.

    -   The following figure shows the procedure by using the ECS console. You must set the Execution user and Password name parameters.

        ![Console result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5157898161/p240635.png)

        user01 is able to run the Cloud Assistant command, but an error is reported when the system user runs the command.

    -   The following figure shows the procedure by using the CLI. user01 is able to run the Cloud Assistant command, but an error is reported when the system user runs the command.

        ![CLI result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5157898161/p240636.png)


