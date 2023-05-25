---
title: 用户定义的功能板
description: 了解如何构建和管理自定义仪表板，以便在其中创建、添加和编辑定制构件以可视化关键量度。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 8507ecceca47fac3d321b89e4fed018ee9784777
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 3%

---

# 用户定义的仪表板

Adobe Experience Platform功能板可帮助您通过用户定义的功能加快洞察并自定义可视化图表。 此功能允许您构建和管理自定义仪表板，您可以在其中创建、添加和编辑定制小组件，以可视化与您的组织相关的关键量度。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 创建自定义仪表板

要创建自定义功能板，请首先导航到功能板清单。 选择 **[!UICONTROL 仪表板]** 从Platform UI的左侧导航栏中，其后是 **[!UICONTROL 创建功能板]**.

![左侧导航中带有功能板的功能板清单和“创建功能板”突出显示。](./images/user-defined-dashboards/create-dashboard.png)

在添加自定义功能板之前，功能板清单为空并显示“未找到功能板”。 消息。 创建后，您的所有用户定义的功能板都会在功能板清单中列出。

>[!NOTE]
>
>要编辑现有功能板，请从库存列表中选择功能板名称，后跟铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))

此 [!UICONTROL 创建功能板] 对话框。 为要创建的构件集合输入便于用户使用的描述性名称，然后选择 **[!UICONTROL 保存]**.

![创建功能板对话框。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新创建的空白仪表板将出现在视图的左上角，其中包含您选择的名称。

## 创建构件 {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="最大构件数"
>abstract="用户定义的仪表板支持最多 10 个构件。将 10 个构件添加到仪表板后，[!UICONTROL 添加新构件]选项将被禁用并显示为灰色。"

从新功能板视图中，选择 **[!UICONTROL 添加新构件]** 以开始构件创建过程。

>[!IMPORTANT]
>
>用户定义的仪表板支持最多 10 个构件。将 10 个构件添加到仪表板后，[!UICONTROL 添加新构件]选项将被禁用并显示为灰色。

![突出显示具有添加新小部件的新空仪表板。](./images/user-defined-dashboards/add-new-widget.png)

### 构件编辑器

此时将显示构件编辑器工作区。 接下来，选择 **[!UICONTROL 选择数据]** 以选择要从中向小部件添加属性的数据模型。

![构件编辑器工作区。](./images/user-defined-dashboards/widget-composer.png)

#### 选择数据模型 {#select-data-model}

此 [!UICONTROL 选择数据模型] 对话框。 从左列中选择一个数据模型，以显示所有可用表的预览列表。 Real-time Customer Data Platform的预配置数据模型已命名为 [!UICONTROL CDPInsights].

>[!TIP]
>
>选择信息图标(![信息图标。](./images/user-defined-dashboards/info-icon.png))，以查看完整的数据模型名称（如果它太长而无法显示在数据边栏中）。

![选择数据对话框。](./images/user-defined-dashboards/select-data-model-dialog.png)

预览列表提供有关数据模型中所包含表的详细信息。 下表提供了列字段及其潜在值的说明。

| 列字段 | 描述 |
|---|---|
| [!UICONTROL 标题] | 表的名称。 |
| [!UICONTROL 表类型] | 表的类型。 可能的类型包括： `fact`， `dimension`、和 `none`. |
| [!UICONTROL 记录] | 与所选表关联的记录数。 |
| [!UICONTROL 查找] | 连接到所选表的表数。 |
| [!UICONTROL 属性] | 所选表的属性数。 |

选择 **[!UICONTROL 下一个]** 以确认对数据模型的选择。 下一个视图在左边栏中显示可用表的列表。 选择一个表以查看选定表中包含的数据的完整划分。

### 填充构件 {#populate-widget}

此 [!UICONTROL 预览] 面板包含选项卡 [!UICONTROL 示例记录] 和 [!UICONTROL 属性]. 此 [!UICONTROL 示例记录] 选项卡在表格视图中提供所选表格中记录的子集。 此 [!UICONTROL 属性] 选项卡为与所选表关联的每个属性提供属性名称、数据类型和源表。

从左边栏中可用的列表中选择一个表，以便为小组件提供数据，然后选择 **[!UICONTROL 选择]** 以返回到构件编辑器。

![选择数据对话框，其中突出显示了select。](./images/user-defined-dashboards/select-a-table.png)

构件编辑器现在填充了来自所选表的数据。

数据模型和当前选定的表显示在左边栏的顶部，可用于创建小部件的属性列在 [!UICONTROL 属性] 列。 您可以使用搜索栏查找属性，而不是滚动列表，或通过选择铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))中。

![构件编辑器中填充了数据的构件。](./images/user-defined-dashboards/populated-widget-composer.png)

#### 添加和筛选属性 {#add-and-filter-attributes}

选择添加图标(![添加图标。](./images/user-defined-dashboards/add-icon.png))来将属性添加到小组件。 显示的下拉菜单允许您添加属性作为X轴、Y轴、颜色或小部件的过滤器。 此 [!UICONTROL 颜色] 属性允许您根据颜色区分X轴和Y轴标记的结果。 它通过根据第三属性的组成将结果分割为不同的颜色来完成此操作。

>[!TIP]
>
>如果要反转X轴和Y轴的排列，请选择向上和向下箭头图标(![向上箭头和向下箭头图标。](./images/user-defined-dashboards/switch-axis-icon.png))，以切换其排列方式。

![突出显示添加图标下拉菜单的小组件编辑器。](./images/user-defined-dashboards/attributes-dropdown.png)

