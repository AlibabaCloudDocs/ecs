---
keyword: [itemized billing, batch, search, tag, ecs]
---

# Create or bind a tag

This topic describes how to create or bind a tag to resources in the ECS console. If multiple resources that are associated with each other exist in your account, you can bind tags to the resources. This allows you to categorize and manage the resources in a centralized manner.

-   For more information about resource types to which you can bind tags, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md).
-   A maximum of 20 tags can be bound for a resource. If the number of tags bound to a resource exceeds the upper limit, you must unbind some of the tags before you bind new tags.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

3.  In the left-side navigation pane, click **Tags**.

4.  In the top navigation bar, select a region.

5.  On the Tags tab, click **Create/Bind Tags**.

6.  In the Create/Bind Tags dialog box, perform the following steps:

    1.  Create a tag or select an existing tag. Click **Next**.

        -   **Tag Key**: required. You can select an existing tag key or enter a new tag key. You can perform fuzzy search by prefix and bind up to 10 tag keys at a time.

            The tag key can be up to 128 characters in length and cannot contain http:// or https://. It cannot start with acs: or aliyun.

            **Note:** If you want to bind an existing tag, select its tag key. If you want to create a tag, enter a new tag key.

        -   **Tag Value**: optional. You can select an existing tag value or enter a tag value.

            The tag value can be up to 128 characters in length and cannot contain http:// or https://. It cannot start with acs: or aliyun.

            **Note:** If you want to bind an existing tag, select its tag value.

        ![Create a tag](../images/p103306.png)

    2.  Click **Next**.

    3.  Select one or more resources of the same type and click **OK**. For example, you can select four ECS instances.

    4.  Click **Bind Other Resources** to go back to the **Select Resources** step and continue to select one or more resources of the same type.

        ![Results](../images/p103307.png)

    5.  Click **Close**.


On the Tags tab, select the tags you have bound and click the **Refresh** icon to view the list of resources to which the tags are bound.

![Refresh](../images/p49484.png)

**Related topics**  


[TagResources](/intl.en-US/API Reference/Tags/TagResources.md)

