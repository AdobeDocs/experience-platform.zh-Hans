---
title: 标准仪表板
description: 了解如何构建和管理自定义仪表板，以便在其中创建、添加和编辑定制构件以可视化关键量度。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 3%

---

# 标准仪表板

使用Adobe Experience Platform功能板，可通过功能板加速分析并自定义可视化图表。 使用此功能可构建和管理自定义仪表板，您可以在其中创建、添加和编辑定制构件，以可视化与您的组织相关的关键量度。


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 创建自定义仪表板

要创建自定义功能板，请先导航到功能板清单。 从Experience Platform UI的左侧导航中选择&#x200B;**[!UICONTROL 仪表板]**，然后选择&#x200B;**[!UICONTROL 创建仪表板]**。

![左侧导航中包含功能板的功能板清单和“创建功能板”突出显示。](./images/standard-dashboards/create-dashboard.png)

在添加自定义功能板之前，功能板清单为空，并显示“未找到功能板”。 消息。 创建后，您的所有功能板都会在功能板清单中列出。

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](/help/images/icons/edit.png))
>![A custom inventory listed in the dashboard inventory.](./images/standard-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

出现[!UICONTROL 创建仪表板]对话框。 为要创建的构件集合输入一个人性化的描述性名称，然后选择&#x200B;**[!UICONTROL 保存]**。

![创建仪表板对话框。](./images/standard-dashboards/create-dashboard-dialog.png)

购买了Data Distiller SKU的用户可以选择使用自定义SQL查询创建其见解。 有关此工作流的说明，请参阅[查询专业模式概述](./sql-insights-query-pro-mode/overview.md)。

新创建的空白仪表板会在视图的左上角显示您选择的名称。

## 创建小组件 {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="最大小组件数"
>abstract="仪表板服务最多支持十个小组件。将 10 个小组件添加到仪表板后，[!UICONTROL 添加新小组件]选项将被禁用并显示为灰色。"

从新仪表板视图中，选择&#x200B;**[!UICONTROL 添加新构件]**&#x200B;以开始构件创建过程。

>[!IMPORTANT]
>
>每个仪表板最多支持10个小组件。 将 10 个小组件添加到仪表板后，[!UICONTROL 添加新小组件]选项将被禁用并显示为灰色。

![突出显示带有添加新小部件的新空仪表板。](./images/standard-dashboards/add-new-widget.png)

### 构件编辑器

此时将显示构件编辑器工作区。 接下来，选择&#x200B;**[!UICONTROL 选择数据]**&#x200B;以选择要向小部件添加属性的数据模型。

![构件编辑器工作区。](./images/standard-dashboards/widget-composer.png)

#### 选择数据模型 {#select-data-model}

出现[!UICONTROL 选择数据模型]对话框。 从左列中选择一个数据模型，以显示所有可用表的预览列表。 Real-Time Customer Data Platform的预配置数据模型名为[!UICONTROL CDPInsights]。

>[!TIP]
>
>选择信息图标(![信息图标。](/help/images/icons/info.png))以查看完整的数据模型名称（如果它太长而无法显示在数据边栏中）。

![选择数据对话框。](./images/standard-dashboards/select-data-model-dialog.png)

预览列表提供有关数据模型中所包含表的详细信息。 下表提供了有关列字段及其潜在值的说明。

| 列字段 | 描述 |
|---|---|
| [!UICONTROL 标题] | 表的名称。 |
| [!UICONTROL 表类型] | 表的类型。 潜在类型包括： `fact`、`dimension`和`none`。 |
| [!UICONTROL 记录] | 与所选表关联的记录数。 |
| [!UICONTROL 查找] | 连接到所选表的表数。 |
| [!UICONTROL 属性] | 所选表的属性数。 |

选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以确认您选择的数据模型。 下一个视图在左边栏中显示可用表的列表。 选择一个表以查看选定表中包含的数据的全面划分。

### 填充构件 {#populate-widget}

[!UICONTROL 预览]面板包含[!UICONTROL 样本记录]和[!UICONTROL 属性]的选项卡。 [!UICONTROL 示例记录]选项卡在表格视图中提供了所选表中记录的子集。 [!UICONTROL 属性]选项卡为与选定表关联的每个属性提供属性名称、数据类型和源表。

从左边栏中可用的列表中选择一个表，以便为您的小组件提供数据，然后选择&#x200B;**[!UICONTROL 选择]**&#x200B;以返回到小组件编辑器。

![突出显示了select的“选择数据”对话框。](./images/standard-dashboards/select-a-table.png)

构件编辑器现在填充了来自所选表的数据。

数据模型和当前选定的表显示在左边栏顶部，可用于创建小组件的属性列在[!UICONTROL 属性]列中。 您可以使用搜索栏查找属性，而不是滚动列表，或通过选择铅笔图标（![铅笔图标）来更改所选的数据模型。](/help/images/icons/edit.png))。

![小组件编辑器中填充了数据。](./images/standard-dashboards/populated-widget-composer.png)

#### 添加和筛选属性 {#add-and-filter-attributes}

选择添加图标（![添加图标）。](/help/images/icons/add-circle.png))以向小部件中添加属性。 显示的下拉菜单允许您添加属性作为X轴、Y轴、颜色或小部件的过滤器。 [!UICONTROL Color]属性允许您根据颜色区分X轴和Y轴标记的结果。 它通过根据第三属性的组成将结果分割为不同的颜色来实现这一点。

>[!TIP]
>
>如果要翻转X轴和Y轴的排列，请选择向上和向下箭头图标（![向上和向下箭头图标）。](/help/images/icons/switch.png))以切换其排列方式。

![带有高亮显示添加图标下拉菜单的小组件编辑器。](./images/standard-dashboards/attributes-dropdown.png)

