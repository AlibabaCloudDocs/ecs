# Instance families that do not support advanced VPC features

This topic describes instance families that do not support advanced VPC features.

Advanced VPC features include network ACLs, route tables, and flow logs. For more information, see [Overview](/intl.en-US/Network ACL/Overview.md), [Overview](/intl.en-US/Route tables/Overview.md), and [Flow log overview](/intl.en-US/Flow logs/Flow log overview.md).

Limits of advanced VPC features on ECS instances:

-   Instance creation: If advanced features are enabled on a VPC, you cannot create instances of instance families listed in the following table within the VPC.
-   Instance upgrade or downgrade: If the instance type of an ECS instance supports advanced features and those advanced features are enabled on the corresponding VPC, the instance cannot be changed to an instance that belongs to instance families listed in the following table. The methods to change instance configurations include upgrading, downgrading, renewal and downgrading, and changing instance types.

When you enable advanced features on a VPC, the system automatically detects the instances within the VPC that must be upgraded or downgraded. Then, you can upgrade or downgrade configurations of these instances. For more information, see [Change the instance type of a pay-as-you-go instance](/intl.en-US/Instance/Change configurations/Change instance types/Change the instance type of a pay-as-you-go instance.md) or [Upgrade the instance types of subscription instances](/intl.en-US/Instance/Change configurations/Change instance types/Upgrade the instance types of subscription instances.md).

The following table describes instance families that do not support advanced VPC features.

|Instance family type|Instance family|
|--------------------|---------------|
|General purpose instance families|sn2 \(retired\)|
|Compute optimized instance families|sn1 \(retired\)|
|Memory optimized instance families|se1|
|Big data instance families|d1|
|Instance families with local SSDs|i1|
|Instance families with high clock speed|-   c4 \(retired\)
-   ce4 \(retired\)
-   cm4 \(retired\) |
|GPU-accelerated compute optimized instance families|-   gn4
-   gn5 |
|GPU-accelerated instance families with graphics acceleration capabilities|ga1 \(retired\)|
|Shared instance families|-   n1 \(retired\)
-   n2 \(retired\)
-   e3 \(retired\)
-   xn4
-   n4
-   mn4
-   e4 |
|Generation I instance families|-   t1 \(retired\)
-   s1 \(retired\)
-   s2 \(retired\)
-   s3 \(retired\)
-   m1 \(retired\)
-   m2 \(retired\)
-   c1 \(retired\)
-   c2 \(retired\) |

