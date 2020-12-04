---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: 使用模式模式编辑器定义两个模式之间的关系
description: 此文档提供了一个教程，用于使用Experience Platform用户界面中的模式编辑器定义两个模式之间的关系。
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

了解不同渠道客户之间的关系及其与您品牌的互动是Adobe Experience Platform的重要部分。 在(XDM)模式结构中定 [!DNL Experience Data Model] 义这些关系，使您能够对客户数据获得复杂的洞察。

虽然模式关系可以通过使用合并模式来推断， [!DNL Real-time Customer Profile]但这仅适用于共享同一类的模式。 要在属于不同类的两个模式之间建立关系，必须向源模式添加专用关系字段，该字段引用目标模式的标识。

此文档提供了一个教程，用于使用用户界面中的模式编辑器定义两个模式之 [!DNL Experience Platform] 间的关系。 有关使用API定义模式关系的步骤，请参阅使用 [模式注册表API定义关系的教程](relationship-api.md)。

## 入门指南

本教程需要对UI中的 [!DNL XDM System] 模式编辑器和编辑器有 [!DNL Experience Platform] 所了解。 在开始本教程之前，请查阅以下文档：

* [Experience Platform中的XDM系统](../home.md):XDM及其实施概述 [!DNL Experience Platform]。
* [模式合成基础](../schema/composition.md):介绍XDM模式的构件。
* [使用以下图标创建模式 [!DNL Schema Editor]](create-schema-ui.md):一个教程，其中介绍使用的基础知 [!DNL Schema Editor]识。

## 定义源和目标模式

您应已创建将在关系中定义的两个模式。 为便于演示，本教程在组织的忠诚度项目(在“”模式中定义)的成员与其最喜爱的酒店(在“”模式中定义)之间[!DNL Loyalty Members][!DNL Hotels]创建关系。

>[!IMPORTANT]
>
>要建立关系，两个模式必须定义主身份并启用 [!DNL Real-time Customer Profile]。 如果您需要有关如何 [相应配置模式的指导](./create-schema-ui.md#profile) ，请参阅模式创建教程中有关启用模式以在用户档案中使用的部分。

模式关系由源模式内的专用字 **段表示** ，该专用字段引用目标模式 **内的其他字段**。 在接下来的步骤中，[!DNL Loyalty Members]“”将作为源模式，而“[!DNL Hotels]”将作为目标模式。

为便于参考，以下各节将介绍本教程中在定义关系之前使用的每个模式的结构。

### [!DNL Loyalty Members] 模式

源模式“[!DNL Loyalty Members]”基于类 [!DNL XDM Individual Profile] ，是在教程中构建的用于在UI [中创建模式的模式](create-schema-ui.md)。 它在其命名空间 `loyalty` 下包含一个 `_tenantId` 对象，该对象包括若干特定于忠诚度的字段。 其中一个字段 `loyaltyId`在“电子邮件”模式下充当命名空间的主 [!UICONTROL 要标识] 。 如“模式 **[!UICONTROL 属性]**”下所示，此模式已在中启用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 模式

目标模式[!DNL Hotels]“”基于自定义“[!DNL Hotels]”类，并包含描述酒店的字段。 在自 `hotelId` 定义模式下，该字段用作该命名空间的主标 `hotelId` 识。 与模式 [!DNL Loyalty Members] 一样，此模式也已启用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/hotels.png)

## 创建关系混合

>[!NOTE]
>
>仅当源模式没有专用的字符串类型字段用作目标模式的引用时，才需要执行此步骤。 如果此字段已在源模式中定义，请跳到定义关系字 [段的下一步](#relationship-field)。

要定义两个模式之间的关系，源模式必须有一个专用字段，用作对目标模式的引用。 您可以通过创建新混音将此字段添加到源模式。

开始，方 **[!UICONTROL 法是]** 在Mixins **[!UICONTROL 部分选择]** Add。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

将出 [!UICONTROL 现“添加混合] ”对话框。 在此处，选择“ **[!UICONTROL 创建新混音”]**。 在显示的文本字段中，输入新混音的显示名称和说明。 完成 **[!UICONTROL 后选择]** “添加混音”。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

画布将重新显示，“[!DNL Favorite Hotel]”显示在“ **[!UICONTROL Mixins]** ”部分。 选择混音名称，然后选 **[!UICONTROL 择根级]** 字段旁的“添加 `Loyalty Members` 字段”。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中的命名空间下将显示一个新字 `_tenantId` 段。 在“ **[!UICONTROL 字段属性]**”下，提供字段的字段名称和显示名称，并将其类型设置为“[!UICONTROL 字符串]”。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，选择“ **[!UICONTROL 应用]**”。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新后 `favoriteHotel` 的字段将显示在画布中。 选择 **[!UICONTROL 保存]** ，以完成对模式所做的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源模式定义关系字段 {#relationship-field}

在源模式定义了专用的引用字段后，您可以将其指定为关系字段。

在画布 `favoriteHotel` 中选择字段，然后在字段属性下 **[!UICONTROL 向下滚动]** ，直到 **[!UICONTROL 出现“关系]** ”复选框。 选中此复选框可显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

选择引用 **[!UICONTROL 模式的下拉]** 框，然后选择关系的目标模式([!DNL Hotels]本例中为“”)。 如果为启用目标模式 [!DNL Profile]，则引 **[!UICONTROL 用标识]** 命名空间字段将自动设置为目标模式的主标识命名空间。 如果模式未定义主标识，则必须从下拉菜单中手动选择您计划使用的命名空间。 完成后 **[!UICONTROL 选择]** “应用”。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

现 `favoriteHotel` 在，该字段在画布中高亮显示为关系，显示目标模式的名称和引用标识命名空间。 选择 **[!UICONTROL 保存]** ，以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过遵循本教程，您已成功地使用创建了两个模式之间的一对一关系 [!DNL Schema Editor]。 有关如何使用API定义关系的步骤，请参阅有关使用 [模式注册表API定义关系的教程](relationship-api.md)。