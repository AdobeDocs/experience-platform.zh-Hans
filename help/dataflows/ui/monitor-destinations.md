---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了从“源”工作区查看现有数据流的步骤。
solution: Experience Platform
title: 监视数据流
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 791ad61f2f28da03ef3e5cb5efdd89154e9b1a0b
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---


# 在UI中监视目标的数据流

目的地允许您将您的数据从Adobe Experience Platform激活到无数外部合作伙伴。 本教程提供了如何使用Experience Platform用户界面监视目标的数据流的说明。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [目标](../../destinations/home.md):目标是预建的与常用应用程序的集成，允许跨渠道营销活动、电子邮件活动、定向广告和许多其他用例无缝激活来自平台的数据。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 监视数据流

在平 **[!UICONTROL 台]** UI中的目标工作区中，导航到 **[!UICONTROL 浏览]** 选项卡，然后选择要视图的目标名称。

![](../assets/ui/monitor-destinations/select-destination.png)

出现一列表现有数据流。 本页是可查看数据流的列表，包括有关其目标、用户名、数据流数和状态的信息。

有关状态的详细信息，请参阅下表：

| 状态 | 描述 |
| ------ | ----------- |
| 已启用 | 状 `Enabled` 态表示数据流处于活动状态，并且正在根据它提供的计划接收数据。 |
| 已禁用 | 状 `Disabled` 态表示数据流处于非活动状态，不接收任何数据。 |
| 处理时间 | 状 `Processing` 态表示数据流尚未激活。 创建新数据流后，通常会立即遇到此状态。 |
| 错误 | 状 `Error` 态表示数据流的激活进程已中断。 |

## [!UICONTROL 数据流运行]

“数 [!UICONTROL 据流运行] ”选项卡提供数据流运行到批处理目标的度量数据。 将显示单个运行及其特定度量的列表，以及用户档案记录的以下总计：

- **[!UICONTROL 用户档案记录已激活]**:为用户档案创建或更新的激活记录总数。
- **[!UICONTROL 用户档案记录已跳过]**: 根据用户档案退出或缺少属性，为激活跳过的用户档案记录总数。

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>根据目标数据流的计划频率生成数据流运行。 对应用于段的每个合并策略执行单独的数据流运行。

要视图特定数据流运行的详细信息，请从列表中选择运行的开始时间。 数据流运行的详细信息页面包含其他信息，如已处理数据的大小和错误诊断的详细信息所发生的任何错误的列表。

![](../assets/ui/monitor-destinations/dataflow.png)