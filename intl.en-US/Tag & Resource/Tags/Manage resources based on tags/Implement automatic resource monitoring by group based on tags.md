# Implement automatic resource monitoring by group based on tags

You can bind a tag to multiple ECS instances that run the same business. Then, you can use the application group feature of Cloud Monitor to configure smart tag synchronization for these instances. Cloud Monitor automatically assigns the ECS instances that are bound with the same tag to the same application group to implement automatic resource monitoring by group. In ECS, only ECS instances support this feature.

The application group feature of Cloud Monitor allows you to manage alert rules and view monitoring data by group. This makes management less complex. For more information, see [Application group](/intl.en-US/Quick Start/Application group.md). In this topic, ECS instances that are automatically created in a scaling group are bound with the `testKey:testValue` tag. Then, Cloud Monitor uses the configuration rules of the application group to identify and assign the ECS instances to the application group based on the tag.

You can use one of the following methods to implement automatic resource monitoring by group based on tags:

-   Create resources that are bound with tags or bind tags to existing resources. Then, use Cloud Monitor to create an application group for which the smart tag synchronization feature is enabled. Make sure that the tags that match the application group are the same as those bound to the resources.
-   Create an application group for which the smart tag synchronization feature is enabled, and add a custom tag to the matching rules of the application group. Then, create resources that are bound with the same tag as the application group or bind the same tag as the application group to existing resources. The resources are automatically assigned to the application group.

## Step 1: Create instances that are bound with the same tag

You can create instances that are bound with the same tag or bind a tag to existing instances. For more information, see [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Manage tags/Create or bind a tag.md). Alternatively, you can perform the following operations to use Auto Scaling to bind a tag to the instances in a scaling group:

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  Create a scaling group.

    For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md). In this example:

    -   Specify **Multi-zone Scaling Policy** to implement high-availability automatic scaling based on your business requirements.
    -   Set **Minimum Number of Instances** to 4.
    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81641.png)

3.  Create a scaling configuration.

    For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md). You must bind the `testKey:testValue` tag on the **System Configurations \(Optional\)** page.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81642.png)

4.  Go to the scaling group details page, click the **Instances** tab, and then view the ECS instances that are automatically created in the scaling group.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81643.png)


## Step 2: Create a Cloud Monitor application group

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com).

2.  Create a Cloud Monitor application group. For more information, see [t6144.md\#](/intl.en-US/Application groups/Create an application group.md).

    In this example, select **Smart tag synchronization creation** as the creation method and add the `testKey:testValue` tag to the matching rule to create an application group. Then, the instances that are bound with this tag are assigned to the created application group.

    1.  Select **Smart tag synchronization creation** for Creation method.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81647.png)

    2.  In the Match Rule section, set Resource Tag Key to `testKey` and specify the Tag Value parameter. You can set a tag value range. In this example, the tag value range is **Contain**`testValue`.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81650.png)


## Step 3: View monitoring information about the ECS instances

You can use one of the following methods to view the information about the ECS instances:

Method 1: View the monitoring information about the ECS instances based on their application group in the Cloud Monitor console.

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, click **Application Groups**.

3.  In the search bar, select **Resource tags** and enter `testKey` to search for the application group.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81654.png)

4.  Click `testKey-testValue-53** / 22******` in the Group Name / Group ID column to view the resources in the group.

    The automatically created ECS instances in the scaling group are automatically assigned to the application group.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p81657.png)


Method 2: View the monitoring information about the ECS instances in the ECS console.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, click **Tags**.

3.  In the top navigation bar, select a region.

4.  On the **Tags** tab of the **Tags** page, click **Custom Tags**.

    On the **All Custom Tags** page, click **Enable** in the **Automatically Create Cloud Monitoring Application Groups** column to create a Cloud Monitor application group. In the Automatically Create Cloud Monitoring Application Groups column, **Enabled** is displayed with a green check mark for the tags for which application group are created.

    ![tag1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4539803061/p101995.png)

5.  Enter `testKey` in the search box to search for the tag.

6.  Click **View Monitoring Information** in the **Cloud Monitoring Application Group** column.

    ![tag2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5539803061/p101996.png)

    Go to the **CloudMonitor** tab to view the monitoring, alert, and event information about the ECS instances in the application group that correspond to this key.


Monitor ECS instances in real time by using Cloud Monitor. For more information, see [Overview](/intl.en-US/Quick Start/Overview.md).

