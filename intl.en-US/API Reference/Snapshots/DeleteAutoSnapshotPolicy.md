# DeleteAutoSnapshotPolicy {#DeleteAutoSnapshotPolicy .reference}

Creates an automatic snapshot policy. If the target automatic snapshot policy has been applied to a disk, the policy will not be not effective on the disk once the policy is deleted.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DeleteAutoSnapshotPolicy.|
|RegionId|String|Yes|The region ID to which the automatic snapshot policy belongs. For more information, call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|autoSnapshotPolicyId|String|Yes|The ID of the target automatic snapshot policy. You can call [DescribeAutoSnapshotPolicyEx](intl.en-US/API Reference/Snapshots/DescribeAutoSnapshotPolicyEx.md#) to obtain all your automatic snapshot policies.|

## Return parameters {#section_byv_lyz_xdb .section}

All are common parameters. See [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#commonResponseParameters).

## Example { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DeleteAutoSnapshotPolicy
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=p-233e6ylv0
&<Common request parameters>
```

**Response sample** 

**XML format**

```
<DeleteAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId> 
</DeleteAutoSnapshotPolicyResponse>
```

 **JSON format** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more error codes, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs). 

|Error code|Error message|HTTP status code|Meaning|
|:---------|:------------|:---------------|:------|
|ParameterInvalid|The specified automatic snapshot policy does not exist.|404|The specified `AutoSnapshotPolicyId` does not exist.|
|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.| 404|The specified `AutoSnapshotPolicyId` does not exist in the specified region.|

