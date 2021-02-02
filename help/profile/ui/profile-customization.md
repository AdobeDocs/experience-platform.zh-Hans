---
keywords: Experience Platform;用户档案；实时客户用户档案；用户界面；UI；自定义；用户档案详细信息；详细信息
title: 自定义您如何在UI中视图用户档案
description: '本指南提供分步说明，用于自定义在Adobe Experience PlatformUI中显示实时客户用户档案数据的方式。 '
topic: guide
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] 详细自定义  {#profile-detail-customization}

在Adobe Experience Platform用户界面中，您可以视图[!DNL Real-time Customer Profile]数据并以客户用户档案的形式进行交互。 在UI中显示的用户档案信息已从多个用户档案片段合并到一起，以形成每个客户的单个视图。 这包括基本属性、链接身份和渠道首选项等详细信息。 用户档案中显示的默认字段也可以在组织级别更改，以显示首选[!DNL Profile]属性。 本指南提供有关自定义[!DNL Profile]数据在平台UI中显示的方式的分步说明。

有关用户档案UI的完整指南，请访问[用户档案UI指南](user-guide.md)。

## 对卡进行重新排序和调整大小{#reorder-and-resize-cards}

从客户用户档案的&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡中，您可以选择&#x200B;**[!UICONTROL 修改仪表板]**&#x200B;以调整现有卡的大小和对其重新排序。

![](../images/profile-customization/profiles-modify-dashboard.png)

选择修改仪表板后，您可以通过选择卡标题并将卡拖放到所需的顺序来重新排序卡。 您还可以通过选择卡右下角的角度符号(`⌟`)并将卡拖动到所需大小来调整卡的大小。 在此示例中，正在调整&#x200B;**[!UICONTROL 基本属性]**&#x200B;卡的大小。

![](../images/profile-customization/profiles-resize-cards.png)

所选卡根据所需大小进行调整，并动态调整周围的卡。 这可能导致某些卡被移到其他行，需要您向下滚动才能看到所有卡。 例如，当“[!UICONTROL 基本属性]”卡的大小调整为“[!UICONTROL 链接标识]”卡在顶行上不再可见，现在显示在用户档案内的新第二行上（未显示）。 要将“[!UICONTROL 链接标识]”卡返回到顶行，可以将其拖放到“[!UICONTROL 渠道首选项]”卡的当前位置。

![](../images/profile-customization/profiles-card-resized.png)

## 编辑和删除卡

除了调整卡的大小和重新排序卡，您还可以编辑某些卡的内容并从仪表板中完全删除某些卡。 选择卡右上角的省略号(`...`)以编辑或删除它。 此操作会打开一个下拉菜单，其中包含编辑或删除卡的选项，具体取决于所选卡的属性。

>[!NOTE]
>
>并非所有卡都可以编辑或删除。 这是因为某些卡包含只读或必需的信息。 如果卡的右上角没有省略号，则它包含只读的AND必需信息，无法编辑，也无法删除。 如果卡在角中带有省略号，并且选择它时只显示删除卡的选项，则卡信息为只读，无法编辑。

![](../images/profile-customization/profiles-edit-remove-resized.png)

在下拉菜单中选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开&#x200B;**[!UICONTROL 编辑构件]**&#x200B;工作区，在该工作区中，您可以更新卡标题、重新排序或删除可见属性，或使用&#x200B;**[!UICONTROL 添加属性]**&#x200B;按钮添加其他属性。

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## 添加属性{#add-attributes}

从&#x200B;**[!UICONTROL 编辑构件]**&#x200B;屏幕，选择卡右上角的&#x200B;**[!UICONTROL 添加属性]**，开始向该卡添加属性。

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

当&#x200B;**[!UICONTROL 选择合并模式字段]**&#x200B;对话框打开时，对话框的左侧显示完整的[!UICONTROL  XDM单个用户档案模式]，其下嵌套有字段。 有关合并模式的详细信息，请参阅 [!DNL Profile] 用户指南](user-guide.md#union-schema)的[合并模式部分。

对话框右侧的&#x200B;**[!UICONTROL 选定属性]**&#x200B;部分显示当前包含在您正在编辑的卡中的属性。 您也可以在此处删除属性并重新排序。 显示所选属性的总数以及可添加到单个卡的最大属性数(20)。

![](../images/profile-customization/profiles-select-field-before.png)

您可以选择任何可用的合并模式字段，以自定义您正在编辑的卡上的属性。 选定字段旁边将显示一个复选标记，并自动添加到选定属性的列表。 添加您希望在卡上显示的所有属性后，选择&#x200B;**[!UICONTROL 选择]**&#x200B;以返回至&#x200B;**[!UICONTROL 编辑构件]**&#x200B;屏幕。

![](../images/profile-customization/profiles-select-field-after.png)

当您返回&#x200B;**[!UICONTROL 编辑构件]**&#x200B;屏幕时，卡上属性的列表现在应更新以反映您的选择。 您仍然可以根据需要删除或重新排序卡属性或编辑卡标题。 完成编辑后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

保存后，您将返回到&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡，其中显示更新的卡和属性。

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## 添加新卡{#add-a-new-card}

要进一步自定义Experience Platform中用户档案的外观，您可以选择向仪表板添加新卡，并选择要在这些卡上显示的属性。 首先，在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡上选择&#x200B;**[!UICONTROL 修改仪表板]**。

![](../images/profile-customization/profiles-modify-dashboard.png)

接下来，选择仪表板左上角的&#x200B;**[!UICONTROL 添加构件]**。

![](../images/profile-customization/profiles-add-widget.png)

选择添加新卡会打开&#x200B;**[!UICONTROL 编辑构件]**&#x200B;屏幕，您可以在该屏幕中为新卡提供标题并选择您希望该卡显示的属性。 要开始向卡添加属性，请选择&#x200B;**[!UICONTROL 添加属性]**。

![](../images/profile-customization/profiles-edit-new-widget.png)

当&#x200B;**[!UICONTROL 选择合并模式字段]**&#x200B;对话框打开时，对话框的左侧显示完整的[!UICONTROL  XDM单个用户档案]合并模式，对话框右侧的&#x200B;**[!UICONTROL 选定属性]**&#x200B;部分显示您为卡选择的属性。 有关添加属性的详细信息，请参阅有关添加属性](#add-attributes)的[部分，该部分在此文档前面显示。

显示所选属性的总数以及可添加到单个卡的最大属性数(20)。 您还可以从此屏幕中删除选定属性并对其重新排序。 添加您希望在卡上显示的所有属性后，选择&#x200B;**[!UICONTROL 选择]**&#x200B;以返回至&#x200B;**[!UICONTROL 编辑构件]**&#x200B;屏幕。

![](../images/profile-customization/profiles-add-fields-new-widget.png)

当您返回到&#x200B;**[!UICONTROL 编辑构件]**&#x200B;屏幕时，卡上属性的列表应反映您在上一屏幕中的选择。 您还可以根据需要重新排序和删除卡属性。

要保存新卡，您必须首先提供&#x200B;**[!UICONTROL 卡标题]**，然后您可以选择&#x200B;**[!UICONTROL 保存]**&#x200B;并完成卡创建过程。

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

保存后，您将返回到&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡，新卡和属性在该选项卡中可见。

![](../images/profile-customization/profiles-detail-new-widget.png)

## 恢复默认卡

如果您随时决定要恢复删除后的默认卡，您可以快速轻松地恢复。 首先，选择&#x200B;**[!UICONTROL 修改仪表板]**，然后选择&#x200B;**[!UICONTROL 恢复默认卡]**。 显示默认卡后，您可以选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改，或者选择&#x200B;**[!UICONTROL 取消]**（如果您不想恢复默认卡）。

![](../images/profile-customization/profiles-restore-default.png)

## 后续步骤

通过遵循此文档，您现在应该能够更新组织的用户档案视图，包括添加和删除卡、编辑卡详细信息和属性以及重新排列卡和调整其大小。 要进一步了解如何在Experience PlatformUI中使用[!DNL Profile]数据，请参阅[[!DNL Profile] 用户指南](user-guide.md)。