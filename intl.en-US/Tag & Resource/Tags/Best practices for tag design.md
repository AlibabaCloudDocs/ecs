# Best practices for tag design

This topic introduces the best practices for tag design in ECS. Tags can be used to manage, categorize, and search for resources.

## Scenarios

Tags can be used to categorize and manage resources by group. The resources include personnel, finance, and cloud services. Tags are applicable in the following common scenarios:

-   Management of application publishing procedures
-   Resource tracking and tag-based group search and resource management
-   Tag- and group-based automated O&M by using Alibaba Cloud services such as Operation Orchestration Service \(OOS\), Resource Orchestration Service \(ROS\), Auto Scaling, and Cloud Assistant
-   Tag-based cost management and cost allocation
-   Resource- or role-based access control

## Principles

You must implement the best tagging practices based on the following principles:

-   [Mutual exclusivity](#section_p5f_2lf_nbh)
-   [Collective exhaustion](#section_ppj_uul_77a)
-   [Limited values](#section_d5u_xah_gyk)
-   [Considering ramifications of future changes](#section_c52_ooy_5pm)
-   [Simplified design](#section_etm_bzv_jr9)

## Mutual exclusivity

Mutual exclusivity is implemented to ensure that multiple tags cannot be assigned to the same resource attribute. For example, if you use the `key="owner"` tag key to represent the owner attribute, you cannot use other tag keys such as own, belonger, or owner to represent this attribute again.

## Collective exhaustion

Collective exhaustion means that when you plan resources, you must plan tags at the same time and prioritize the tag keys. All resources must be bound with the planned tag keys and their corresponding values.

-   Each tag key-value pair must be named in a standard format.
-   Collective exhaustion is a prerequisite for future tag-based access control, cost tracking, automated O&M, and group search.

## Limited values

Limited values are implemented to remove excess tag values and retain only core tag values.

This principle simplifies procedures such as resource management, access control, automated O&M, and cost allocation. You can also use tags and automation tools under this principle to manage resources. ECS allows you to control tags by using API operations in SDKs, which makes it easy to automatically manage, retrieve, and filter resources.

## Considering ramifications of future changes

During the planning stage, you must consider the impact of adding or deleting tag values to improve the flexibility of modifying tags.

When you modify tags, the tag-based access control, automated O&M, and related billing reports may be changed. For corporate or personal business, the best practice is to create business-related tag groups to manage resources in technical, business, and security dimensions. When you use automated O&M tools to manage resources and services, you can add automation-specific tags to aid in the automation efforts.

## Simplified design

Simplified design allows you to simplify the use of tag keys by creating tag keys that have fixed dimensions during the tag planning stage. This principle can reduce operation errors caused by redundant tag keys.

-   You can create business-related tag groups to manage resources in technical, business, and security dimensions.
-   When you use automated O&M tools to manage resources and services, you can add automation-specific tags.

## Examples of designing tag keys

The following table lists the tag naming examples with common dimensions. We recommend that you use lowercase letters to name tags.

|Dimension|Tag key|Tag value|
|---------|-------|---------|
|Organization|-   company
-   department
-   organization
-   team
-   group

|Organization-specific names|
|Business|-   product
-   business
-   module
-   service

|Business-specific names|
|Role|-   role
-   user

|-   network administrator
-   application administrator
-   system administrator
-   opsuser
-   devuser
-   testuser |
|Purpose|-   purpose
-   use

|Specific purposes|
|Project|-   From project dimensions:
    -   project
    -   risk
    -   schedule
    -   subtask
    -   environment
-   From personnel dimensions:
    -   sponsor
    -   member
    -   decisionmaker or owner
    -   creator

|Project-related values|
|Business department \(to implement cost allocation and business tracking\)|-   costcenter
-   businessunit
-   biz
-   financecontact

|Department-related values|
|Owner from the financial dimension \(to identify the resource owner\)|owner|Names or emails|
|Customer from the financial dimension \(to identify the clients that a particular group of resources serves\)|Custom values or true values|Customer names|
|Project from the financial dimension \(to determine the resource-supported projects\)|project|Project names|
|Order from the financial dimension|order|Order category IDs|

## References

-   [Search for resources by tag](/intl.en-US/Tag & Resource/Tags/Search for resources by tag.md)

## Related API operations

-   [TagResources](/intl.en-US/API Reference/Tags/TagResources.md)
-   [ListTagResources](/intl.en-US/API Reference/Tags/ListTagResources.md)
-   [UntagResources](/intl.en-US/API Reference/Tags/UntagResources.md)

