# 欠费时的API行为

本文介绍了因账号欠费或者包年包月资源过期时的API调用情况。

## API调用情况

欠费指在[DescribeInstances](/intl.zh-CN/API参考/实例/DescribeInstances.md)或者[DescribeDisks](/intl.zh-CN/API参考/磁盘/DescribeDisks.md)返回的传出参数中的`OperationLocks`包含了`LockReason: financial`。

下列表中，**正常逻辑**表示按照接口的正常逻辑执行并返回结果。

|接口|实例欠费|
|:-|:---|
|AllocatePublicIpAddress|报错|
|AttachDisk|报错|
|AuthorizeSecurityGroup|正常逻辑|
|CreateDisk|报错|
|CreateImage|正常逻辑|
|CreateInstance|报错|
|CreateSecurityGroup|正常逻辑|
|CreateSnapshot|正常逻辑|
|DeleteDisk|正常逻辑|
|DeleteImage|正常逻辑|
|DeleteInstance|正常逻辑|
|DeleteSecurityGroup|正常逻辑|
|DeleteSnapshot|正常逻辑|
|DescribeAutoSnapshotPolicy|正常逻辑|
|DescribeDisks|正常逻辑|
|DescribeImages|正常逻辑|
|DescribeInstances|正常逻辑|
|DescribeInstanceStatus|正常逻辑|
|DescribeInstanceTypes|正常逻辑|
|DescribeInstanceMonitorData|正常逻辑|
|DescribeRegions|正常逻辑|
|DescribeSecurityGroupAttribute|正常逻辑|
|DescribeSecurityGroups|正常逻辑|
|DescribeSnapshotAttribute|正常逻辑|
|DescribeSnapshots|正常逻辑|
|DescribeZones|正常逻辑|
|DetachDisk|正常逻辑|
|JoinSecurityGroup|正常逻辑|
|LeaveSecurityGroup|正常逻辑|
|ModifyAutoSnapshotPolicy|正常逻辑|
|ModifyDiskAttribute|正常逻辑|
|ModifyInstanceAttribute|正常逻辑|
|RebootInstance|报错|
|ReInitDisk|报错|
|ReplaceSystemDisk|报错|
|ResetDisk|报错|
|RevokeSecurityGroup|正常逻辑|
|StartInstance|报错|
|StopInstance|报错|

|接口|云盘欠费|
|:-|:---|
|AllocatePublicIpAddress|报错|
|AttachDisk|报错|
|AuthorizeSecurityGroup|正常逻辑|
|CreateDisk|报错|
|CreateImage|正常逻辑|
|CreateInstance|报错|
|CreateSecurityGroup|正常逻辑|
|CreateSnapshot|正常逻辑|
|DeleteDisk|正常逻辑|
|DeleteImage|正常逻辑|
|DeleteInstance|正常逻辑|
|DeleteSecurityGroup|正常逻辑|
|DeleteSnapshot|正常逻辑|
|DescribeAutoSnapshotPolicy|正常逻辑|
|DescribeDisks|正常逻辑|
|DescribeImages|正常逻辑|
|DescribeInstances|正常逻辑|
|DescribeInstanceStatus|正常逻辑|
|DescribeInstanceMonitorData|正常逻辑|
|DescribeRegions|正常逻辑|
|DescribeSecurityGroupAttribute|正常逻辑|
|DescribeSecurityGroups|正常逻辑|
|DescribeSnapshotAttribute|正常逻辑|
|DescribeSnapshots|正常逻辑|
|DescribeZones|正常逻辑|
|DetachDisk|正常逻辑|
|JoinSecurityGroup|正常逻辑|
|LeaveSecurityGroup|正常逻辑|
|ModifyAutoSnapshotPolicy|正常逻辑|
|ModifyDiskAttribute|正常逻辑|
|ModifyInstanceAttribute|报错|
|ModifyInstanceSpec|报错|
|RebootInstance|报错|
|ReInitDisk|报错|
|ReplaceSystemDisk|报错|
|ResetDisk|报错|
|RevokeSecurityGroup|正常逻辑|
|StartInstance|报错|
|StopInstance|报错|

