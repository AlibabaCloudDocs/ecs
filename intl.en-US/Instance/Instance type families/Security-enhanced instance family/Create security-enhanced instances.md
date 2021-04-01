# Create security-enhanced instances

When you create a security-enhanced instance, you must select a specific operating system. If you use an Alibaba Cloud trusted system, you must also obtain the corresponding permissions so that the security-enhanced instance can report the trusted information to Alibaba Cloud Security Center when the instance starts. This topic describes how to create a security-enhanced instance.

## Create a security-enhanced instance in the ECS console

The procedure for creating a security-enhanced instance in the ECS console is similar to that for creating a non-security-enhanced instance. However, you must pay attention to some specific options when you create a security-enhanced instance. This procedure describes the specific configurations to be made when you create a security-enhanced instance. For other general configurations, see [t17291.md\#](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

When you create a security-enhanced instance in the ECS console, you are prompted to complete the following operations:

-   Enable Key Management Service \(KMS\). After KMS is enabled, a service key is automatically created. You do not need to pay for this key.
-   Create a RAM role and grant permissions to this role. Alibaba Cloud provides you with system policies for trusted services. You can follow the wizard to complete the settings when you create an instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Click **Create Instance**.

4.  Configure the settings in the Basic Configurations step.

    Take note of the following items:

    ![Basic configurations](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231806.png)

    -   **Instance Type**: You can select a security-enhanced instance type.

        **Note:** The seventh-generation security-enhanced instance families \(g7t, c7t, and r7t\) support SGX encrypted computing. When you create an instance of the g7t, c7t, or r7t instance family in the ECS console, the Alibaba Cloud SGX runtime is automatically installed. For information about how to build an SGX encrypted computing environment on instances of the g7t, c7t, or r7t instance families, see [t2057424.md\#](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Build an SGX encrypted computing environment.md).

    -   **Image**:

        -   To create an instance of a sixth-generation security-enhanced instance family \(g6t, c6t, or r6t\), you can select **Alibaba Cloud Linux 2.1903 64-bit \(Trusted\)** or **CentOS 7.8 64-bit \(Trusted\)**.
        -   To create an instance of a seventh-generation security-enhanced instance family \(g7t, c7t, or r7t\), you can select **Alibaba Cloud Linux 2.1903 64-bit \(UEFI\)**.
        **Note:** When you create a security-enhanced instance, **Trusted System** is automatically selected. The Alibaba Cloud trusted system verifies the instance when the instance starts. If you want to use a self-managed trusted service system, you can clear **Trusted System**.

5.  Click **Next: Networking**. If the **Enable Key Management Service \(KMS\)** dialog box appears, click **Enable**.

    KMS must be enabled. Otherwise, the security-enhanced instance cannot be created. If you have enabled KMS, the dialog box does not appear. Proceed with the next step.

6.  Configure the settings in the Networking step.

7.  In the System Configurations step, specify **RAM Role**.

    If **Trusted System** is enabled for your instance, you must specify a RAM role for the instance. The RAM role must be granted permissions to access the trusted services. Alibaba Cloud provides you with the corresponding **AliyunECSInstanceForYundunSysTrustRole** service role. We recommend that you configure and select this role by performing the following steps.

    **Note:** If you need more precise or customized configurations, create a role and grant it permissions based on your needs. When you create a RAM role, you must take some precautions. For more information, see [\#section\_y82\_9i9\_35k](#section_y82_9i9_35k).

    1.  Click here to authorize.

        ![Authorize First](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231953.png)

    2.  In the **Cloud Resource Access Authorization** message, click **Confirm Authorization**.

    3.  In the message that appears, click **Confirm Authorization**.

    4.  Click **Authorized**.

        ![Confirm Authorization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231920.png)

    5.  Select **AliyunECSInstanceForYundunSysTrustRole** as the RAM role.

        ![Set RAM Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3684482161/p231921.png)

    **Note:** You can also skip the authorization step and grant permissions after the instance is created. For more information, see the [t9665.md\#](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md) section.

8.  Follow the wizard to create the instance.


## Create a security-enhanced instance by calling an API operation

When you call an API operation to create a security-enhanced instance, take note of the following items:

-   KMS must be enabled. Otherwise, the security-enhanced instance cannot be created. For more information, see [t1864312.md\#](/intl.en-US/Quick Start/Activate KMS.md).
-   If you use an Alibaba Cloud trusted system, you must specify a RAM role for the security-enhanced instance to be created and this role must be granted permissions to access the trusted services. This way, the security-enhanced instance reports the trusted information to Alibaba Cloud Security Center when the instance starts. You can call an API operation to create a RAM role and grant permissions to this role. For more information, see [t9666.md\#](/intl.en-US/Security/Instance RAM roles/Use an instance RAM role by calling API operations.md). When you create a RAM role, you must take some precautions. For more information, see [\#section\_y82\_9i9\_35k](#section_y82_9i9_35k).

    **Note:** If you use a self-managed trusted service system, you do not need to specify the RAM role.


You can call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) or [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md) operation to create security-enhanced instances. The following table describes some parameters to take not of.

|Parameter|Description|Example|
|---------|-----------|-------|
|InstanceType|The instance type of the security-enhanced instance. ECS provides the following security-enhanced instance families:-   g7t
-   c7t
-   r7t
-   g6t
-   c6t

|ecs.c6t.large|
|ImageId|The ID of the image that is used to create the security-enhanced instance. You can call the [DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md) operation to query image IDs.|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210120.vhd|
|SystemDisk.Category|The category of the system disk to attach to the security-enhanced instance. Only enhanced SSDs \(ESSDs\) can be used.|cloud\_essd|
|VSwitchId|The ID of the vSwitch of the security-enhanced instance. This parameter is required because all security-enhanced instances are VPC-type instances.|vsw-bp134jzf285qg9u6w\*\*\*\*|
|RamRoleName|The name of the RAM role. You can also call the [AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md) to attach a RAM role to the instance after the instance is created.|AliyunECSInstanceForYundunSysTrustRole|
|UserData|The installation script used to install the Alibaba Cloud trusted system, which must be encoded in Base64.For the script content in plaintext before the script is encoded in Base64, see [\#section\_zu5\_7il\_en5](#section_zu5_7il_en5).

|```
IyEvYmluL3NoCkNVUlBBVEg9YHB3ZGAKU0NSSVBUX1BBVEg9Ii9kb3dubG9hZC9saW51eC9zY3JpcHQvVHJ1c3RBZ2VudEluc3RhbGwuc2giClJFR0lPTl9JRD1gY3VybCAtcyAtLXJldHJ5IDEgLS1tYXgtdGltZSAzIGh0dHA6Ly8xMDAuMTAwLjEwMC4yMDAvbGF0ZXN0L21ldGEtZGF0YS9yZWdpb24taWRgClVQREFURV9TSVRFMT1odHRwOi8vdHJ1c3RjbGllbnQtJHtSRUdJT05fSUR9Lm9zcy0ke1JFR0lPTl9JRH0taW50ZXJuYWwuYWxpeXVuY3MuY29tClVQREFURV9TSVRFMj1odHRwOi8vdHJ1c3RjbGllbnQtJHtSRUdJT05fSUR9Lm9zcy0ke1JFR0lPTl9JRH0uYWxpeXVuY3MuY29tClVQREFURV9TSVRFMz1odHRwOi8vdC10cnVzdGNsaWVudC0ke1JFR0lPTl9JRH0ub3NzLXskUkVHSU9OX0lEfS1pbnRlcm5hbC5hbGl5dW5jcy5jb20KTVNHX0lORk89ImRvd25sb2FkaW5nIGluc3RhbGwgc2NyaXB0IGZyb20gc2l0ZSIKTVNHX0VSUj0iZG93bmxvYWQgZmlsZSBlcnJvci4iCk1TR19PSz0idHJ1c3QgY2xpZW50IGluaXQgZG9uZS4iCgppbnN0YWxsKCkKewogIGVjaG8gIiR7TVNHX0lORk99IiIgMS4uLiIKICBjdXJsIC1mc1NMICIke1VQREFURV9TSVRFMX0iIiR7U0NSSVBUX1BBVEh9InxzaAogIGlmIFsgJD8gPT0gMCBdOyB0aGVuCiAgICByZXR1cm4gMQogIGZpCiAgZWNobyAiJHtNU0dfSU5GT30iIiAyLi4uIgogIGN1cmwgLWZzU0wgIiR7VVBEQVRFX1NJVEUyfSIiJHtTQ1JJUFRfUEFUSH0ifHNoCiAgaWYgWyAkPyA9PSAwIF07IHRoZW4KICAgIHJldHVybiAyCiAgZmkKICBlY2hvICIke01TR19JTkZPfSIiIDMuLi4iCiAgY3VybCAtZnNTTCAiJHtVUERBVEVfU0lURTN9IiIke1NDUklQVF9QQVRIfSJ8c2gKICBpZiBbICQ/ID09IDAgXTsgdGhlbgogICAgcmV0dXJuIDMKICBmaQogIGVjaG8gIiIgMT4mMgogIGV4aXQgMQp9CgppbnN0YWxsCmVjaG8gIiR7TVNHX09LfSIKCmV4aXQgMAo=
``` |

Sample requests:

```
https://ecs.aliyuncs.com/?Action=RunInstances
&RegionId=cn-hangzhou
&InstanceType=ecs.c6t.large
&ImageId=aliyun_2_1903_x64_20G_secured_alibase_20210120.vhd
&SystemDisk.Category=cloud_essd
&VSwitchId=vsw-bp134jzf285qg9u6w****
&SecurityGroupId=sg-bp1c3o8hzd14dovh****
&RamRoleName=AliyunECSInstanceForYundunSysTrustRole
&UserData=IyEvYmluL3NoCkNVUlBBVEg9YHB3ZGAKU0NSSVBUX1BBVEg9Ii9kb3dubG9hZC9saW51eC9zY3JpcHQvVHJ1c3RBZ2VudEluc3RhbGwuc2giClJFR0lPTl9JRD1gY3VybCAtcyAtLXJldHJ5IDEgLS1tYXgtdGltZSAzIGh0dHA6Ly8xMDAuMTAwLjEwMC4yMDAvbGF0ZXN0L21ldGEtZGF0YS9yZWdpb24taWRgClVQREFURV9TSVRFMT1odHRwOi8vdHJ1c3RjbGllbnQtJHtSRUdJT05fSUR9Lm9zcy0ke1JFR0lPTl9JRH0taW50ZXJuYWwuYWxpeXVuY3MuY29tClVQREFURV9TSVRFMj1odHRwOi8vdHJ1c3RjbGllbnQtJHtSRUdJT05fSUR9Lm9zcy0ke1JFR0lPTl9JRH0uYWxpeXVuY3MuY29tClVQREFURV9TSVRFMz1odHRwOi8vdC10cnVzdGNsaWVudC0ke1JFR0lPTl9JRH0ub3NzLXskUkVHSU9OX0lEfS1pbnRlcm5hbC5hbGl5dW5jcy5jb20KTVNHX0lORk89ImRvd25sb2FkaW5nIGluc3RhbGwgc2NyaXB0IGZyb20gc2l0ZSIKTVNHX0VSUj0iZG93bmxvYWQgZmlsZSBlcnJvci4iCk1TR19PSz0idHJ1c3QgY2xpZW50IGluaXQgZG9uZS4iCgppbnN0YWxsKCkKewogIGVjaG8gIiR7TVNHX0lORk99IiIgMS4uLiIKICBjdXJsIC1mc1NMICIke1VQREFURV9TSVRFMX0iIiR7U0NSSVBUX1BBVEh9InxzaAogIGlmIFsgJD8gPT0gMCBdOyB0aGVuCiAgICByZXR1cm4gMQogIGZpCiAgZWNobyAiJHtNU0dfSU5GT30iIiAyLi4uIgogIGN1cmwgLWZzU0wgIiR7VVBEQVRFX1NJVEUyfSIiJHtTQ1JJUFRfUEFUSH0ifHNoCiAgaWYgWyAkPyA9PSAwIF07IHRoZW4KICAgIHJldHVybiAyCiAgZmkKICBlY2hvICIke01TR19JTkZPfSIiIDMuLi4iCiAgY3VybCAtZnNTTCAiJHtVUERBVEVfU0lURTN9IiIke1NDUklQVF9QQVRIfSJ8c2gKICBpZiBbICQ/ID09IDAgXTsgdGhlbgogICAgcmV0dXJuIDMKICBmaQogIGVjaG8gIiIgMT4mMgogIGV4aXQgMQp9CgppbnN0YWxsCmVjaG8gIiR7TVNHX09LfSIKCmV4aXQgMAo=
&<Common request parameters>
```

Sample success responses:

-   XML format

    ```
    <RunInstancesResponse>
          <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
          <InstanceIdSets>
                <InstanceIdSet>i-bp16byi4f3fti5b3****</InstanceIdSet>
          </InstanceIdSets>
    </RunInstancesResponse>
    ```

-   JSON format

    ```
    {
        "RequestId": "BB694A51-7860-4B5C-B906-9B4077798672",
        "InstanceIdSets": {
            "InstanceIdSet": [
                "i-bp16byi4f3fti5b3****"
            ]
        }
    }
    ```


## Precautions on granting permissions to RAM roles

We recommend that you create a custom permission policy that contains the minimum required permissions and attach the policy to the RAM role. You can set the permission type to **System Policy** \(**AliyunSysTrustFullAccess**\) corresponding to the trusted service. You can also set the permission type to **Custom Policy** to implement precise authorization. The following section shows the precise policy for accessing trusted services.

**Note:** You can select a system policy such as AdministratorAccess that grants greater permissions. However, permissions of RAM roles are related to information security risks. We strongly recommend that you grant permissions based on the principle of least privilege. For more information, see [t12331.md\#](/intl.en-US/Product Introduction/What is RAM?.md).

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

## Script for installing an Alibaba Cloud trusted system

```
#! /bin/sh
CURPATH=`pwd`
SCRIPT_PATH="/download/linux/script/TrustAgentInstall.sh"
REGION_ID=`curl -s --retry 1 --max-time 3 http://100.100.100.200/latest/meta-data/region-id`
UPDATE_SITE1=http://trustclient-${REGION_ID}.oss-${REGION_ID}-internal.aliyuncs.com
UPDATE_SITE2=http://trustclient-${REGION_ID}.oss-${REGION_ID}.aliyuncs.com
UPDATE_SITE3=http://t-trustclient-${REGION_ID}.oss-{$REGION_ID}-internal.aliyuncs.com
MSG_INFO="downloading install script from site"
MSG_ERR="download file error."
MSG_OK="trust client init done."

install()
{
echo "${MSG_INFO}"" 1..."
curl -fsSL "${UPDATE_SITE1}""${SCRIPT_PATH}"|sh
if [ $? == 0 ]; then
return 1
fi
echo "${MSG_INFO}"" 2..."
curl -fsSL "${UPDATE_SITE2}""${SCRIPT_PATH}"|sh
if [ $? == 0 ]; then
return 2
fi
echo "${MSG_INFO}"" 3..."
curl -fsSL "${UPDATE_SITE3}""${SCRIPT_PATH}"|sh
if [ $? == 0 ]; then
return 3
fi
echo "" 1>&2
exit 1
}

install
echo "${MSG_OK}"

exit 0
```

