---
title: 用于扩展应用程序报表的SQL分析
description: 了解如何使用SQL查询生成自定义仪表板的见解。
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# 用于扩展应用报告的 SQL Insights

使用自定义SQL查询从各种结构化数据集有效提取洞察。 技术人员可以使用查询专业模式执行复杂的SQL分析，然后通过自定义仪表板上的图表与非技术用户共享此分析或将它们导出为CSV文件。 这种insight创建方法非常适合具有明确关系的表，并且允许在您的见解和过滤器中进行更大程度的自定义，以适合小范围用例。

>[!IMPORTANT]
>
>查询专业模式仅适用于已购买[Data Distiller SKU](../../query-service/data-distiller/overview.md)的用户。

要从SQL生成见解，必须首先创建功能板。

## 创建自定义仪表板 {#create-custom-dashboard}

要创建自定义仪表板，请从左侧导航面板中选择&#x200B;**[!UICONTROL Dashboards]**&#x200B;以打开仪表板工作区。 接下来，选择 **[!UICONTROL Create dashboard]**。

![突出显示了“创建仪表板”的功能板库存。](../images/sql-insights-query-pro-mode/create-dashboard.png)

出现&#x200B;**[!UICONTROL Create dashboard]**&#x200B;对话框。 有两个选项可供您选择功能板创建方法。 要创建您的见解，您可以将现有数据模型用于[[!UICONTROL Guided design mode]](../standard-dashboards.md)，或者将您自己的SQL用于[!UICONTROL Query pro mode]。

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

