# Use OOS Parameter Store in Cloud Assistant commands

You can use custom parameters in Cloud Assistant commands to write scripts and improve the reusability of commands. Operation Orchestration Service \(OOS\) provides the Parameter Store feature that allows you to configure common parameters and encryption parameters. You can use the Parameter Store feature of OOS in Cloud Assistant commands to manage custom parameters.

-   The Elastic Compute Service \(ECS\) instance on which you want to run Cloud Assistant commands meets the following requirements:
    -   The instance is in the **Running** \(`Running`\) state.
    -   The instance has the Cloud Assistant client installed. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).
-   OOS is activated. For more information, see [Introduction to OOS](https://www.alibabacloud.com/help/doc-detail/120556.htm).
-   Key Management Service \(KMS\) is activated if you want to use encryption parameters. For more information, see [What is Key Management Service?](/intl.en-US/Product Introduction/What is Key Management Service?.md)

You can use `{{parameterName}}` to indicate a custom parameter in Cloud Assistant commands. For example, you can run the `adduser {{username}}` command to add a username for a Linux instance. In this command, username indicates a custom parameter. You can specify its value in the Parameters parameter of [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md) or [InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md).

You can reference parameters in OOS Parameter Store to use them for a variety of purposes. Parameters in Parameter Store are classified into common parameters and encryption parameters. Cloud Assistant uses `{{oos:}}` to define common parameters and uses `{{oos-secret:}}` to define encryption parameters.

-   We recommend that you use common parameters to store non-sensitive data. For more information, see [Use common parameters in Cloud Assistant commands](#section_cdy_0u6_hbo).
-   We recommend that you use encryption parameters to store sensitive data such as passwords. For more information, see [Use encryption parameters in Cloud Assistant commands](#section_1m4_3wb_7s1).

## Use common parameters in Cloud Assistant commands

If you run a Cloud Assistant command as a RAM user, you must attach a policy to the RAM user. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md) and [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md). RAM users must have the API permissions from Cloud Assistant and OOS Parameter Store to run Cloud Assistant commands by using common parameters. The following code provides an example on the policy to attach to the RAM user.

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
                "ecs:InstallCloudAssistant",
                "oos:GetParameters",
                "oos:GetParameter"
            ],
            "Resource": "*"
        }
    ],
    "Version": "1"
}
```

If your command does not involve sensitive data, you can use common parameters. This section describes how to use common parameters of OOS Parameter Store in a Cloud Assistant command. In the example, a user is added to a Linux instance.

1.  Create common parameters by using OOS Parameter Store. For more information, see [Manage common parameters]().

    The following table provides an example of adding a username parameter to the common parameters. The value of the parameter is set to user01. You can change the value to suit your needs.

    |Parameter|Example|
    |---------|-------|
    |**Parameter Name**|username|
    |**Parameter Type**|String|
    |**Value**|user01|

2.  Use ECS SDK for Java to call the [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md) operation to run a Cloud Assistant command.

    The following code provides an example on how to create a user for a Linux instance by running a Cloud Assistant command. The command content is `adduser {{oos:username}}`. In this command, `{{oos:username}}` indicates that the username is specified by the username parameter.

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.ecs.model.v20140526.RunCommandRequest;
    import com.aliyuncs.ecs.model.v20140526.RunCommandResponse;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    
    import java.util.ArrayList;
    import java.util.List;
    
    public class addUserName {
        public static void main(String[] args) {
            # Set the region ID and the AccessKey pair. 
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            RunCommandRequest request = new RunCommandRequest();
            # Set the region ID of the instance. 
            request.setRegionId("cn-hangzhou");
            # Set the language of the Cloud Assistant command. In this example, shell is used. 
            request.setType("RunShellScript");
            # Set the command content. In this example, a user is added to a Linux instance. The username parameter specifies the username of the user. 
            request.setCommandContent("adduser {{oos:username}}");
    
            List<String> instanceIdList = new ArrayList<String>();
            # Set the ID of the instance on which to run the Cloud Assistant command. 
            instanceIdList.add("i-bp1dktddjsg7oh11****");
            request.setInstanceIds(instanceIdList);
            # Set the Cloud Assistant command to support custom parameters. 
            request.setEnableParameter(true);
    
            try {
                RunCommandResponse response = client.getAcsResponse(request);
                System.out.println(new Gson().toJson(response));
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
        }
    }
    ```

    The following command output is returned:

    ```
    {
        "requestId": "67D1BD1A-0D08-42C3-AFD9-A3397CD67CD1",
        "commandId": "c-hz01hkgs19i****",
        "invokeId": "t-hz01hkgs19s****"
    }
    ```

3.  Check the output of the Cloud Assistant command.

    You can log on to the ECS instance to check whether the Cloud Assistant command has taken effect. Perform the following steps to check whether user01 is added to the Linux instance:

    1.  Log on to the ECS instance. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

    2.  Run the following command to check whether user01 is added:

        ```
        cat /etc/passwd |grep user01
        ```

        If the following command output is returned, user01 is added.

        ![Add user01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7247091261/p266512.png)


## Use encryption parameters in Cloud Assistant commands

