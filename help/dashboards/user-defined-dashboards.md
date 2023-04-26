---
title: 用户定义的功能板
description: 了解如何构建和管理自定义功能板，您可以在其中创建、添加和编辑定制小组件以可视化关键量度。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 8507ecceca47fac3d321b89e4fed018ee9784777
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 3%

---

# 用户定义的功能板

Adobe Experience Platform功能板可帮助您通过用户定义的功能板功能加快分析和自定义可视化。 此功能允许您构建和管理自定义功能板，您可以在其中创建、添加和编辑定制小组件，以可视化与您的组织相关的关键量度。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 创建自定义功能板

要创建自定义功能板，请首先导航到功能板库存。 选择 **[!UICONTROL 功能板]** 从Platform UI的左侧导航开始，然后 **[!UICONTROL 创建功能板]**.

![左侧导航中包含功能板的功能板清单和“创建功能板”突出显示。](./images/user-defined-dashboards/create-dashboard.png)

添加自定义功能板之前，功能板库存为空，并显示“未找到功能板”。 消息。 创建后，所有用户定义的功能板都会列在功能板清单中。

>[!NOTE]
>
>要编辑现有功能板，请从清单列表中选择功能板名称，然后单击铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))

的 [!UICONTROL 创建功能板] 对话框。 为要创建的小组件集合输入人类友好的描述性名称，然后选择 **[!UICONTROL 保存]**.

![创建功能板对话框。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新创建的空白功能板将随您选择的名称一起显示在视图的左上角。

## 创建小组件 {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="最大构件数"
>abstract="用户定义的仪表板支持最多 10 个构件。将 10 个构件添加到仪表板后，[!UICONTROL 添加新构件]选项将被禁用并显示为灰色。"

从新功能板视图中，选择 **[!UICONTROL 添加新小组件]** 以开始小组件创建过程。

>[!IMPORTANT]
>
>用户定义的仪表板支持最多 10 个构件。将 10 个构件添加到仪表板后，[!UICONTROL 添加新构件]选项将被禁用并显示为灰色。

![突出显示了“添加新小组件”的新空仪表板。](./images/user-defined-dashboards/add-new-widget.png)

### 小组件编辑器

将显示小组件编辑器工作区。 接下来，选择 **[!UICONTROL 选择数据]** ，以选择向小组件添加属性的数据模型。

![小组件编辑器工作区。](./images/user-defined-dashboards/widget-composer.png)

#### 选择数据模型 {#select-data-model}

的 [!UICONTROL 选择数据模型] 对话框。 从左列中选择一个数据模型，以显示所有可用表的预览列表。 预配置的Real-time Customer Data Platform数据模型名为 [!UICONTROL CDPInsights].

>[!TIP]
>
>选择信息图标(![信息图标。](./images/user-defined-dashboards/info-icon.png))，以查看完整的数据模型名称（如果该名称在数据边栏中显示时过长）。

![选择数据对话框。](./images/user-defined-dashboards/select-data-model-dialog.png)

预览列表提供有关数据模型中包含的表的详细信息。 下表提供了列字段及其潜在值的描述。

| 列字段 | 描述 |
|---|---|
| [!UICONTROL 标题] | 表的名称。 |
| [!UICONTROL 表类型] | 表的类型。 潜在类型包括： `fact`, `dimension`和 `none`. |
| [!UICONTROL 记录] | 与所选表关联的记录数。 |
| [!UICONTROL 查找] | 连接到所选表的表数。 |
| [!UICONTROL 属性] | 所选表的属性数。 |

选择 **[!UICONTROL 下一个]** 以确认您选择的数据模型。 下一个视图在左边栏中显示可用表格的列表。 选择一个表格，可查看所选表格中所包含数据的全面划分。

### 填充小组件 {#populate-widget}

的 [!UICONTROL 预览] 面板包含选项卡 [!UICONTROL 示例记录] 和 [!UICONTROL 属性]. 的 [!UICONTROL 示例记录] 选项卡在列表视图中提供来自所选表的记录子集。 的 [!UICONTROL 属性] 选项卡为与选定表关联的每个属性提供属性名称、数据类型和源表。

从左边栏的列表中选择一个表格，为小组件提供数据，然后选择 **[!UICONTROL 选择]** 返回小组件编辑器。

![选择数据对话框，其中选择高亮显示。](./images/user-defined-dashboards/select-a-table.png)

小组件编辑器现在填充了所选表格中的数据。

数据模型和当前选定的表将显示在左边栏的顶部，可用于创建小组件的属性列在 [!UICONTROL 属性] 列。 您可以使用搜索栏来查找属性，而不是滚动列表，或通过选择铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))。

![在小组件编辑器中填充了数据的小组件。](./images/user-defined-dashboards/populated-widget-composer.png)

#### 添加和过滤属性 {#add-and-filter-attributes}

选择添加图标(![添加图标。](./images/user-defined-dashboards/add-icon.png))以向小组件添加属性。 显示的下拉菜单允许您为小组件添加X轴、Y轴、颜色或滤镜属性。 的 [!UICONTROL 颜色] 属性允许您根据颜色区分X轴和Y轴标记的结果。 为此，会根据结果对第三个属性的构成，将结果拆分为不同的颜色。

>[!TIP]
>
>如果要反转X轴和Y轴的排列，请选择向上和向下箭头图标(![向上和向下箭头图标。](./images/user-defined-dashboards/switch-axis-icon.png))来切换其安排。