使用现有数据模型的优点在于，它可以为您的特定业务需求提供结构化、高效和可伸缩的框架。 要了解如何[从现有数据模型](../standard-dashboards.md#create-widget)创建见解，请参阅自定义仪表板指南。

从SQL查询生成的见解提供了更大的灵活性和自定义设置。 技术人员可以使用查询专业模式对SQL执行复杂的分析，然后通过此仪表板功能与非技术用户共享此分析。 依次选择&#x200B;**[!UICONTROL Query pro mode]**&#x200B;和&#x200B;**[!UICONTROL Save]**。

>[!NOTE]
>
>做出选择后，将无法在该功能板中更改此选择。 相反，您必须使用不同的仪表板创建方法创建新仪表板。

![突出显示了带有Query pro模式和Save的[!UICONTROL Create dashboard]对话框。](../images/sql-insights-query-pro-mode/query-pro-mode.png)

## Query pro模式概述 {#query-pro-mode}

Query pro模式是一个基于SQL编辑器的工作流，可指导您完成在Adobe Experience Platform UI中使用自定义SQL查询生成洞察的过程。 您必须先创建功能板，然后才能使用自定义SQL查询生成见解。

## 撰写SQL {#compose-sql}

选择使用query pro模式创建仪表板后，将显示&#x200B;**[!UICONTROL Enter SQL]**&#x200B;对话框。 从下拉菜单中选择要查询的数据库（见解数据模型），然后在查询专家编辑器中为您的数据集输入合适的查询。

>[!NOTE]
>
>Query Pro模式仅适用于已购买Data Distiller SKU的用户。 [[!UICONTROL Guided design mode]](../standard-dashboards.md)可供所有用户从现有数据模型创建见解。

有关其UI元素的信息，请参阅[查询编辑器用户指南](../../query-service/ui/user-guide.md#query-authoring)。

![带有数据集下拉菜单和突出显示的运行图标的[!UICONTROL Enter SQL]对话框。该对话框已填充SQL查询并显示查询参数选项卡。](../images/sql-insights-query-pro-mode/enter-sql-database-dropdown.png)

### 查询参数 {#query-parameters}

若要包含[全局](./filters/global-filter.md)或[日期筛选器](./filters/date-filter.md)，您的查询&#x200B;**必须**&#x200B;使用查询参数。 在查询专业模式下构成语句时，如果查询使用查询参数，则必须提供示例值。 示例值允许您执行SQL语句并构建图表。 请注意，合成语句时提供的示例值会被您在运行时为日期或全局过滤器选择的实际值替换。

>[!IMPORTANT]
>
>如果要使用全局筛选器，则必须在SQL中放置一个查询参数，然后将该查询参数链接到构件编辑器中的全局筛选器。 在下面的屏幕快照中，`CONSENT_VALUE_FILTER`在SQL中用作全局筛选器的查询参数。 有关如何执行此操作的详细信息，请参阅[全局筛选器文档](./filters/global-filter.md#enable-global-filter)。

要执行查询，请选择运行图标（![运行图标）。](/help/images/icons/play.png))。 查询编辑器将显示结果选项卡。 接下来，要确认配置并打开构件编辑器，请选择&#x200B;**[!UICONTROL Select]**。

>[!TIP]
>
>如果查询使用查询参数，请运行一次查询以预填充所有使用的查询参数键。 查询将失败，但UI会自动显示“查询参数”选项卡并列出所有包含的键值。 为键添加适当的值。

![带有SQL输入的[!UICONTROL Enter SQL]对话框、显示的结果选项卡和突出显示的选择。](../images/sql-insights-query-pro-mode/enter-sql-select.png)

## 填充构件 {#populate-widget}

构件编辑器现在使用已执行SQL中的列进行填充。 仪表板的类型显示在左上方，在此例中为[!UICONTROL Manual SQL Entry]。 选择铅笔图标(![A铅笔图标。](/help/images/icons/edit.png))以随时编辑SQL。

>[!TIP]
>
>可用属性是从执行的SQL中获取的列。

要创建小组件，请使用[!UICONTROL Attributes]列中列出的属性。 您可以使用搜索栏查找属性或滚动列表。

![创建方法和属性列突出显示的构件编辑器。](../images/sql-insights-query-pro-mode/creation-method-and-attribute-column.png)

### 添加属性 {#add-attributes}

要向小组件添加属性，请选择加号图标(![A加号图标。](/help/images/icons/add-circle.png))。 显示的下拉菜单允许您根据SQL确定的选项向图表添加属性。 不同的图表类型具有不同的选项，例如X轴和Y轴下拉列表。

在此圆环图示例中，选项包括大小和颜色。 颜色划分圆环图结果，大小是实际使用的量度。 向[!UICONTROL Color]字段添加一个属性，以根据结果的组成将结果拆分为不同的颜色。

>[!TIP]
>
>选择向上和向下箭头图标(![向上和向下箭头图标。](/help/images/icons/switch.png))以切换条形图或折线图上X轴和Y轴的排列。

![带有添加图标下拉菜单和开关箭头的Widget Composer突出显示。](../images/sql-insights-query-pro-mode/add-icon-and-switch-arrows.png)

要更改小组件的图形或图表类型，请从[!UICONTROL Marks]下拉菜单的可用选项中选择。 选项包括[!UICONTROL Line]、[!UICONTROL Donut]、[!UICONTROL Big number]和[!UICONTROL Bar]。 选中后，将生成构件当前设置的预览可视化图表。

![突出显示具有构件预览的构件编辑器。](../images/sql-insights-query-pro-mode/widget-preview.png)

## 高级表属性 {#advanced-attributes}

要对表中的任何列或所有列应用自动排序功能，请选择&#x200B;**[!UICONTROL Edit]**&#x200B;以编辑整个仪表板。

![突出显示编辑的自定义仪表板。](../images/sql-insights-query-pro-mode/advanced-edit-dashboard.png)

在表图表中选择要添加列排序的省略号(`...`)，然后选择&#x200B;**[!UICONTROL Edit]**。

![显示突出显示“编辑”的省略号菜单的表。](../images/sql-insights-query-pro-mode/advanced-table-edit.png)

要为任何列启用排序，请选中&#x200B;**[!UICONTROL Sortable]**&#x200B;框。

![突出显示可排序复选框的表编辑页。](../images/sql-insights-query-pro-mode/advanced-table-sortable.png)

选择属性图标(![属性图标。](/help/images/icons/properties.png))以打开[!UICONTROL Properties]面板。 在&#x200B;**[!UICONTROL Properties]**&#x200B;面板中，使用下拉菜单选择&#x200B;**[!UICONTROL Default sort]**&#x200B;列，然后使用下拉菜单选择&#x200B;**[!UICONTROL Sort direction]**。 最后，选择&#x200B;**[!UICONTROL Save and close]**。

![带有属性图标、默认排序、排序方向以及保存并关闭的小组件编辑器突出显示。](../images/sql-insights-query-pro-mode/advanced-table-properties.png)

要了解有关使用排序、调整列大小和分页功能的详细信息，请参阅[查看更多](./view-more.md)。

## 小组件属性 {#properties}

选择属性图标(![属性图标。](/help/images/icons/properties.png))以打开属性面板。 在[!UICONTROL Properties]面板的&#x200B;**[!UICONTROL Widget title]**&#x200B;文本字段中输入小组件的名称。 您还可以重命名图表的各个方面。

>[!NOTE]
>
>属性侧边栏中可用的特定字段因您编辑的图表类型而异。

![突出显示属性图标和小组件标题字段的小组件编辑器。](../images/sql-insights-query-pro-mode/widget-properties-title-text.png)

## 保存您的构件 {#save-widget}

在小组件编辑器中保存会将小组件本地保存到您的仪表板。 如果要保存工作并稍后继续，请选择&#x200B;**[!UICONTROL Save]**。 构件名称下方的勾号图标表示构件已保存。 或者，如果您对您的小组件感到满意，请选择&#x200B;**[!UICONTROL Save and close]**，以便该小组件可供所有有权访问您仪表板的其他用户使用。 选择“取消”以放弃您的工作并返回您的自定义仪表板。

![包含“保存”、“保存并关闭”的Widget编辑器突出显示。](../images/sql-insights-query-pro-mode/insight-saved.png)

## 编辑仪表板和图表 {#edit}

选择&#x200B;**[!UICONTROL Edit]**&#x200B;以编辑您的整个仪表板或任何见解。 在编辑模式下，您可以调整小部件大小、编辑SQL或创建并应用全局和临时过滤器。 这些过滤器会限制仪表板小组件中显示的数据。 它是一种针对不同用例快速更新和微调见解的便捷方法。

![突出显示编辑的自定义仪表板。](../images/sql-insights-query-pro-mode/edit-dashboard.png)

选择&#x200B;**[!UICONTROL Add filter]**&#x200B;以创建[[!UICONTROL Date filter]](#create-date-filter)或[[!UICONTROL Global filter]](#create-global-filter)。 创建后，所有全局和日期筛选器都可以从[筛选器图标](#select-global-filter) （![筛选器图标）中使用。](/help/images/icons/filter.png))。

![突出显示了“添加筛选器”下拉菜单的自定义仪表板。](../images/sql-insights-query-pro-mode/add-filter.png)

## 编辑、复制或删除insight

有关如何[编辑、复制或删除现有小组件](../standard-dashboards.md#duplicate)的说明，请参阅自定义仪表板指南。

## 后续步骤

阅读本文档后，您现在知道如何在Adobe Experience Platform UI中编写SQL查询来生成自定义仪表板的图表。 接下来，您应该了解如何通过[创建日期过滤器](./filters/date-filter.md)或[创建全局过滤器](./filters/global-filter.md)来进一步扩充您的数据。

您还可以了解有关其他自定义分析功能的详细信息，包括[针对您SQL分析数据的不同查看选项](./view-more.md)或如何[查看自定义分析背后的SQL](./view-sql.md)。
