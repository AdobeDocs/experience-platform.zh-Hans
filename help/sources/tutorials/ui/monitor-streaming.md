---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流
description: Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了从源工作区监控流数据流的步骤。
solution: Experience Platform
title: 在UI中监控流源的数据流
topic-legacy: overview
type: Tutorial
source-git-commit: 58761cbe8465f4a00f07f33f751f481d34493cf7
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---


# 在UI中监控流源的数据流

本教程介绍了使用[!UICONTROL Sources]工作区监控流源数据流的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [数据流](../../../dataflows/home.md):数据流是跨平台移动数据的数据作业的表示形式。数据流是跨不同的服务配置的，有助于将数据从源连接器移动到目标数据集，移动到[!DNL Identity]和[!DNL Profile]，以及[!DNL Destinations]。
   * [数据流运行](../../notifications.md):数据流运行是基于所选数据流的频率配置的定期计划作业。
* [来源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 监控流源的数据流

在平台UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示可为其创建帐户的各种源。

要查看流源的现有数据流，请从顶部标头中选择&#x200B;**[!UICONTROL 数据流]**。

![目录](../../images/tutorials/monitor-streaming/catalog.png)

[!UICONTROL 数据流]页包含组织中所有现有数据流的列表，包括其源数据、帐户名称和数据流运行状态的信息。

选择要查看的数据流的名称。

![数据流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含有关数据流运行状态的更多信息：

| 状态 | 描述 |
| ------ | ----------- |
| 已完成 | `Completed`状态表示相应数据流运行的所有记录都在1小时内进行处理。 `Completed`状态仍可能包含数据流运行中的错误。 |
| 处理时间 | `Processing`状态表示数据流尚未处于活动状态。 此状态通常会在创建新数据流后立即出现。 |
| 错误 | `Error`状态表示数据流的激活过程已中断。 |

[!UICONTROL 数据流活动]页显示有关流数据流的特定信息。 顶部横幅包含在选定日期范围内所有流数据流运行的摄取记录和失败记录的累计数量。

页面的下半部分显示有关每个流运行接收、摄取和失败的记录数的信息。 每次流量运行都记录在每小时的窗口中。

![数据流活动](../../images/tutorials/monitor-streaming/dataflow-activity.png)

每个数据流运行都显示以下详细信息：

* **[!UICONTROL 数据流运行开始]**:数据流运行开始的时间。
* **[!UICONTROL 处理时间]**:数据流处理所花费的时间。
* **[!UICONTROL 收到的记录]**:数据流中从源连接器接收的记录总数。
* **[!UICONTROL 摄取的记录]**:摄取到的记录总数计 [!DNL Data Lake]数。
* **[!UICONTROL 记录失败]**:由于数据中的错误而未 [!DNL Data Lake] 摄取到的记录数。
* **[!UICONTROL 摄取率]**:摄取到中的记录的成功率 [!DNL Data Lake]。启用[!UICONTROL 部分摄取]时，此量度适用。
* **[!UICONTROL 状态]**:表示数据流处于的状态：完成  或 [!UICONTROL 处理]。 完成表示在一小时内处理了相应数据流运行的所有记录。 处理意味着数据流运行尚未完成。

默认情况下，显示的数据包含过去七天的摄取率。 选择&#x200B;**[!UICONTROL 最近7天]**&#x200B;以调整显示的记录的时间范围。

![更改时间](../../images/tutorials/monitor-streaming/change-time.png)

此时会出现日历弹出窗口，为您提供替代摄取时间范围的选项。 选择&#x200B;**[!UICONTROL 最近30天]**，然后选择&#x200B;**[!UICONTROL 应用]**。

![日历](../../images/tutorials/monitor-streaming/calendar.png)

要查看特定数据流运行的详细信息（包括其错误），请从列表中选择运行的开始时间。

![选择失败](../../images/tutorials/monitor-streaming/select-fail.png)

“[!UICONTROL 数据流运行概述]”页包含有关数据流的其他信息，如其相应的数据流运行ID、目标数据集和IMS组织ID。

出现错误的流还包含[!UICONTROL 数据流运行错误]面板，该面板显示导致运行失败的特定错误以及失败的记录总数。

![失败](../../images/tutorials/monitor-streaming/failure.png)

## 后续步骤

在本教程中，您已成功使用[!UICONTROL Sources]工作区来监视流数据流并识别导致任何失败数据流的错误。 有关更多信息，请参阅以下文档：

* [源概述](../../home.md)
* [数据流概述](../../../dataflows/home.md)