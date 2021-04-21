---
keywords: Experience Platform；主页；热门主题；更新数据流；编辑计划
description: 本教程介绍了使用“源”工作区更新数据流计划的步骤，包括其摄取频率和间隔速率。
solution: Experience Platform
title: 在UI中更新源连接数据流
topic-legacy: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# 更新UI中的数据流

本教程提供了有关如何使用[!UICONTROL Sources]工作区更新现有源数据流的步骤，包括有关编辑数据流计划和映射的信息。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [来源](../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
- [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 编辑映射

>[!NOTE]
>
>以下源当前不支持编辑映射功能：Adobe Analytics、Adobe Audience Manager、HTTP API和[!DNL Marketo Engage]。

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 从顶部标题中选择&#x200B;**[!UICONTROL Dataflows]**&#x200B;以视图现有数据流的列表。

![目录](../../images/tutorials/update-dataflows/catalog.png)

[!UICONTROL Dataflows]页面包含所有现有数据流的列表，包括有关其运行状态、上次运行日期和帐户名称的信息。

选择左上角的过滤器图标![过滤器](../../images/tutorials/update/filter.png)以启动排序面板。

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用源的列表。 您可以从列表中选择多个源，以访问属于不同源的已过滤数据流的选定内容。

选择要处理的源，以查看其现有数据流的列表。 确定要更新的数据流后，请选择帐户名称旁边的省略号(`...`)。

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

此时将显示一个下拉菜单，其中提供了用于更新所选数据流的选项。 在此处，您可以选择更新数据流的映射集和摄取计划。 您还可以选择选项以在监视仪表板中检查数据流，以及禁用或删除数据流。

选择&#x200B;**[!UICONTROL Edit source]**&#x200B;以更新其映射。

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

出现[!UICONTROL Add data]步骤。 选择适当的数据格式以查看所选数据的内容，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![add-data](../../images/tutorials/update-dataflows/add-data.png)

[!UICONTROL Mapping]页为您提供了一个界面，您可以在该界面中添加和删除与数据集关联的映射集。

>[!TIP]
>
>映射更新仅应用于将来计划的数据流运行。

选择&#x200B;**[!UICONTROL Add new mapping]**&#x200B;以添加新映射集。

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

然后，输入相应的源字段属性和目标XDM字段值以完成其他映射集。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![新增映射](../../images/tutorials/update-dataflows/new-mapping-added.png)

将出现[!UICONTROL Scheduling]步骤，允许您更新数据流的摄取计划，并使用更新的映射自动摄取所选源数据。

>[!NOTE]
>
>您无法更新为一次性摄取而开始时间已过去的数据流的映射集。

![调度](../../images/tutorials/update-dataflows/scheduling.png)

在[!UICONTROL Dataflow detail]页中，您可以为数据流提供更新的名称和说明，并重新配置数据流的错误阈值。

提供更新值后，请选择&#x200B;**[!UICONTROL Next]**。

![数据流详细信息](../../images/tutorials/update-dataflows/dataflow-detail.png)

将显示&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在更新数据流之前对其进行查看。

查看数据流后，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;并为要创建新映射集的数据流留出一些时间。

![审查](../../images/tutorials/update-dataflows/review.png)

## 编辑计划

要编辑现有数据流的摄取计划，请选择数据流名称旁边的省略号(`...`)，然后从下拉菜单中选择&#x200B;**[!UICONTROL Edit schedule]**。

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

通过本教程，您已成功使用[!UICONTROL Sources]工作区更新了数据流的摄取计划和映射集。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关使用流服务API](../../tutorials/api/update-dataflows.md)更新数据流的教程。[
