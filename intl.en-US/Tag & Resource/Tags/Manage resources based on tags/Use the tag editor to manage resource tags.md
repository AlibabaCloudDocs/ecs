# Use the tag editor to manage resource tags

The tag editor is a tool to query and manage tags. You can use this tool to query 5,000 resource data entries across services and regions. You can also use it to edit resource tags and export resource information.

The tag editor allows you to query the following ECS resources: instances, Block Storage devices, images, snapshots, security groups, Elastic Network Interfaces, dedicated hosts, and SSH key pairs.

## Search resources

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, click **Tags**.

3.  On the **Tags** page, click the **Tag Editor** tab.

4.  In the **Search** section, configure query conditions and click **Search**.

    ![search](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1827948951/p133825.png)

    In the **Search Results** section, you can click the ![4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1827948951/p94278.png) icon to set the items to be displayed.


## Edit tags of selected resources

You can edit tags for multiple found resources at a time.

1.  In the **Search Results** section, select one or more resources, and click **Edit Tags**.

2.  Manage resource tags.

    -   Click **Add Tag** to add tags to the selected resources.
    -   Click **Delete Tag** to delete tags from the selected resources.
    -   After a tag that is bound to a resource is deleted, you can click **Cancel Deletion** to restore the tag.
3.  Click **Submit**.


## Export resource information

You can export the information of found resources.

1.  In the **Search Results** section, select one or more resources, and then click **Export**.

2.  Use one of the following methods to export information of resources:

    **Note:** You can click the ![4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1827948951/p94278.png) icon to view all properties of the selected resources or customize properties to be displayed.

    -   In the Export drop-down list, click **Export All Data** to export information of the selected resources as a CSV file.
    -   In the Export drop-down list, click **Export Visible Columns** to export the displayed information as a CSV file.

**Related topics**  


[TagResources](/intl.en-US/API Reference/Tags/TagResources.md)

[ListTagResources](/intl.en-US/API Reference/Tags/ListTagResources.md)

[UntagResources](/intl.en-US/API Reference/Tags/UntagResources.md)

[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

