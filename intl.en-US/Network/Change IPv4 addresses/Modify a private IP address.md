---
keyword: private IP address
---

# Modify a private IP address

After you create a Virtual Private Cloud-type \(VPC-type\) Elastic Compute Service \(ECS\) instance, you can modify the private IP address of the instance directly or by changing the vSwitch of the instance.

-   No secondary private IP addresses are configured for elastic network interfaces \(ENIs\) of the instance.
-   The instance whose private IP address you want to modify is in the Stopped state.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to modify the private IP address and choose **More** \> **Network and Security Group** \> **Modify Private IP Address** in the **Actions** column.

5.  In the **Modify Private IP Address** dialog box, modify the parameters and click **Modify**.

    -   If you want to change the vSwitch, make sure that the selected vSwitch resides within the same zone as the instance.
    -   If you do not want to change the vSwitch, modify only the private IP address.
    ![Modify Private IP Address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2257298951/p5483.png)

6.  Choose **More** \> **Instance Status** \> **Start** in the **Actions** column.

    **Note:** The new private IP address takes effect after the ECS instance is restarted.


**Related topics**  


[ModifyInstanceVpcAttribute](/intl.en-US/API Reference/Networks/ModifyInstanceVpcAttribute.md)

