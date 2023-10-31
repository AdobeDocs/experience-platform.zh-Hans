---
title: 在UI中按需引入源数据流
description: 了解如何使用Experience Platform用户界面按需为源连接创建数据流。
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 在UI中按需引入源数据流

您可以使用Adobe Experience Platform用户界面中的源工作区中的按需摄取来触发现有数据流的流运行迭代。

本文档提供了有关如何根据需要为来源创建数据流的步骤，以及如何重试已处理或已失败的流运行的步骤。

>[!BEGINSHADEBOX]

**什么是流量运行？**

流运行表示数据流执行的实例。 例如，如果数据流计划在早上9:00、晚上10:00和晚上11:00每小时运行，则您将有三次流运行实例。 流量运行特定于您的特定组织。

>[!ENDSHADEBOX]

## 快速入门

本文档要求您对Experience Platform的以下组件有一定的了解：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [数据流](../../../dataflows/home.md)：数据流表示跨Platform移动数据的数据作业。 数据流在不同的服务中配置，帮助将数据从源连接器移动到目标数据集、身份服务和实时客户档案以及目标。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 按需创建数据流 {#create-a-dataflow-on-demand}

导航至 *[!UICONTROL 数据流]* “源”工作区的选项卡。 从此处，查找要按需运行的数据流，然后选择省略号(**`...`**)。

![源工作区中的数据流列表。](../../images/tutorials/on-demand/select-dataflow.png)

接下来，选择 **[!UICONTROL 按需运行]** 从出现的下拉菜单中。

![已选中按需运行选项的下拉菜单。](../../images/tutorials/on-demand/run-on-demand.png)

配置按需引入的时间表。 选择 **[!UICONTROL 摄取开始时间]**， **[!UICONTROL 日期范围开始时间]**，和 **[!UICONTROL 日期范围结束时间]**.

| 计划配置 | 描述 |
| --- | --- |
| [!UICONTROL 摄取开始时间] | 按需流运行的计划开始时间。 |
| [!UICONTROL 日期范围开始时间] | 从中检索数据的最早日期和时间。 |
| [!UICONTROL 日期范围结束时间] | 检索数据的日期和时间。 |

选择 **[!UICONTROL 计划]** 并留出一些时间触发您的按需数据流。

![按需摄取的计划配置窗口。](../../images/tutorials/on-demand/configure-schedule.png)

选择数据流名称以查看数据流活动。 在这里，您将看到已处理的数据流运行的列表。 选择数据流运行，然后选择 **[!UICONTROL 重试]** 从右边栏重新尝试摄取选定的数据流运行迭代。

![针对所选数据流运行的已处理流列表。](../../images/tutorials/on-demand/processed.png)

选择 **[!UICONTROL 已计划]** 用于查看安排在将来摄取的数据流运行的列表。

![选定数据流的计划流运行列表。](../../images/tutorials/on-demand/scheduled.png)

## 后续步骤

通过阅读本文档，您已了解如何根据需要为现有源数据流创建流运行。 欲知关于来源的更多信息，请阅读 [源概述](../../home.md)
