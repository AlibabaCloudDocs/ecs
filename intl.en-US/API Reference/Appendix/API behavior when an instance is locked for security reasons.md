# API behavior when an instance is locked for security reasons

This topic describes the API behavior when your resource is locked due to security concerns.

## API behavior

When `OperationLocks` in the response returned for an instance by the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) operation contains `LockReason: security`, the instance is locked for security reasons.

**Note:** If a disk on the instance is in the `In_use` state, the behavior of API operations related to the disk is subject to the `OperationLocks` settings of the instance. If the disk is in another state, the `OperationLocks` settings can be ignored.

In the following table, **Normal logic** indicates that the operation is called and the result is returned.

|Operation|Behavior|
|:--------|:-------|
|AllocatePublicIpAddress|Error|
|AttachDisk|Error|
|AuthorizeSecurityGroup|Normal logic|
|CreateDisk|Normal logic|
|CreateImage|Normal logic|
|CreateInstance|Error|
|CreateSecurityGroup|Normal logic|
|CreateSnapshot|Returns an error only when the disk is attached to the instance and is in the In\_use state.|
|DeleteDisk|Normal logic|
|DeleteImage|Normal logic|
|DeleteInstance|Normal logic|
|DeleteSecurityGroup|Normal logic|
|DeleteSnapshot|Normal logic|
|DescribeAutoSnapshotPolicy|Normal logic|
|DescribeDisks|Normal logic|
|DescribeImages|Normal logic|
|DescribeInstances|Normal logic|
|DescribeInstanceStatus|Normal logic|
|DescribeInstanceTypes|Normal logic|
|DescribeInstanceMonitorData|Normal logic|
|DescribeRegions|Normal logic|
|DescribeSecurityGroupAttribute|Normal logic|
|DescribeSecurityGroups|Normal logic|
|DescribeSnapshotAttribute|Normal logic|
|DescribeSnapshots|Normal logic|
|DescribeZones|Normal logic|
|DetachDisk|Error|
|JoinSecurityGroup|Error|
|LeaveSecurityGroup|Error|
|ModifyAutoSnapshotPolicy|Normal logic|
|ModifyDiskAttribute|Normal logic|
|ModifyInstanceAttribute|Error|
|RebootInstance|Error|
|ReInitDisk|-   Returns an error when the disk is in the In\_use state.
-   Normal logic when the disk is in another state. |
|ReplaceSystemDisk|Normal logic|
|ResetDisk|Error|
|RevokeSecurityGroup|Normal logic|
|StartInstance|Error|
|StopInstance|Error|

