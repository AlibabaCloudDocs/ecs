# Use RAM roles to access other Alibaba Cloud services

This topic describes how to enable applications on ECS instances to access other Alibaba Cloud services by using STS temporary credentials through RAM roles. The examples show how to enable Python to access Object Storage Service \(OSS\).

An instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

Previously, applications deployed on an ECS instance needed to use AccessKey pairs \(AKs\) to access other Alibaba Cloud services. An AK allows you to access Alibaba Cloud APIs with full permissions for your account. To facilitate the management of the AK by applications, you must store the AK in the application configuration files or otherwise store the AK in an ECS instance. These operations makes it more complicated to manage the AK and keep it confidential. If you need consistent deployment across regions, the AK is spread along with the images or instances created from the images. In these cases, you must update and redeploy each instance and image individually whenever you make changes to the AK.

You can attach a RAM role to an ECS instance, and use an STS temporary credential to access other cloud services from the applications within the instance. STS temporary credentials are generated and updated automatically. Applications can obtain the STS temporary credentials by using the instance metadata URL. You can use RAM roles and authorization policies to grant ECS instances with different or identical permissions to access other cloud services.

**Note:** All operations in this topic are performed in [OpenAPI Explorer](https://api.aliyun.com/?spm=a2c4g.11186623.2.16.21a418efIOhoV6) to help you get started with the examples. OpenAPI Explorer obtains a temporary AK of the current account through the information of the logged user, and initiates online resource operations on the current account. You will be charged for creating an instance. Release the instance after the operations are complete.

## Procedure

To enable Python to access OSS by using the STS temporary credential through RAM roles, perform the following operations:

1.  [Step 1. Create a RAM role and configure an authorization policy.](#section_bjf_m1b_l19)
2.  [Step 2. Create an ECS instance and attach the RAM role to the instance.](#section_z5t_5l9_x28)
3.  [Step 3. Access the instance metadata URL within the instance to obtain the STS temporary credential.](#section_r5g_ndb_7kj)
4.  [Step 4. Use SDK for Python to access OSS by using the STS temporary credential.](#section_fgc_wkp_1gq)

## Step 1. Create a RAM role and configure an authorization policy.

Perform the following operations to create a RAM role and configure an authorization policy:

1.  Create a RAM role.

    Call the CreateRole operation to create a RAM role.

    -   RoleName: Set the name of the RAM role. Set the parameter based on your needs. EcsRamRoleTest is used in this example.
    -   AssumeRolePolicyDocument: Specify a policy as follows to set the created role as a service role and authorize an Alibaba Cloud service \(ECS in this example\) to assume the role.

        ```
        {
            "Statement": [
                {
                    "Action": "sts:AssumeRole", 
                    "Effect": "Allow", 
                    "Principal": {
                        "Service": [
                            "ecs.aliyuncs.com"
                        ]
                    }
                }
            ], 
            "Version": "1"
        }
        ```

2.  Create an authorization policy.

    Call the CreatePolicy operation to create an authorization policy.

    -   PolicyName: the name of the authorization policy. EcsRamRolePolicyTest is used in this example.
    -   PolicyDocument: the content of the authorization policy. The following content is used in the example, indicating that the role has the OSS read-only permission.

        ```
        {
            "Statement": [
                {
                    "Action": [
                        "oss:Get*", 
                        "oss:List*"
                    ], 
                    "Effect": "Allow", 
                    "Resource": "*"
                }
            ], 
            "Version": "1"
        }
        ```

3.  Grant permissions to the role. Call the AttachPolicyToRole operation to grant permissions to the role.

    -   PolicyType: Set the parameter to Custom.
    -   PolicyName: Set the parameter to the name of the authorization policy created in the second step. EcsRamRolePolicyTest is used in this example.
    -   RoleName: Set the parameter to the name of the role created in the first step. EcsRamRoleTest is used in this example.

## Step 2. Create an ECS instance and attach the RAM role to the instance.

You can use one of the following methods to create an ECS instance and attach the RAM role to the instance:

-   Attach the RAM role to an existing ECS.

    Call the AttachInstanceRamRole operation to attach a RAM role to an existing VPC-type instance. The parameters are configured as follows:

    -   RegionId: the region ID of the ECS instance.
    -   RamRoleName: the name of the RAM role. EcsRamRoleTest is used in this example.
    -   InstanceIds: the IDs of VPC-type instances to which you want to attach the RAM role. \["i-bXXXXXXXX"\] is used in this example.
-   Create an ECS instance and attach the RAM role to the instance.

    To create an ECS instance and attach the RAM role to the instance, perform the following steps:

    1.  Create an instance.

        Call the CreateInstance operation and set parameters based on your actual needs. The following parameters are required:

        -   RegionId: the region ID of the instance. cn-hangzhou is used in this example.
        -   ImageId: the image of the instance. centos\_7\_03\_64\_40G\_alibase\_20170503.vhd is used in this example.
        -   InstanceType: the instance type of the instance. ecs.g6.large is used in this example.
        -   VSwitchId: the ID of the VSwitch in the VPC to which the instance belongs. RAM roles can be attached to only VPC-type ECS instances. Therefore, the VSwitchId parameter is required.
        -   RamRoleName: the name of the RAM role. EcsRamRoleTest is used in this example.
        If you want to authorize a RAM user to create an ECS instance with the specified RAM role attached, in addition to the permission to create an ECS instance, the RAM user must have the PassRole permission. Therefore, you must customize an authorization policy as follows and attach it to the RAM user.

        -   If you want to configure the RAM user to create an ECS instance, \[ECS RAM Action\] filed can be replaced with `ecs:CreateInstance`. You can also grant more permissions to the RAM user based on your actual needs.
        -   If you want to grant all ECS permissions to the RAM user, \[ECS RAM Action\] must be replaced with `ecs:*`.
        **Note:** For more information about values of \[ECS RAM Action\], see [Authentication rules](/intl.en-US/API Reference/Authentication rules.md).

        ```
        {
            "Statement": [
                {
                    "Action": "[ECS RAM Action]", 
                    "Resource": "*", 
                    "Effect": "Allow"
                }, 
                {
                    "Action": "ram:PassRole", 
                    "Resource": "*", 
                    "Effect": "Allow"
                }
            ], 
            "Version": "1"
        }
        ```

    2.  Configure the password and start the instance.
    3.  Configure the instance to access the Internet in the ECS console or by calling an API operation.

## Step 3. Access the instance metadata URL within the instance to obtain the STS temporary credential.

To obtain the STS temporary credential of the instance, perform the following steps.

**Note:** A new STS temporary credential is generated 30 minutes before the current one expires. Both STS credentials can be used during this period of time.

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Access `http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest` to obtain the STS temporary credential. The last part of the URL is the RAM role name, which must be replaced with the name you specified.

    **Note:** In this example, the `curl` command is used to access the preceding URL. If your instance is a Windows instance, see [Metadata](/intl.en-US/Instance/Manage instances/Metadata/Overview of instance metadata.md).

    The following content shows the sample response:

    ```
    [root@local ~]# curl http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest
    {
    "AccessKeyId" : "STS.J8XXXXXXXXXX4",
    "AccessKeySecret" : "9PjfXXXXXXXXXBf2XAW",
    "Expiration" : "2017-06-09T09:17:19Z",
    "SecurityToken" : "CAIXXXXXXXXXXXwmBkleCTkyI+",
    "LastUpdated" : "2017-06-09T03:17:18Z",
    "Code" : "Success"
    }
    ```


## Step 4. Use SDK for Python to access OSS by using the STS temporary credential.

In this example, SDK for Python is used to list 10 files in a specified OSS bucket located within the same region as the instance through the STS temporary credential.

Prerequisites:

-   The ECS instance is connected.
-   The ECS instance is installed with Python. If your instance is a Linux instance, pip is required.
-   An OSS bucket is created in the same region as the instance and the name and endpoint of the bucket are obtained. In this example, the bucket name is `ramroletest`, and the endpoint is `oss-cn-hangzhou.aliyuncs.com`.

Perform the following steps to use SDK for Python to access OSS:

1.  Run the `pip install oss2` command to install OSS SDK for Python.

2.  Run the following commands to test whether SDK for Python can be used to list 10 files in the specified OSS bucket:

    ```
    import oss2
    from itertools import islice
    auth = oss2.StsAuth(<AccessKeyId>, <AccessKeySecret>, <SecurityToken>)
    bucket = oss2.Bucket(auth, <Your endpoint>, <Your bucket name>)
    for b in islice(oss2.ObjectIterator(bucket), 10):
      print(b.key)
    ```

    where:

    -   The three parameters of `oss2.StsAuth` correspond to the AccessKeyId, AccessKeySecret, and SecurityToken values returned in the [Step 3. Access the instance metadata URL within the instance to obtain the STS credential](#section_r5g_ndb_7kj) section.
    -   The last two parameters of `oss2.Bucket` correspond to the name and endpoint of the bucket.
    The following content shows the sample response:

    ```
    [root@local ~]# python
    Python 2.7.5 (default, Nov  6 2016, 00:28:07)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-11)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import oss2
    >>> from itertools import islice
    >>> auth = oss2.StsAuth("STS.J8XXXXXXXXXX4", "9PjfXXXXXXXXXBf2XAW", "CAIXXXXXXXXXXXwmBkleCTkyI+")
    >>> bucket = oss2.Bucket(auth, "oss-cn-hangzhou.aliyuncs.com", "ramroletest")
    >>> for b in islice(oss2.ObjectIterator(bucket), 10):
    ...     print(b.key)
    ...
    ramroletest.txt
    test.shh
    ```


