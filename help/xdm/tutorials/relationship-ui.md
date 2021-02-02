---
keywords: Experience Platform；主题；主题；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；用户界面；
solution: Experience Platform
title: 使用模式模式编辑器定义两个模式之间的关系
description: 此文档提供了一个教程，用于使用Experience Platform用户界面中的模式编辑器定义两个模式之间的关系。
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# 使用[!DNL Schema Editor]定义两个模式之间的关系

了解不同渠道客户之间的关系及其与您品牌的互动是Adobe Experience Platform的重要部分。 在[!DNL Experience Data Model](XDM)模式的结构中定义这些关系使您能够获得对客户数据的复杂洞察。

虽然模式关系可以通过使用合并模式和[!DNL Real-time Customer Profile]来推断，但这仅适用于共享同一类的模式。 要在属于不同类的两个模式之间建立关系，必须向源模式添加专用关系字段，该字段引用目标模式的标识。

此文档提供了一个教程，用于使用[!DNL Experience Platform]用户界面中的模式编辑器定义两个模式之间的关系。 有关使用API定义模式关系的步骤，请参阅教程[中使用模式注册表API](relationship-api.md)定义关系。

## 入门指南

本教程要求您在[!DNL Experience Platform] UI中对[!DNL XDM System]和模式编辑器有正确的了解。 在开始本教程之前，请查阅以下文档：

* [Experience Platform中的XDM系统](../home.md):XDM及其实施概述 [!DNL Experience Platform]。
* [模式合成基础](../schema/composition.md):介绍XDM模式的构件。
* [使用以下图标创建模式 [!DNL Schema Editor]](create-schema-ui.md):一个教程，其中介绍使用的基础知 [!DNL Schema Editor]识。

## 定义源和目标模式

您应已创建将在关系中定义的两个模式。 为了进行演示，本教程在组织的忠诚度项目(在“[!DNL Loyalty Members]”模式中定义)的成员与其最喜爱的酒店(在“[!DNL Hotels]”模式中定义)之间建立了关系。

>[!IMPORTANT]
>
>要建立关系，两个模式都必须定义主身份，并为[!DNL Real-time Customer Profile]启用。 如果您需要有关如何相应配置模式的指导，请参阅模式创建教程中的[启用用户档案](./create-schema-ui.md#profile)一节。

模式关系由&#x200B;**源模式**&#x200B;中的专用字段表示，该专用字段引用&#x200B;**目标模式**&#x200B;中的另一个字段。 在接下来的步骤中，“[!DNL Loyalty Members]”将作为源模式，而“[!DNL Hotels]”将作为目标模式。

为便于参考，以下各节将介绍本教程中在定义关系之前使用的每个模式的结构。

### [!DNL Loyalty Members] 模式

源模式“[!DNL Loyalty Members]”基于[!DNL XDM Individual Profile]类，是教程中为[在UI](create-schema-ui.md)中创建模式而构建的模式。 它在其`_tenantId`命名空间下包含一个`loyalty`对象，该对象包括若干特定于忠诚度的字段。 其中一个字段`loyaltyId`在[!UICONTROL 电子邮件]模式下充当该命名空间的主要标识。 如&#x200B;**[!UICONTROL 模式属性]**&#x200B;下所示，此模式已启用以在[!DNL Real-time Customer Profile]中使用。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 模式

目标模式“[!DNL Hotels]”基于自定义“[!DNL Hotels]”类，并包含描述酒店的字段。 在自定义`hotelId`模式下，`hotelId`字段用作该命名空间的主标识。 与[!DNL Loyalty Members]模式一样，[!DNL Real-time Customer Profile]也启用了此模式。

![](../images/tutorials/relationship/hotels.png)

## 创建关系混合

>[!NOTE]
>
>仅当源模式没有专用的字符串类型字段用作目标模式的引用时，才需要执行此步骤。 如果此字段已在源模式中定义，请跳到定义关系字段](#relationship-field)的下一步。[

要定义两个模式之间的关系，源模式必须有一个专用字段，用作对目标模式的引用。 您可以通过创建新混音将此字段添加到源模式。

开始，在&#x200B;**[!UICONTROL Mixins]**&#x200B;部分选择&#x200B;**[!UICONTROL 添加]**。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

出现[!UICONTROL 添加混音]对话框。 从此处，选择&#x200B;**[!UICONTROL 新建混音]**。 在显示的文本字段中，输入新混音的显示名称和说明。 完成后，选择&#x200B;**[!UICONTROL 添加mixin]**。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

画布将重新出现，“[!DNL Favorite Hotel]”显示在&#x200B;**[!UICONTROL Mixins]**&#x200B;部分。 选择混音名称，然后选择根级别`Loyalty Members`字段旁的&#x200B;**[!UICONTROL 添加字段]**。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中的`_tenantId`命名空间下将显示新字段。 在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下，提供字段名和显示名称，并将其类型设置为“[!UICONTROL 字符串]”。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，选择&#x200B;**[!UICONTROL 应用]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的`favoriteHotel`字段将显示在画布中。 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成对模式所做的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源模式{#relationship-field}定义关系字段

在源模式定义了专用的引用字段后，您可以将其指定为关系字段。

在画布中选择`favoriteHotel`字段，然后在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下向下滚动，直到出现&#x200B;**[!UICONTROL 关系]**&#x200B;复选框。 选中此复选框可显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

选择&#x200B;**[!UICONTROL 引用模式]**&#x200B;的下拉列表，并选择关系的目标模式（本例中为“[!DNL Hotels]”）。 如果为[!DNL Profile]启用目标模式，则&#x200B;**[!UICONTROL 引用标识命名空间]**&#x200B;字段将自动设置为目标模式的主标识命名空间。 如果模式未定义主标识，则必须从下拉菜单中手动选择您计划使用的命名空间。 完成后，选择&#x200B;**[!UICONTROL 应用]**。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

`favoriteHotel`字段现在在画布中以关系突出显示，显示目标模式的名称和引用标识命名空间。 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过遵循本教程，您使用[!DNL Schema Editor]成功创建了两个模式之间的一对一关系。 有关如何使用API定义关系的步骤，请参阅教程[中的使用模式注册表API](relationship-api.md)定义关系。