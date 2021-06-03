# Instance families that support instance type changes

This topic describes the instances types and instance families that support instance type changes. Before you change the instance type of an instance, check whether the instance type can be changed and identify the compatible instance types. If the instance type can be changed, choose a method to change the instance type.

## Impacts of instance type changes

Impacts of instance type changes vary based on the network types of instances.

-   Classic network-type instances:
    -   For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, instance information including the private IP addresses, disk device names, and software license codes are changed. For Linux instances, the device names of basic disks \(`cloud`\) are identified as xvd\* such as `xvda` or `xvdb`, and the device names of ultra disks \(`cloud_efficiency`\) and standard SSDs \(`cloud_ssd`\) are identified as vd\* such as `vda` or `vdb`.
    -   For instance types that belong to an available instance family, the private IP addresses of instances are changed.
-   VPC-type instances:

    For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, instance information including the disk device names and software license codes are changed. For Linux instances, the device names of basic disks \(`cloud`\) are identified as xvd\* such as `xvda` or `xvdb`, and the device names of ultra disks \(`cloud_efficiency`\) and standard SSDs \(`cloud_ssd`\) are identified as vd\* such as `vda` or `vdb`.


## Instance families that do not support instance type changes

The following instance families do not support instance type changes across different instance families or within the same instance family:

-   Persistent memory optimized instance families: re6p and re6p-redis
-   Security-enhanced instance families: g7t, c7t, and r7t
-   Big data instance families: d2c, d2s, d1, and d1ne
-   Instance families equipped with local SSDs: i1, i2, i2g, i2ne, i2gne, i3, and i3g
-   GPU-accelerated compute optimized instance families: vgn5i and gn5
-   FPGA-accelerated compute optimized instance families: f1 and f3
-   ECS Bare Metal Instance families:
    -   ebmgn7, ebmgn6e, ebmgn6v, and ebmgn6i
    -   ebmg6, ebmg5s, ebmg5, ebmc6, ebmc5s, ebmc4, ebmre6p, ebmr6, and ebmr5s
    -   ebmhfg6, ebmhfg5, ebmhfc6, and ebmhfr6
-   Super Computing Cluster \(SCC\) instance families: scchfg6, scchfc6, scchfr6, sccg5, scch5, sccgn6e, and sccgn6

## Instance families that support instance type changes

The following tables list the instance families that support instance type changes. The instance types of subscription and pay-as-you-go instances can be changed across or within these instance families. For more information about how to change instance types, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

