---
keywords: Experience Platform；主页；热门主题；更新数据流；编辑计划
description: 本教程介绍了使用“源”工作区更新数据流计划的步骤，包括其摄取频率和间隔速率。
solution: Experience Platform
title: 在UI中更新源连接数据流计划
topic: 概述
type: 教程
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# 更新UI中的数据流

本教程介绍使用[!UICONTROL Sources]工作区更新数据流计划的步骤，包括其摄取频率和间隔速率。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [来源](../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
- [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 编辑计划

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 从顶部标题中选择&#x200B;**[!UICONTROL Dataflows]**&#x200B;以视图现有数据流的列表。

![目录](../../images/tutorials/update-dataflows/catalog.png)

[!UICONTROL Dataflows]页面包含所有现有数据流的列表，包括有关其运行状态、上次运行日期和帐户名称的信息。

选择左上角的过滤器图标![过滤器](../../images/tutorials/update/filter.png)以启动排序面板。

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用源的列表。 您可以从列表中选择多个源，以访问属于不同源的已过滤数据流的选定内容。

选择要处理的源，以查看其现有数据流的列表。 确定要重新计划的数据流后，请选择帐户名称旁边的省略号(`...`)。

![重新](../../images/tutorials/update-dataflows/reschedule.png)

此时将显示一个下拉菜单，其中提供了&#x200B;**[!UICONTROL Edit schedule]**、**[!UICONTROL Disable dataflow]**、**[!UICONTROL View in monitoring]**&#x200B;和&#x200B;**[!UICONTROL Delete]**&#x200B;的选项。 从菜单中选择 **[!UICONTROL Edit schedule]**。

![edit-计划](../../images/tutorials/update-dataflows/edit-schedule.png)

**[!UICONTROL Edit schedule]**&#x200B;对话框为您提供用于更新数据流的摄取频率和间隔速率的选项。 设置更新的频率和间隔值后，请选择&#x200B;**[!UICONTROL Save]**。

>[!NOTE]
>
>无法重新安排一次性摄取的数据流。

![计划对话框](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| 计划 | 描述 |
| ---------- | ----------- |
| 频度 | 数据流收集数据的频率。 可接受的值用于编辑现有数据流的频率计划，包括：`minute`、`hour`、`day`或`week`。 |
| 间隔 | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数，且必须大于或等于`15`。 |

稍后，屏幕底部会显示一个确认框，确认更新成功。

![计划确认](../../images/tutorials/update-dataflows/schedule-confirm.png)

## 后续步骤

通过本教程，您已成功使用[!UICONTROL Sources]工作区更新了数据流的摄取计划。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关使用流服务API](../../tutorials/api/update-dataflows.md)更新数据流的教程。[