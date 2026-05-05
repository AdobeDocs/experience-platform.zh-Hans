---
keywords: Experience Platform；查询服务；数据Distiller；加速器；参数化查询；SQL模板
solution: Experience Platform
title: 数据Distiller加速器
description: 使用Data Distiller加速器在查询服务UI中运行和计划经Adobe批准的参数化SQL模板。 加速器是只读的，并且由Adobe管理；请使用**[!UICONTROL Create custom template]**克隆和编辑它们。
source-git-commit: 5ee579c15fc2d9954673062b08280d9060b5205a
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 0%

---

# 数据Distiller加速器 {#data-distiller-accelerators}

数据Distiller加速器是Adobe创作、参数化的SQL模板，专为常见分析方案而设计。 使用加速器运行常见分析而不从头开始编写SQL。 加速器是只读的，并由Adobe进行维护，从而确保整个组织的一致性。 如果需要修改一个模板，可以将其克隆为自定义模板。

阅读本指南，了解如何在[!UICONTROL Queries]工作区中运行、计划和克隆加速器。

>[!AVAILABILITY]
>
>数据Distiller加速器仅适用于具有Data Distiller SKU的组织。 [!UICONTROL Accelerators]选项卡和相关工作流需要Data Distiller加载项。 请参阅[Data Distiller概述](../data-distiller/overview.md)或联系您的Adobe代表以了解更多信息。

## 先决条件 {#prerequisites}

在开始之前，请确保您满足以下要求：

* 您有权访问Experience Platform中的[!UICONTROL Queries]工作区。
* 您了解[如何使用查询编辑器并运行查询](./user-guide.md)。
* 您熟悉[参数化查询](./parameterized-queries.md)（在运行时替换了SQL中的占位符）。

## 何时使用加速器 {#when-to-use}

