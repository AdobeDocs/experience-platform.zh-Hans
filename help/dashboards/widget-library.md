---
keywords: Experience Platform；用户界面；UI;仪表板;仪表板;用户档案；区段；目标；许可证使用
title: 使用Widget库添加和创建仪表板Widget
description: '本指南提供了有关添加标准构件和创建自定义构件以在Adobe Experience Platform中可视化仪表板数据的分步说明。 '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---

# （测试版）Widget库{#widget-library}

>[!IMPORTANT]
>
>仪表板功能当前处于测试阶段，并非所有用户都可用。 文档和功能可能会发生变化。

在Adobe Experience Platform用户界面中，您可以使用多个仪表板视图组织的数据并与其交互。 您还可以通过向仪表板视图添加新构件来更新其中一些仪表板。 除了Adobe提供的标准构件，您还可以创建自定义构件并在整个组织中共享它们。

本指南提供了有关添加标准构件和创建自定义构件的分步说明，以自定义在平台UI的[!UICONTROL Profiles]和[!UICONTROL Segments]仪表板中显示的信息。

有关如何修改[!UICONTROL Profiles]、[!UICONTROL Destinations]和[!UICONTROL Segments]仪表板中构件的位置和大小的信息，请参阅[修改仪表板指南](modify.md)。

>[!NOTE]
>
>无法自定义[!UICONTROL License usage]仪表板中显示的构件。 要进一步了解此独特仪表板，请阅读[许可证使用仪表板文档](guides/license-usage.md)。

## 访问Widget库

从任何仪表板(例如，用户档案仪表板)中，您可以选择&#x200B;**[!UICONTROL Modify dashboard]**&#x200B;后跟&#x200B;**[!UICONTROL Widget library]**&#x200B;以访问Widget库。

>[!NOTE]
>
>[!UICONTROL Widget library]按钮仅在选择[!UICONTROL Modify dashboard]后出现。

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

[!UICONTROL Widget library]包含两个选项卡，分别为[!UICONTROL Standard]和[!UICONTROL Custom]。

* **[!UICONTROL Standard]**&#x200B;选项卡包含由Adobe创建的构件，并允许您使用这些标准量度更新仪表板。 要了解有关向仪表板添加标准构件的更多信息，请参阅本指南中的[标准构件](#standard-widgets)部分。
* **[!UICONTROL Custom]**&#x200B;选项卡允许您在组织内创建和共享构件。 有关创建您自己的构件的完整步骤，请参阅本指南中的[自定义构件](#custom-widgets)部分。

![](images/customization/widget-library.png)

## 标准构件{#standard-widgets}

**[!UICONTROL Standard]**&#x200B;选项卡包含由Adobe创建的构件，分为类别。 选择类别后，将显示该仪表板的可用构件。 每个Widget都显示为一张卡，提供量度的标题、描述和示例可视化。

>[!NOTE]
>
>构件只能添加到与所选仪表板匹配的类别。 例如，只能将[!UICONTROL Profiles]类别中的构件添加到[!UICONTROL Profiles]仪表板。

![](images/customization/standard-widgets.png)

要选择要添加到仪表板的标准Widget，请突出显示该Widget并选中该Widget的复选框。 选择至少一个构件后，**[!UICONTROL Add widget]**&#x200B;按钮被照亮。

>[!NOTE]
>
>构件库右上角的计数器显示所选构件的总数。

选择&#x200B;**[!UICONTROL Add widget]**&#x200B;以将选定的构件添加到您的仪表板。

![](images/customization/add-widget.png)

## 自定义构件{#custom-widgets}

>[!IMPORTANT]
>
>您的单位在构件库中最多可创建20个自定义构件。

要进一步自定义Experience Platform中仪表板的外观，您可以创建构件并与组织中的其他用户共享它们。 从构件库中，选择&#x200B;**[!UICONTROL Custom]**&#x200B;选项卡以开始创建自定义构件。 在[!UICONTROL Custom]选项卡上，您的组织创建的所有构件都可见。 在此示例中，尚未创建自定义构件。

![](images/customization/custom-widgets.png)

### 选择属性

要创建自定义构件，必须识别实时客户用户档案属性，以确保将数据作为每日快照的一部分包含在内。 如果您的单位尚未选择任何用户档案属性，则[!UICONTROL Configure schema]按钮将显示在Widget库的右上角。

选择至少一个自定义属性后，Widget库的右上角将显示[!UICONTROL Edit schema]按钮。 选择&#x200B;**[!UICONTROL Edit schema]**&#x200B;以打开&#x200B;**[!UICONTROL Select union schema field]**&#x200B;对话框，以视图选定的属性并添加更多属性。

>[!IMPORTANT]
>
>一个组织最多可以选择20个属性。

![](images/customization/edit-schema.png)

要选择属性，请导航到合并模式中的属性（或使用搜索），然后选中该属性旁边的复选框。 选中此复选框还会将属性添加到对话框右侧的&#x200B;**[!UICONTROL Selected Attributes]**&#x200B;列表。

>[!NOTE]
>
>要使某个属性可见以进行选择，它必须是以下属性之一：String、Date、Date-Time、Boolean、Short、Long、Integer或Byte。 映射和多次数据类型不受支持，并且呈灰显，因此无法选择它们。

选择要添加的属性后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存属性并返回到自定义构件选项卡。

刷新数据时，新选择的属性在每日快照之后可用。

![](images/customization/select-attribute.png)

### 创建自定义Widget

要创建自定义Widget，请从Widget库的中心选择&#x200B;**[!UICONTROL Create]**，或者，如果已创建自定义Widget，请从Widget库的右上角选择&#x200B;**[!UICONTROL Create widget]**。

![](images/customization/create-widget.png)

在&#x200B;**[!UICONTROL Create widget]**&#x200B;对话框中，您可以为新Widget提供标题和说明，并选择希望Widget显示的属性。 要选择属性，请选择要添加的属性旁边的单选按钮。

>[!NOTE]
>
>每个Widget只能选择一个属性。 此外，如果已经为某个属性创建了Widget，则该属性将灰显。

![](images/customization/create-widget-dialog.png)

对话框中将显示新构件的预览，其中显示包含模拟数据的水平条形图。

>[!NOTE]
>
>当前所有属性唯一支持的量度是用户档案计数，而当前支持自定义构件的唯一可视化是水平条形图。
>
>示例Widget中显示的数据仅供说明之用。 该预览不显示您组织的实际数据。

![](images/customization/create-widget-select-attribute.png)

要保存新Widget并返回[!UICONTROL Custom]选项卡，请选择&#x200B;**[!UICONTROL Create]**。 现在，您可以通过从库中选择Widget并选择&#x200B;**[!UICONTROL Add widget]**，将新Widget添加到仪表板。

### 存档自定义Widget

将Widget添加到库后，可以使用&#x200B;**[!UICONTROL Archive]**&#x200B;按钮将其存档。 您还可以编辑Widget以更新标题或描述字段。

## 后续步骤

在阅读此文档后，您现在可以访问[!UICONTROL Widget library]并使用它向仪表板添加构件或为组织创建自定义构件。 要修改仪表板中构件的大小和位置，请参阅[修改仪表板指南](modify.md)。
