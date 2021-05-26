---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用
title: 使用小组件库添加和创建功能板小组件
description: '本指南提供了有关添加标准小组件和创建自定义小组件以在Adobe Experience Platform中显示功能板数据的分步说明。 '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 63f855d7dd3c3591da76a23ca8d673477378c1c3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# 小组件库{#widget-library}

在Adobe Experience Platform用户界面中，您可以使用多个功能板查看组织的数据并与之交互。 您还可以通过向功能板视图添加新小组件来更新其中一些功能板。 除了由Adobe提供的标准小组件之外，您还可以创建自定义小组件并在整个组织内共享这些小组件。

本指南提供了添加标准小组件和创建自定义小组件的分步说明，这些小组件用于自定义在Platform UI的[!UICONTROL Profiles]、[!UICONTROL Segments]和[!UICONTROL Destinations]功能板中显示的信息。

有关如何修改[!UICONTROL Profiles]、[!UICONTROL 目标]和[!UICONTROL 区段]功能板中小组件的位置和大小的信息，请参阅[修改功能板指南](modify.md)。

>[!NOTE]
>
>无法自定义[!UICONTROL 许可证使用情况]功能板中显示的小组件。 要了解有关此唯一功能板的更多信息，请阅读[许可证使用功能板文档](guides/license-usage.md)。

## 访问小组件库

在任何功能板（例如，“配置文件”功能板）中，您可以选择&#x200B;**[!UICONTROL Modify功能板]**，后跟&#x200B;**[!UICONTROL Widget库]**&#x200B;以访问小组件库。

>[!NOTE]
>
>选择[!UICONTROL 修改功能板]后，才会显示[!UICONTROL 小组件库]按钮。

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

## 查看小组件库

[!UICONTROL 小组件库]包含两个选项卡，分别是[!UICONTROL Standard]和[!UICONTROL Custom]。

* **[!UICONTROL Standard]**&#x200B;选项卡包含由Adobe创建的小组件，允许您使用这些标准量度更新功能板。 要了解有关向功能板添加标准小组件的更多信息，请参阅本指南中的[标准小组件](#standard-widgets)部分。
* **[!UICONTROL Custom]**&#x200B;选项卡允许您在组织内创建和共享小组件。 有关创建您自己的小组件的完整步骤，请参阅本指南中的[自定义小组件](#custom-widgets)部分。

![](images/customization/widget-library.png)

## 标准小组件{#standard-widgets}

**[!UICONTROL 标准]**&#x200B;选项卡包含由Adobe创建的小组件，这些小组件根据可用的功能板划分为不同的类别。 所选类别与您从中进入小组件库的仪表板匹配。 换言之，如果您从[!UICONTROL Profiles]功能板中选择了小组件库，则会选择[!UICONTROL Profiles]类别，而其他类别则显示为灰显。

随即会显示选定类别的可用小组件。 每个小组件都显示为一张卡片，其中提供了量度的标题、描述和示例可视化图表。

>[!NOTE]
>
>小组件只能添加到与选定类别匹配的功能板中。 例如，只有[!UICONTROL Profiles]类别中的小组件才能添加到[!UICONTROL Profiles]功能板中。

![](images/customization/standard-widgets.png)

### 将标准小组件添加到功能板

要选择要添加到功能板的标准小组件，请突出显示该小组件，然后选中该小组件的复选框。 选择至少一个小组件后，**[!UICONTROL 添加小组件]**&#x200B;按钮会被点亮。

>[!NOTE]
>
>小组件库右上角的计数器显示所选小组件的总数。

选择&#x200B;**[!UICONTROL 添加小组件]**&#x200B;以将选定的小组件添加到功能板。

![](images/customization/add-widget.png)

## 自定义小组件{#custom-widgets}

要进一步自定义Experience Platform中功能板的外观，您可以创建小组件并将其与组织中的其他用户共享。

>[!IMPORTANT]
>
>贵组织在小组件库中最多可创建20个自定义小组件。

在小组件库中，选择&#x200B;**[!UICONTROL Custom]**&#x200B;选项卡，以开始创建自定义小组件或查看您的组织已创建的自定义小组件。

![](images/customization/custom-widgets.png)

### 编辑模式

要创建自定义小组件，必须识别实时客户资料属性，以确保数据包含在每日快照中。 如果贵组织未选择任何配置文件属性，则小组件库右上角会显示[!UICONTROL 配置架构]按钮。

至少选择一个自定义属性后，小组件库右上角会显示[!UICONTROL 编辑架构]按钮。 选择&#x200B;**[!UICONTROL 编辑架构]**&#x200B;以打开&#x200B;**[!UICONTROL 选择并集架构字段]**&#x200B;对话框，以查看所选属性并添加更多属性。

>[!IMPORTANT]
>
>组织最多可选择20个属性。

![](images/customization/edit-schema.png)

要选择属性，请导航到并集架构中的属性（或使用搜索），然后选中属性旁边的复选框。 选中此复选框还会将属性添加到对话框右侧的&#x200B;**[!UICONTROL 选定属性]**&#x200B;列表。

>[!NOTE]
>
>要使属性可见以供选择，该属性必须是以下属性之一：字符串、日期、日期时间、布尔值、短、长、整数或字节。 映射和双重数据类型不受支持，且呈灰显状态，因此无法选择它们。

选择要添加的属性后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存您的属性并返回到自定义小组件选项卡。

刷新数据时，新选择的属性会在每日快照之后可用。

![](images/customization/select-attribute.png)

### 创建自定义小组件

要创建自定义小组件，请从小组件库的中心选择&#x200B;**[!UICONTROL 创建]**，或者如果已创建自定义小组件，请从小组件库的右上角选择&#x200B;**[!UICONTROL 创建小组件]**。

![](images/customization/create-widget.png)

在&#x200B;**[!UICONTROL 创建小组件]**&#x200B;对话框中，您可以为新小组件提供标题和描述，并选择您希望小组件显示的属性。 要选择属性，请选择要添加属性旁边的单选按钮。

>[!NOTE]
>
>每个小组件只能选择一个属性。 此外，如果已为属性创建小组件，则该属性将呈灰显状态。

![](images/customization/create-widget-dialog.png)

对话框中会显示新小组件的预览，其中显示了包含模拟数据的水平条形图。

>[!NOTE]
>
>当前所有属性唯一支持的量度是配置文件计数，而当前唯一支持自定义小组件的可视化是水平条形图。
>
>示例小组件中显示的数据仅供说明之用。 预览不显示您组织的实际数据。

![](images/customization/create-widget-select-attribute.png)

要保存新小组件并返回到[!UICONTROL Custom]选项卡，请选择&#x200B;**[!UICONTROL Create]**。 现在，您可以通过从库中选择小组件并选择&#x200B;**[!UICONTROL 添加小组件]**，将新小组件添加到功能板。

### 存档自定义小组件

将小组件添加到库后，可以使用&#x200B;**[!UICONTROL Archive]**&#x200B;按钮将其存档。 您还可以编辑小组件以更新标题或描述字段。

## 后续步骤

阅读本文档后，您现在可以访问[!UICONTROL 小组件库]，并使用它向功能板添加小组件或为贵组织创建自定义小组件。 要修改功能板中小组件的大小和位置，请参阅[modify功能板指南](modify.md)。
