# DescribeInstances

You can call this operation to query the details of one or more Elastic Compute Service \(ECS\) instances.

## Description

-   You can specify multiple request parameters to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions. However, if InstanceIds is set to an empty JSON array, it is regarded as a valid filter condition and an empty result is returned.
-   If you are using a RAM user or RAM role, an empty list is returned when the user or the role does not have the permission to call this operation. You can include the `DryRun` parameter in your request to check whether the empty list is caused by the lack of permissions.
-   When you call an API operation by using Alibaba Cloud Command Line Interface \(CLI\), you must specify request parameter values of different data types in the required formats. For more information, see [Parameter format overview](~~110340~~).
-   You can use one of the following methods to check the responses:
    -   Method 1: Use `NextToken` to configure the query token. Set this parameter to the `NextToken` value returned in the last call to the DescribeInstances operation. Then, use `MaxResults` to specify the maximum number of entries to return on each page.
    -   Method 2: Use `PageSize` to specify the number of entries to return on each page and then use `PageNumber` to specify the number of the page to return.

        You can use only one of the preceding methods. If a large number of entries are to be returned, we recommend that you use method 1. If NextToken is set, the PageSize and PageNumber request parameters become invalid.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstances|The operation that you want to perform. Set the value to DescribeInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|VpcId|String|No|v-bp67acfmxazb4p\*\*\*\*|The ID of the virtual private cloud \(VPC\). |
|VSwitchId|String|No|vsw-bp67acfmxazb4p\*\*\*\*|The ID of the vSwitch to which the instance is connected. |
|ZoneId|String|No|cn-hangzhou-g|The zone ID of the instance. |
|InstanceNetworkType|String|No|vpc|The network type of the instance. Valid values:

 -   classic: classic network
-   vpc: VPC |
|SecurityGroupId|String|No|sg-bp67acfmxazb4p\*\*\*\*|The ID of the security group to which the instance belongs. |
|InstanceIds|String|No|\["i-bp67acfmxazb4p\*\*\*\*", "i-bp67acfmxazb4p\*\*\*\*", ... "i-bp67acfmxazb4p\*\*\*\*"\]|The IDs of instances. The value can be a JSON array that consists of up to 100 instance IDs. Separate multiple instance IDs with commas \(,\). |
|PageNumber|Integer|No|1|The number of the page to return.

 Pages start from page 1.

 Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

 Maximum value: 100.

 Default value: 10. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The query token. Set the value to the `NextToken` value returned in the last call. |
|MaxResults|Integer|No|10|The maximum number of entries to return on each page.

 Maximum value: 100.

 Default value: 10. |
|InnerIpAddresses|String|No|\["10.1.1.1", "10.1.2.1", ... "10.1.10.1"\]|The internal IP addresses of classic network-type instances. This parameter is valid when InstanceNetworkType is set to classic. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|PrivateIpAddresses|String|No|\["172.16.1.1", "172.16.2.1", ... "172.16.10.1"\]|The private IP addresses of VPC-type instances. This parameter is valid when InstanceNetworkType is set to vpc. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|PublicIpAddresses|String|No|\["42.1.1.\*\*", "42.1.2.\*\*", ... "42.1.10.\*\*"\]|The public IP addresses of instances. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|EipAddresses|String|No|\["42.1.1.\*\*", "42.1.2.\*\*", ... "42.1.10.\*\*"\]|The elastic IP addresses \(EIPs\) of instance. This parameter is valid when InstanceNetworkType is set to vpc. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|InstanceChargeType|String|No|PostPaid|The billing method of the instance. Valid values:

 -   PostPaid: pay-as-you-go
-   PrePaid: subscription |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

 -   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic

 **Note:** When the **pay-by-traffic** billing method is used, the maximum inbound and outbound bandwidths are the upper limits of bandwidths and for reference only. When resources are insufficient, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method for network usage. |