当您需要为常见分析模式（如funnel分析、移动平均值或受众重叠）预建SQL时，请使用加速器。 如果没有符合您使用案例的加速器，请[在查询编辑器](./user-guide.md#query-authoring)中编写自定义查询，或请求新的加速器（请参阅[请求新的加速器](#request-accelerator)）。

一小部分加速器作为功能板打开以供立即分析，而其他加速器在查询编辑器中打开，您可以在其中运行、计划或调整逻辑。 请参阅[与仪表板关联的加速器](#dashboard-accelerators)部分，了解这些预配置的可视化图表如何提供有关受众数据的见解。

要开始使用加速器，请导航到&#x200B;**[!UICONTROL Queries]**&#x200B;工作区，然后打开&#x200B;**[!UICONTROL Accelerators]**&#x200B;选项卡或&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡。

## 加速器发现路径 {#discovery-paths}

您可以通过两种方式从查询工作区中访问加速器，具体取决于您是要获取完整目录还是推荐模板。

### 使用“加速器”选项卡

当您要浏览所有可用的加速器时，请使用此路径。 要打开完整的加速器目录，请在左侧导航中选择&#x200B;**[!UICONTROL Queries]**，然后选择&#x200B;**[!UICONTROL Accelerators]**&#x200B;选项卡。

工作区会显示一个包含名称、SQL预览和时间戳的加速器的表。 选取加速器名称，以在“查询编辑器”中将其打开。

>[!NOTE]
>
>从&#x200B;**[!UICONTROL Accelerators]**&#x200B;选项卡中选择的所有加速器将在查询编辑器中打开。

![选择“加速器”选项卡的查询工作区显示加速器表。](../images/ui/accelerators/accelerators-tab-table.png)

### 使用“概述”选项卡

当您希望快速访问高度推荐的加速器时，请使用此路径。 导航到&#x200B;**[!UICONTROL Queries]**，然后选择&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡。 接下来，从&#x200B;**[!UICONTROL Recommended Data Distiller accelerators]**&#x200B;部分中选择一张信息卡。

大多数加速器在查询编辑器中打开。 一小部分加速器作为具有预建可视化图表的功能板打开。 如果卡片打开的是仪表板而不是查询编辑器，请参阅[与仪表板关联的加速器](#dashboard-accelerators)。

![选择了“概述”选项卡的“查询”工作区，其中显示了一个推荐的Data Distiller加速器列表。](../images/ui/accelerators/queries-overview-accelerators.png)

## 在查询编辑器中打开加速器 {#open-accelerator}

本节介绍在查询编辑器中打开加速器时会发生什么情况，以及下一步可以执行的操作，包括运行加速器、安排加速器时间或创建自定义模板。

打开加速器后，您可以&#x200B;**运行**&#x200B;加速器以查看结果，**安排**&#x200B;加速器自动运行，或&#x200B;**创建自定义模板**&#x200B;以修改SQL。

>[!NOTE]
>
>在查询编辑器中打开加速器时，SQL以只读状态预加载，并且工具栏操作（如[!UICONTROL Show results]、[!UICONTROL Undo text]、[!UICONTROL Format text]）被禁用。

右侧面板显示元数据（如&#x200B;**[!UICONTROL Accelerator ID]**、**[!UICONTROL Name]**&#x200B;和修改详细信息），并通过&#x200B;**[!UICONTROL Add schedule]**&#x200B;提供对计划的访问权限。

![打开了快捷键的查询编辑器，显示SQL区域、查询参数选项卡和右侧面板。](../images/ui/accelerators/accelerator-query-editor.png)

### 提供参数并运行加速器 {#provide-parameters-execute}

要运行加速器，必须首先为所有必需的参数提供值。 参数使用`${PARAMETER_NAME}`语法并显示在编辑器下方的&#x200B;**[!UICONTROL Query parameters]**&#x200B;选项卡中。 例如，`${START_DATE}`需要`YYYY-MM-DD`格式的日期值（例如，`2024-01-01`），`${AUDIENCE_ID}`需要特定的受众标识符。

要运行加速器，请执行以下操作：

1. 选择&#x200B;**[!UICONTROL Query parameters]**&#x200B;并为每个参数输入一个值。
2. 选择播放图标（![播放图标。](../../images/icons/play.png)） 工具栏中。

加速器运行并在&#x200B;**[!UICONTROL Results]**&#x200B;选项卡中显示结果。 除非您使用&#x200B;**[!UICONTROL Run as CTAS]**&#x200B;或计划加速器，否则这些结果将不会保留到数据集中。

有关参数化查询的详细信息，请参阅查询编辑器中的[参数化查询](./parameterized-queries.md)。

## 保留来自加速器的结果 {#persist-results}

运行加速器并确认结果后，可以将输出保留到数据集。

若要从结果创建数据集，请选择&#x200B;**[!UICONTROL Save]**&#x200B;以将加速器另存为模板，然后选择&#x200B;**[!UICONTROL Run as CTAS]**。 出现&#x200B;**[!UICONTROL Enter output dataset details]**&#x200B;对话框。 输入数据集名称和可选描述，然后确认以创建数据集。 此操作创建新数据集并将结果写入其中。

![已填充包含数据集名称和描述的[!UICONTROL Enter output dataset details]对话框。](../images/ui/accelerators/output-dataset-details-dialog.png)

## 计划加速器 {#schedule-accelerator}

要计划使用固定参数值自动运行的加速器，请在右侧面板中选择&#x200B;**[!UICONTROL Add schedule]**。

>[!TIP]
>
>在计划之前，请确保您了解所需的参数值。 首先运行加速器以验证结果。

此时将显示计划配置对话框。

![显示频率、日期范围、输出数据集和参数字段的计划配置对话框。](../images/ui/accelerators/schedule-details.png)

在计划配置对话框中，必须再次提供频率、时间范围、输出数据集和参数值。 在查询编辑器中输入的参数值不会纳入计划配置中。 在&#x200B;**[!UICONTROL Dataset details]**&#x200B;部分中，您可以选择&#x200B;**[!UICONTROL Append into existing dataset]**&#x200B;或&#x200B;**[!UICONTROL Create and append into new dataset]**。 配置计划后，加速器会根据您的设置自动运行，并将结果写入所选数据集。

有关完整的分步说明，请参阅[创建查询计划](./query-schedules.md#create-schedule)指南。

## 从加速器创建自定义模板 {#create-custom-template}

如果需要修改SQL或在自己的配置下重用逻辑，则可以从加速器创建自定义模板。 首先，在查询编辑器中打开加速器，然后选择&#x200B;**[!UICONTROL Create custom template]**。 根据需要修改SQL和详细信息，然后选择&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Save and close]**&#x200B;以存储模板。

保存后，该模板即可编辑，并且可以运行、计划或与CTA一起使用。 模板将保存到&#x200B;**[!UICONTROL Templates]**&#x200B;选项卡，您可以在其中像管理任何其他模板一样管理模板。 有关详细信息，请参阅[查询模板](./query-templates.md)。

### 创建自定义模板时发生了什么变化 {#custom-template-differences}

克隆的模板与原始加速器不同，因为SQL可以编辑，您可以保存更改、删除模板以及对其进行调度。 **[!UICONTROL Modified by]**&#x200B;字段显示您的姓名。 在&#x200B;**[!UICONTROL Templates]**&#x200B;选项卡中找到了该模板，而不是&#x200B;**[!UICONTROL Accelerators]**。

## 功能板链接的加速器 {#dashboard-accelerators}

“**[!UICONTROL Overview]**”选项卡上的某些加速器以仪表板形式打开，而不是SQL查询。 这些加速器为分析受众数据提供了预建的可视化图表，并且无需参数输入或手动执行。

以下加速器在&#x200B;**[!UICONTROL Dashboards]**&#x200B;工作区中打开：

**[!UICONTROL Advanced Audience Overlaps]**&#x200B;分析选定受众之间或整个受众集的交叉点以确定重叠模式。 利用这些见解来优化分段并减少冗余定位。

**[!UICONTROL Audience Comparison]**&#x200B;在两个受众之间并排比较关键量度，包括大小、身份构成和随时间发生的变化。 使用此视图可评估性能差异并告知目标定位决策。

**[!UICONTROL Audience Trends]**&#x200B;跟踪受众量度随时间的变化，包括受众大小和身份计数。 使用这些趋势监控增长并评估分段策略的影响。

**[!UICONTROL Audience Identity Overlaps]**&#x200B;检查所选受众中标识类型的重叠方式，以了解标识关系。 使用此分析可以提高身份拼接和分段准确性。

![仪表板视图显示具有图表和筛选器的受众分析可视化图表。](../images/ui/accelerators/dashboard-accelerator-template-example.png)

仪表板打开后，使用可用的控件和筛选器来浏览和比较受众数据。 有关详细信息，请参阅[仪表板模板](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)。

## 请求新加速器 {#request-accelerator}

如果您有一个现有加速器未涵盖的重复用例，请通过您的Adobe支持渠道提交请求。 Adobe会根据常见使用模式和行业适用性来评估请求。

## 后续步骤 {#next-steps}

您现在可以使用加速器运行和自动执行常见分析查询。

要扩展您的工作流，请创建和浏览[查询模板](./query-templates.md#browse)、作者[参数化查询](./parameterized-queries.md)、计划[查询](./query-schedules.md)或探索[查询服务工作流](./user-guide.md)。
