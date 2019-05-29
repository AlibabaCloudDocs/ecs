# Stop a preemptible instance {#concept_k4c_5rw_wgb .concept}

This topic describes how to stop a preemptible instance and whether it can start successfully after being stopped in different cases.

## Procedure {#section_qdc_jt5_ydb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Instances**.
3.  On the Instances page, click **More** \> **Instance Status** \> **Stop** in the actions column to the right of the target instance.
4.  In both the Notes and Stop dialog boxes that appear in order, click **OK**.

Alternatively, you can call [StopInstance](../reseller.en-US/API Reference/Instances/StopInstance.md#) to stop a preemptible instance by using developer tools such as Alibaba Cloud CLI, OpenAPI Explorer, and Alibaba Cloud SDK.

## Can preemptible instances be restarted after they are stopped? {#section_xqv_yxn_4gb .section}

All preemptible instances can be restarted after they are stopped during and after their guaranteed duration. However, the network type, bidding mode, and stop mode of an instance affect the conditions of the instance restart. The following table describes these differences.  

**Note:** Only preemptible instances in a VPC support the [No fees for stopped VPC instances](https://www.alibabacloud.com/help/doc-detail/63353.htm#concept-js1-1fd-5db) feature.

|Network type|Bidding mode|Stop mode|Can the stopped instance be restarted?|
|:-----------|:-----------|---------|:-------------------------------------|
|Classic network|SpotWithPriceLimit|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance can only be restarted successfully if your bid is not lower than the market price and if there are sufficient resources.|
|SpotAsPriceGo|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance cannot be restarted if there are insufficient resources.  |
|VPC|SpotWithPriceLimit|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance can only be restarted successfully if your bid is not lower than the market price and if there are sufficient resources.|
|Stop/Force Stop \(no fees will be incurred if either of the options is selected\)|During the guaranteed duration, the instance can be restarted successfully as long as there are sufficient resources. However, after the guaranteed duration, the instance can only be restarted successfully if your bid is not lower than the market price and if there are sufficient resources . |
|SpotAsPriceGo|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance cannot be restarted if there are insufficient resources.|
|Stop/Force Stop \(no fees will be incurred if either of the options is selected\)|During the guaranteed duration, the instance can be restarted successfully as long as there are sufficient resources. However, after the guaranteed duration, the instance cannot be restarted if there are insufficient resources.  |

