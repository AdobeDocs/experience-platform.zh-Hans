---
keywords: Experience Platform;用户档案；实时客户用户档案；用户界面；UI；自定义；用户档案详细信息；详细信息
title: 用户档案详细信息自定义
description: '本指南提供分步说明，用于自定义在Adobe Experience Platform UI中显示实时客户用户档案数据的方式。 '
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] 详细信息自定义  {#profile-detail-customization}

在Adobe Experience Platform用户界面中，您可以视图[!DNL Real-time Customer Profile]数据并以客户用户档案的形式与其交互。 在UI中显示的用户档案信息已从多个用户档案片段合并到一起，以形成每个客户的单个视图。 这包括基本属性、链接身份和渠道首选项等详细信息。 用户档案中显示的默认字段也可以在组织级别更改，以显示首选[!DNL Profile]属性。 本指南提供了有关自定义[!DNL Profile]数据在平台UI中的显示方式的分步说明。

有关用户档案UI的完整指南，请访问[用户档案UI指南](user-guide.md)。

## 对卡{#reorder-and-resize-cards}重新排序和调整大小

从客户用户档案的&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡中，您可以选择&#x200B;**[!UICONTROL Modify dashboard]**&#x200B;以调整现有卡的大小和对其重新排序。

![](../images/profile-customization/profiles-modify-dashboard.png)

选择修改仪表板后，可以通过选择卡标题并将卡拖放到所需顺序来对卡重新排序。 您还可以通过选择卡右下角的角度符号(`⌟`)并将卡拖动到所需大小来调整卡的大小。 在此示例中，将调整&#x200B;**[!UICONTROL Basic attributes]**&#x200B;卡的大小。

![](../images/profile-customization/profiles-resize-cards.png)

所选卡根据所需大小进行调整，并动态地重新定位周围的卡。 这可能导致某些卡被移动到其他行，这要求您向下滚动以查看所有卡。 例如，当“[!UICONTROL Basic attributes]”卡的大小调整为大小时，“[!UICONTROL Linked identities]”卡在顶行上不再可见，现在显示在用户档案内新的第二行上（未显示）。 要将“[!UICONTROL Linked identities]”卡返回到顶行，可将其拖放到“[!UICONTROL Channel preferences]”卡的当前位置。

![](../images/profile-customization/profiles-card-resized.png)

## 编辑和删除卡

除了调整卡的大小和重新排序卡之外，您还可以编辑某些卡的内容并完全从仪表板中删除某些卡。 选择卡右上角的省略号(`...`)以编辑或删除它。 这将打开一个下拉列表，其中包含编辑或删除卡的选项，具体取决于所选卡的属性。

>[!NOTE]
>
>并非所有卡都可以编辑或删除。 这是因为某些卡包含只读信息或必需信息。 如果卡的右上角没有省略号，则它包含只读的AND必需信息，无法编辑，也无法删除。 如果卡在角中带有省略号，且选择该卡后，将仅显示删除卡的选项，则卡信息为只读，无法编辑。

![](../images/profile-customization/profiles-edit-remove-resized.png)

在下拉列表中选择&#x200B;**[!UICONTROL Edit]**&#x200B;以打开&#x200B;**[!UICONTROL Edit widget]**&#x200B;工作区，您可以在其中更新卡标题、重新排序或删除可见属性，或使用&#x200B;**[!UICONTROL Add attributes]**&#x200B;按钮添加其他属性。

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## 添加属性{#add-attributes}

从&#x200B;**[!UICONTROL Edit widget]**&#x200B;屏幕中，选择卡右上角的&#x200B;**[!UICONTROL Add attributes]**&#x200B;以开始向该卡添加属性。

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

当&#x200B;**[!UICONTROL Select union schema field]**&#x200B;对话框打开时，对话框的左侧显示完整的[!UICONTROL XDM Individual Profile]合并模式，其下嵌有字段。 有关合并模式的详细信息，请参阅 [!DNL Profile] 用户指南](user-guide.md#union-schema)的[合并模式部分。

对话框右侧的&#x200B;**[!UICONTROL Selected Attributes]**&#x200B;部分显示当前包含在正在编辑的卡中的属性。 您也可以在此处删除属性并重新排序。 显示所选属性的总数以及可添加到单个卡的最大属性数(20)。

![](../images/profile-customization/profiles-select-field-before.png)

您可以选择任何可用的合并模式字段，以自定义您正在编辑的卡上的属性。 选定字段旁边将显示一个复选标记，并自动添加到选定属性的列表。 添加要在卡上显示的所有属性后，选择&#x200B;**[!UICONTROL Select]**&#x200B;返回至&#x200B;**[!UICONTROL Edit widget]**&#x200B;屏幕。

![](../images/profile-customization/profiles-select-field-after.png)

返回&#x200B;**[!UICONTROL Edit widget]**&#x200B;屏幕时，卡上属性的列表现在应更新以反映您的选择。 您仍可以删除卡属性或对卡属性重新排序，或根据需要编辑卡标题。 完成编辑后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改。

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

保存后，您将返回到&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡，其中显示更新的卡和属性。

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## 添加新卡{#add-a-new-card}

要进一步自定义Experience Platform中用户档案的外观，您可以选择向仪表板添加新卡并选择要在这些卡上显示的属性。 要开始，请在&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡上选择&#x200B;**[!UICONTROL Modify dashboard]**。

![](../images/profile-customization/profiles-modify-dashboard.png)

接下来，选择仪表板左上角的&#x200B;**[!UICONTROL Add widget]**。

![](../images/profile-customization/profiles-add-widget.png)

选择添加新卡会打开&#x200B;**[!UICONTROL Edit widget]**&#x200B;屏幕，您可以在其中提供新卡的标题并选择您希望该卡显示的属性。 要开始向卡添加属性，请选择&#x200B;**[!UICONTROL Add attributes]**。

![](../images/profile-customization/profiles-edit-new-widget.png)

当&#x200B;**[!UICONTROL Select union schema field]**&#x200B;对话框打开时，对话框的左侧显示完整的[!UICONTROL XDM Individual Profile]合并模式，对话框右侧的&#x200B;**[!UICONTROL Selected Attributes]**&#x200B;部分显示您为卡选择的属性。 有关添加属性的详细信息，请参阅有关添加属性](#add-attributes)的[部分，该部分在此文档前面显示。

显示所选属性的总数以及可添加到单个卡的最大属性数(20)。 您还可以从此屏幕中删除选定属性并对其重新排序。 添加要在卡上显示的所有属性后，选择&#x200B;**[!UICONTROL Select]**&#x200B;返回至&#x200B;**[!UICONTROL Edit widget]**&#x200B;屏幕。

![](../images/profile-customization/profiles-add-fields-new-widget.png)

返回&#x200B;**[!UICONTROL Edit widget]**&#x200B;屏幕时，卡上属性的列表应反映您在上一屏幕中的选择。 您还可以根据需要重新排序和删除卡属性。

要保存新卡，您必须首先提供&#x200B;**[!UICONTROL Card title]**，然后您可以选择&#x200B;**[!UICONTROL Save]**&#x200B;并完成卡创建过程。

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

保存后，您将返回到&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡，新卡和属性可见。

![](../images/profile-customization/profiles-detail-new-widget.png)

## 恢复默认卡

如果您在任何时候决定要恢复删除后的默认卡，您可以快速轻松地恢复。 首先，选择&#x200B;**[!UICONTROL Modify dashboard]**，然后选择&#x200B;**[!UICONTROL Restore default cards]**。 显示默认卡后，您可以选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改，或者选择&#x200B;**[!UICONTROL Cancel]**（如果您不希望恢复默认卡）。

![](../images/profile-customization/profiles-restore-default.png)

## 后续步骤

通过遵循此文档，您现在应该可以更新组织的用户档案视图，包括添加和删除卡、编辑卡详细信息和属性以及重新排序和调整卡大小。 要了解有关在Experience Platform UI中使用[!DNL Profile]数据的更多信息，请参阅[[!DNL Profile] 用户指南](user-guide.md)。
