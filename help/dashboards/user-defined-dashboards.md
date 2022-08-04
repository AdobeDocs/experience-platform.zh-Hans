---
title: 用户定义的功能板
description: 了解如何构建和管理自定义功能板，您可以在其中创建、添加和编辑定制小组件以可视化关键量度。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: bf2b35e3366c71c51c58b6257cc55f7c9b0cd9c7
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 用户定义的功能板（测试版）

>[!IMPORTANT]
>
>用户定义的功能板功能处于测试阶段。 其功能和文档可能会发生更改。

Adobe Experience Platform功能板可帮助您通过用户定义的功能板功能加快分析和自定义可视化。 此功能允许您构建和管理自定义功能板，您可以在其中创建、添加和编辑定制小组件，以可视化与您的组织相关的关键量度。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 创建自定义功能板

要创建自定义功能板，请首先导航到功能板库存。 选择 **[!UICONTROL 功能板]** 从Platform UI的左侧导航开始，然后 **[!UICONTROL 创建功能板]**.

![左侧导航中包含功能板的功能板清单和“创建功能板”突出显示。](./images/user-defined-dashboards/create-dashboard.png)

添加自定义功能板之前，功能板库存为空，并显示“未找到功能板”。 消息。 创建后，所有用户定义的功能板都会列在功能板清单中。

的 [!UICONTROL 创建功能板] 对话框。 为要创建的小组件集合输入人类友好的描述性名称，然后选择 **[!UICONTROL 保存]**.

![创建功能板对话框。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新创建的空白功能板将随您选择的名称一起显示在视图的左上角。

## 创建小组件

从新功能板视图中，选择 **[!UICONTROL 添加新小组件]** 以开始小组件创建过程。

![突出显示了“添加新小组件”的新空仪表板。](./images/user-defined-dashboards/add-new-widget.png)

### 小组件编辑器

将显示小组件编辑器工作区。 接下来，选择 **[!UICONTROL 选择数据]** ，以选择向小组件添加属性的数据模型。

![小组件编辑器工作区。](./images/user-defined-dashboards/widget-composer.png)

的 [!UICONTROL 选择数据] 对话框。 从左列中选择一个数据模型，以显示所有可用表的预览列表。

>[!NOTE]
>
>用户定义的功能板当前仅支持配置文件数据模型。 将支持更多选项。

![选择数据对话框。](./images/user-defined-dashboards/select-data-dialog.png)

预览列表提供有关数据模型中包含的表的详细信息。 下表提供了列字段及其潜在值的描述。

| 列字段 | 描述 |
|---|---|
| [!UICONTROL 标题] | 表的名称。 |
| [!UICONTROL 表类型] | 表的类型。 潜在类型包括： `fact`, `dimension`和 `none`. |
| [!UICONTROL 查找] | 连接到所选表的表数。 |

选择 **[!UICONTROL 下一个]** 以确认您选择的数据模型。 下一个视图在左边栏中显示可用表格的列表。 选择一个表格，可查看所选表格中所包含数据的全面划分。

的 [!UICONTROL 预览] 面板包含选项卡 [!UICONTROL 示例记录] 和 [!UICONTROL 属性]. 的 [!UICONTROL 示例记录] 选项卡在列表视图中提供来自所选表的记录子集。 的 [!UICONTROL 属性] 选项卡为与选定表关联的每个属性提供属性名称、数据类型和源表。

从左边栏的列表中选择一个表格，为小组件提供数据，然后选择 **[!UICONTROL 选择]** 返回小组件编辑器。

![选择数据对话框，其中选择高亮显示。](./images/user-defined-dashboards/select-a-table.png)

小组件编辑器现在填充了所选表格中的数据。

数据模型和当前选定的表将显示在左边栏的顶部，可用于创建小组件的属性列在“属性”列中。

![在小组件编辑器中填充了数据的小组件。](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>您可以通过选择铅笔图标(![铅笔图标。](./images/user-defined-dashboards/edit-icon.png))。

选择添加图标(./images/user-defined-dashboards/add-icon.png)来向X轴或Y轴添加属性。

![小组件编辑器中突出显示了添加图标下拉菜单，可将属性添加到小组件轴。](./images/user-defined-dashboards/attributes-dropdown.png)

接下来，从 [!UICONTROL 标记] 用于生成小组件当前设置的预览可视化图表的下拉菜单。 在 [!UICONTROL 属性] 在屏幕右侧的边栏中，输入小组件的名称(位于 [!UICONTROL 小组件标题] 文本。

![小组件编辑器中突出显示了“标记”下拉列表和“小组件标题”文本字段。](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

当您对小组件选择满意时 **[!UICONTROL 保存]**. 小组件名称下方的勾号图标表示小组件已保存。

>[!NOTE]
>
>在小组件编辑器中保存，会将小组件保存在本地到功能板。 如果您在退出功能板编辑器时未保存功能板，则小组件将不会保存到功能板。

![新小组件保存确认。](./images/user-defined-dashboards/save-confirmation.png)

选择 **[!UICONTROL 取消]** 以返回到自定义功能板。

![使用创建的示例小组件的小组件编辑器。](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>选择功能板名称旁边的设置图标，可查看有关其创建的详细信息。 您可以在显示的对话框中更改功能板的名称。

在此工作区中，可以重新排列小组件并调整其大小。 选择 **[!UICONTROL 保存]** 以保留功能板名称和配置的布局。

![带有自定义小组件的用户定义功能板和突出显示的保存按钮。](./images/user-defined-dashboards/user-defined-dashboard.png)

## 后续步骤

通过阅读本文档，您可以更好地了解如何创建自定义功能板，以及如何为该功能板创建、编辑和更新自定义小组件。

要了解 [用户档案](./guides/profiles.md#standard-widgets), [区段](./guides/segments.md#standard-widgets)和 [目标](./guides/destinations.md#standard-widgets) 功能板中，请参阅相应文档中的标准小组件列表。
