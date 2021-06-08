---
keyword: [calling method, Alibaba Cloud, ECS, API, quick start]
---

# Quick start

This topic describes how to use a developer tool such as Alibaba Cloud Command Line Interface \(CLI\), OpenAPI Explorer, or Alibaba Cloud Software Development Kit \(SDK\) to call Elastic Compute Service \(ECS\) API operations. In the examples, CreateSnapshot is used.

Before you call an API operation, you must understand related instructions in the API documentation and obtain the values of the required request parameters. If an error code is returned after you send a request, you can obtain the description of the error code in the API documentation.

## Methods used to make API requests

-   [Example of calling an ECS API operation by using Alibaba Cloud CLI](#section_rmm_adh_0cj): Alibaba Cloud CLI is applicable to scenarios where command line tools are frequently used. Make sure that Alibaba Cloud CLI is installed on the ECS instance. For more information about how to install Alibaba Cloud CLI in different operating systems, see the following topics:
    -   [Windows]()
    -   [Linux]()
    -   [MacOS]()
-   [Example of calling an ECS API operation by using OpenAPI Explorer](#section_2zj_7qp_m49): OpenAPI Explorer is applicable to users who frequently use interactive operation interfaces or developers who are unfamiliar with Alibaba Cloud products. You can debug API operations and obtain sample SDK requests in OpenAPI Explorer. For more information about OpenAPI Explorer, see [What is OpenAPI Explorer?](https://www.alibabacloud.com/help/doc-detail/74407.htm)
-   [Example of calling an ECS API operation by using SDK for Java](#section_vo7_pwb_e6u): SDK for Java is applicable to scenarios such as SDK encoding or DevOps. To use ECS SDK for Java, make sure that the SDK is installed. For more information, see [Install ECS SDK for Java](/intl.en-US/SDK Reference/Java example/Install ECS SDK for Java.md).

## Example of calling an ECS API operation by using Alibaba Cloud CLI

1.  Use one of the following methods to obtain the instance ID:

    -   If you are connected to the ECS instance, you can obtain the instance ID from the instance metadata.

        ```
        curl http://100.100.100.200/2016-01-01/meta-data/instance-id
        ```

    -   On your computer, you can call the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) operation to obtain the instance ID.

        ```
        aliyun ecs DescribeInstances --output cols=InstanceId,InstanceName rows=Instances.Instance[]
        ```

2.  Call the [DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md) operation to obtain the ID of a disk.

    ```
    aliyun ecs DescribeDisks --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69****** --output cols=DiskId rows=Disks.Disk[]
    ```

3.  Call the [CreateSnapshot](/intl.en-US/API Reference/Snapshots/CreateSnapshot.md) operation to create a snapshot based on the obtained disk ID.

    ```
    aliyun ecs CreateSnapshot --DiskId d-bp19pjyf12hebp******
    ```

    If the following information is returned, the task to create a snapshot is initiated:

    ```
    {"RequestId":"16B856F6-EFFB-4397-8A8A-CB73FA******","SnapshotId":"s-bp1afnc98r8kjh******"}
    ```

4.  Call the [DescribeSnapshots](/intl.en-US/API Reference/Snapshots/DescribeSnapshots.md) operating to query the progress of snapshot creation.

    ```
    aliyun ecs DescribeSnapshots --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69******
    ```

    If both `"SnapshotId"="s-bp1afnc98r8kjh******"` and `"Status":"accomplished"` are returned, the snapshot is created.


## Example of calling an ECS API operation by using OpenAPI Explorer

1.  Call the [DescribeInstances](https://api.aliyun.com/new#/?product=Ecs&api=DescribeInstances) operation to obtain the instance ID and the ID of a disk.

2.  Call the [CreateSnapshot](https://api.aliyun.com/new#/?product=Ecs&api=CreateSnapshot) operation to create a snapshot based on the obtained disk ID.

3.  Call the [DescribeSnapshots](https://api.aliyun.com/new#/?product=Ecs&api=DescribeSnapshots) operation to query the progress of snapshot creation.

    If both `"SnapshotId"="s-bp1afnc98r8kjh******"` and `"Status":"accomplished"` are returned, the snapshot is created.


## Example of calling an ECS API operation by using SDK for Java

You must specify the values of the following parameters in the sample code:

-   <AccessKey\>: Enter your AccessKey ID. For more information about how to obtain your AccessKey pair, see [Create an AccessKey pair]().
-   <AccessSecret\>: Enter your AccessKey secret.
-   <RegionId\>: Enter the region ID of the ECS instance. For information about the valid values, see [Regions and zones]() or [DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md).
-   <DiskId\>: Enter the disk ID. For information about the valid values, see [DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md).

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.ecs.model.v20140526.CreateSnapshotRequest;
import com.aliyuncs.ecs.model.v20140526.CreateSnapshotResponse;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;

/* pom.xml
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>3.0.9</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-ecs</artifactId>
    <version>4.10.1</version>
</dependency>
*/  

public class CreateSnapshotExample {

    private String accessKeyId = "<AccessKey>";
    private String accessSecret = "<AccessSecret>";

    /**
     * The region ID of the disk
     */
    private String regionId = "<RegionId>";

    /**
     * The ID of the disk for which you want to create a snapshot
     */
    private String diskId = "<DiskId>";

    public void createSnapshot() {
        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessSecret);
        IAcsClient client = new DefaultAcsClient(profile);

        CreateSnapshotRequest request = new CreateSnapshotRequest();
        request.setRegionId(regionId);
        request.setDiskId(diskId);
        try {
            CreateSnapshotResponse response = client.getAcsResponse(request);
            logInfo(response.getSnapshotId());
        } catch (ServerException e) {
            logInfo(String.format("Fail. Something with your connection with Aliyun go incorrect. ErrorCode: %s",
                e.getErrCode()));
        } catch (ClientException e) {
            logInfo(String.format("Fail. Business error. ErrorCode: %s, RequestId: %s",
                e.getErrCode(), e.getRequestId()));
        }
    }

    private static void logInfo(String message) {
        System.out.println(message);
    }

    public static void main(String[] args) {
        new CreateSnapshotExample().createSnapshot();
    }
}
```

