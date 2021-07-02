---
keyword: [itemized billing, batch, search, tag, ECS]
---

# Search for resources by tag

After you bind tags to resources, you can use one of the following methods to quickly search for resources. Exact match and fuzzy search are supported.

## Search for resources on the Tags page

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

3.  In the left-side navigation pane, click **Tags**.

4.  In the top navigation bar, select a region.

5.  Click the Tags tab and select a tag key from the tag list.

6.  In the corresponding tag value list, view values in the Bind Resources and Cloud Monitoring Application Groups columns.

    ![tag value list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9727948951/p103653.png)

7.  Click a tag value. Click **Resources** tab to view the resources bound to the tag. You can click a resource ID to go to the resource details page.

    ![resources](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0827948951/p103654.png)


## Search for resources on the Resources page

In the ECS console, pages of instances, disks, snapshots, images, security groups, and Elastic Network Interface allow you to set tags to search for these resources. For example, you can complete the following steps to search for ECS instances:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the Instances page, click **Tags** and then select a tag key. If you do not select a tag value, all ECS instances to which the tag key is bound are displayed.

    ![instances & tag](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0827948951/p103657.png)


**References**  


[Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Manage tags/Create or bind a tag.md)

[Delete or unbind a tag](/intl.en-US/Tag & Resource/Tags/Manage tags/Delete or unbind a tag.md)

[ListTagResources](/intl.en-US/API Reference/Tags/ListTagResources.md)

[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