|InstanceName|String|No|Test|The name of the instance. Fuzzy search by using the asterisk \(\*\) wildcard is supported. |
|ImageId|String|No|m-bp67acfmxazb4p\*\*\*\*|The ID of the image. |
|Status|String|No|Running|The status of the instance. Valid values:

 -   Pending
-   Running
-   Starting
-   Stopping
-   Stopped |
|LockReason|String|No|security|The reason why the instance is locked. |
|Filter.1.Key|String|No|CreationStartTime|The key of filter 1 used to query resources. Set the value to `CreationStartTime`. You can set both `Filter.1.Key` and `Filter.1.Value` to specify the beginning of the time range in which to query created resources. |
|Filter.2.Key|String|No|CreationEndTime|The key of filter 2 used to query resources. Set the value to `CreationEndTime`. You can set both `Filter.2.Key` and `Filter.2.Value` to specify the end of the time range in which to query created resources. |
|Filter.3.Key|String|No|ExpiredStartTime|The key of filter 3 used to query resources. Set the value to `ExpiredStartTime`. You can set both `Filter.3.Key` and `Filter.3.Value` to specify the beginning of the time range in which to query expired resources. |
|Filter.4.Key|String|No|ExpiredEndTime|The key of filter 4 used to query resources. Set the value to `ExpiredEndTime`. You can set both `Filter.4.Key` and `Filter.4.Value` specify the end of the time range in which to query expired resources. |
|Filter.1.Value|String|No|2017-12-05T22:40Z|The value of filter 1 used to query resources. Set the value to the beginning of the time range to query. When you specify this parameter, you must also specify `Filter.1.Key`. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Filter.2.Value|String|No|2017-12-06T22:40Z|The value of filter 2 used to query resources. Set the value to the end of the time range to query. When you specify this parameter, you must also specify `Filter.2.Key`. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Filter.3.Value|String|No|2017-12-07T22:40Z|The value of filter 3 used to query resources. Set the value to the beginning of the time range to query. When you specify this parameter, you must also specify `Filter.3.Key`. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Filter.4.Value|String|No|2017-12-08T22:40Z|The value of filter 4 used to query resources. Set the value to the end of the time range to query. When you specify this parameter, you must also specify `Filter.4.Key`. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|IoOptimized|Boolean|No|true|Specifies whether the instance is I/O optimized. |
|Tag.N.value|String|No|valueTest|The value of tag N.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure future compatibility. |
|Tag.N.key|String|No|keyTest|The key of tag N.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure future compatibility. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the instance. Valid values of N: 1 to 20.

 If a single tag is specified to query resources, up to 1,000 resources that are bound with this tag can be displayed in the response. If multiple tags are specified to query resources, up to 1,000 resources that are bound with all these tags can be displayed in the response. To query more than 1,000 resources that are bound with specified tags, call the [ListTagResources](~~110425~~) operation. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the instance. Valid values of N: 1 to 20. |
|InstanceType|String|No|ecs.g5.large|The instance type of the instance. |
|InstanceTypeFamily|String|No|ecs.g5|The instance family of the instance. |
|KeyPairName|String|No|KeyPairNameTest|The name of the Secure Shell \(SSH\) key pair for the instance. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the instance belongs. If this parameter is specified to query resources, up to 1,000 resources that belong to the specified resource group can be displayed in the response. |
|HpcClusterId|String|No|hpc-bp67acfmxazb4p\*\*\*\*|The ID of the High Performance Computing \(HPC\) cluster to which the instance belongs. |
|RdmaIpAddresses|String|No|10.10.10.102|The Remote Direct Memory Access \(RDMA\) IP addresses of HPC instances. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

 -   true: The validity of the request is checked but the request is not made. Check items include whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are specified. If the check fails, the corresponding error is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made. |
|AdditionalAttributes.N|RepeatList|No|META\_OPTIONS|The value of attribute N. Valid values of N: 1 to 20. Valid values:

 -   META\_OPTIONS: instance metadata
