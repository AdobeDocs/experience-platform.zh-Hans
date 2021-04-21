---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流；目标
description: 目标允许您将您的数据从Adobe Experience Platform激活到无数外部合作伙伴。 本教程说明了如何使用Experience Platform用户界面监视目标的数据流。
solution: Experience Platform
title: 在UI中监视目标的数据流
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---

# 在UI中监视目标的数据流

目标允许您将您的数据从Adobe Experience Platform激活到无数外部合作伙伴。 本教程说明了如何使用Experience Platform用户界面监视目标的数据流。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [目标](../../destinations/home.md):目标是与常用应用程序预建集成，允许从平台无缝激活数据，以实现跨渠道营销活动、电子邮件活动、定向广告和许多其他使用案例。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 监视数据流

在平台UI的&#x200B;**[!UICONTROL Destinations]**&#x200B;工作区中，导航到&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，然后选择要视图的目标名称。

![](../assets/ui/monitor-destinations/select-destination.png)

将出现一列表现有数据流。 本页是可查看数据流的列表，包括有关其目标、用户名、数据流数量和状态的信息。

有关状态的详细信息，请参阅下表：

| 状态 | 描述 |
| ------ | ----------- |
| 已启用 | `Enabled`状态指示数据流处于活动状态，并根据提供的计划接收数据。 |
| 已禁用 | `Disabled`状态指示数据流处于非活动状态且未摄取任何数据。 |
| 处理时间 | `Processing`状态指示数据流尚未处于活动状态。 通常在创建新数据流后立即遇到此状态。 |
| 错误 | `Error`状态表示数据流的激活进程已中断。 |

## [!UICONTROL Dataflow runs]

[!UICONTROL Dataflow runs]选项卡提供数据流上到批处理目标的量度数据。 将显示单个运行及其特定量度的列表，以及用户档案记录的以下总计：

- **[!UICONTROL Profile records activated]**:为用户档案创建或更新的激活记录的总数。
- **[!UICONTROL Profile records skipped]**:根据用户档案退出或缺少属性，为激活而跳过的用户档案记录总数。

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>根据目标数据流的计划频率生成数据流运行。 将为应用于区段的每个合并策略单独运行数据流。

要视图特定数据流运行的详细信息，请从列表中选择该运行的开始时间。 数据流运行的详细信息页包含其他信息，如处理的数据大小和对错误诊断的详细信息所发生的任何错误的列表。

![](../assets/ui/monitor-destinations/dataflow.png)