![小组件编辑器中突出显示了添加图标下拉菜单。](./images/user-defined-dashboards/attributes-dropdown.png)

要更改小组件的图形或图表类型，请选择 [!UICONTROL 标记] 下拉列表，然后从可用选项中进行选择。 选项包括条、点、刻度、线或区域。 选择后，将生成小组件当前设置的预览可视化。

![突出显示标记下拉菜单的小组件编辑器。](./images/user-defined-dashboards/marks-dropdown.png)

通过添加属性作为过滤器，您可以选择要包含或排除的小组件值。 从属性列表添加过滤器后， [!UICONTROL 过滤器] 将显示对话框，您可以在其中使用其复选框选择或取消选择值。

![用于从小组件中筛选值的筛选器对话框。](./images/user-defined-dashboards/filter-dialog.png)

#### 过滤历史数据 {#filter-historical-data}

要从小组件生成的分析中过滤掉历史数据，请添加 `date_key` 属性，然后选择 **[!UICONTROL 最近日期]** 后跟 **[!UICONTROL 应用]**. 此过滤器可确保用于获取分析的数据是从最新的系统快照中获取的。

![的 [!UICONTROL 过滤器：date_key] 对话框 [!UICONTROL 最近日期] 和 [!UICONTROL 应用] 突出显示。](./images/user-defined-dashboards/recent-date.png)

或者，您也可以创建一个自定义句点，以按过滤数据。 选择 **[!UICONTROL 选择日期]** 以使用可用日期列表扩展对话框。 使用 **[!UICONTROL 全选]** 复选框可启用或禁用所有可用选项，或单独选中每天的复选框。 最后，选择 **[!UICONTROL 应用]** 以确认您的选择。

>[!NOTE]
>
>如果 `date_key` 属性已添加为过滤器，请选择省略号后跟 **[!UICONTROL 编辑]** 从下拉选项更改过滤器时段。

![的 [!UICONTROL 过滤器：date_key] 复选框且选中或取消选中单日复选框。](./images/user-defined-dashboards/select-dates.png)

### 小组件属性

选择属性图标(![属性图标。](./images/user-defined-dashboards/properties-icon.png))以打开“属性”面板。 在 [!UICONTROL 属性] 面板中，在 [!UICONTROL 小组件标题] 文本。

![属性面板中突出显示了属性图标和小组件标题字段。](./images/user-defined-dashboards/properties-panel.png)

从小组件属性面板中，您可以编辑小组件的多个方面。 您可以完全控制以编辑小组件图例的位置。 要移动图例，请选择 [!UICONTROL 图例放置] 下拉菜单，然后从可用选项列表中选择所需的位置。 您还可以通过在 [!UICONTROL 图例标题] 文本字段，或 [!UICONTROL 轴标签] 文本。

#### 保存小组件 {#save-widget}

在小组件编辑器中保存，会将小组件保存在本地到功能板。 如果希望保存您的工作并稍后恢复，请选择 **[!UICONTROL 保存]**. 小组件名称下方的勾号图标表示小组件已保存。 或者，如果您对小组件满意，请选择 **[!UICONTROL 保存并关闭]** 以使该小组件可供所有其他用户访问您的功能板。 选择 **[!UICONTROL 取消]** 以放弃您的工作并返回到自定义仪表板。

![新小组件保存确认。](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>选择属性图标(![属性图标。](./images/user-defined-dashboards/properties-icon.png))以查看有关其创建的详细信息。 您可以在显示的对话框中更改功能板的名称。

在此工作区中，可以重新排列小组件并调整其大小。 选择 **[!UICONTROL 保存]** 以保留功能板名称和配置的布局。

![带有自定义小组件的用户定义功能板和突出显示的保存按钮。](./images/user-defined-dashboards/user-defined-dashboard.png)

为确保Adobe Real-time Customer Data Platform分析功能板的每个查询都拥有足够的资源来高效执行，API通过为每个查询分配并发插槽来跟踪资源使用情况。 系统最多可以处理四个并发查询，因此在任何给定时间都有四个并发查询槽。 查询将基于并发插槽放入队列中，然后在队列中等待足够的并发插槽可用。

### 复制小组件

创建小组件后，您可以复制整个小组件并自定义其属性，以创建独特的小组件，而无需从头开始。 要复制小组件，请首先导航到功能板库存。 然后，从库存列表中选择功能板名称。 此时会显示您的自定义功能板。

![突出显示功能板和自定义功能板名称的平台UI。](./images/user-defined-dashboards/dashbaord-inventory.png)

选择铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))以进入编辑模式。

![突出显示了铅笔图标的自定义仪表板。](./images/user-defined-dashboards/edit-mode.png)

接下来，选择要复制的小组件右上角的省略号，然后 **[!UICONTROL 复制]** 列表。

![用户定义的功能板中的小组件，并突出显示省略号和复制小组件。](./images/user-defined-dashboards/duplicate.png)

在用户定义的功能板中会显示一个重复的小组件。 选择新小组件的省略号，然后 **[!UICONTROL 编辑]**，以自定义新小组件。

## 后续步骤和其他资源

通过阅读本文档，您可以更好地了解如何创建自定义功能板，以及如何为该功能板创建、编辑和更新自定义小组件。

要了解 [用户档案](./guides/profiles.md#standard-widgets), [区段](./guides/segments.md#standard-widgets)和 [目标](./guides/destinations.md#standard-widgets) 功能板中，请参阅相应文档中的标准小组件列表。

要加深您对Experience Platform中用户定义的功能板的了解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