**Note:** The compatible instance types and instance families can be affected by limits such as zones. Information displayed in the console prevails. You can also go to the [ECS Instance Types Available for Each Region](https://ecs-buy.aliyun.com/instanceTypes) page to query available instance types.

|Original instance family|Compatible instance family|
|------------------------|--------------------------|
|t6|-   t6
-   s6
-   g6, c6, r6, hfg6, hfc6, and hfr6 |
|t5|-   t5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, n4, mn4, xn4, and e4 |
|s6|-   s6
-   t6
-   g6, c6, r6, hfg6, hfc6, and hfr6 |
|n4, mn4, xn4, and e4|-   n4, mn4, xn4, and e4
-   sn1, sn2, se1, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, and t5 |

|Original instance family|Compatible instance family and type|
|------------------------|-----------------------------------|
|g7, c7, and r7|g7, c7, and r7|
|g7ne|-   g7ne
-   g7, c7, and r7
-   hfc7, hfg7, and hfr7 |
|g6, c6, and r6|-   g6, c6, and r6
-   g7, c7, and r7
-   hfg7, hfc7, and hfr7
-   g6e, c6e, and r6e
-   re6, hfg6, hfc6, and hfr6
-   t6 and s6

**Note:**

-   To upgrade an instance of the g6, c6, or r6 instance family to an enhanced sixth-generation instance family \(g6e, c6e, or r6e\) or a seventh-generation instance family \(hfc7, hfg7, hfr7, g7, c7, or r7\), [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). You cannot downgrade the instance type of the instance after the upgrade is complete.
-   Instances of the enhanced sixth-generation instance families \(g6e, c6e, and r6e\) and the seventh-generation instance families \(hfc7, hfg7, hfr7, g7, c7, and r7\) support only enhanced SSDs \(ESSDs\). If an instance has disks of other categories attached, the disks are replaced with ESSDs when you upgrade the instance to a seventh-generation or enhanced sixth-generation instance family. Data on the disks must be manually migrated to the ESSDs. For information about the pricing of ESSDs, see the Pricing tab on the [Elastic Computer Service page](https://www.alibabacloud.com/product/ecs). |
|g6se|g6se|
|g6a, c6a, and r6a|g6a, c6a, and r6a|
|g6t and c6t|g6t and c6t|
|g6e, c6e, and r6e|-   g6e, c6e, and r6e
-   ebmg6e, ebmc6e, and ebmr6e
-   g7, c7, and r7
-   hfc7, hfg7, and hfr7
-   g7ne |
|ebmg6a, ebmc6a, and ebmr6a|ebmg6a, ebmc6a, and ebmr6a|
|ebmg6e, ebmc6e, and ebmr6e|-   ebmg6e, ebmc6e, and ebmr6e
-   g6e, c6e, and r6e |
|g5, g5ne, r5, c5, and ic5|-   g5, g5ne, r5, c5, and ic5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, re4, t5, n4, mn4, xn4, and e4

**Note:**

-   To upgrade the instance type of an instance of a basic fifth-generation instance family \(g5, c5, r5, or ic5\) to an instance type that belongs to an enhanced sixth-generation instance family \(g6e, c6e, or r6e\), [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). You cannot downgrade the instance type of the instance after the upgrade is complete.
-   Instances of the enhanced sixth-generation instance families \(g6e, c6e, and r6e\) support only ESSDs. If an instance has disks of other categories attached, the disks are replaced with ESSDs when you upgrade the instance type of the instance to an instance type that belongs to an enhanced sixth-generation instance family. Data on the disks must be manually migrated to the ESSDs. For information about the pricing of ESSDs, see the Pricing tab on the [Elastic Computer Service page](https://www.alibabacloud.com/product/ecs). |
|sn1ne, sn2ne, and se1ne|-   sn1ne, sn2ne, and se1ne
-   c4, cm4, ce4, hfc5, hfg5, g5, g5ne, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|se1|-   se1
-   sn1, sn2, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|re6|-   re6
-   g6, c6, r6, hfc6, hfg6, hfr6, and re4

**Note:** You can change the instance types of instances among ecs.ebmre6-6t.52xlarge, ecs.re6.26xlarge, ecs.re4.40xlarge, and ecs.re4e.40xlarge. |
|re4|-   re4
-   re6, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, t5, n4, mn4, xn4, e4, and ecs.se1.14xlarge

**Note:** You can change the instance types of instances among ecs.ebmre6-6t.52xlarge, ecs.re6.26xlarge, ecs.re4.40xlarge, and ecs.re4e.40xlarge. |
|hfc7, hfg7, and hfr7|-   hfc7, hfg7, and hfr7
-   g7, c7, and r7
-   g7ne |
|hfc6, hfg6, and hfr6|-   hfc6, hfg6, and hfr6
-   hfc7, hfg7, and hfr7
-   g6, c6, r6, and re6
-   t6 and s6

**Note:**

-   To upgrade an instance of the hfc6, hfg6, or hfr6 instance family to a seventh-generation instance family \(hfc7, hfg7, or hfr7\), [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). You cannot downgrade the instance type of the instance after the upgrade is complete.
-   Instances of the seventh-generation instance families \(hfc7, hfg7, and hfr7\) support only ESSDs. If an instance has disks of other categories attached, the disks are replaced with ESSDs when you upgrade the instance to a seventh-generation instance family. Data on the disks must be manually migrated to the ESSDs. For information about the pricing of ESSDs, see the Pricing tab on the [Elastic Computer Service page](https://www.alibabacloud.com/product/ecs). |
|hfc5 and hfg5|-   hfc5 and hfg5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|gn7|gn7|
|vgn6i|vgn6i|
|gn6i|gn6i|
|gn5i|gn5i|
|gn6e|gn6e|
|gn6v|gn6v|
|t1, s1, s2, s3, m1, m2, c1, and c2|-   t1, s1, s2, s3, m1, m2, c1, and c2
-   sn1, sn2, se1, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|n1, n2, and e3|-   n1, n2, and e3
-   sn1, sn2, se1, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|sn1 and sn2|-   sn1 and sn2
-   se1, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|c4, ce4, and cm4|-   c4, ce4, and cm4
-   sn1ne, sn2ne, se1ne, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |

