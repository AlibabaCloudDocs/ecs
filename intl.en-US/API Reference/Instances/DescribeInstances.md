# DescribeInstances

You can call this operation to query details of one or more instances.

## Description

-   You can specify multiple request parameters to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions. However, if InstanceIds is set to an empty JSON array, it is regarded as a valid filter condition and an empty result is returned.
-   If you are using a RAM user or RAM role, an empty list is returned when the user or the role has no permission to call this operation. You can add the `DryRun` parameter in your request to determine whether the empty list is caused by the lack of permission.
-   When you call an API operation by using Alibaba Cloud Command Line Interface \(CLI\), you must specify request parameter values of different data types in the required formats. For more information, see [CLI parameter format](~~110340~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstances|The operation that you want to perform. Set the value to DescribeInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|VpcId|String|No|v-bp67acfmxazb4p\*\*\*\*|The ID of the VPC. |
|VSwitchId|String|No|vsw-bp67acfmxazb4p\*\*\*\*|The ID of the vSwitch to which the instance is connected. |
|ZoneId|String|No|cn-hangzhou-g|The zone ID of the instance. |
|InstanceNetworkType|String|No|vpc|The network type of the instance. Valid values:

-   classic: classic network
-   vpc: VPC |
|SecurityGroupId|String|No|sg-bp67acfmxazb4p\*\*\*\*|The ID of the security group to which the instance belongs. |
|InstanceIds|String|No|\["i-bp67acfmxazb4p\*\*\*\*", "i-bp67acfmxazb4p\*\*\*\*", ... "i-bp67acfmxazb4p\*\*\*\*"\]|The IDs of instances. The value can be a JSON array that consists of up to 100 instance IDs. Separate multiple instance IDs with commas \(,\). |
|PageNumber|Integer|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1 |
|PageSize|Integer|No|10|The number of entries to return on each page.

Valid values: 1 to 100

Default value: 10 |
|InnerIpAddresses|String|No|\["10.1.1.1", "10.1.2.1", ... "10.1.10.1"\]|The internal IP addresses of classic network-type instances. This parameter takes effect when InstanceNetworkType is set to classic. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|PrivateIpAddresses|String|No|\["172.16.1.1", "172.16.2.1", ... "172.16.10.1"\]|The private IP addresses of VPC-type instances. This parameter takes effect when InstanceNetworkType is set to vpc. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|PublicIpAddresses|String|No|\["42.1.1. \*\*", "42.1.2. \*\*", ... "42.1.10. \*\*"\]|The public IP addresses of instances. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|EipAddresses|String|No|\["42.1.1. \*\*", "42.1.2. \*\*", ... "42.1.10. \*\*"\]|The elastic IP addresses \(EIPs\) of the instances. This parameter takes effect when InstanceNetworkType is set to vpc. The value can be a JSON array that consists of up to 100 IP addresses. Separate multiple IP addresses with commas \(,\). |
|InstanceChargeType|String|No|PostPaid|The billing method of the instance. Valid values:

-   PostPaid: pay-as-you-go
-   PrePaid: subscription |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

-   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic

**Note:** When the **pay-by-traffic** billing method is used, the peak inbound and outbound bandwidths are used as bandwidth limits instead of guaranteed performance metrics. In scenarios where demands exceed resource supplies, the peak bandwidths may be limited. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method. |
|InstanceName|String|No|Test|The name of the instance. Fuzzy search with the asterisk \(\*\) wildcard is supported. |
|ImageId|String|No|m-bp67acfmxazb4p\*\*\*\*|The ID of the image. |
|Status|String|No|Running|The status of the instance. Valid values:

-   Pending
-   Running
-   Starting
-   Stopping
-   Stopped |
|LockReason|String|No|security|The reason why the instance is locked. |
|IoOptimized|Boolean|No|true|Specifies whether the instance is I/O optimized. |
|Tag.N.value|String|No|valueTest|The value of tag N.

**Note:** We recommend that you use the Tag.N.Value parameter to ensure future compatibility. |
|Tag.N.key|String|No|keyTest|The key of tag N.

**Note:** We recommend that you use the Tag.N.Key parameter to ensure future compatibility. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the instance. Valid values of N: 1 to 20.

If a single tag is specified to query resources, up to 1,000 resources that are bound with this tag can be displayed in the response. If multiple tags are specified to query resources, up to 1,000 resources that are bound with all these tags can be displayed in the response. To query more than 1,000 resources that are bound with specified tags, call the [ListTagResources](~~110425~~) operation. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the instance. Valid values of N: 1 to 20. |
|InstanceType|String|No|ecs.g5.large|The instance type. |
|InstanceTypeFamily|String|No|ecs.g5|The instance family. |
|KeyPairName|String|No|KeyPairNameTest|The name of the SSH key pair bound to the instance. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the instance belongs. If this parameter is specified to query resources, up to 1,000 resources that belong to the specified resource group can be displayed in the response. |
|HpcClusterId|String|No|hpc-bp67acfmxazb4p\*\*\*\*|The ID of the HPC cluster to which the instance belongs. |
|RdmaIpAddresses|String|No|10.10.10.102|The RDMA IP addresses of HPC instances. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are specified. If the check fails, the corresponding error is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made. |
|AdditionalAttributes.N|RepeatList|No|META\_OPTIONS|The value of attribute N. Valid values of N: 1 to 20. Valid values:

-   META\_OPTIONS: instance metadata
-   DDH\_CLUSTER: dedicated host cluster |
|HttpEndpoint|String|No|enabled|Specifies whether the access channel for instance metadata is enabled. Valid values:

-   enabled
-   disabled

Default value: enabled

**Note:** For more information about instance metadata, see [Overview of instance metadata](~~49122~~). |
|HttpTokens|String|No|optional|Specifies whether the security hardening mode \(IMDSv2\) is forcibly used to access instance metadata. Valid values:

-   optional: The security hardening mode \(IMDSv2\) is not forcibly used.
-   required: The security hardening mode \(IMDSv2\) is forcibly used. After you set this parameter to required, you cannot access the instance metadata in normal mode.

Default value: optional

**Note:** For more information about modes of accessing instance metadata, see [Modes of accessing instance metadata](~~150575~~). |

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
|CreationTime|String|2017-12-10T04:04Z|The time when the instance was created. |
|CreditSpecification|String|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: standard mode. For more information, see the "Standard mode" section of [Burstable instances](~~59977~~).
-   Unlimited: unlimited mode. For more information, see the "Unlimited mode" section of [Burstable instances](~~59977~~). |
|DedicatedHostAttribute|Struct| |The attributes of the hosts. The DedicatedHostClusterId, DedicatedHostId, and DedicatedHostName parameters are provided. |
|DedicatedHostClusterId|String|dc-bp67acfmxazb4h\*\*\*\*|The ID of the dedicated host cluster. |
|DedicatedHostId|String|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host. |
|DedicatedHostName|String|testDedicatedHostName|The name of the dedicated host. |
|DedicatedInstanceAttribute|Struct| |The attribute of the instance on the dedicated host. |
|Affinity|String|default|Indicates whether the instance on the dedicated host is associated with the dedicated host. Valid values:

-   default: The instance is not associated with the dedicated host. When the instance is restarted from the No Fees for Stopped Instances \(VPC-Connected\) state, the instance may be automatically deployed to another dedicated host in the automatic deployment resource pool.
-   host: The instance is associated with the dedicated host. When the instance is restarted from the No Fees for Stopped Instances \(VPC-Connected\) state, the instance still resides on the original dedicated host. |
|Tenancy|String|default|Indicates whether the instance is hosted on a dedicated host. Valid values:

-   default: The instance is not hosted on a dedicated host.
-   host: The instance is hosted on a dedicated host. |
|DeletionProtection|Boolean|false|The release protection attribute of the instance. It indicates whether you can use the ECS console or call the DeleteInstance operation to release the instance.

-   true: Release protection is enabled for the instance.
-   false: Release protection is disabled for the instance.

**Note:** This parameter is applicable only to pay-as-you-go instances. It can protect only against manual releases, not against automatic releases. |
|DeploymentSetGroupNo|Integer|1|The group No. of the instance in a deployment set when the deployment set is used to distributed instances across multiple physical machines. |
|DeploymentSetId|String|ds-bp67acfmxazb4p\*\*\*\*|The ID of the deployment set. |
|Description|String|testDescription|The description of the instance. |
|DeviceAvailable|Boolean|true|Indicates whether data disks can be attached to the instance. |
|EcsCapacityReservationAttr|Struct| |The capacity reservation attributes of the ECS instance. |
|CapacityReservationId|String|cr-bp67acfmxazb4p\*\*\*\*|The ID of the capacity reservation. |
|CapacityReservationPreference|String|cr-bp67acfmxazb4p\*\*\*\*|The preference of the capacity reservation. |
|EipAddress|Struct| |Details about the EIP associated with the instance. |
|AllocationId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance with which the EIP is associated. |
|Bandwidth|Integer|5|The peak value for public bandwidth of the EIP. Unit: Mbit/s. |
|InternetChargeType|String|PayByTraffic|The billing method of the EIP.

-   PayByBandwidth
-   PayByTraffic |
|IpAddress|String|42.112.17.\*\*|The EIP. |
|IsSupportUnassociate|Boolean|true|Indicates whether the EIP can be disassociated. |
|ExpiredTime|String|2017-12-10T04:04Z|The expiration time of the instance. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|GPUAmount|Integer|4|The number of GPUs for the instance type. |
|GPUSpec|String|NVIDIA V100|The category of GPUs for the instance type. |
|HostName|String|testHostName|The hostname of the instance. |
|HpcClusterId|String|hpc-bp67acfmxazb4p\*\*\*\*|The ID of the HPC cluster to which the instance belongs. |
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|The ID of the image that the instance is running. |
|InnerIpAddress|List|10.170.\*\*. \*\*|The internal IP address of the instance. |
|InstanceChargeType|String|PostPaid|The billing method of the instance. Valid values:

-   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|InstanceName|String|InstanceNameTest|The name of the instance. |
|InstanceNetworkType|String|vpc|The network type of the instance. Valid values:

-   classic: classic network
-   vpc: VPC |
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
|Memory|Integer|1024|The memory size of the instance. Unit: MiB. |
|MetadataOptions|Struct| |The metadata options. |
|HttpEndpoint|String|enabled|Indicates whether the access channel for instance metadata was enabled. Valid values:

-   enabled
-   disabled |
|HttpPutResponseHopLimit|Integer|0|This parameter is not available. |
|HttpTokens|String|optional|Indicates whether the security hardening mode \(IMDSv2\) was forcibly used to access instance metadata. Valid values:

-   optional: The security hardening mode \(IMDSv2\) was not forcibly used.
-   required: The security hardening mode \(IMDSv2\) was forcibly used. |
|NetworkInterfaces|Array of NetworkInterface| |The ENIs of the instance. |
|NetworkInterface| | | |
|MacAddress|String|00:16:3e:32:b4:\*\*|The MAC address of the ENI. |
|NetworkInterfaceId|String|eni-2zeh9atclduxvf1z\*\*\*\*|The ID of the ENI. |
|PrimaryIpAddress|String|172.17.\*\*. \*\*\*|The private IP address of the primary ENI. |
|OSName|String|CentOS 7.4 64-bit|The name of the operating system for the instance. |
|OSNameEn|String|CentOS 7.4 64 bit|The English name of the operating system for the instance. |
|OSType|String|linux|The operating system type of the instance, including Windows Server and Linux. Valid values:

-   windows
-   linux |
|OperationLocks|Array of LockReason| |The reasons why the instance was locked. |
|LockReason| | | |
|LockMsg|String|The specified instance is locked due to financial reason.|The message returned because the instanced was locked. |
|LockReason|String|Recycling|The type of the reason why the instance was locked. Valid values:

-   financial: The instance was locked due to overdue payments.
-   security: The instance was locked due to security reasons.
-   recycling: The preemptible instance was locked and is pending for release.
-   dedicatedhostfinancial: The instance was locked due to overdue payments on the dedicated host.
-   refunded: The instance was locked because a refund was made for the instance. |
|PublicIpAddress|List|121.40.61.\*\*\*|The public IP address of the instance. |
|RdmaIpAddress|List|10.10.10.102|The RDMA IP address of the HPC instance. |
|Recyclable|Boolean|false|Indicates whether the instance can be recycled. |
|RegionId|String|cn-hangzhou|The region ID of the instance. |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the instance belongs. |
|SaleCycle|String|month|The billing cycle of the instance. |
|SecurityGroupIds|List|sg-bp67acfmxazb4p\*\*\*\*|The IDs of security groups to which the instance belongs. |
|SerialNumber|String|51d1353b-22bf-4567-a176-8b3e12e4\*\*\*\*|The serial number of the instance. |
|SpotDuration|Integer|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

-   The values 2, 3, 4, 5, and 6 of this parameter are in invitational preview. Submit a ticket if you want to use these values.
-   If this parameter is set to 0, the preemptible instance has no protection period. |
|SpotPriceLimit|Float|0.98|The maximum hourly price for the instance. A maximum of three decimal places are allowed. This parameter takes effect when the SpotStrategy parameter is set to SpotWithPriceLimit. |
|SpotStrategy|String|NoSpot|The preemption policy for the preemptible instance. Valid values:

-   NoSpot: The instance is a regular pay-as-you-go instance.
-   SpotWithPriceLimit: The instance is a preemptible instance that has a user-defined maximum hourly price.
-   SpotAsPriceGo: The instance is a preemptible instance whose price is based on the market price. |
|StartTime|String|2017-12-10T04:04Z|The start time of the bidding mode for the preemptible instance. |
|Status|String|Running|The status of the instance. |
|StoppedMode|String|KeepCharging|Indicates whether the instance continues to be billed after it is stopped. Valid values:

-   KeepCharging: The billing of the instance continues after it is stopped, and resources are reserved for the instance.
-   StopCharging: The billing of the instance stops after it is stopped. After the instance is stopped, its resources such as the public IP address, vCPUs, and memory are released. You may be unable to restart the instance if some types of resources are insufficient in the current region.
-   Not-applicable: The No Fees for Stopped Instances \(VPC-Connected\) feature is not applicable to the instance. |
|Tags|Array of Tag| |The tags of the instances. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the instance. |
|TagValue|String|TestValue|The tag value of the instance. |
|VlanId|String|10|The VLAN ID of the instance.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|VpcAttributes|Struct| |The VPC attributes of the instance. |
|NatIpAddress|String|172.17.\*\*. \*\*|The IP address of the instance. It is used by ECS instances in different VPCs for communication. |
|PrivateIpAddress|List|172.17.\*\*. \*\*|The private IP address of the instance. |
|VSwitchId|String|vsw-2zeh0r1pabwtg6wcs\*\*\*\*|The ID of the vSwitch to which the instance is connected. |
|VpcId|String|vpc-2zeuphj08tt7q3brd\*\*\*\*|The ID of the VPC. |
|ZoneId|String|cn-hangzhou-g|The zone ID of the instance. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|1|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|58|The total number of instances queried. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstances
&RegionId=cn-hangzhou
&PageSize=1
PageNumber=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstancesResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>58</TotalCount>
      <PageSize>1</PageSize>
      <RequestId>97935DF1-0289-4AA2-9DD1-72377838B16B</RequestId>
      <Instances>
            <Instance>
                  <ImageId>centos_7_06_64_20G_alibase_20190711.vhd</ImageId>
                  <VlanId></VlanId>
                  <EipAddress>
                        <IpAddress></IpAddress>
                        <AllocationId></AllocationId>
                        <InternetChargeType></InternetChargeType>
                  </EipAddress>
                  <ZoneId>cn-hangzhou-f</ZoneId>
                  <IoOptimized>true</IoOptimized>
                  <SerialNumber>51d1353b-22bf-4567-a176-8b3e12e43***</SerialNumber>
                  <Cpu>2</Cpu>
                  <Memory>8192</Memory>
                  <DeviceAvailable>true</DeviceAvailable>
                  <SecurityGroupIds>
                        <SecurityGroupId>sg-bp17zljqpohu6j2i****</SecurityGroupId>
                  </SecurityGroupIds>
                  <SaleCycle></SaleCycle>
                  <AutoReleaseTime></AutoReleaseTime>
                  <ResourceGroupId></ResourceGroupId>
                  <OSType>linux</OSType>
                  <OSName>CentOS  7.6 64-bit</OSName>
                  <InstanceNetworkType>classic</InstanceNetworkType>
                  <HostName>iZbp1j4i2jdf3owlheb****</HostName>
                  <CreationTime>2019-11-11T08:35Z</CreationTime>
                  <Tags>
                        <Tag>
                              <TagValue>asg-bp1d8uuut40f4qc4****</TagValue>
                              <TagKey>acs:autoscaling:scalingGroupId</TagKey>
                        </Tag>
                        <Tag>
                              <TagValue>ESS</TagValue>
                              <TagKey>ESS</TagKey>
                        </Tag>
                  </Tags>
                  <EcsCapacityReservationAttr>
                        <CapacityReservationPreference>none</CapacityReservationPreference>
                        <CapacityReservationId></CapacityReservationId>
                  </EcsCapacityReservationAttr>
                  <RegionId>cn-hangzhou</RegionId>
                  <DeletionProtection>false</DeletionProtection>
                  <OperationLocks>
            </OperationLocks>
                  <ExpiredTime>2099-12-31T15:59Z</ExpiredTime>
                  <CpuOptions>
                        <Numa></Numa>
                        <ThreadsPerCore>2</ThreadsPerCore>
                        <CoreCount>1</CoreCount>
                  </CpuOptions>
                  <InnerIpAddress>
                        <IpAddress>10.80. **. **</IpAddress>
                  </InnerIpAddress>
                  <InstanceTypeFamily>ecs.mn4</InstanceTypeFamily>
                  <InstanceId>i-bp1j4i2jdf3owlhe****</InstanceId>
                  <InternetMaxBandwidthIn>50</InternetMaxBandwidthIn>
                  <CreditSpecification></CreditSpecification>
                  <InternetChargeType>PayByTraffic</InternetChargeType>
                  <SpotStrategy>NoSpot</SpotStrategy>
                  <StoppedMode>Not-applicable</StoppedMode>
                  <InternetMaxBandwidthOut>1</InternetMaxBandwidthOut>
                  <VpcAttributes>
                        <NatIpAddress></NatIpAddress>
                        <PrivateIpAddress>
                </PrivateIpAddress>
                        <VSwitchId></VSwitchId>
                        <VpcId></VpcId>
                  </VpcAttributes>
                  <SpotPriceLimit>0</SpotPriceLimit>
                  <StartTime>2019-11-11T08:35Z</StartTime>
                  <InstanceName>ECS-asg-MyFirstScalingGroup</InstanceName>
                  <Description>ECS</Description>
                  <OSNameEn>CentOS  7.6 64 bit</OSNameEn>
                  <PublicIpAddress>
                        <IpAddress>121.40. **. **</IpAddress>
                  </PublicIpAddress>
                  <InstanceType>ecs.mn4.large</InstanceType>
                  <Status>Running</Status>
                  <MetadataOptions>
                        <HttpTokens></HttpTokens>
                        <HttpEndpoint></HttpEndpoint>
                  </MetadataOptions>
                  <Recyclable>false</Recyclable>
                  <ClusterId></ClusterId>
                  <GPUSpec></GPUSpec>
                  <InstanceChargeType>PostPaid</InstanceChargeType>
                  <GPUAmount>0</GPUAmount>
                  <DedicatedHostAttribute>
                        <DedicatedHostId></DedicatedHostId>
                        <DedicatedHostName></DedicatedHostName>
                  </DedicatedHostAttribute>
                  <DedicatedInstanceAttribute>
                        <Affinity></Affinity>
                        <Tenancy></Tenancy>
                  </DedicatedInstanceAttribute>
                  <DeploymentSetId></DeploymentSetId>
            </Instance>
      </Instances>
</DescribeInstancesResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 58,
    "PageSize": 1,
    "RequestId": "97935DF1-0289-4AA2-9DD1-72377838B16B",
    "Instances": {
        "Instance": [
            {
                "ImageId": "centos_7_06_64_20G_alibase_20190711.vhd",
                "VlanId": "",
                "EipAddress": {
                    "IpAddress": "",
                    "AllocationId": "",
                    "InternetChargeType": ""
                },
                "ZoneId": "cn-hangzhou-f",
                "IoOptimized": true,
                "SerialNumber": "51d1353b-22bf-4567-a176-8b3e12e43***",
                "Cpu": 2,
                "Memory": 8192,
                "DeviceAvailable": true,
                "SecurityGroupIds": {
                    "SecurityGroupId": [
                        "sg-bp17zljqpohu6j2i****"
                    ]
                },
                "SaleCycle": "",
                "AutoReleaseTime": "",
                "ResourceGroupId": "",
                "OSType": "linux",
                "OSName": "CentOS 7.6 64-bit",
                "InstanceNetworkType": "classic",
                "HostName": "iZbp1j4i2jdf3owlheb****",
                "CreationTime": "2019-11-11T08:35Z",
                "Tags": {
                    "Tag": [
                        {
                            "TagValue": "asg-bp1d8uuut40f4qc4****",
                            "TagKey": "acs:autoscaling:scalingGroupId"
                        },
                        {
                            "TagValue": "ESS",
                            "TagKey": "ESS"
                        }
                    ]
                },
                "EcsCapacityReservationAttr": {
                    "CapacityReservationPreference": "none",
                    "CapacityReservationId": ""
                },
                "RegionId": "cn-hangzhou",
                "DeletionProtection": false,
                "OperationLocks": {
                    "LockReason": []
                },
                "ExpiredTime": "2099-12-31T15:59Z",
                "CpuOptions": {
                    "Numa": "",
                    "ThreadsPerCore": 2,
                    "CoreCount": 1
                },
                "InnerIpAddress": {
                    "IpAddress": [
                        "10.80. **. **"
                    ]
                },
                "InstanceTypeFamily": "ecs.mn4",
                "InstanceId": "i-bp1j4i2jdf3owlhe****",
                "InternetMaxBandwidthIn": 50,
                "CreditSpecification": "",
                "InternetChargeType": "PayByTraffic",
                "SpotStrategy": "NoSpot",
                "StoppedMode": "Not-applicable",
                "InternetMaxBandwidthOut": 1,
                "VpcAttributes": {
                    "NatIpAddress": "",
                    "PrivateIpAddress": {
                        "IpAddress": []
                    },
                    "VSwitchId": "",
                    "VpcId": ""
                },
                "SpotPriceLimit": 0,
                "StartTime": "2019-11-11T08:35Z",
                "InstanceName": "ECS-asg-MyFirstScalingGroup",
                "Description": "ECS",
                "OSNameEn": "CentOS  7.6 64 bit",
                "PublicIpAddress": {
                    "IpAddress": [
                        "121.40. **. **"
                    ]
                },
                "InstanceType": "ecs.mn4.large",
                "Status": "Running",
                "MetadataOptions": {
                    "HttpTokens": "",
                    "HttpEndpoint": ""
                },
                "Recyclable": false,
                "ClusterId": "",
                "GPUSpec": "",
                "InstanceChargeType": "PostPaid",
                "GPUAmount": 0,
                "DedicatedHostAttribute": {
                    "DedicatedHostId": "",
                    "DedicatedHostName": ""
                },
                "DedicatedInstanceAttribute": {
                    "Affinity": "",
                    "Tenancy": ""
                },
                "DeploymentSetId": ""
            }
        ]
    }
}
```

## Error codes

|HTTP status ode|Error code|Error message|Description|
|---------------|----------|-------------|-----------|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|404|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid|The error message returned because the specified InternetChargeType parameter is invalid.|
|404|InvalidLockReason.NotFound|The specified LockReason is not found|The error message returned because the specified LockReason parameter does not exist.|
|404|InvalidFilterKey.NotFound| |The error message returned because the specified start time or end time is invalid.|
|404|InvalidNetworkType.NotFound|The specified InstanceNetworkType is not found|The error message returned because the specified InstanceNetworkType parameter does not exist.|
|404|InvalidStatus.NotFound|The specified Status is not found|The error message returned because the specified resource status does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned because the specified Tag.N.Key and Tag.N.Value parameters do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the number of specified tags exceeds the upper limit.|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|The error message returned because the specified HpcClusterId parameter does not exist.|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|The error message returned because the specified HPC cluster is being created.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

