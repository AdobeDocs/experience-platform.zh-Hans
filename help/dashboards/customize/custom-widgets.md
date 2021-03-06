---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用情况；小组件；量度；
title: 为功能板创建自定义小组件
description: '本指南提供了有关创建自定义小组件以便在Adobe Experience Platform功能板中使用的分步说明。 '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---


# 为功能板创建自定义小组件

在Adobe Experience Platform中，您可以使用多个功能板查看组织的数据并与之交互。 您还可以通过向功能板视图添加新小组件来更新某些功能板。 除了由Adobe提供的标准小组件之外，您还可以创建自定义小组件并在整个组织内共享这些小组件。

本指南提供了有关创建自定义小组件并将其添加到Platform UI中的[!UICONTROL Profiles]、[!UICONTROL 区段]和[!UICONTROL 目标]功能板的分步说明。

要了解有关标准小组件的更多信息，请参阅[向功能板添加标准小组件的指南](standard-widgets.md)。

>[!NOTE]
>
>无法自定义[!UICONTROL 许可证使用情况]功能板中显示的小组件。 要了解有关此唯一功能板的更多信息，请阅读[许可证使用功能板文档](../guides/license-usage.md)。

## 构件库 {#widget-library}

本指南要求您访问Experience Platform中的[!UICONTROL Widget库]。 要进一步了解小组件库以及如何在UI中访问该库，请首先阅读[小组件库概述](widget-library.md)。

## 自定义小组件快速入门

在小组件库中，通过&#x200B;**[!UICONTROL Custom]**&#x200B;选项卡，您可以创建小组件并将其与组织中的其他用户共享，以便自定义功能板的外观。

>[!IMPORTANT]
>
>贵组织在小组件库中最多可创建20个自定义小组件。

选择&#x200B;**[!UICONTROL Custom]**&#x200B;选项卡以开始创建自定义小组件或查看您的组织已创建的自定义小组件。

![](../images/customization/custom-widgets.png)

## 创建自定义小组件

要创建自定义小组件，请从小组件库的右上角选择&#x200B;**[!UICONTROL 创建小组件]**，或者，如果这是您组织的第一个自定义小组件，请从小组件库的中心选择&#x200B;**[!UICONTROL 创建]**。

![](../images/customization/create-widget.png)

在&#x200B;**[!UICONTROL 创建小组件]**&#x200B;对话框中，为新小组件提供标题和说明，并选择您希望小组件显示的属性。

>[!NOTE]
>
>可用属性的列表取决于为贵组织配置的架构。 要了解有关属性选择和架构配置的更多信息，请阅读[编辑架构以创建自定义小组件](edit-schema.md)的指南。

要选择属性，请选择要添加属性旁边的单选按钮。

>[!NOTE]
>
>每个小组件只能选择一个属性，每个属性只能创建一个小组件。 如果已为属性创建小组件，则该属性将呈灰显状态。

![](../images/customization/create-widget-dialog.png)

## 选择可视化

选择属性后，对话框中会显示新小组件的预览。 人工智能用于自动选择最适合属性数据的可视化，并提供其他可手动选择的可视化选项。

根据属性，AI会推荐不同的可视化选项。 可视化图表的完整列表包括：

* 水平条形图：水平线用于表示值。
* 竖条图：垂直线用于表示值。
* 圆环图：与饼图类似，值显示为整体的一部分或部分。
* 散点图：使用水平和垂直轴来指示值。
* 折线图：值使用单行显示，以显示一段时间内的更改。
* 数字卡：显示表示单个键值的概要数字。
* 数据表：值在表中显示为行。

>[!NOTE]
>
>当前所有属性唯一支持的量度是配置文件计数。
>
>示例小组件中显示的数据仅供说明之用。 预览不显示您组织的实际数据。

要保存新小组件并返回到[!UICONTROL Custom]选项卡，请选择&#x200B;**[!UICONTROL Create]**。

![](../images/customization/create-widget-select-attribute.png)

现在，您可以通过从库中选择小组件并选择&#x200B;**[!UICONTROL 添加小组件]**，将新小组件添加到功能板。

![](../images/customization/custom-widgets-new.png)

## 隐藏自定义小组件

将小组件添加到库后，可通过以下操作来隐藏该组件：选择小组件卡上的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 隐藏小组件]**。 您还可以从同一下拉菜单中预览和编辑小组件。

要查看已隐藏的小组件，请选择小组件库右上角的&#x200B;**[!UICONTROL 显示隐藏的小组件]**。

>[!WARNING]
>
>在库中隐藏小组件不会从单个用户的仪表板中删除该小组件。 如果贵组织不应再使用小组件，请确保您将此小组件直接传达给所有Platform用户，因为他们需要从其功能板中删除该小组件。

![](../images/customization/hide-widget.png)

## 编辑自定义小组件

您可以在小组件库中编辑自定义小组件，方法是选择小组件卡上的省略号(`...`)，然后从下拉菜单中选择&#x200B;**[!UICONTROL 编辑]**。

![](../images/customization/custom-widget-edit.png)

在&#x200B;**[!UICONTROL 编辑小组件]**&#x200B;对话框中，您可以编辑小组件的标题和说明，以及预览和选择不同的可视化。 进行编辑后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存所做更改并返回到自定义小组件选项卡。

>[!WARNING]
>
>在库中编辑小组件不会为个人用户更新小组件。 如果小组件已更新，请确保您直接将其与所有Platform用户通信，因为用户需要从其功能板中删除过时的小组件，然后从小组件库中选择并添加更新的小组件。

![](../images/customization/edit-widget.png)

## 后续步骤

阅读本文档后，您可以访问小组件库，并使用它为贵组织创建和添加自定义小组件。 要修改功能板中显示的小组件的大小和位置，请参阅[modify功能板指南](modify.md)。