要更改小组件的图形或图表类型，请选择[!UICONTROL 标记]下拉菜单并从可用选项中进行选择。 选项包括条形、点、刻度、线条或区域。 选中后，将生成构件当前设置的预览可视化图表。

![突出显示带有标记下拉菜单的小组件编辑器。](./images/standard-dashboards/marks-dropdown.png)

通过将属性添加为过滤器，您可以选择要从小部件中包括或排除哪些值。 从属性列表中添加筛选器后，将显示[!UICONTROL 筛选器]对话框，您可以在其中使用值的复选框选择或取消选择值。

![用于从小部件中筛选值的筛选器对话框。](./images/standard-dashboards/filter-dialog.png)

#### 过滤掉历史数据 {#filter-historical-data}

若要从构件生成的分析中过滤掉历史数据，请添加`date_key`属性作为过滤器，然后依次选择&#x200B;**[!UICONTROL 最近日期]**&#x200B;和&#x200B;**[!UICONTROL 应用]**。 此过滤器可确保从最近的系统快照获取用于获取见解的数据。

![带有[!UICONTROL 最近日期]和[!UICONTROL 应用]的[!UICONTROL 筛选器： date_key]对话框突出显示。](./images/standard-dashboards/recent-date.png)

或者，您可以创建一个自定义时间段，以按筛选数据。 选择&#x200B;**[!UICONTROL 选择日期]**&#x200B;以使用可用日期列表扩展对话框。 使用&#x200B;**[!UICONTROL 全选]**&#x200B;复选框启用或禁用所有可用选项，或单独选中每天的复选框。 最后，选择&#x200B;**[!UICONTROL 应用]**&#x200B;以确认您的选择。

>[!NOTE]
>
>如果已将`date_key`属性添加为筛选器，请从下拉选项中选择省略号后跟&#x200B;**[!UICONTROL 编辑]**&#x200B;以更改筛选器时段。

![带有单独日期复选框的[!UICONTROL 筛选器： date_key]对话框已选中和取消选中。](./images/standard-dashboards/select-dates.png)

### 小组件属性

选择属性图标(![属性图标。](/help/images/icons/properties.png))以打开属性面板。 在[!UICONTROL 属性]面板的[!UICONTROL 构件标题]文本字段中输入构件的名称。

![属性面板中突出显示了属性图标和小组件标题字段。](./images/standard-dashboards/properties-panel.png)

从构件属性面板，可以编辑构件的多个方面。 您可以完全控制以编辑构件图例的位置。 要移动图例，请选择[!UICONTROL 图例位置]下拉列表，然后从可用选项列表中选择所需的位置。 您还可以通过在[!UICONTROL 图例标题]文本字段或[!UICONTROL 轴标签]文本字段中分别输入新名称来重命名与图例以及X轴或Y轴关联的标签。

#### 保存您的构件 {#save-widget}

在小组件编辑器中保存会将小组件本地保存到您的仪表板。 如果您希望保存工作并在以后继续，请选择&#x200B;**[!UICONTROL 保存]**。 构件名称下方的勾号图标表示构件已保存。 或者，如果对您的小组件感到满意，请选择&#x200B;**[!UICONTROL 保存并关闭]**，以便其他所有有权访问您仪表板的用户都可以使用该小组件。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以放弃您的工作并返回您的自定义仪表板。

![新构件保存确认。](./images/standard-dashboards/save-confirmation.png)

>[!TIP]
>
>选择属性图标(![属性图标。](/help/images/icons/properties.png))，查看有关其创建的详细信息。 您可以在显示的对话框中更改仪表板的名称。

在此工作区中时，可以重新排列构件并调整其大小。 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保留您的仪表板名称和配置的布局。

![带有自定义小部件和突出显示“保存”按钮的用户定义仪表板。](./images/standard-dashboards/user-defined-dashboard.png)

为了确保Adobe Real-Time Customer Data Platform分析功能板的每个查询都有足够的资源来高效执行，API会通过为每个查询分配并发插槽来跟踪资源使用情况。 系统最多可以处理4个并发查询，因此可以在任意给定时间使用4个并发查询插槽。 查询基于并发插槽放入队列中，然后在队列中等待，直到有足够的并发插槽可用。

### 编辑、复制或删除构件 {#duplicate}

创建构件后，您可以从自定义仪表板中编辑、复制或删除整个构件。

>[!TIP]
>
>要在任何现有的自定义功能板之间切换，请在左侧导航栏中选择“功能板” ，然后从清单列表中选择该功能板名称。

选择铅笔图标(![A铅笔图标。](/help/images/icons/edit.png))以进入编辑模式。

![突出显示铅笔图标的自定义仪表板。](./images/standard-dashboards/edit-mode.png)

接下来，选择要编辑、复制或删除的构件右上角的省略号。 从下拉菜单中选择相应的操作。

![自定义仪表板中突出显示有椭圆和重复小部件的小组件。](./images/standard-dashboards/duplicate.png)

>[!NOTE]
>
>利用复制功能，您可以自定义洞察的属性以创建唯一的构件，而无需从头开始。 如果复制构件，该构件会显示在您的自定义仪表板中。 然后，可选择新小部件的省略号，随后可选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以自定义您的见解。

## 后续步骤和其他资源

通过阅读本文档，您可以更好地了解如何创建自定义仪表板，以及如何为该仪表板创建、编辑和更新自定义构件。

要发现[配置文件](./guides/profiles.md#standard-widgets)、[区段](./guides/audiences.md#standard-widgets)和[目标](./guides/destinations.md#standard-widgets)功能板的可用预配置量度和可视化图表，请参阅其各自文档中的标准构件列表。

要加深您对Experience Platform中的功能板的了解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/3413779?quality=12&learn=on&captions=chi_hans)
