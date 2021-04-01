---
keyword: [event notification, system event, automation, message notification, ECS]
---

# Snapshot event notifications

You can subscribe to notifications for snapshot creation events.

## Snapshot creation

After a snapshot is created for a disk, ECS sends you a notification to indicate whether the operation succeeded. Example:

```
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:snapshot/s-bp1fis********b859b3",
  "level": "INFO",
  "name": "Snapshot:CreateSnapshotCompleted",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
    "result": "accomplished",
    "snapshotId": "s-bp1fis********b859b3",
    "snapshotName": "test-snapshot",
    "snapshotType": "user",
    "diskId": "d-bp1bwa********9ol4mi",
    "startTime": "2019-04-22T08:36:09Z",
    "endTime": "2019-04-22T08:37:11Z"
  }
}
```

The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|result|The operation result. Valid values: -   accomplished: Snapshot creation succeeded.
-   failed: Snapshot creation failed.

|accomplished|
|snapshotId|The ID of the snapshot.|s-bp1fis\*\*\*\*\*\*\*\*b859b3|
|snapshotName|The name of the snapshot.|test-snapshot|
|snapshotType|The type of the snapshot. Valid values:-   user: manual snapshots
-   timer: snapshots that are created as scheduled
-   copied: copied snapshots
-   imported: imported snapshots

|user|
|diskId|The ID of the disk.|d-bp1bwa\*\*\*\*\*\*\*\*9ol4mi|
|startTime|The time when the snapshot starts to be created. The time is in UTC.|2019-04-22T08:36:09Z|
|endTime|The time when the snapshot finishes being created. The time is in UTC.|2019-04-22T08:37:11Z|

