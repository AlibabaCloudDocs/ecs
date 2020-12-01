# Authorize a RAM user to manage an instance RAM role

If you want to bind, replace, or unbind an instance RAM role by using a RAM user, you must use the Alibaba Cloud account to authorize the RAM user to manage the instance RAM role. This operation can be performed only by an Alibaba Cloud account.

When you authorize a RAM user to manage an instance RAM role, you must grant the RAM user the PassRole permission on the instance RAM role. Without the PassRole permission, the RAM user cannot execute the permissions specified in role policies.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  In the left-side navigation pane, click **Users** under **Identities**.

3.  In the **User Logon Name/Display Name** column, find the target RAM user.

4.  Click **Add Permissions**. On the page that appears, the principal is automatically filled in.

5.  Click **Create Policy** to create a custom policy.

    The following code describes the custom policy. \[ECS RAM Action\] indicates the permissions that can be granted to the RAM user. For more information, see [Authentication rules](/intl.en-US/API Reference/Authentication rules.md).

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ecs: [ECS RAM Action]",
                    "ecs: CreateInstance",
                    "ecs: AttachInstanceRamRole",
                    "ecs: DetachInstanceRAMRole"
                ],
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": "ram:PassRole",
                "Resource": "*"
            }
        ]
    }
    ```

6.  Go back to the **Add Permissions** panel and click **Custom Policy** in the **Select Policy** section.

7.  In the **Authorization Policy Name** column, select the custom policy by clicking the corresponding row.

    **Note:** If you want to remove a policy, click the **×** icon corresponding to the policy in the Selected section.

8.  Click **OK**.

9.  Click **Finished**.


**Related topics**  


[CreatePolicy](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/CreatePolicy.md)

[AttachPolicyToRole](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/AttachPolicyToRole.md)

