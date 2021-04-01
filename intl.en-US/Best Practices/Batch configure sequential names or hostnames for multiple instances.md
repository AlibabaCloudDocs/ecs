# Batch configure sequential names or hostnames for multiple instances

You can create multiple ECS instances by using the ECS console or by calling the RunInstances operation. When you create multiple ECS instances, you can customize the instance names or hostnames to facilitate subsequent instance management. This topic describes how to batch configure sequential instance names or hostnames for multiple instances.

## Background information

You can batch configure sequential instance names or hostnames by specifying a sequence or by using automatic sorting.

This topic describes how to use the ECS console or call an API operation to configure sequential instance names and hostnames for three instances in four scenarios.

-   By using the ECS console:
    -   [\#section\_tw3\_97t\_q27](#section_tw3_97t_q27)
    -   [\#section\_xuq\_yf6\_1zo](#section_xuq_yf6_1zo)
-   By calling an API operation:
    -   [\#section\_qxi\_4aw\_tru](#section_qxi_4aw_tru)
    -   [\#section\_a1u\_1vp\_58m](#section_a1u_1vp_58m)

For more information about specific configuration rules, see the [\#section\_e1f\_5fl\_dbn](#section_e1f_5fl_dbn), [\#section\_5bc\_mo1\_2b3](#section_5bc_mo1_2b3), and [\#section\_ij0\_dy9\_ir4](#section_ij0_dy9_ir4) sections.

## Scenario 1: Set the instance names or hostnames of three instances to be sorted in a specified sequence by using the ECS console

In this example, instance names or hostnames are set to be sorted in the specified sequence in the ECS console. For more information about other configurations, see [t17291.md\#](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab in the ECS console.
2.  Complete the configurations in the Basic Configurations and Networking steps.

    In this example, the instance quantity is set to 3 on the Basic Configurations step.

3.  In the System Configurations step, configure the parameters.

    Set the values of Instance Name and Host in the following format: name\_prefix\[begin\_number,bits\]name\_suffix. For more information about how to specify sorting rules, see the [\#section\_5bc\_mo1\_2b3](#section_5bc_mo1_2b3) section.

    In this example, both the instance names and hostnames are specified to start with k8s-node- and increment starting from 0006, and the hostnames are specified to end with -ecshost. Set Instance Name to k8s-node-\[6,4\] and Host to k8s-node-\[6,4\]-ecshost.

    **Note:** In this example, the sorting rules only specify instance names and hostnames. Sequential Suffix is disabled by default.

    ![Example of specifying a sequence](../images/p203038.png "Example of specifying a sequence")

4.  Complete the configurations in the Grouping step and confirm the order.

    You can view the new instances on the Instances page. In this example, the generated instance names are k8s-node-0006, k8s-node-0007, and k8s-node-0008, and the generated hostnames are k8s-node-0006-ecshost, k8s-node-0007-ecshost, and k8s-node-0008-ecshost.


## Scenario 2: Set the instance names or hostnames of three instances to be sorted in an automatic sequence by using the ECS console

In this example, instance names or hostnames are set to be automatically sorted in the ECS console. For more information, see [t17291.md\#](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab in the ECS console.
2.  Complete the configurations in the Basic Configurations and Networking step.

    In this example, the instance quantity is set to 3 on the Basic Configurations tab.

3.  In the System Configurations step, configure the parameters.

    Select Sequential Suffix. The system adds sequential suffixes to the Instance Name and Host values and sorts the values. The added suffix starts from 001 and increments with each instance. For rules of automatic sorting, see the [\#section\_ij0\_dy9\_ir4](#section_ij0_dy9_ir4) section.

    In this example, set Instance Name to ecs and Host to ecshost.

    ![Example of automatic sorting](../images/p203046.png "Example of automatic sorting")

4.  Complete the configurations in the Grouping step and confirm the order.

    You can view the new instances on the Instances page. In this example, the generated instance names are ecs001, ecs002, and ecs003, and the generated hostnames are ecshost001, ecshost002, and ecshost003.


## Scenario 3: Set the instance names or hostnames of three instances to be sorted in a specified sequence by calling the RunInstances operation

This section describes how to configure parameters used to specify a sequence. For more information about other parameters, see [t9856.md\#](/intl.en-US/API Reference/Instances/RunInstances.md).

Set the values of InstanceName and HostName in the following format: name\_prefix\[begin\_number,bits\]name\_suffix. For more information about how to specify sorting rules, see the [\#section\_5bc\_mo1\_2b3](#section_5bc_mo1_2b3) section.

In this example, the instance names and hostnames of the three instances are specified to start with k8s-node- and increment starting from 0006, and the hostnames are specified to end with -ecshost. Configure the following parameters:

-   Amount: 3
-   InstanceName: k8s-node-\[6,4\]
-   HostName: k8s-node-\[6,4\]-ecshost

**Note:** In this example, the sorting rules only specify instance names and hostnames. UniqueSuffix is disabled by default.

In this example, the generated instance names are k8s-node-0006, k8s-node-0007, and k8s-node-0008, and the generated hostnames are k8s-node-0006-ecshost, k8s-node-0007-ecshost, and k8s-node-0008-ecshost.

## Scenario 4: Set the instance names or hostnames of three instances to be sorted in an automatic sequence by calling the RunInstances operation

This section describes how to configure parameters used to specify the automatic sorting. For more information about other parameters, see [t9856.md\#](/intl.en-US/API Reference/Instances/RunInstances.md).

Set UniqueSuffix to true. The system adds sequential suffixes to the InstanceName and HostName values and sorts the values. The added suffix starts from 001 and increments with each instance. For rules of automatic sorting, see the [\#section\_ij0\_dy9\_ir4](#section_ij0_dy9_ir4) section.

In this example, the instance names or hostnames of three instances are set to be automatically sorted. Configure the following parameters:

-   Amount: 3
-   InstanceName: ecs
-   HostName: ecshost
-   UniqueSuffix: true

In this example, the generated instance names are ecs001, ecs002, and ecs003, and the generated hostnames are ecshost001, ecshost002, and ecshost003.

## Naming conventions

-   Instance name: The name must be 2 to 128 characters in length and must start with a letter. It can contain letters, digits, periods \(.\), underscores \(\_\), colons \(:\), and hyphens \(-\).
-   Hostname:
    -   For Windows instances, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot start or end with a hyphen \(-\), contain consecutive hyphens \(-\), or contain only digits.
    -   For other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate a name into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). However, the hostname cannot contain consecutive periods \(.\) or hyphens \(-\). It cannot start or end with a period \(.\) or a hyphen \(-\).

## Specify a sequence

Set the parameter value in the following format: name\_prefix\[begin\_number,bits\]name\_suffix.

|Field|Description|Example|
|-----|-----------|-------|
|name\_prefix|The prefix of instance names or hostnames. **Note:** A prefix is required when you specify sequential names. Otherwise, names are regarded as common names.

|k8s-node-|
|\[begin\_number,bits\]|The ordered numeric values for instance names or hostnames. After you specify this field, the numbers in the names increment in sequence. -   begin\_number: the number from which the ordered numeric values of instances start. Valid values: 0 to 999999. Default value: 0.
-   bits: the number of digits of an ordered value. Valid values: 1 to 6. Default value: 6.

**Note:**

-   The \[begin\_number,bits\] field cannot contain spaces.
-   If the value of begin\_number has more digits than the value of bits, the value of bits is 6.
-   A maximum of 999,999 ECS instances can share the same prefix and suffix. Extra instances use 999999 as the prefix.

|\[0,6\]|
|name\_suffix|The suffix of the instance names or hostnames.|-ecshost|

|Example|Generated names \(for three instances\)|
|-------|---------------------------------------|
|k8s-node-\[\]-ecshost or k8s-node-\[,\]-ecshost|k8s-node-000000-ecshost, k8s-node-000001-ecshost, and k8s-node-000002-ecshost|
|k8s-node-\[99\]-ecshost or k8s-node-\[99,\]-ecshost|k8s-node-000099-ecshost, k8s-node-000100-ecshost, and k8s-node-000101-ecshost|
|k8s-node-\[99,1\]-ecshost|k8s-node-000099-ecshost, k8s-node-000100-ecshost, and k8s-node-000101-ecshost|
|k8s-node-\[999998\]-ecshost|k8s-node-999998-ecshost, k8s-node-999999-ecshost, and k8s-node-999999-ecshost|
|k8s-node-\[0,4\]|k8s-node-0000, k8s-node-0001, and k8s-node-0002|

## Automatic sorting

When you create multiple instances, you can enable the automatic sorting feature to automatically add sequential suffixes to the instance names and hostnames. The sequential numbers in the suffix range from 001 to 999.

**Note:** By default, the automatic sorting feature is disabled.

|Format \(instance name or hostname\)|Example|Generated names \(for three instances\)|
|------------------------------------|-------|---------------------------------------|
|Common names|ecs|ecs001, ecs002, and ecs003|
|Sequential names to be sorted in a specified sequence: name\_prefix\[begin\_number,bits\]name\_suffix|k8s-node-\[\]-ecshost or k8s-node-\[,\]-ecshost|k8s-node-000000-ecshost001, k8s-node-000001-ecshost002, and k8s-node-000002-ecshost003**Note:** The specified sequence and automatic sorting take effect at the same time. |
|Sequential names to be sorted in a specified sequence: name\_prefix\[begin\_number,bits\]|k8s-node-\[0,4\]|k8s-node-0000, k8s-node-0001, and k8s-node-0002**Note:** name\_suffix is not specified, and automatic sorting does not take effect. |

