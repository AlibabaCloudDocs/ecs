---
keyword: [itemized billing, batch, search, tag, ECS, remove tags]
---

# Delete or unbind a tag

This topic describes how to delete or unbind a tag in the ECS console. You can unbind a tag from a resource when the tag is no longer needed. If you unbind a tag from a resource and the tag is not bound to any other resources, this tag is automatically deleted.

The resource is bound to a tag.

Before you unbind a tag, take note of the following items:

-   You can unbind up to 20 tags at a time.
-   If you unbind a tag from all its resources such as ECS instances, snapshots, and security groups, this tag is deleted.

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

3.  In the left-side navigation pane, click **Tags**.

4.  On the **Tags** page, click a tag key.

5.  In the tag value list, click a tag value.

6.  On the **Tag Value** page that appears, click the **Resources** tab.

7.  Select one or more resources, move the pointer over **Batch Operation**, and click **Unbind Tags**.

    ![unbindtag](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6827948951/p103647.png)

8.  On the **Resources** tab, click **Refresh** to check whether the tags are unbound.


If you implement access control or automated O&M, or generate bill reports based on tags, you need to pay attention to the business changes caused by tag unbinding. For more information, see the "Considering ramifications of future changes" section in [Best practices for tag design](/intl.en-US/Best Practices/Best practices for tag design.md).

**Related topics**  


[UntagResources](/intl.en-US/API Reference/Tags/UntagResources.md)