要更改小组件的图形或图表类型，请选择 [!UICONTROL 标记] 下拉菜单并从可用选项中进行选择。 选项包括条形、点、刻度、线条或区域。 选择后，将生成构件当前设置的预览可视化图表。

![突出显示标记下拉列表的构件编辑器。](./images/user-defined-dashboards/marks-dropdown.png)

通过将属性添加为过滤器，可以选择要从小部件中包括或排除的值。 从属性列表中添加过滤器后， [!UICONTROL 筛选条件] 此时将显示一个对话框，您可以在其中使用复选框选择或取消选择值。

![用于筛选构件中的值的过滤器对话框。](./images/user-defined-dashboards/filter-dialog.png)

#### 筛选出历史数据 {#filter-historical-data}

要从构件生成的分析中过滤出历史数据，请添加 `date_key` 属性作为筛选条件并选择 **[!UICONTROL 最近日期]** 后接 **[!UICONTROL 应用]**. 此过滤器可确保用于获取见解的数据取自最近的系统快照。

![此 [!UICONTROL 筛选器：date_key] 对话框 [!UICONTROL 最近日期] 和 [!UICONTROL 应用] 突出显示。](./images/user-defined-dashboards/recent-date.png)

或者，您可以创建一个自定义时段，以按筛选数据。 选择 **[!UICONTROL 选择日期]** 使用可用日期列表来扩展对话框。 使用 **[!UICONTROL 全选]** 选中此复选框可启用或禁用所有可用选项，或者分别选中每天的复选框。 最后，选择 **[!UICONTROL 应用]** 以确认您的选择。

>[!NOTE]
>
>如果 `date_key` 属性已添加为过滤器，请选择省略号后跟 **[!UICONTROL 编辑]** 从下拉选项更改筛选期限。

![此 [!UICONTROL 筛选器：date_key] 对话框中的单个日期复选框均已选中和取消选中。](./images/user-defined-dashboards/select-dates.png)

### 构件属性

选择属性图标(![属性图标。](./images/user-defined-dashboards/properties-icon.png))以打开“属性”面板。 在 [!UICONTROL 属性] 面板中，为小组件输入名称 [!UICONTROL 构件标题] 文本字段。

![属性面板，其中属性图标和小组件标题字段突出显示。](./images/user-defined-dashboards/properties-panel.png)

在构件属性面板中，可以编辑构件的多个方面。 您拥有编辑构件图例位置的完全控制权。 要移动图例，请选择 [!UICONTROL 图例位置] 下拉列表，然后从可用选项列表中选择所需的位置。 您还可以通过输入新名称来重命名与图例关联的标签，以及X轴或Y轴 [!UICONTROL 图例标题] 文本字段，或 [!UICONTROL 轴标签] 文本字段。

#### 保存构件 {#save-widget}

在构件编辑器中保存会将构件本地保存到您的仪表板。 如果要保存工作并在以后恢复，请选择 **[!UICONTROL 保存]**. 构件名称下方的勾号图标表示构件已保存。 或者，如果满意您的小组件，请选择 **[!UICONTROL 保存并关闭]** 使该小组件可供具有您的仪表板访问权限的所有其他用户使用。 选择 **[!UICONTROL 取消]** 以放弃您的工作并返回到自定义仪表板。

![新构件保存确认。](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>选择属性图标(![属性图标。](./images/user-defined-dashboards/properties-icon.png))，查看有关其创建的详细信息。 您可以在出现的对话框中更改操控板的名称。

在此工作区中时，可以重新排列构件并调整其大小。 选择 **[!UICONTROL 保存]** 以保留您的功能板名称和配置的布局。

![带有自定义小部件的用户定义的仪表板，其保存按钮突出显示。](./images/user-defined-dashboards/user-defined-dashboard.png)

为了确保Adobe Real-time Customer Data Platform分析仪表板的每个查询都有足够的资源来高效执行，API通过为每个查询分配并发插槽来跟踪资源使用情况。 系统最多可以处理4个并发查询，因此可以在任意给定时间使用4个并发查询插槽。 根据并发插槽将查询放入队列中，然后在队列中等待，直到有足够的并发插槽可用。

### 复制构件

创建构件后，您可以复制整个构件并自定义其属性以创建唯一构件，而无需从头开始。 要复制构件，请首先导航到功能板库存。 然后，从库存列表中选择仪表板名称。 您的自定义仪表板随即出现。

![突出显示了包含功能板和自定义功能板名称的Platform UI。](./images/user-defined-dashboards/dashbaord-inventory.png)

选择铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))，以进入编辑模式。

![突出显示铅笔图标的自定义仪表板。](./images/user-defined-dashboards/edit-mode.png)

接下来，选择要复制的构件右上角的省略号，然后选择 **[!UICONTROL 复制]** 从可用选项列表中。

![用户定义的仪表板中的构件，其中突出显示了椭圆形和重复构件。](./images/user-defined-dashboards/duplicate.png)

您的用户定义的功能板中会显示一个重复构件。 选择新小部件的省略号，然后 **[!UICONTROL 编辑]**，以自定义您的新构件。

## 后续步骤和其他资源

通过阅读本文档，您可以更好地了解如何创建自定义功能板，以及如何为该功能板创建、编辑和更新自定义构件。

发现预配置的可用量度和可视化图表 [用户档案](./guides/profiles.md#standard-widgets)， [区段](./guides/segments.md#standard-widgets)、和 [目标](./guides/destinations.md#standard-widgets) 功能板，请参阅其各自文档中的标准构件列表。

要加深您对Experience Platform中用户定义的功能板的了解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
