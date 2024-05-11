---
title: Query Pro模式
description: 了解如何在Adobe Experience Platform UI中使用SQL查询为自定义仪表板生成图表。
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Query pro模式 {#query-pro-mode}

Query pro模式是一个基于SQL编辑器的工作流，可指导您完成在Adobe Experience Platform UI中使用自定义SQL查询生成洞察的过程。 首先，您必须使用自定义SQL查询生成见解 [创建功能板](./overview.md#create-custom-dashboard).

## 撰写SQL {#compose-sql}

选择使用查询专业模式创建操控板后， **[!UICONTROL 输入SQL]** 出现对话框。 从下拉菜单中选择要查询的数据库（见解数据模型），然后在查询专家编辑器中为您的数据集输入合适的查询。

>[!NOTE]
>
>Query Pro模式仅适用于已购买Data Distiller SKU的用户。 此 [[!UICONTROL 引导式设计模式]](../../user-defined-dashboards.md) 可供所有用户从现有数据模型创建见解。

请参阅 [查询编辑器用户指南](../../../query-service/ui/user-guide.md#query-authoring) 以了解有关其UI元素的信息。

![此 [!UICONTROL 输入SQL] 对话框，其中数据集下拉菜单和运行图标突出显示。该对话框已填充SQL查询，并且显示查询参数选项卡。](../../images/customizable-insights/enter-sql-database-dropdown.png)

### 查询参数 {#query-parameters}

要包含 [全局](./filters/global-filter.md) 或 [日期过滤器](./filters/date-filter.md) 您的查询 **必须** 使用查询参数。 在查询专业模式下构成语句时，如果查询使用查询参数，则必须提供示例值。 示例值允许您执行SQL语句并构建图表。 请注意，合成语句时提供的示例值会被您在运行时为日期或全局过滤器选择的实际值替换。



>[!IMPORTANT]
>
>如果要使用全局筛选器，则必须在SQL中放置一个查询参数，然后将该查询参数链接到构件编辑器中的全局筛选器。 在下面的屏幕截图中， `CONSENT_VALUE_FILTER` 在SQL中用作全局筛选器的查询参数。 请参阅 [全局过滤器文档](./filters/global-filter.md#enable-global-filter) 以了解有关如何执行此操作的更多信息。

要执行查询，请选择运行图标(![运行图标。](../../images/customizable-insights/run-icon.png))。查询编辑器将显示结果选项卡。 接下来，要确认您的配置并打开构件编辑器，请选择 **[!UICONTROL 选择]**.

>[!TIP]
>
>如果查询使用查询参数，请运行一次查询以预填充所有使用的查询参数键。 查询将失败，但UI会自动显示“查询参数”选项卡并列出所有包含的键值。 为键添加适当的值。

![此 [!UICONTROL 输入SQL] 对话框，其中显示SQL输入、结果选项卡和突出显示的选择。](../../images/customizable-insights/enter-sql-select.png)

## 填充构件 {#populate-widget}

构件编辑器现在使用已执行SQL中的列进行填充。 仪表板的类型显示在左上方，在本例中为 [!UICONTROL 手动SQL输入]. 选择铅笔图标(![铅笔图标。](../../images/customizable-insights/edit-icon.png))，以随时编辑SQL。

>[!TIP]
>
>可用属性是从执行的SQL中获取的列。

要创建构件，请使用 [!UICONTROL 属性] 列。 您可以使用搜索栏查找属性或滚动列表。

![突出显示创建方法和属性列的构件编辑器。](../../images/customizable-insights/creation-method-and-attribute-column.png)

### 添加属性 {#add-attributes}

要向小组件添加属性，请选择加号图标(![加号图标。](../../images/customizable-insights/add-icon.png))。 显示的下拉菜单允许您根据SQL确定的选项向图表添加属性。 不同的图表类型具有不同的选项，例如X轴和Y轴下拉列表。

在此圆环图示例中，选项包括大小和颜色。 颜色划分圆环图结果，大小是实际使用的量度。 将属性添加到 [!UICONTROL 颜色] 字段，用于根据结果的组成将结果拆分为不同的颜色。

>[!TIP]
>
>选择向上和向下箭头图标(![向上箭头和向下箭头图标。](../../images/customizable-insights/switch-axis-icon.png))，以切换条形图或折线图上X轴和Y轴的排列。

![带有添加图标下拉菜单和开关箭头的小组件编辑器会突出显示。](../../images/customizable-insights/add-icon-and-switch-arrows.png)

要更改小组件的图形或图表类型，请从 [!UICONTROL 标记] 下拉菜单。 选项包括 [!UICONTROL 折线图]， [!UICONTROL 圆环图]， [!UICONTROL 大数字]、和 [!UICONTROL 条形图]. 选中后，将生成构件当前设置的预览可视化图表。

![突出显示具有构件预览的构件编辑器。](../../images/customizable-insights/widget-preview.png)

## 构件属性 {#properties}

选择属性图标(![属性图标。](../../images/customizable-insights/properties-icon.png))以打开属性面板。 在 [!UICONTROL 属性] 面板中，为小组件输入名称 **[!UICONTROL 构件标题]** 文本字段。 您还可以重命名图表的各个方面。

>[!NOTE]
>
>属性侧边栏中可用的特定字段因您编辑的图表类型而异。

![突出显示属性图标和小组件标题字段的小组件编辑器。](../../images/customizable-insights/widget-properties-title-text.png)

## 保存您的构件 {#save-widget}

在小组件编辑器中保存会将小组件本地保存到您的仪表板。 如果要保存工作并稍后继续，请选择 **[!UICONTROL 保存]**. 构件名称下方的勾号图标表示构件已保存。 或者，如果对小组件满意，请选择 **[!UICONTROL 保存并关闭]** 使该小组件可供对您的仪表板具有访问权限的所有其他用户使用。 选择“取消”以放弃您的工作并返回您的自定义仪表板。

![包含保存、保存和关闭的构件编辑器突出显示。](../../images/customizable-insights/insight-saved.png)

## 编辑仪表板和图表 {#edit}

选择 **[!UICONTROL 编辑]** 以编辑您的整个仪表板或任何见解。 在编辑模式下，您可以调整小部件大小、编辑SQL或创建并应用全局和临时过滤器。 这些过滤器会限制仪表板小组件中显示的数据。 它是一种针对不同用例快速更新和微调见解的便捷方法。

![突出显示“编辑”的自定义功能板。](../../images/customizable-insights/edit-dashboard.png)

选择 **[!UICONTROL 添加筛选器]** 创建 [[!UICONTROL 日期过滤器]](#create-date-filter) 或 [[!UICONTROL 全局筛选器]](#create-global-filter). 创建后，所有全局和日期筛选器都可从以下位置获得： [过滤器图标](#select-global-filter) (![过滤器图标。](../../images/customizable-insights/filter.png))。

![突出显示添加过滤器下拉菜单的自定义仪表板。](../../images/customizable-insights/add-filter.png)

## 编辑、复制或删除分析

有关如何执行操作的说明，请参阅自定义功能板指南 [编辑、复制或删除现有构件](../../user-defined-dashboards.md#duplicate).

## 后续步骤

阅读本文档后，您现在知道如何在Adobe Experience Platform UI中编写SQL查询来生成自定义仪表板的图表。 接下来，您应该学习如何通过以下方式进一步扩充您的数据 [创建日期过滤器](./filters/date-filter.md)，或 [创建全局过滤器](./filters/global-filter.md).

您还可以详细了解其他自定义分析功能，包括 [SQL分析数据的不同查看选项](./view-more.md) 或如何 [查看自定义分析背后的SQL](./view-sql.md).