If you run a Cloud Assistant command as a RAM user, you must attach a policy to the RAM user. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md) and [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md). RAM users must have the API permissions from Cloud Assistant, OOS Parameter Store, and KMS to run Cloud Assistant commands by using encryption parameters. The following code provides an example on the policy to attach to the RAM user.

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
                "ecs:InstallCloudAssistant",
                "oos:GetParameters",
                "oos:GetSecretParameters",
                "oos:GetParameter",
                "oos:GetSecretParameter",
                "kms:GetSecretValue"
            ],
            "Resource": "*"
        }
    ],
    "Version": "1"
}
```

If your command involves sensitive data such as passwords used to log on to your server or database, we recommend that you use encryption parameters to improve the security of your command. This section describes how to use encryption parameters of OOS Parameter Store in a Cloud Assistant command. In the example, the password of a Linux instance user is modified.

**Note:** Before you perform the following operations, you must have created a user for the instance. For information about how to add users to Linux instances, see [Use common parameters in Cloud Assistant commands](#section_cdy_0u6_hbo).

1.  Create encryption parameters and common parameters by using OSS Parameter Store. For more information, see [Manage common parameters]() and [Manage encryption parameters]().

    The following tables provide examples of creating a username parameter and a password parameter in OOS Parameter Store.

    -   Add a username parameter to the common parameters. The value of the parameter is set to user01. You can change the value to suit your needs.

        |Parameter|Example|
        |---------|-------|
        |**Parameter Name**|username|
        |**Parameter Type**|String|
        |**Value**|user01|

    -   Add a password parameter to the encryption parameters. The value of the parameter is set to MyPassword01. You can change the value to suit your needs.

        |Parameter|Example|
        |---------|-------|
        |**Parameter Name**|password|
        |**KMS Key ID**|Default Service CMK|
        |**Value**|MyPassword01**Note:** The password used in this example is for reference only. Do not use it in the online environment. |

2.  Bind a RAM role to the ECS instance.

    1.  Create a RAM role. For more information, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md).

        The following table provides a configuration example.

        |Parameter|Example|
        |---------|-------|
        |**Trusted entity type**|Select **Alibaba Cloud Service**.|
        |**Role Type**|Select **Normal Service Role**.|
        |**RAM Role Name**|AxtParametersRamRole|
        |**Select Trusted Service**|Select **Elastic Compute Service** from the drop-down list.|

    2.  Create a policy for the RAM role. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

        The policy name is AxtParametersRamPolicy. The following code shows the policy content. The policy allows calls to the following KMS and OOS API operations: GetSecretValue, GetParameters, GetSecretParameters, GetParameter, and GetSecretParameter.

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
                        "oos:GetParameters",
                        "oos:GetSecretParameters",
                        "oos:GetParameter",
                        "oos:GetSecretParameter"
                    ],
                    "Effect": "Allow",
                    "Resource": "*"
                }
            ]
        }
        ```

    3.  Attach the AxtParametersRamPolicy policy to the AxtParametersRamRole role. For more information, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).

    4.  Bind the AxtParametersRamRole role to the ECS instance. For more information, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).

3.  Use ECS SDK for Java to call the [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md) operation to run a Cloud Assistant command.

    The following example describes how to modify the password for a Linux instance user by running a Cloud Assistant command. The following code shows the command content:

    ```
    echo '{{oos-secret:password}}' | passwd '{{oos:username}}' --stdin"
    ```

    In this command, `{{oos-secret:password}}` indicates that the new password is specified by the password parameter. `{{oos:username}}` indicates that the username is specified by the username parameter.

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.ecs.model.v20140526.RunCommandRequest;
    import com.aliyuncs.ecs.model.v20140526.RunCommandResponse;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    
    import java.util.ArrayList;
    import java.util.List;
    
    public class changePassword {
        public static void main(String[] args) {
            # Set the region ID and the AccessKey pair. 
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            RunCommandRequest request = new RunCommandRequest();
            # Set the region ID of the instance. 
            request.setRegionId("cn-hangzhou");
            # Set the language of the Cloud Assistant command. In this example, shell is used. 
            request.setType("RunShellScript");
            # In this example, the password of the Linux instance user is modified. The username is specified by the username parameter and the password is specified by the password parameter. 
            request.setCommandContent(
                    "echo '{{oos-secret:password}}' | passwd '{{oos:username}}' --stdin");
    
            List<String> instanceIdList = new ArrayList<String>();
            instanceIdList.add("i-bp1dktddjsg7oh11****");
            request.setInstanceIds(instanceIdList);
            request.setEnableParameter(true);
    
            try {
                RunCommandResponse response = client.getAcsResponse(request);
                System.out.println(new Gson().toJson(response));
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
        }
    
    }
    ```

    The following command output is returned:

    ```
    {
        "requestId": "C73D7B90-6503-4DB4-844C-9412AC55ECC5",
        "commandId": "c-hz01hnyd4e8****",
        "invokeId": "t-hz01hnyd4ed****"
    }
    ```

4.  Check the output of the Cloud Assistant command.

    You can log on to the ECS instance by using the new password to check whether the Cloud Assistant command has taken effect. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).


