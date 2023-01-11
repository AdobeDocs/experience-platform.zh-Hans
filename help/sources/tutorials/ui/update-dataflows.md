---
keywords: Experience Platform；主页；热门主题；更新数据流；编辑计划
description: 本教程介绍了使用“源”工作区更新数据流计划的步骤，包括其摄取频率和间隔速率。
solution: Experience Platform
title: 在UI中更新源连接数据流
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# 更新UI中的数据流

本教程将为您提供有关如何使用源工作区更新现有数据流（包括其计划和映射）的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 更新数据流

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 选择 **[!UICONTROL 数据流]** 来查看现有数据流的列表。

![目录](../../images/tutorials/update-dataflows/catalog.png)

的 [!UICONTROL 数据流] 页面包含所有现有数据流的列表，包括有关其相应目标数据集、源和帐户名称的信息。

要对列表进行排序，请选择过滤器图标 ![过滤器](../../images/tutorials/update/filter.png) 来使用排序面板。

![过滤数据流](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供了所有可用源的列表。 您可以从列表中选择多个源以访问属于不同源的已过滤数据流选择。

选择要处理的源，以查看其现有数据流的列表。 确定要更新的数据流后，选择省略号(`...`)。

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

此时会出现一个下拉菜单，为您提供用于更新所选数据流的选项。 在此，您可以选择更新数据流的映射集和摄取计划。 您还可以选择选项以在监控仪表板中检查数据流，订阅警报，以及禁用或删除数据流。

要更新数据流的信息，请选择 **[!UICONTROL 更新数据流]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### 添加数据

的 [!UICONTROL 添加数据] 中。 选择相应的数据格式以查看所选数据的内容，然后选择 **[!UICONTROL 下一个]** 以继续。

![添加数据](../../images/tutorials/update-dataflows/add-data.png)

### 数据流详细信息

在 [!UICONTROL 数据流详细信息] 页面上，您可以为数据流提供更新的名称和描述，以及重新配置数据流的错误阈值。 在此步骤中，您还可以配置或修改警报订阅的设置。

提供更新的值后，请选择 **[!UICONTROL 下一个]**.

![数据流详细信息](../../images/tutorials/update-dataflows/dataflow-detail.png)

### 映射

>[!NOTE]
>
>以下源当前不支持编辑映射功能：Adobe Analytics、Adobe Audience Manager、HTTP API和 [!DNL Marketo Engage].

的 [!UICONTROL 映射] 该页面提供了一个界面，您可以在其中添加和删除与数据流关联的映射集。

映射界面会显示数据流的现有映射集，而不是新的推荐映射集。 映射更新仅应用于将来计划运行的数据流。 计划进行一次性摄取的数据流无法更新其映射集。

在此，您可以使用映射界面修改应用于数据流的映射集。 有关如何使用映射界面的完整步骤，请参阅 [数据准备UI指南](../../../data-prep/ui/mapping.md) 以了解更多信息。

![映射](../../images/tutorials/update-dataflows/mapping.png)

### 计划

的 [!UICONTROL 计划] 步骤，允许您更新数据流的摄取计划，并使用更新的映射自动摄取选定的源数据。

>[!NOTE]
>
>您无法重新计划计划一次性摄取的数据流。

![新计划](../../images/tutorials/update-dataflows/new-schedule.png)

您还可以使用数据流页面中提供的行内更新选项来更新数据流的摄取计划。

从数据流页面中，选择省略号(`...`)，然后选择 **[!UICONTROL 编辑计划]** 下拉菜单中。

![编辑时间表](../../images/tutorials/update-dataflows/edit-schedule.png)

的 **[!UICONTROL 编辑计划]** 对话框为您提供用于更新数据流的摄取频率和间隔率的选项。 设置更新的频度和间隔值后，请选择 **[!UICONTROL 保存]**.

![计划弹出窗口](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### 审阅

的 **[!UICONTROL 审阅]** 步骤，允许您在更新数据流之前查看数据流。

审核数据流后，选择 **[!UICONTROL 完成]** 并为要创建新映射集的数据流留出一些时间。

![审查](../../images/tutorials/update-dataflows/review.png)

## 后续步骤

通过阅读本教程，您已成功使用 [!UICONTROL 源] 工作区以更新数据流的摄取计划和映射集。

有关如何使用 [!DNL Flow Service] API，请参阅 [使用流服务API更新数据流](../../tutorials/api/update-dataflows.md).
