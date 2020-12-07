# API behavior for accounts that have overdue payments

This topic describes the API behavior when your account has an overdue payment or your subscription resources expire.

## API behavior

When `OperationLocks` in the response returned for an instance by the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) or [DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md) operation contains `LockReason: financial`, overdue payments are generated.

In the following table, **Normal logic** indicates that the operation is called and the result is returned.

|Operation|Instance for which overdue payments are generated|
|:--------|:------------------------------------------------|
|AllocatePublicIpAddress|Error|
|AttachDisk|Error|
|AuthorizeSecurityGroup|Normal logic|
|CreateDisk|Error|
|CreateImage|Normal logic|
|CreateInstance|Error|
|CreateSecurityGroup|Normal logic|
|CreateSnapshot|Normal logic|
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
|DetachDisk|Normal logic|
|JoinSecurityGroup|Normal logic|
|LeaveSecurityGroup|Normal logic|
|ModifyAutoSnapshotPolicy|Normal logic|
|ModifyDiskAttribute|Normal logic|
|ModifyInstanceAttribute|Normal logic|
|RebootInstance|Error|
|ReInitDisk|Error|
|ReplaceSystemDisk|Error|
|ResetDisk|Error|
|RevokeSecurityGroup|Normal logic|
|StartInstance|Error|
|StopInstance|Error|

|Operation|Disk for which overdue payments are generated|
|:--------|:--------------------------------------------|
|AllocatePublicIpAddress|Error|
|AttachDisk|Error|
|AuthorizeSecurityGroup|Normal logic|
|CreateDisk|Error|
|CreateImage|Normal logic|
|CreateInstance|Error|
|CreateSecurityGroup|Normal logic|
|CreateSnapshot|Normal logic|
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
|DescribeInstanceMonitorData|Normal logic|
|DescribeRegions|Normal logic|
|DescribeSecurityGroupAttribute|Normal logic|
|DescribeSecurityGroups|Normal logic|
|DescribeSnapshotAttribute|Normal logic|
|DescribeSnapshots|Normal logic|
|DescribeZones|Normal logic|
|DetachDisk|Normal logic|
|JoinSecurityGroup|Normal logic|
|LeaveSecurityGroup|Normal logic|
|ModifyAutoSnapshotPolicy|Normal logic|
|ModifyDiskAttribute|Normal logic|
|ModifyInstanceAttribute|Error|
|ModifyInstanceSpec|Error|
|RebootInstance|Error|
|ReInitDisk|Error|
|ReplaceSystemDisk|Error|
|ResetDisk|Error|
|RevokeSecurityGroup|Normal logic|
|StartInstance|Error|
|StopInstance|Error|

