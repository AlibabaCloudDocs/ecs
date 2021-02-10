# Use security-enhanced instances

This topic describes how to use and maintain security-enhanced instances.

## Filter security-enhanced instances

Security-enhanced instances are bound with the **acs:ecs:supportVtpm** tag. If you have a large number of instances within a region, you can filter the instances by tag.

On the **Instances** page, click **Tags** and select **acs:ecs:supportVtpm**.

![Tag filtering 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232035.png)

## View the trusted state of an instance

1.  On the instances page or the instance details page of the ECS console, find and click the icon next to **Trusted State**.

    You are automatically redirected to the **Assets** page in the Security Center console.

    ![View trusted state](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232105.png)

2.  Click the **Trusted Information** tab to view the trusted status of the instance.

    ![Trusted Information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232107.png)

    The circles in the ①**Asset startup overview** section are mapped with the component list in the ②**Trusted Status of components in assets** section. pcr refers to Platform Configuration Registers. Each pcr represents a specific stage in the instance startup process.

    If all of the circles are green, the instance startup process is normal. In this case, **Actual measure** \(that is, the actual status collected by the system trusted feature\) is consistent with the **Standard value**.

    If an error occurs at one stage during the instance startup process, the corresponding circle turns red and those that follow turn gray. You can view the specific information of this stage on the **Security alarm processing** tab and try to fix it. For more information, see [Handle trusted exceptions](#section_t7d_mvb_fzo).


## Handle trusted exceptions

If an error occurs at one stage during the instance startup process, the corresponding circle on the **Trusted Information** tab turns red. You must go to the **Security alarm processing** tab to view detailed alert information and fix exceptions.

1.  Click the **Alerts** tab and set **Alert type** to **Trusted exception**.

    ![Select an alert type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232142.png)

2.  On the right side of the alert information, click **Details** to view detailed error information.

    **Note:** If the alert information has not been processed, alerts are prompted periodically, but no more alerts are generated. Only the time of the latest alert is displayed in the **Latest Occurrence** column.

3.  Contact the system administrator to check whether system upgrades and maintenance operations have been performed recently, such as upgrading the operating system kernel, changing the operating system startup parameters, and modifying the initial file system \(InitRamFS\). Then, take different measures to fix trusted exceptions based on specific situations.

    -   **Scenario 1: If no system upgrades or maintenance operations are performed recently, ignore the alert after you check and fix the exception.**

        In this scenario, an abnormal alert may occur because a security event has occurred to your instance. For example, the instance is damaged by malware such as rootkit or bootkit. We recommend that you contact the system administrator to perform a drill-down check on the system and fix the related exceptions and then ignore the alert. Perform the following steps:

        1.  Enable and use the **Anti-Virus** and **Vulnerabilities** features in the Security Center console. Then, upgrade the latest virus library, check the status of malware in the current system, and then fix the vulnerability.
        2.  On the **Alerts** tab, click **Handle**.
        3.  Select **Ignore** and click **Immediate processing**.

            If an alert is generated on multiple instances, you can select the **Handle the same alarms at the same time** check box to handle the same alert on each instance at a time.

            **Note:** Alerts handled in **ignore** mode are still displayed on the **Trusted Information** tab. The ignored alerts are continuously generated because the Security Center periodically generates alerts. These situations persist until you restart the system and pass the verification.

    -   **Scenario 2: If a system upgrade or maintenance operation is performed recently, add the exception to the whitelist after repair.**

        If a system upgrade or maintenance operation is performed recently, the modified system status becomes the new standard status of your system. The status value of each phase in the startup process also become the new standard value of the corresponding PCR. In this case, you must select **Add whitelist**.

        After the collected integrity measurement values are added to the whitelist, the values become the new benchmark measurement values.


