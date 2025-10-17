---
title: 在UI中按需引入源数据流
description: 了解如何使用Experience Platform用户界面按需为源连接创建数据流。
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: fabacf273fb5774ddcee42d0cdcf12281eb0216b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# 在UI中按需引入源数据流

您可以使用Adobe Experience Platform用户界面中的源工作区中的按需摄取来触发现有数据流的流运行迭代。

本文档提供了有关如何根据需要为来源创建数据流的步骤，以及如何重试已处理或已失败的流运行的步骤。

>[!BEGINSHADEBOX]

**什么是流运行？**

流运行表示数据流执行的实例。 例如，如果数据流计划在上午9:00、上午10:00和上午11:00每小时运行，则您将运行三个流实例。 流量运行特定于您的特定组织。

>[!ENDSHADEBOX]

## 快速入门

>[!NOTE]
>
>要创建流运行，您必须首先具有计划为一次性摄取的数据流的流ID。

本文档要求您对Experience Platform的以下组件有一定的了解：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [数据流](../../../dataflows/home.md)：数据流是跨Experience Platform移动数据的数据作业的表示形式。 数据流在不同的服务中配置，帮助将数据从源连接器移动到目标数据集、身份服务和实时客户档案以及目标。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 按需创建数据流 {#create-a-dataflow-on-demand}

导航到源工作区的&#x200B;*[!UICONTROL 数据流]*&#x200B;选项卡。 从此处，查找要按需运行的数据流，然后选择数据流名称旁边的省略号(**`...`**)。

![源工作区中的数据流列表。](../../images/tutorials/on-demand/select-dataflow.png)

接下来，从出现的下拉菜单中选择&#x200B;**[!UICONTROL 按需运行]**。

![已选择“按需运行”选项的下拉菜单。](../../images/tutorials/on-demand/run-on-demand.png)

配置按需引入的时间表。 选择&#x200B;**[!UICONTROL 摄取开始时间]**、**[!UICONTROL 日期范围开始时间]**&#x200B;和&#x200B;**[!UICONTROL 日期范围结束时间]**。

| 计划配置 | 描述 |
| --- | --- |
| [!UICONTROL 引入开始时间] | 按需流运行的计划开始时间。 |
| [!UICONTROL 日期范围开始时间] | 从中检索数据的最早日期和时间。 |
| [!UICONTROL 日期范围结束时间] | 检索数据的日期和时间。 |

选择&#x200B;**[!UICONTROL 计划]**，并等待几分钟让您的按需数据流触发。

![按需引入的计划配置窗口。](../../images/tutorials/on-demand/configure-schedule.png)

选择数据流名称以查看数据流活动。 在这里，您将看到已处理的数据流运行的列表。 无论数据流运行是失败还是成功，您都可以重新运行其各个迭代。 对于失败的运行迭代，您可以在诊断并解决创建过程中可能遇到的任何错误后，使用&#x200B;**[!UICONTROL 重试]**&#x200B;再次启动运行。

>[!TIP]
>
>重试流运行将只处理时间戳在原始运行范围内的文件。

![所选数据流已处理的流运行列表。](../../images/tutorials/on-demand/processed.png)

选择&#x200B;**[!UICONTROL 已计划]**&#x200B;可查看已计划将来摄取的数据流运行列表。

![选定数据流的计划流运行列表。](../../images/tutorials/on-demand/scheduled.png)

## 后续步骤

通过阅读本文档，您已了解如何根据需要为现有源数据流创建流运行。 有关源的更多信息，请阅读[源概述](../../home.md)
