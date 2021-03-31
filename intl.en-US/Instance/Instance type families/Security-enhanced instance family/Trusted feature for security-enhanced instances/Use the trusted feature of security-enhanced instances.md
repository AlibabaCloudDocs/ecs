# Use the trusted feature of security-enhanced instances

This topic describes how to use and maintain security-enhanced instances. These operations include quickly filtering instances, viewing the trusted state of instances, and handling state exceptions.

## Filter security-enhanced instances

Security-enhanced instances are bound with the **acs:ecs:supportVtpm** tag. If you have a large number of security-enhanced instances within a region, you can filter the instances by tag.

On the **Instances** page, click **Tags** and select **acs:ecs:supportVtpm** from the Tag Key drop-down list.

![Tag filtering 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232035.png)

## View the trusted state of an instance

The baseline measurement is generated when an instance is created. The measurement values collected on subsequent instance startups are compared with the baseline measurement to determine whether the instance has changed. The comparison result indicates the trusted status of the instance and is displayed in the Security Center console.

1.  On the **Instances** or **Instance Details** page of the ECS console, find and click the icon above **Trusted State**.

    You are automatically redirected to the **Assets** page in the Security Center console.

    ![View the trusted state](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232105.png)

    **Note:** If you move the pointer over the icon above **Trusted State** on the **Instance Details** page and **Unmeasured** appears, no valid measurement results have been reported for the security-enhanced instance for an extended period of time. In this case, no detailed trusted information is displayed in the Security Center console. For information about how to handle cases where no measurement is made, see [Handle the unmeasured state](#section_y78_r14_wbz).

2.  Click the **Trusted Information** tab to view the trusted state of the instance.

    ![Trusted information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232107.png)

    The circles in the ①**Asset startup overview** section are mapped with the component list in the ② **Trusted Status of components in assets** section. The color of a circle in the ①**Asset startup overview** section indicates whether the stage is normal:

    -   If all of the circles are green, the instance startup process is normal. In this case, the **actual measurement value** \(the actual status collected by the system trusted feature\) is the same as the **standard value**.
    -   If an error occurs at one stage during the instance startup process, the corresponding circle turns red and those that follow turn gray. You can view the specific information of this stage on the **Alerts** tab and try to fix it. For more information, see [Handle trusted exceptions](#section_t7d_mvb_fzo).
    Platform Configuration Registers \(PCRs\) are storage units of trusted security devices and are capable of reliably storing the status information collected during the instance startup process. Each PCR corresponds to a specific stage of the instance startup process and the PCR value represents the status of the measured object at each stage. If the actual measurement value stored in the PCR is the same as the expected standard value, this stage is considered to be as expected. The following objects are measured at each stage of the instance startup process:

    -   pcr0: the SRTM, BIOS, embedded optional ROM, and PI driver.
    -   pcr1: the host platform configurations.
    -   pcr2: the UEFI driver and application code.
    -   pcr3: the UEFI driver, application configurations, and application data.
    -   pcr4: the UEFI startup management code \(typically MBR\).
    -   pcr5: the UEFI startup management code \(typically MBR\), startup-related data \(data used by the UEFI startup management code\), and GPT partition table.
    -   pcr6: the specific UEFI firmware defined by the platform manufacturer.
    -   pcr7: the secure startup policy.
    -   pcr8: the key commands to be run as provided in configuration files such as grub.cfg and command line information transmitted to the Linux kernel. Non-critical commands are not measured, such as the command used to define boot menu titles.
    -   pcr9: the GRUB module, Linux kernel, and initramfs.
    **Note:** ISO provides detailed definitions. For more information, visit *ISO/IEC 11889:2015 Trusted Platform Module Library*.


## Handle trusted exceptions

If an error occurs at one stage during the instance startup process, the corresponding circle on the **Trusted Information** tab turns red. You must go to the **Alerts** tab to view detailed alert information and fix the exceptions.

1.  Click the **Alerts** tab and set **Alert type** to **Trusted exception**.

    ![Select an alert type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7646482161/p232142.png)

2.  On the right side of alert information, click **Details** to view detailed error information.

    **Note:** If the alert information has not been processed, alerts are periodically raised, but no more alerts are generated. Only the time of the latest alert is displayed in the **Latest Occurrence** column.

3.  Contact the system administrator to check whether system upgrade and maintenance operations such as upgrading the operating system kernel, changing the operating system startup parameters, and modifying the initial file system \(initramfs\) have been performed recently. Then, take different measures to fix trusted exceptions based on specific situations.

    -   **Scenario 1: If no system upgrade or maintenance operations have been performed recently, ignore the alert after you check and fix the exception.**

        In this scenario, an abnormal alert may occur because a security event has occurred to your instance. For example, the instance is damaged by malware such as rootkit or bootkit. We recommend that you contact the system administrator to perform a drill-down check on the system, fix the related exceptions, and then ignore the alert. Perform the following steps:

        1.  Enable and use the **Anti-Virus** and **Vulnerabilities** features in the Security Center console. Then, upgrade the latest virus library, check the status of malware in the system, and then fix the vulnerability.
        2.  On the **Alerts** tab, click **Handle**.
        3.  Select **Ignore** and click **Immediate processing**.

            If an alert is generated on multiple instances, you can select **Handle the same alarms at the same time** to handle the same alert on each instance at a time.

            **Note:** Alerts handled in **ignore** mode are still displayed on the **Trusted Information** tab. The ignored alerts are continuously generated because Security Center periodically generates security alerts. These situations persist until you restart the system and pass the verification.

    -   **Scenario 2: If a system upgrade or maintenance operation is performed recently, add the exception to the whitelist after repair.**

        If a system upgrade or maintenance operation has been performed recently, the modified system status becomes the new standard status of your system. The status value of each stage during the instance startup process also becomes the new standard value of the corresponding PCR. In this case, you must select **Add whitelist**.

        After the collected actual measurement values are added to the whitelist, the values become the new benchmark measurement values.


## Handle the unmeasured state

If you move the pointer over the icon next to **Trusted State** on the **Instance Details** page and **Unmeasured** appears, no valid measurement results are reported for the security-enhanced instance for an extended period of time. This is typically because the trusted client is unable to access the trusted service. In this case, you can perform the following steps to troubleshoot the problem:

1.  Check the instance RAM role.

    If you have not specified a RAM role for the security-enhanced instance, specify one as required. If you have specified a RAM role for the security-enhanced instance, check whether the RAM role has the required permissions to access the trusted service. For more information, see [Create security-enhanced instances](/intl.en-US/Instance/Instance type families/Security-enhanced instance family/Create security-enhanced instances.md).

2.  Check the network connection.

    Run the following command in the security-enhanced instance to check the network connection:

    ```
    ping trusted-server-vpc.[region-id].aliyuncs.com
    ```

    Replace \[region-id\] with the ID of the region where the security-enhanced instance resides. If an output is returned, the network connection is normal.

3.  Check the security group settings.

    Check the settings of the security group to which the security-enhanced instance belongs, and make sure that the access to trusted-server-vpc.\[region-id\].aliyuncs.com is not denied.


