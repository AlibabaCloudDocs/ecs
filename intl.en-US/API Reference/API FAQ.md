---
keyword: [InvalidDataDiskCategory.NotSupported, Incomplete display, Temporarily upgrade bandwidth, IP address occupied, Public IP address]
---

# API FAQ

This topic provides answers to commonly asked questions about ECS API operations.

-   [What is ECS API?](#section_2mf_wov_wfu)
-   [What do I do if the error code InvalidDataDiskCategory.NotSupported is returned when I create an ECS instance?](#section_rqe_51b_fkf)
-   [How do I set sequential instance names or hostnames when I create multiple ECS instances?](#howToAddSequentialSuffix)
-   [How can I create an ECS instance that is assigned a public IP address?](#section_iop_1gx_4ub)
-   [Why can't the public IP address of the instance be pinged after I create an ECS instance by using an ECS API operation?](#section_2pr_bjo_kqj)
-   [What do I do if the error message "The specified IP is already in use." is returned when I use an ECS API operation to bind a public IP address to my instance?](#section_qxl_ubh_cso)
-   [Can I specify an effective period of time for the new bandwidth configurations when I modify the public bandwidth configurations of my instance by using an ECS API operation?](#section_opz_hdk_3ab)
-   [Why cannot all the security group rules in a security group be displayed when I use an ECS API operation or ECS SDK to query the details of the security group?](#section_0gg_gvb_36g)
-   [Why does a query made by using the ECS API, ECS SDK, or Alibaba Cloud CLI return only ten entries?](#section_vto_62a_f45)

## What is ECS API?

ECS API is an open source remote procedure call \(RPC\) API that provides API services for Alibaba Cloud users. You can use this API to manage and use ECS instances. The following figure shows the path along which a request is forwarded to call an API. For more information about how to call the ECS API, see [Quick start](/intl.en-US/API Reference/Quick start.md).

![What is ECS API?](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3713559951/p49776.png)

## What do I do if the error code InvalidDataDiskCategory.NotSupported is returned when I create an ECS instance?

-   Problem description: After you call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation to create an ECS instance, the following error information is returned:

    ```
    {
        "Code": "InvalidDataDiskCategory.NotSupported",
        "Message": "Specified disk category is not supported."
    }
    ```

-   Cause: The error occurred because disks of the specified category cannot be created in the specified zone.
-   Solution: We recommend that you call the [DescribeAvailableResource](/intl.en-US/API Reference/Regions/DescribeAvailableResource.md) operation to view the resources available in the zone where you want to create the ECS instance and make sure that resources in the zone are sufficient. You can also change the value of ZoneId and try again.

    ```
    aliyun ecs RunInstances --ImageId win2008_64_ent_r2_cn_40G_alibase_20150429.vhd --InstanceType ecs.g5.large --SecurityGroupId <TheSecuriytyGroupId> --SystemDiskCategory cloud_efficiency --ZoneId cn-hangzhou-c
    ```


## How do I set sequential instance names or hostnames when I create multiple ECS instances?

We recommend that you call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation to create multiple ECS instances. RunInstances contains the InstanceName and HostName parameters. You can set the instance name and the hostname that comply with the naming conventions.

Use the following methods to set the sequential instance names or hostnames for multiple ECS instances:

-   Add the sequential suffix specified by the UniqueSuffix parameter to the instance name specified by the InstanceName parameter or the hostname specified by the HostName parameter. The sequential suffix can be in the range from 001 to 999. Example: LocalHost001 and LocalHost002, and MyInstance001 and MyInstance002.
-   You must specify the instance names or hostnames for multiple ECS instances in the name\_prefix\[begin\_number,bits\]name\_suffix format. For example, if you set the InstanceName parameter to k8s-node-\[1,4\]-alibabacloud, the first ECS instance name is k8s-node-0001-alibabacloud. A maximum of 999,999 ECS instances are supported based on the instance names or hostnames that share the same prefix and suffix.
    -   name\_prefix: the prefix of the instance name or hostname. In the sequential naming convention, prefix is required. Otherwise, prefix is used as an common name.
    -   \[begin\_number,bits\]: the starting of the number in the instance name or hostname. Numbers in instance names or hostnames are incremental. These numbers identify different ECS instance names or hostnames. The \[begin\_number,bits\] field cannot contain spaces.
        -   begin\_number: the number from which starts the instance name. Valid values: 0 to 999999. Default value: 0.
        -   bits: the count of bits of the number in the instance name. Valid values: 1 to 6. Default value: 6.
        -   If you specify `[]` or `[,]`, begin\_number starts from 0 and bits is set to 6.
        -   If you specify `[99]` or `[99,]`, begin\_number starts from 99 and bits is set to 6.
        -   If the count of the digits occupied by begin\_number is greater than the value of bits, the digits of begin\_number takes precedence. For example, bits is set to 1 in \[1234,1\], and the value of begin\_number is set to 1234. bits is set to 6.
        -   If the sum of the begin\_number value and the number of ECS instances exceeds the maximum value of 999999, all ECS instances whose names that contain numbers greater than the maximum value use 999999.
    -   name\_suffix: the suffix of an instance name or hostname.

**Note:** If you do not add suffixes to the instance names or hostnames by using name\_suffix, but use the name\_prefix\[begin\_number,bits\] format, the UniqueSuffix parameter is ignored. For example, when InstanceName is set to instance-\[99,3\], and UniqueSuffix is set to true, the instance name is `instance099` instead of `instance099001`.

## How can I create an ECS instance that is assigned a public IP address?

-   Method 1: Call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation by using InternetMaxBandwidthOut set to a value greater than 0 to create an ECS instance. The new ECS instance is automatically assigned a public IP address.
-   Method 2: Call the [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md) operation to create an ECS instance. Then, call the [AllocatePublicIpAddress](/intl.en-US/API Reference/Networks/AllocatePublicIpAddress.md) operation to assign a public IP address to the instance.

## Why can't the public IP address of the instance be pinged after I create an ECS instance by using an ECS API operation?

-   Problem description: The new ECS instance that you created by using an ECS API operation cannot connect to the public network, and the public IP address of the instance cannot be pinged.
-   Cause: You do not add a security group rule to allow the public network to access the instance.
-   Solution: Call the [AuthorizeSecurityGroup](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md) operation to add an inbound rule to the security group to which the instance belongs to allow the public network to access the instance. For example, you can send the following request where IpProtocol is set to ICMP to call the AuthorizeSecurityGroup operation and add an inbound rule that allows the public IP address of this instance to be pinged from any other IP addresses:

    ```
    https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
    &SecurityGroupId=sg-bp15ed6xe1yxeycg7***
    &SourceCidrIp=0.0.0.0/0
    &IpProtocol=ICMP
    &PortRange=-1/-1
    &<Common request parameters>
    ```


## What do I do if the error message "The specified IP is already in use." is returned when I use an ECS API operation to bind a public IP address to my instance?

-   Problem description: When you call the [AllocatePublicIpAddress](/intl.en-US/API Reference/Networks/AllocatePublicIpAddress.md) operation to assign the public IP address specified by IpAddress to your ECS instance, the following error information is returned:

    ```
    {
        "Code": "IpInUse",
        "Message": "The specified IP is already in use."
    }
    ```

-   Cause: The specified IP address is already in use.
-   Solution: Check whether the IP address is already in use. If yes, try another IP address.

## Can I specify an effective period of time for the new bandwidth configurations when I modify the public bandwidth configurations of my instance by using an ECS API operation?

You can call the [ModifyInstanceNetworkSpec](/intl.en-US/API Reference/Networks/ModifyInstanceNetworkSpec.md) operation to modify the public bandwidth configurations of your ECS instance. The new bandwidth configurations take effect on the instance immediately after the modification is completed. If you want to temporarily modify the bandwidth configurations of your instance, set StartTime and EndTime to define an effective period of time.

If you are using an elastic IP address \(EIP\), you can call the [ModifyEipAddressAttribute](/intl.en-US/API reference/EIP/ModifyEipAddressAttribute.md) operation to make the modification but you cannot specify an effective period of time.

## Why cannot all the security group rules in a security group be displayed when I use an ECS API operation or ECS SDK to query the details of the security group?

Security group rules can be distinguished by their NIC types, public NIC \(internet\), and internal NIC \(intranet\). When you call the [DescribeSecurityGroupAttribute](/intl.en-US/API Reference/Security groups/DescribeSecurityGroupAttribute.md) operation to query the details of a security group, the NIC parameter is not required. However, if this parameter is not specified, the default value internet is used. Therefore, when you run the following CLI command to call the DescribeSecurityGroupAttribute operation, only the public security group rules, not all security group rules, in the queried security group are displayed:

```
aliyun ecs DescribeSecurityGroupAttribute --SecurityGroupId <TheSecurityGroupId> --RegionId <TheRegionId>
```

If you want to view the internal security group rules in a security group \(such as internal security group rules that allow access across internal networks or that are configured for the VPN firewall of Finance Cloud\), run the following command where NicType is set to intranet:

```
aliyun ecs DescribeSecurityGroupAttribute --SecurityGroupId <TheSecurityGroupId> --RegionId <TheRegionId> --NicType intranet
```

## Why does a query made by using the ECS API, ECS SDK, or Alibaba Cloud CLI return only ten entries?

For more information, see [Why only ten entries are returned for query request by using APIs or SDK](/intl.en-US/API Reference/Appendix/Why only ten entries are returned for query request by using APIs or SDK.md).

