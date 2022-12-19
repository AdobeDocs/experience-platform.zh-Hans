---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件详细信息；详细信息
title: UI中的配置文件详细信息自定义
description: 本指南提供了关于自定义在Adobe Experience Platform UI中显示实时客户资料数据的方式的分步说明。
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: d2790ddab74f989ebb5ca522ce44323033c53911
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] 详细自定义 {#profile-detail-customization}

在Adobe Experience Platform用户界面中，您可以查看和交互 [!DNL Real-time Customer Profile] 以客户用户档案形式提供的数据。 UI中显示的配置文件信息已从多个配置文件片段合并到一起，以形成每个客户的单个视图。 这包括基本属性、链接的身份和渠道首选项等详细信息。 用户档案中显示的默认字段也可以在组织级别更改以显示首选字段 [!DNL Profile] 属性。 本指南提供了自定义 [!DNL Profile] 数据显示在平台UI中。

有关用户档案UI的完整指南，请访问 [配置文件UI指南](user-guide.md).

## 重新排序和调整信息卡大小 {#reorder-and-resize-cards}

从 **[!UICONTROL 详细信息]** 选项卡，您可以选择 **[!UICONTROL 自定义配置文件详细信息]** 以调整现有信息卡的大小和重新排序。

![](../images/profile-customization/customize-profile-details.png)

选择修改功能板后，您可以通过选择信息卡标题并将信息卡拖放到所需的顺序来重新排序信息卡。 您还可以通过选择信息卡右下角的角度符号来调整信息卡的大小(`⌟`)并将信息卡拖动到所需的大小。 在本例中， **[!UICONTROL 基本属性]** 正在调整卡的大小。

![](../images/profile-customization/resize.png)

所选卡根据所需大小进行调整，并动态地重新定位周围的卡。 这可能会导致某些信息卡被移动到其他行，这要求您向下滚动以查看所有信息卡。 例如，当[!UICONTROL 基本属性]“ ”卡的大小已调整为“ ”[!UICONTROL 链接的身份]“卡片不再显示在顶行上，现在显示在配置文件的新第二行上（未显示）。 返回“[!UICONTROL 链接的身份]“卡到顶行，您可以将其拖放到“ ”的当前位置[!UICONTROL 渠道首选项]”卡。

![](../images/profile-customization/resized.png)

## 编辑和删除信息卡

除了调整信息卡大小和重新排序信息卡外，您还可以编辑某些信息卡的内容，并从功能板中完全删除某些信息卡。 选择省略号(`...`)以编辑或删除它。 此时将打开一个下拉列表，其中包含用于编辑或删除卡的选项，具体取决于所选卡的属性。

>[!NOTE]
>
>并非所有卡都可以编辑或删除。 这是因为某些信息卡包含只读或必需的信息。 如果信息卡的右上角没有省略号，则它包含只读的AND必需信息，无法编辑，也无法删除。 如果卡片的角部有省略号，选择该卡片后，将只显示删除卡片的选项，则卡片信息为只读，无法编辑。

![](../images/profile-customization/edit-card.png)

选择 **[!UICONTROL 编辑]** 在下拉菜单中，打开 **[!UICONTROL 编辑小组件]** 工作区中，您可以在其中更新卡片标题、重新排序或删除可见属性，或使用添加其他属性 **[!UICONTROL 添加属性]** 按钮。

![](../images/profile-customization/basic-attributes.png)

## 添加属性 {#add-attributes}

从 **[!UICONTROL 编辑小组件]** 屏幕，选择 **[!UICONTROL 添加属性]** ，以开始向该卡添加属性。

![](../images/profile-customization/add-attributes.png)

当 **[!UICONTROL 选择并集架构字段]** 对话框打开时，对话框的左侧将显示 [!UICONTROL XDM个人配置文件] 并集架构，下面嵌套了字段。 有关并集模式的更多信息，请参阅 [合并模式部分 [!DNL Profile] 用户指南](user-guide.md#union-schema).

的 **[!UICONTROL 选定属性]** 对话框右侧的部分显示当前包含在您编辑的卡片中的属性。 您也可以在此处删除属性并重新排序属性。 将显示所选属性的总数，以及可添加到单个卡片中的最大属性数(20)。

![](../images/profile-customization/select-before.png)

您可以选择任意可用的并集架构字段，以自定义您正在编辑的卡片上的属性。 选定字段旁会显示一个复选标记，并自动添加到选定属性的列表。 添加要在卡片上显示的所有属性后，选择 **[!UICONTROL 选择]** 返回 **[!UICONTROL 编辑小组件]** 屏幕。

![](../images/profile-customization/select-after.png)

当您返回到 **[!UICONTROL 编辑小组件]** 屏幕上，卡片上的属性列表现在应会更新以反映您所做的选择。 您仍可以删除或重新排序卡片属性，或根据需要编辑卡片标题。 编辑完成后，选择 **[!UICONTROL 保存]** 以保存更改。

![](../images/profile-customization/new-attributes.png)

保存后，您将返回到 **[!UICONTROL 详细信息]** 选项卡，其中会显示更新的卡片和属性。

![](../images/profile-customization/added-attributes.png)

## 添加新信息卡 {#add-a-new-card}

要进一步自定义Experience Platform中用户档案的外观，您可以选择向功能板添加新卡片，并选择要在这些卡片上显示的属性。 要开始，请选择 **[!UICONTROL 修改功能板]** 在 **[!UICONTROL 详细信息]** 选项卡。

![](../images/profile-customization/customize-profile-details.png)

接下来，选择 **[!UICONTROL 添加小组件]** 功能板的左上角。

![](../images/profile-customization/add-widget.png)

选择添加新信息卡会打开 **[!UICONTROL 编辑小组件]** 屏幕，您可以为新信息卡提供标题并选择您希望信息卡显示的属性。 要开始向信息卡添加属性，请选择 **[!UICONTROL 添加属性]**.

![](../images/profile-customization/edit-widget.png)

当 **[!UICONTROL 选择并集架构字段]** 对话框打开时，对话框的左侧将显示 [!UICONTROL XDM个人配置文件] 并集模式和 **[!UICONTROL 选定属性]** 对话框右侧的部分将显示您为卡片选择的属性。 有关添加属性的更多信息，请参阅 [添加属性一节](#add-attributes) 在本文档中的前面部分。

将显示所选属性的总数，以及可添加到单个卡片中的最大属性数(20)。 您还可以从此屏幕中删除和重新排序您的选定属性。 添加要在卡片上显示的所有属性后，选择 **[!UICONTROL 选择]** 返回 **[!UICONTROL 编辑小组件]** 屏幕。

![](../images/profile-customization/add-widget-attributes.png)

当您返回到 **[!UICONTROL 编辑小组件]** 屏幕中，卡片上的属性列表应反映您在上一个屏幕中所做的选择。 您还可以根据需要重新排序和删除卡片属性。

要保存新信息卡，您必须先提供 **[!UICONTROL 卡片标题]**，则您将能够选择 **[!UICONTROL 保存]** 并完成卡片创建过程。

![](../images/profile-customization/new-widget.png)

保存后，您将返回到 **[!UICONTROL 详细信息]** 选项卡，其中显示了新卡和属性。

![](../images/profile-customization/added-widget.png)

## 恢复默认卡

如果您随时决定要恢复删除后的默认信息卡，则可以快速轻松地恢复。 首先，选择 **[!UICONTROL 修改功能板]**，然后选择 **[!UICONTROL 恢复默认卡]**. 显示默认卡片后，您可以选择 **[!UICONTROL 保存]** 保存更改或选择 **[!UICONTROL 取消]** 如果您不希望恢复默认卡。

![](../images/profile-customization/restore-default.png)

## 后续步骤

通过阅读本文档，您现在应该能够更新贵组织的配置文件视图，包括添加和删除信息卡、编辑信息卡详细信息和属性，以及重新排序和调整信息卡大小。 了解有关使用的更多信息 [!DNL Profile] Experience PlatformUI中的数据，请参阅 [[!DNL Profile] 用户指南](user-guide.md).
