# Use Cloud Assistant plug-ins

Cloud Assistant provides plug-ins that allow you to maintain and manage ECS instances.

|Cloud Assistant plug-in|Description|
|-----------------------|-----------|
|Running method|-   Log on to an ECS instance by using SSH and then run commands on the instance. This method is applicable only to Linux ECS instances.
-   Use the [Cloud Assistant console](https://ecs.console.aliyun.com/#/cloudAssistant/region/cn-hangzhou) in the ECS console. |
|Usage|-   To query plug-ins, run the `acs-plugin-manager --list` command.
-   To run a specific plug-in, run the `acs-plugin-manager --exec --plugin <Plug-in name>` command. |
|Usage example|-   [Configure kdump](#section_qoj_m21_naf)
-   [Automatically configure an ENI](#section_okd_pex_wj4)
-   [Configure NIC multi-queue](#section_xeh_s2g_rju)
-   [Manage Intel Hyper-Threading](#section_5rc_xrv_ya1) |

## Configure kdump

The `ecs_dump_config` plug-in can be used to enable and disable the dump feature, and query the status of the feature.

-   Enable dump.

    ```
    acs-plugin-manager --exec   --plugin=ecs_dump_config --params --enable
    ```

-   Disable dump.

    ```
    acs-plugin-manager --exec   --plugin=ecs_dump_config --params --disable
    ```

-   Query the status of dump.

    ```
    acs-plugin-manager --exec   --plugin=ecs_dump_config --params --status
    ```


## Automatically configure an ENI

Typically, you must manually configure the network for an elastic network interface \(ENI\) after you add the ENI. The `multi-nic-util` plug-in can be used to automatically configure the network for your ENI.

```
acs-plugin-manager  --exec   --plugin=multi-nic-util
```

## Configure NIC multi-queue

NIC multi-queue enables an ECS instance to use multiple NIC queues to improve the network performance. Performance bottlenecks may occur when a single vCPU of an instance is used to process NIC interrupts. To solve this issue, you can use NIC multi-queue to distribute NIC interrupts across different vCPUs to improve network performance. You can run the `ethtool -l ehtname` command to query the current number of NIC queues and the supported number of NIC queues.

The `ecs_tools_multiqueue` plug-in can be used to set the number of queues to the supported maximum number on all NICs.

```
acs-plugin-manager  --exec   --plugin=ecs_tools_multiqueue
```

## Manage Intel Hyper-Threading

ECS bare metal instances require Intel Hyper-Threading \(HT\) to be disabled for specific business scenarios. The `ecs_disable_intel_hyper-threading` plug-in can implement this feature.

To use this plug-in, you can add the `nr_cpus` kernel parameter to the grub file and set the parameter to half of the number of vCPUs of the instance type. Then, the **nr\_cpus** parameter limits the maximum number of vCPUs supported by the kernel and disables HT.

After the kernel parameter is configured, you must restart the instance for the parameter to take effect. After the plug-in is executed, the output prompts you to restart the instance.

**Note:** This plug-in cannot have HT disabled on ECS instances that are not ECS bare metal instances. If you run the plug-in on an instance that is not an ECS bare metal instance, the system prompts you that the instance is not an ECS bare metal instance and exits.

```
acs-plugin-manager  --exec   --plugin=ecs_disable_intel_hyper-threading
```

