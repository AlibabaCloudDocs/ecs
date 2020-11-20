---
keyword: private IP address
---

# Modify a private IP address

After you create a VPC-type ECS instance, you can change the private IP address of the instance directly or by changing the VSwitch of the instance.

No secondary private IP addresses are configured for elastic network interfaces \(ENIs\) of the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to modify the private IP address and choose **More** \> **Instance Status** \> **Stop** in the **Actions** column.

5.  After the instance is stopped, click the instance ID.

6.  In the **Configuration Information** section, choose **More** \> **Modify Private IP Address**.

7.  In the Modify Private IP Address dialog box, modify the parameters and click **Modify**.

    -   If you need to change the VSwitch, make sure that the selected VSwitch resides within the same zone as the instance.
    -   If you do not need to change the VSwitch, modify the private IP address.
    ![Modify Private IP Address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2257298951/p5483.png)

8.  Go back to the Instances page. Find the instance and choose **More** \> **Instance Status** \> **Start** in the **Actions** column.

    **Note:** The new private IP address takes effect after the ECS instance is started.


**Related topics**  


[ModifyInstanceVpcAttribute](/intl.en-US/API Reference/Networks/ModifyInstanceVpcAttribute.md)

