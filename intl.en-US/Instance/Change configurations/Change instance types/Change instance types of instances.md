# Change instance types of instances

This topic describes the instance types and families that support instance type changes. If your current instance type does not meet your business needs, check whether the instance type can be changed. If yes, choose a method to change the instance type.

## Impact of instance type changes

The impact of an instance type change varies depending on the network type of the instance.

-   Classic network-type instances:
    -   For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, instance information including the private IP address, disk device names, and software authorization codes will be changed. For Linux instances, the device names of basic disks \(`cloud`\) will be identified as `xvda` or `xvdb`, and the device names of ultra disks \(`cloud_efficiency`\) and standard SSDs \(`cloud_ssd`\) will be identified as `vda` or `vdb`.
    -   If the instance belongs to an available instance family, the private IP address of the instance will be changed.
-   VPC-type instances:

    For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, the software authorization codes and the disk device names of the instance will be changed. For Linux instances, the device names of basic disks \(`cloud`\) will be identified as `xvda` or `xvdb`, and the device names of ultra disks \(`cloud_efficiency`\) and standard SSDs \(`cloud_ssd`\) will be identified as `vda` or `vdb`.


## Instance families that do not support instance type changes

The following instance families do not support instance type changes between different families or within the same family:

-   Big data instance families: d2c, d2s, d1, and d1ne
-   Instance families with local SSDs: i1, i2, i2g, i2ne, and i2gne
-   GPU-accelerated compute optimized instance families: vgn5i and gn5
-   FPGA-accelerated compute optimized instance families: f1 and f3
-   ECS Bare Metal Instance families: ebmgn6e, ebmgn6v, ebmgn6i, ebmc6, ebmg6, ebmr6, ebmhfc6, ebmhfg6, ebmhfr6, ebmc5s, ebmg5s, ebmr5s, ebmhfg5, ebmc4, and ebmg5
-   Super Computing Cluster \(SCC\) instance families: scchfc6, scchfg6, scchfr6, sccg5, scch5, and sccgn6

## Instance families that support instance type changes

The following tables list instance families that support instance type changes. The compatible instance families apply to both subscription and pay-as-you-go instances. For more information about how to change instance types, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

**Note:** Some instance types may not be available in all zones. Before you change the instance type of an instance, check whether the compatible instance type or instance family is available in the current zone.

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

|Original instance family|Compatible instance family \(type\)|
|------------------------|-----------------------------------|
|g6, c6, and r6|-   g6, c6, and r6
-   hfc7, hfg7, and hfr7
-   g6e, c6e, and r6e
-   re6, hfc6, hfg6, and hfr6
-   t6 and s6

**Note:**

-   To upgrade an instance that belongs to the g6, c6, or r6 instance family to an instance type that belongs to an enhanced sixth-generation instance family such as g6e, c6e, or r6e, or to a seventh-generation instance family such as hfc7, hfg7, or hfr7, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). After the upgrade is complete, you will not be able to downgrade the instance type of the instance.
-   Instances of the enhanced sixth-generation instance families such as g6e, c6e, and r6e, and instances of the seventh-generation instance families such as hfc7, hfg7, and hfr7 support only enhanced SSDs \(ESSDs\). If your instance is attached with disks of other categories, the disks will be replaced with ESSDs and the data on the disks must be manually migrated to the ESSDs when you upgrade the instance to an instance type that belongs to an enhanced sixth-generation instance family or an seventh-generation instance family. For information about the pricing of ESSDs, see [ECS pricing](https://www.alibabacloud.com/product/ecs). |
|g6a, c6a, and r6a|g6a, c6a, and r6a|
|g6t and c6t|g6t and c6t|
|g6e, c6e, and r6e|-   g6e, c6e, and r6e
-   ebmg6e, ebmc6e, and ebmr6e
-   hfc7, hfg7, and hfr7

**Note:** To upgrade an instance that belongs to the g6e, c6e, or r6e instance family to an instance type that belongs to a seventh-generation instance family such as hfc7, hfg7, or hfr7, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). After the upgrade is complete, you will not be able to downgrade the instance type of the instance. |
|ebmg6a, ebmc6a, and ebmr6a|ebmg6a, ebmc6a, and ebmr6a|
|ebmg6e, ebmc6e, and ebmr6e|-   ebmg6e, ebmc6e, and ebmr6e
-   g6e, c6e, and r6e |
|g5, g5ne, r5, c5, and ic5|-   g5, g5ne, r5, c5, and ic5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, re4, t5, n4, mn4, xn4, and e4

**Note:**

-   To upgrade an instance that belongs to a basic fifth-generation instance family such as g5, c5, r5, or ic5 to an instance type that belongs to an enhanced sixth-generation instance family such as g6e, c6e, or r6e, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). After the upgrade is complete, you will not be able to downgrade the instance type of the instance.
-   Instances of the enhanced sixth-generation instance families such as g6e, c6e, and r6e support only ESSDs. If your instance is attached with disks of other categories, the disks will be replaced with ESSDs and the data on the disks must be manually migrated to the ESSDs when you upgrade the instance to an instance type that belongs to an enhanced sixth-generation instance family. For information about the pricing of ESSDs, see [ECS pricing](https://www.alibabacloud.com/product/ecs). |
|sn1ne, sn2ne, and se1ne|-   sn1ne, sn2ne, and se1ne
-   c4, cm4, ce4, hfc5, hfg5, g5, g5ne, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|se1|-   se1
-   sn1, sn2, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|re6|-   re6
-   g6, c6, r6, hfc6, hfg6, hfr6, and re4

**Note:** You can change the instance types of instances between ecs.ebmre6-6t.52xlarge, ecs.re6.26xlarge, ecs.re4.40xlarge, and ecs.re4e.40xlarge. |
|re4|-   re4
-   re6, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, t5, n4, mn4, xn4, e4, and ecs.se1.14xlarge

**Note:** You can change the instance types of instances between ecs.ebmre6-6t.52xlarge, ecs.re6.26xlarge, ecs.re4.40xlarge, and ecs.re4e.40xlarge. |
|hfc7, hfg7, and hfr7|hfc7, hfg7, and hfr7|
|hfc6, hfg6, and hfr6|-   hfc6, hfg6, and hfr6
-   hfc7, hfg7, and hfr7
-   g6, c6, r6, and re6
-   t6 and s6

**Note:**

-   To upgrade an instance that belongs to the six-generation instance families such as hfc6, hfg6, or hfr6 to an instance type that belongs to a seventh-generation instance family such as hfc7, hfg7, or hfr7, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). After the upgrade is complete, you will not be able to downgrade the instance type of the instance.
-   Instances of the seventh-generation instance families such as hfc7, hfg7, and hfr7 support only ESSDs. If your instance is attached with disks of other categories, the disks will be replaced with ESSDs and the data on the disks must be manually migrated to the ESSDs when you upgrade the instance to an instance type that belongs to a seventh-generation instance family. For information about the pricing of ESSDs, see [ECS pricing](https://www.alibabacloud.com/product/ecs). |
|hfc5 and hfg5|-   hfc5 and hfg5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, and e4 |
|gn4|gn4|
|gn5i|gn5i|
|gn6i|gn6i|
|vgn6i|vgn6i|
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

