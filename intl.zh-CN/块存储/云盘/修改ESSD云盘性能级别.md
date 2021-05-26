---
keyword: 
---

# 修改ESSD云盘性能级别

您可以在使用ESSD云盘的过程中，在线升级性能级别。如果要降低性能级别，只支持降低按量付费ESSD云盘的性能级别。您也可以调用API ModifyDiskSpec修改ESSD云盘的性能级别。修改后，性能级别立即生效，您无需创建新盘或者迁移数据。

创建ECS实例时，您可以选择ESSD云盘作为系统盘或者数据盘，也可以单独创建一块ESSD云盘。更多有关ESSD云盘的信息，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。

修改ESSD云盘性能级别时，您需要注意以下内容：

-   您的账号不能处于欠费状态。
-   若ESSD云盘已挂载到包年包月ECS实例上，则实例不能处于过期状态。
-   新创建的ESSD云盘请您等待云盘进入**待挂载**（Available）状态后再升级ESSD云盘性能级别。
-   升级ESSD云盘性能级别后，系统按照新性能级别单价计算消费账单。
-   若您需要将ESSD云盘PL0升级为PL1、PL2或PL3，可以通过云盘变配功能实现。具体操作，请参见[变更云盘类型](/intl.zh-CN/块存储/云盘/变更云盘类型.md)。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**存储与快照** \> **云盘**。

3.  在顶部菜单栏左上角处，选择地域。

4.  找到目标ESSD云盘，在**操作**列，单击**更多** \> **修改性能级别**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9263359951/p50139.png)

5.  在修改性能级别窗口中，选择新的**性能级别**，单击**确定**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9263359951/p50141.png)


由于ESSD云盘可以选择的性能级别与存储容量有关，如果您的ESSD云盘无法选择更高性能级别，可以先[扩容云盘](/intl.zh-CN/块存储/扩容云盘/扩容概述.md)，再升级ESSD云盘性能级别。

**相关文档**  


[ModifyDiskSpec](/intl.zh-CN/API参考/磁盘/ModifyDiskSpec.md)

