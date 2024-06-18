---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件详细信息；详细信息
title: UI中的配置文件详细信息自定义
description: 本指南提供了分步说明，用于自定义在Adobe Experience Platform UI中实时客户个人资料数据的显示方式。
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 69ac6d3f98675df11183082ecbbb49d18ddb57af
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 详细信息自定义 {#profile-detail-customization}

在Adobe Experience Platform用户界面中，您可以查看和交互 [!DNL Real-Time Customer Profile] 以客户个人资料形式呈现的数据。 UI中显示的配置文件信息已从多个配置文件片段合并在一起，形成每个客户的单个视图。 这包括基本属性、链接身份和渠道偏好设置等详细信息。 用户档案中显示的默认字段也可以在组织级别更改为显示首选字段 [!DNL Profile] 属性。 本指南提供了有关自定义以下各项的方式的分步说明： [!DNL Profile] 数据显示在Platform UI中。

有关“配置文件”UI的完整指南，请访问 [配置文件UI指南](user-guide.md).

## 重新排序卡片并调整其大小 {#reorder-and-resize-cards}

从 **[!UICONTROL 详细信息]** 选项卡，您可以选择 **[!UICONTROL 自定义配置文件详细信息]** 以调整现有卡的大小和重新排序。

![自定义配置文件详细信息按钮在用户档案仪表板中突出显示。](../images/profile-customization/customize-profile-details.png)

选择修改功能板后，您可以通过选择卡片标题并将卡片拖放到所需顺序来重新排列卡片。 您还可以通过选择卡片右下角的角度符号来调整卡片的大小(`⌟`)，并将卡拖动到所需大小。 在此示例中， **[!UICONTROL 基本属性]** 正在调整卡的大小。

![调整大小按钮在基本属性卡中突出显示。](../images/profile-customization/resize.png)

所选卡片调整到所需的大小，并且周围卡片动态地重新定位。 这可能会导致某些信息卡被移动到其他行，从而需要您向下滚动才能看到所有信息卡。 例如，当&quot;[!UICONTROL 基本属性]“卡已调整大小。 ”[!UICONTROL 链接的身份]“信息卡在顶行不再可见，现在显示在配置文件新的第二行中（未显示）。 返回&quot;[!UICONTROL 链接的身份]”卡片放到顶行，您可以将其拖放到的当前位置“[!UICONTROL 渠道首选项]“ ”卡。

![重新调整大小的卡会突出显示。](../images/profile-customization/resized.png)

## 编辑和删除信息卡

除了调整卡片大小并重新排序之外，您还可以编辑某些卡片的内容并从功能板中完全删除某些卡片。 选择省略号(`...`)以对其进行编辑或将其删除。 这将打开一个下拉菜单，其中包含编辑或删除信息卡的选项，具体取决于所选信息卡的属性。

>[!NOTE]
>
>并非所有信息卡都可以编辑或删除。 这是因为某些信息卡包含只读或必需信息。 如果卡片的右上角没有省略号，则它包含只读的AND必需信息，不能编辑也不能删除它。 如果信息卡在角部有椭圆形，选择该信息卡将仅显示删除信息卡的选项，则信息卡为只读信息且无法编辑。

![将突出显示编辑卡片下拉列表。 其中包括编辑或移除卡片的选项。](../images/profile-customization/edit-card.png)

选择 **[!UICONTROL 编辑]** 在下拉菜单中打开 **[!UICONTROL 编辑构件]** 工作区，您可以在其中更新卡片标题、重新排序或删除可见属性，或使用添加其他属性 **[!UICONTROL 添加属性]** 按钮。

![此时将显示“基本属性”信息卡。](../images/profile-customization/basic-attributes.png)

## 添加属性 {#add-attributes}

从 **[!UICONTROL 编辑构件]** 屏幕，选择 **[!UICONTROL 添加属性]** 图标，以开始向该卡添加属性。

![“基本属性”信息卡中的“添加属性”按钮会突出显示。](../images/profile-customization/add-attributes.png)

当 **[!UICONTROL 选择合并架构字段]** 对话框打开，对话框左侧显示完整的 [!UICONTROL XDM个人资料] 合并架构，字段嵌套在下。 有关合并模式的详细信息，请参阅 [合并模式部分 [!DNL Profile] 用户指南](user-guide.md#union-schema).

此 **[!UICONTROL 选定的属性]** 对话框右侧的部分显示当前包含在所编辑信息卡中的属性。 您也可以在此处删除和重新排序属性。 显示选定的属性总数，以及可添加到单个卡片的最大属性数(20)。

![当前构成卡片属性的属性会突出显示。](../images/profile-customization/select-before.png)

您可以选择任何可用的合并架构字段，以自定义您正在编辑的卡片上的属性。 选择字段时，您可以选择查看文件路径名或显示名称。 要在这两种显示之间切换，请选择 **[!UICONTROL 显示显示名称]** 切换。

![此 [!UICONTROL 显示显示名称] 切换在“配置文件详细信息”页面中突出显示。](../images/profile-customization/show-display-names.png)

所选字段旁边会显示复选标记，并且会自动添加到所选属性列表中。 添加要显示在信息卡上的所有属性后，选择 **[!UICONTROL 选择]** 以返回 **[!UICONTROL 编辑构件]** 屏幕。

![新添加的属性会突出显示。](../images/profile-customization/select-after.png)

当您返回 **[!UICONTROL 编辑构件]** 屏幕上，卡片上的属性列表现在应该更新以反映您的选择。 您仍然可以根据需要删除卡片属性或重新排序卡片属性或编辑卡片标题。 编辑完成后，选择 **[!UICONTROL 保存]** 以保存更改。

![新添加的属性将显示在编辑的卡片上。](../images/profile-customization/new-attributes.png)

保存后，您将返回到 **[!UICONTROL 详细信息]** 选项卡，其中显示了更新的信息卡和属性。

![新添加的属性将显示在配置文件功能板的卡片上。](../images/profile-customization/added-attributes.png)

## 添加新信息卡 {#add-a-new-card}

要进一步自定义Experience Platform中配置文件的外观，您可以选择向功能板添加新信息卡，并选择希望在这些信息卡上显示的属性。 要开始，请选择 **[!UICONTROL 修改仪表板]** 在 **[!UICONTROL 详细信息]** 选项卡。

![自定义配置文件详细信息按钮突出显示。](../images/profile-customization/customize-profile-details.png)

接下来，选择 **[!UICONTROL 添加构件]** 在仪表板的左上角。

![“添加构件”按钮突出显示。](../images/profile-customization/add-widget.png)

选择添加新信息卡会打开 **[!UICONTROL 编辑构件]** 一个屏幕，您可以在其中为新信息卡提供标题，并选择您希望信息卡显示的属性。 要开始向信息卡添加属性，请选择 **[!UICONTROL 添加属性]**.

![“编辑构件”屏幕中显示空白的新构件卡。](../images/profile-customization/edit-widget.png)

当 **[!UICONTROL 选择合并架构字段]** 对话框打开，对话框左侧显示完整的 [!UICONTROL XDM个人资料] 合并模式和 **[!UICONTROL 选定的属性]** 对话框右侧的部分显示了您为信息卡选择的属性。 有关添加属性的详细信息，请参阅 [关于添加属性的部分](#add-attributes) 此文档前面显示的URL值。

显示选定的属性总数，以及可添加到单个卡片的最大属性数(20)。 您还可以从此屏幕中删除所选属性并重新排序。 添加要显示在信息卡上的所有属性后，选择 **[!UICONTROL 选择]** 以返回 **[!UICONTROL 编辑构件]** 屏幕。

![要添加到信息卡的字段会突出显示。](../images/profile-customization/add-widget-attributes.png)

当您返回 **[!UICONTROL 编辑构件]** 屏幕上，卡片上的属性列表应反映您在上一个屏幕中所做的选择。 您还可以根据需要重新排序和移除卡属性。

要保存您的新卡，您必须首先提供 **[!UICONTROL 卡片标题]**，然后您便能够选择 **[!UICONTROL 保存]** 并完成信息卡创建过程。

![新构件会在“编辑构件”屏幕中预览。](../images/profile-customization/new-widget.png)

保存后，您将返回到 **[!UICONTROL 详细信息]** 选项卡，您可在其中看到新卡和属性。

![新构件将添加到用户档案仪表板。](../images/profile-customization/added-widget.png)

## 恢复默认信息卡

如果在任何时候您决定要恢复已移除的默认信息卡，则可以快速轻松地恢复默认信息卡。 首先，选择 **[!UICONTROL 修改仪表板]**，然后选择 **[!UICONTROL 恢复默认信息卡]**. 显示默认信息卡后，您可以选择 **[!UICONTROL 保存]** 保存更改或选择 **[!UICONTROL 取消]** 如果您不想恢复默认卡。

![恢复默认信息卡按钮在配置文件仪表板中突出显示。](../images/profile-customization/restore-default.png)

## 后续步骤

通过阅读本文档，您现在应该能够更新组织的配置文件视图，包括添加和删除信息卡、编辑信息卡详细信息和属性，以及重新排序信息卡和调整信息卡大小。 要了解有关使用的更多信息，请执行以下操作 [!DNL Profile] 数据，请参阅Experience PlatformUI中的 [[!DNL Profile] 用户指南](user-guide.md).
