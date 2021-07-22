---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用情况；小组件；量度；
title: 为功能板创建自定义小组件
description: '本指南提供了有关创建自定义小组件以便在Adobe Experience Platform功能板中使用的分步说明。 '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '589'
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

要创建自定义小组件，请从小组件库的中心选择&#x200B;**[!UICONTROL 创建]**，或者如果已创建自定义小组件，请从小组件库的右上角选择&#x200B;**[!UICONTROL 创建小组件]**。

![](../images/customization/create-widget.png)

在&#x200B;**[!UICONTROL 创建小组件]**&#x200B;对话框中，您可以为新小组件提供标题和描述，并选择您希望小组件显示的属性。

>[!NOTE]
>
>可用属性的列表取决于为贵组织配置的架构。 要了解有关属性选择和架构配置的更多信息，请阅读[编辑架构以创建自定义小组件](edit-schema.md)的指南。

要选择属性，请选择要添加属性旁边的单选按钮。

>[!NOTE]
>
>每个小组件只能选择一个属性，每个属性只能创建一个小组件。 如果已为属性创建小组件，则该属性将呈灰显状态。

![](../images/customization/create-widget-dialog.png)

## 预览自定义小组件

对话框中会显示新小组件的预览，其中显示了包含模拟数据的水平条形图。

>[!NOTE]
>
>当前所有属性唯一支持的量度是配置文件计数，而当前唯一支持自定义小组件的可视化是水平条形图。
>
>示例小组件中显示的数据仅供说明之用。 预览不显示您组织的实际数据。

![](../images/customization/create-widget-select-attribute.png)

要保存新小组件并返回到[!UICONTROL Custom]选项卡，请选择&#x200B;**[!UICONTROL Create]**。 现在，您可以通过从库中选择小组件并选择&#x200B;**[!UICONTROL 添加小组件]**，将新小组件添加到功能板。

## 存档自定义小组件

将小组件添加到库后，可以使用&#x200B;**[!UICONTROL Archive]**&#x200B;按钮将其存档。 您还可以编辑小组件以更新标题或描述字段。

## 后续步骤

阅读本文档后，您可以访问小组件库，并使用它为贵组织创建和添加自定义小组件。 要修改功能板中显示的小组件的大小和位置，请参阅[modify功能板指南](modify.md)。