-   DDH\_CLUSTER: dedicated host cluster
-   NETWORK\_PRIMARY\_ENI\_IP: secondary IP addresses associated with the primary elastic network interface \(ENI\) of the instance |
|HttpEndpoint|String|No|enabled|Specifies whether to enable the access channel for instance metadata. Valid values:

 -   enabled
-   disabled

 Default value: enabled.

 **Note:** For more information about instance metadata, see [Metadata](~~49122~~). |
|HttpTokens|String|No|optional|Specifies whether to forcibly use the security-enhanced mode \(IMDSv2\) to access instance metadata. Valid values:

 -   optional: does not forcibly use the security-enhanced mode \(IMDSv2\).
-   required: forcibly uses the security-enhanced mode \(IMDSv2\). After you set this parameter to required, you cannot access the instance metadata in normal mode.

 Default value: optional.

 **Note:** For more information about the modes of accessing instance metadata, see [Access mode of instance metadata](~~150575~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Instances|Array of Instance| |Details about the instances. |
|Instance| | | |
|AutoReleaseTime|String|2017-12-10T04:04Z|The automatic release time of the pay-as-you-go instance. |
|ClusterId|String|c-bp67acfmxazb4p\*\*\*\*|The ID of the cluster to which the instance belongs.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|Cpu|Integer|8|The number of vCPUs. |
|CpuOptions|Struct| |The CPU options. |
|CoreCount|Integer|2|The number of CPU cores. |
|Numa|String|2|The number of threads allocated. Valid value: 2. |
|ThreadsPerCore|Integer|4|The number of threads per core. |
|CreationTime|String|2017-12-10T04:04Z|The time when the instance was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. For more information, see [ISO 8601](~~25696~~). |
|CreditSpecification|String|Standard|The performance mode of the burstable instance. Valid values:

 -   Standard: the standard mode. For more information, see the "Standard mode" section in [Overview](~~59977~~).
-   Unlimited: the unlimited mode. For more information, see the "Unlimited mode" section in [Overview](~~59977~~). |
|DedicatedHostAttribute|Struct| |Details about the dedicated hosts. It is an array that consists of the DedicatedHostClusterId, DedicatedHostId, and DedicatedHostName parameters. |
|DedicatedHostClusterId|String|dc-bp67acfmxazb4h\*\*\*\*|The ID of the dedicated host cluster. |
|DedicatedHostId|String|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host. |
|DedicatedHostName|String|testDedicatedHostName|The name of the dedicated host. |
|DedicatedInstanceAttribute|Struct| |The attributes of the instance on a dedicated host. |
|Affinity|String|default|Indicates whether the instance on a dedicated host is associated with the dedicated host. Valid values:

 -   default: The instance is not associated with the dedicated host. When the instance is restarted from the No Fees for Stopped Instances \(VPC-Connected\) state, the instance may be automatically deployed to another dedicated host in the automatic deployment resource pool.
-   host: The instance is associated with the dedicated host. When the instance is restarted from the No Fees for Stopped Instances \(VPC-Connected\) state, the instance still resides on the original dedicated host. |
|Tenancy|String|default|Indicates whether the instance is hosted on a dedicated host. Valid values:

 -   default: The instance is not hosted on a dedicated host.
-   host: The instance is hosted on a dedicated host. |
|DeletionProtection|Boolean|false|The release protection attribute of the instance. This parameter indicates whether you can use the ECS console or call the DeleteInstance operation to release the instance.

 -   true: Release protection is enabled for the instance.
-   false: Release protection is disabled for the instance.

 **Note:** This parameter is applicable only to pay-as-you-go instances. It can protect only against manual releases, not against automatic releases. |
|DeploymentSetGroupNo|Integer|1|The group number of the instance in a deployment set when the deployment set is used to distribute instances across multiple physical machines. |
|DeploymentSetId|String|ds-bp67acfmxazb4p\*\*\*\*|The ID of the deployment set. |
|Description|String|testDescription|The description of the instance. |
|DeviceAvailable|Boolean|true|Indicates whether data disks can be attached to the instance. |
|EcsCapacityReservationAttr|Struct| |Details about the capacity reservation related to the instance. |
|CapacityReservationId|String|cr-bp67acfmxazb4p\*\*\*\*|The ID of the capacity reservation. |
|CapacityReservationPreference|String|cr-bp67acfmxazb4p\*\*\*\*|The preference of the capacity reservation. |
|EipAddress|Struct| |Details about the EIP associated with the instance. |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*|The ID of the EIP. |
|Bandwidth|Integer|5|The maximum public bandwidth of the EIP. Unit: Mbit/s. |
|InternetChargeType|String|PayByTraffic|The billing method of the EIP. Valid values:

 -   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic |
|IpAddress|String|42.112.\*\*.\*\*|The EIP. |
|IsSupportUnassociate|Boolean|true|Indicates whether the EIP can be disassociated. |
|ExpiredTime|String|2017-12-10T04:04Z|The expiration time of the instance. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. For more information, see [ISO 8601](~~25696~~). |
|GPUAmount|Integer|4|The number of GPUs for the instance type. |
|GPUSpec|String|NVIDIA V100|The category of GPUs for the instance type. |
|HibernationOptions|Struct| |**Note:** This parameter is in invitational preview and unavailable. |
|Configured|Boolean|false|**Note:** This parameter is in invitational preview and unavailable. |
|HostName|String|testHostName|The hostname of the instance. |
|HpcClusterId|String|hpc-bp67acfmxazb4p\*\*\*\*|The ID of the HPC cluster to which the instance belongs. |
|ISP|String|null|**Note:** This parameter is in invitational preview and unavailable. |
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|The ID of the image that the instance is running. |
|InnerIpAddress|List|10.170.\*\*.\*\*|The internal IP address of the classic network-type instance. |
|InstanceChargeType|String|PostPaid|The billing method of the instance. Valid values:

 -   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|InstanceName|String|InstanceNameTest|The name of the instance. |
|InstanceNetworkType|String|vpc|The network type of the instance. Valid values:

 -   classic: classic network
-   vpc |
|InstanceType|String|ecs.g5.large|The instance type of the instance. |
|InstanceTypeFamily|String|ecs.g5|The instance family of the instance. |
|InternetChargeType|String|PayByTraffic|The billing method for network usage. Valid values:

 -   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic |
|InternetMaxBandwidthIn|Integer|50|The maximum inbound public bandwidth. Unit: Mbit/s. |
|InternetMaxBandwidthOut|Integer|5|The maximum outbound public bandwidth. Unit: Mbit/s. |
|IoOptimized|Boolean|true|Indicates whether the instance is I/O optimized. |
|KeyPairName|String|testKeyPairName|The name of the key pair. |
|LocalStorageAmount|Integer|2|The number of local disks attached to the instance. |
|LocalStorageCapacity|Long|1000|The capacity of local disks attached to the instance. |
|Memory|Integer|16384|The memory size of the instance. Unit: MiB. |
|MetadataOptions|Struct| |The metadata options. |
|HttpEndpoint|String|enabled|Indicates whether the access channel for instance metadata was enabled. Valid values:

 -   enabled
-   disabled |
|HttpPutResponseHopLimit|Integer|0|This parameter is unavailable. |
|HttpTokens|String|optional|Indicates whether to forcibly use the security hardening mode \(IMDSv2\) to access instance metadata. Valid values:

 -   optional: does not forcibly use the security-enhanced mode \(IMDSv2\).
-   required: forcibly uses the security-enhanced mode \(IMDSv2\). |
|NetworkInterfaces|Array of NetworkInterface| |The ENIs bound to the instance. |
|NetworkInterface| | | |
|Ipv6Sets|Array of Ipv6Set| |The IPv6 addresses assigned to the ENI. This parameter has a value only when the `AdditionalAttributes.N` request parameter is set to `NETWORK_PRIMARY_ENI_IP`. |
|Ipv6Set| | | |
|Ipv6Address|String|2408:4321:180:1701:94c7:bc38:3bfa:\*\*\*|The IPv6 address assigned to the ENI. |
|MacAddress|String|00:16:3e:32:b4:\*\*|The MAC address of the ENI. |
|NetworkInterfaceId|String|eni-2zeh9atclduxvf1z\*\*\*\*|The ID of the ENI. |
|PrimaryIpAddress|String|172.17.\*\*.\*\*\*|The primary private IP address of the ENI. |
|PrivateIpSets|Array of PrivateIpSet| |Details about the private IP addresses of the ENI. |
|PrivateIpSet| | | |
|Primary|Boolean|true|Indicates whether the IP address is the primary private IP address. |
|PrivateIpAddress|String|172.17.\*\*.\*\*|The private IP address of the instance. |
|Type|String|Primary|The type of the ENI. Valid values:

 -   Primary
-   Secondary |
|OSName|String|CentOS 7.4 64-bit|The name of the operating system for the instance. |
|OSNameEn|String|CentOS 7.4 64 bit|The English name of the operating system for the instance. |
|OSType|String|linux|The type of the operating system for the instance. Valid values:

 -   windows: Windows Server
-   linux |
|OperationLocks|Array of LockReason| |The reasons why the instance was locked. |
|LockReason| | | |
|LockMsg|String|The specified instance is locked due to financial reason.|The description of the locked instance. |
|LockReason|String|Recycling|The reason why the instance was locked. Valid values:

 -   financial: The instance was locked due to overdue payments.
-   security: The instance was locked due to security reasons.
-   recycling: The preemptible instance is locked and pending for release.
-   dedicatedhostfinancial: The instance was locked due to overdue payments for the dedicated host.
-   refunded: The instance was locked because a refund was made for the instance. |
|PublicIpAddress|List|121.40.\*\*.\*\*|The public IP address of the instance. |
|RdmaIpAddress|List|10.10.10.102|The RDMA IP address of the HPC instance. |
|Recyclable|Boolean|false|Indicates whether the instance can be recycled. |
|RegionId|String|cn-hangzhou|The region ID of the instance. |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the instance belongs. |
|SaleCycle|String|month|The billing cycle of the instance. |
|SecurityGroupIds|List|sg-bp67acfmxazb4p\*\*\*\*|The IDs of the security groups to which the instance belongs. |
|SerialNumber|String|51d1353b-22bf-4567-a176-8b3e12e4\*\*\*\*|The serial number of the instance. |
|SpotDuration|Integer|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

 -   Protection periods of 2, 3, 4, 5, and 6 hours are in invitational preview. If you want to set the protection period value to one of these values, submit a ticket.
-   A value of 0 indicates that the preemptible instance has no protection period. |
|SpotPriceLimit|Float|0.98|The maximum hourly price for the instance. It can be accurate to three decimal places. This parameter is valid when the SpotStrategy parameter is set to SpotWithPriceLimit. |
|SpotStrategy|String|NoSpot|The bidding policy for the preemptible instance. Valid values:

 -   NoSpot: The instance is a regular pay-as-you-go instance.
-   SpotWithPriceLimit: The instance is a preemptible instance with a user-defined maximum hourly price.
-   SpotAsPriceGo: The instance is a preemptible instance for which the market price is automatically used as the bid price. The market price can be up to the pay-as-you-go price. |
|StartTime|String|2017-12-10T04:04Z|The time when the instance was last started. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. For more information, see [ISO 8601](~~25696~~). |
|Status|String|Running|The status of the instance. |
|StoppedMode|String|KeepCharging|Indicates whether the instance continues to be billed after it is stopped. Valid values:

 -   KeepCharging: The billing of the instance continues after it is stopped, and resources are retained for the instance.
-   StopCharging: The billing of the instance stops when it is stopped. When the instance is stopped, its resources such as vCPUs, memory, and public IP address are released. You may be unable to restart the instance if some types of resources are out of stock in the current region.
-   Not-applicable: The No Fees for Stopped Instances \(VPC-Connected\) feature is not applicable to the instance. |
|Tags|Array of Tag| |The tags of the instance. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the instance. |
|TagValue|String|TestValue|The tag value of the instance. |
|VlanId|String|10|The virtual local area network \(VLAN\) ID of the instance.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|VpcAttributes|Struct| |The VPC attributes of the instance. |
|NatIpAddress|String|172.17.\*\*.\*\*|The Network Address Translation \(NAT\) IP address of the instance. It is used by ECS instances in different VPCs for communication. |
|PrivateIpAddress|List|172.17.\*\*.\*\*|The private IP address of the instance. |
|VSwitchId|String|vsw-2zeh0r1pabwtg6wcs\*\*\*\*|The ID of the vSwitch. |
|VpcId|String|vpc-2zeuphj08tt7q3brd\*\*\*\*|The ID of the VPC. |
|ZoneId|String|cn-hangzhou-g|The zone ID of the instance. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The value of the query token returned in this call. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|1|The total number of instances returned. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstances
&RegionId=cn-hangzhou
&PageSize=1
&PageNumber=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstancesResponse>
      <Instances>
            <Instance>
                  <ResourceGroupId>rg-bp67acfmxazb4p****</ResourceGroupId>
                  <Memory>16384</Memory>
                  <InstanceChargeType>PostPaid</InstanceChargeType>
                  <Cpu>8</Cpu>
                  <OSName>CentOS  7.4 64-bit</OSName>
                  <InstanceNetworkType>vpc</InstanceNetworkType>
                  <InnerIpAddress>
            </InnerIpAddress>
                  <ExpiredTime>2017-12-10T04:04Z</ExpiredTime>
                  <ImageId>m-bp67acfmxazb4p****</ImageId>
                  <EipAddress>
                        <AllocationId>eip-2ze88m67qx5z****</AllocationId>
                        <IpAddress>42.112.**.**</IpAddress>
                        <InternetChargeType>PayByTraffic</InternetChargeType>
                  </EipAddress>
                  <HostName>testHostName</HostName>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
                  <VlanId></VlanId>
                  <Status>Running</Status>
                  <MetadataOptions>
                        <HttpTokens>optional</HttpTokens>
                        <HttpEndpoint>enabled</HttpEndpoint>
                  </MetadataOptions>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <StoppedMode>KeepCharging</StoppedMode>
                  <CpuOptions>
                        <ThreadsPerCore>2</ThreadsPerCore>
                        <Numa>2</Numa>
                        <CoreCount>4</CoreCount>
                  </CpuOptions>
                  <StartTime>2017-12-10T04:04Z</StartTime>
                  <DeletionProtection>false</DeletionProtection>
                  <SecurityGroupIds>
                        <SecurityGroupId>sg-bp67acfmxazb4p****</SecurityGroupId>
                  </SecurityGroupIds>
                  <VpcAttributes>
                        <PrivateIpAddress>
                              <IpAddress>172.17.**.**</IpAddress>
                        </PrivateIpAddress>
                        <VpcId>vpc-2zeuphj08tt7q3brd****</VpcId>
                        <VSwitchId>vsw-2zeh0r1pabwtg6wcs****</VSwitchId>
                        <NatIpAddress>172.17.**.**</NatIpAddress>
                  </VpcAttributes>
                  <InternetChargeType>PayByTraffic</InternetChargeType>
                  <InstanceName>InstanceNameTest</InstanceName>
                  <DeploymentSetId></DeploymentSetId>
                  <InternetMaxBandwidthOut>5</InternetMaxBandwidthOut>
                  <SerialNumber>51d1353b-22bf-4567-a176-8b3e12e4****</SerialNumber>
                  <OSType>linux</OSType>
                  <CreationTime>2017-12-10T04:04Z</CreationTime>
                  <AutoReleaseTime>2017-12-10T04:04Z</AutoReleaseTime>
                  <Description>testDescription</Description>
                  <InstanceTypeFamily>ecs.g5</InstanceTypeFamily>
                  <DedicatedInstanceAttribute>
                        <Tenancy>default</Tenancy>
                        <Affinity>default</Affinity>
                  </DedicatedInstanceAttribute>
                  <PublicIpAddress>
                        <IpAddress>121.40.**.**</IpAddress>
                  </PublicIpAddress>
                  <GPUSpec></GPUSpec>
                  <NetworkInterfaces>
                        <NetworkInterface>
                              <Type>Primary</Type>
                              <PrimaryIpAddress>172.17.**.***</PrimaryIpAddress>
                              <NetworkInterfaceId>eni-2zeh9atclduxvf1z****</NetworkInterfaceId>
                              <MacAddress>00:16:3e:32:b4:**</MacAddress>
                              <PrivateIpSets>
                                    <PrivateIpSet>
                                          <PrivateIpAddress>172.17.**.**</PrivateIpAddress>
                                          <Primary>true</Primary>
                                    </PrivateIpSet>
                              </PrivateIpSets>
                        </NetworkInterface>
                  </NetworkInterfaces>
                  <SpotPriceLimit>0.98</SpotPriceLimit>
                  <DeviceAvailable>true</DeviceAvailable>
                  <SaleCycle>month</SaleCycle>
                  <InstanceType>ecs.g5.large</InstanceType>
                  <OSNameEn>CentOS  7.4 64 bit</OSNameEn>
                  <SpotStrategy>NoSpot</SpotStrategy>
                  <IoOptimized>true</IoOptimized>
                  <ZoneId>cn-hangzhou-g</ZoneId>
                  <ClusterId>c-bp67acfmxazb4p****</ClusterId>
                  <EcsCapacityReservationAttr>
                        <CapacityReservationPreference></CapacityReservationPreference>
                        <CapacityReservationId></CapacityReservationId>
                  </EcsCapacityReservationAttr>
                  <DedicatedHostAttribute>
                        <DedicatedHostId>dh-bp67acfmxazb4p****</DedicatedHostId>
                        <DedicatedHostName>testDedicatedHostName</DedicatedHostName>
                        <DedicatedHostClusterId>dc-bp67acfmxazb4h****</DedicatedHostClusterId>
                  </DedicatedHostAttribute>
                  <GPUAmount>4</GPUAmount>
                  <OperationLocks>
            </OperationLocks>
                  <InternetMaxBandwidthIn>50</InternetMaxBandwidthIn>
                  <Recyclable>false</Recyclable>
                  <RegionId>cn-hangzhou</RegionId>
                  <CreditSpecification></CreditSpecification>
            </Instance>
      </Instances>
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
</DescribeInstancesResponse>
```

`JSON` format

```
{
	"Instances": {
		"Instance": [
			{
				"ResourceGroupId": "rg-bp67acfmxazb4p****",
				"Memory": 16384,
				"InstanceChargeType": "PostPaid",
				"Cpu": 8,
				"OSName": "CentOS  7.4 64-bit",
				"InstanceNetworkType": "vpc",
				"InnerIpAddress": {
					"IpAddress": []
				},
				"ExpiredTime": "2017-12-10T04:04Z",
				"ImageId": "m-bp67acfmxazb4p****",
				"EipAddress": {
					"AllocationId": "eip-2ze88m67qx5z****",
					"IpAddress": "42.112.**.**",
					"InternetChargeType": "PayByTraffic"
				},
				"HostName": "testHostName",
				"Tags": {
					"Tag": [
						{
							"TagKey": "TestKey",
							"TagValue": "TestValue"
						}
					]
				},
				"VlanId": "",
				"Status": "Running",
				"MetadataOptions": {
					"HttpTokens": "optional",
					"HttpEndpoint": "enabled"
				},
				"InstanceId": "i-bp67acfmxazb4p****",
				"StoppedMode": "KeepCharging",
				"CpuOptions": {
					"ThreadsPerCore": 2,
					"Numa": "2",
					"CoreCount": 4
				},
				"StartTime": "2017-12-10T04:04Z",
				"DeletionProtection": false,
				"SecurityGroupIds": {
					"SecurityGroupId": [
						"sg-bp67acfmxazb4p****"
					]
				},
				"VpcAttributes": {
					"PrivateIpAddress": {
						"IpAddress": [
							"172.17.**.**"
						]
					},
					"VpcId": "vpc-2zeuphj08tt7q3brd****",
					"VSwitchId": "vsw-2zeh0r1pabwtg6wcs****",
					"NatIpAddress": "172.17.**.**"
				},
				"InternetChargeType": "PayByTraffic",
				"InstanceName": "InstanceNameTest",
				"DeploymentSetId": "",
				"InternetMaxBandwidthOut": 5,
				"SerialNumber": "51d1353b-22bf-4567-a176-8b3e12e4****",
				"OSType": "linux",
				"CreationTime": "2017-12-10T04:04Z",
				"AutoReleaseTime": "2017-12-10T04:04Z",
				"Description": "testDescription",
				"InstanceTypeFamily": "ecs.g5",
				"DedicatedInstanceAttribute": {
					"Tenancy": "default",
					"Affinity": "default"
				},
				"PublicIpAddress": {
					"IpAddress": [
						"121.40.**.**"
					]
				},
				"GPUSpec": "",
				"NetworkInterfaces": {
					"NetworkInterface": [
						{
							"Type": "Primary",
							"PrimaryIpAddress": "172.17.**.***",
							"NetworkInterfaceId": "eni-2zeh9atclduxvf1z****",
							"MacAddress": "00:16:3e:32:b4:**",
							"PrivateIpSets": {
								"PrivateIpSet": [
									{
										"PrivateIpAddress": "172.17.**.**",
										"Primary": true
									}
								]
							}
						}
					]
				},
				"SpotPriceLimit": 0.98,
				"DeviceAvailable": true,
				"SaleCycle": "month",
				"InstanceType": "ecs.g5.large",
				"OSNameEn": "CentOS  7.4 64 bit",
				"SpotStrategy": "NoSpot",
				"IoOptimized": true,
				"ZoneId": "cn-hangzhou-g",
				"ClusterId": "c-bp67acfmxazb4p****",
				"EcsCapacityReservationAttr": {
					"CapacityReservationPreference": "",
					"CapacityReservationId": ""
				},
				"DedicatedHostAttribute": {
					"DedicatedHostId": "dh-bp67acfmxazb4p****",
					"DedicatedHostName": "testDedicatedHostName",
					"DedicatedHostClusterId": "dc-bp67acfmxazb4h****"
				},
				"GPUAmount": 4,
				"OperationLocks": {
					"LockReason": []
				},
				"InternetMaxBandwidthIn": 50,
				"Recyclable": false,
				"RegionId": "cn-hangzhou",
				"CreditSpecification": ""
			}
		]
	},
	"TotalCount": 1,
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"PageSize": 10,
	"PageNumber": 1,
    "NextToken": "caeba0bbb2be03f84eb48b699f0a4883"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|404|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid|The error message returned because the specified InternetChargeType parameter is invalid.|
|404|InvalidLockReason.NotFound|The specified LockReason is not found|The error message returned because the specified LockReason parameter does not exist.|
|404|InvalidFilterKey.NotFound| |The error message returned because the specified start time or end time is invalid.|
|404|InvalidNetworkType.NotFound|The specified InstanceNetworkType is not found|The error message returned because the specified InstanceNetworkType parameter does not exist.|
|404|InvalidStatus.NotFound|The specified Status is not found|The error message returned because the specified Status parameter does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned because the specified Tag.N.Key and Tag.N.Value parameters do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the number of specified tags exceeds the upper limit.|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|The error message returned because the specified HpcClusterId parameter does not exist.|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|The error message returned because the specified HPC cluster to which the instance belongs is being created.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

