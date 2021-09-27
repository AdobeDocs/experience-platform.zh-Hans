---
keywords: Experience Platform；主页；热门主题；UI;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；创建；关系；参考；引用；
solution: Experience Platform
title: 使用模式编辑器定义两个模式之间的关系
description: 本文档提供了一个教程，用于使用Experience Platform用户界面中的架构编辑器定义两个架构之间的关系。
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 2118dc175b421e856c6b0a33a83a7238f01b7ee3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# 使用[!DNL Schema Editor]定义两个架构之间的关系

>[!NOTE]
>
>如果您使用的是Real-time Customer Data Platform B2B Edition，请参阅[创建B2B关系](./relationship-b2b.md)的指南。

了解客户之间的关系以及客户与品牌在各种渠道中的交互是Adobe Experience Platform的重要组成部分。 在[!DNL Experience Data Model](XDM)架构的结构中定义这些关系使您能够对客户数据进行复杂的分析。

虽然架构关系可以通过使用并集架构和[!DNL Real-time Customer Profile]来推断，但这仅适用于共享同一类的架构。 要在属于不同类的两个架构之间建立关系，必须将专用关系字段添加到源架构中，该源架构引用目标架构的标识。

本文档提供了使用[!DNL Experience Platform]用户界面中的架构编辑器定义两个架构之间的关系的教程。 有关使用API定义架构关系的步骤，请参阅[上的教程（使用架构注册API](relationship-api.md)定义关系）。

## 快速入门

本教程需要对[!DNL XDM System]和[!DNL Experience Platform] UI中的架构编辑器有正确的了解。 在开始使用本教程之前，请查阅以下文档：

* [Experience Platform中的XDM系统](../home.md):XDM及其实施的概 [!DNL Experience Platform]述。
* [架构组合的基础知识](../schema/composition.md):介绍XDM模式的构建基块。
* [使用 [!DNL Schema Editor]](create-schema-ui.md)创建架构：一个教程，其中涵盖使用的基础知 [!DNL Schema Editor]识。

## 定义源架构和目标架构

您应该已经创建了将在关系中定义的两个架构。 出于演示目的，本教程将在组织忠诚度计划（在“[!DNL Loyalty Members]”模式中定义）的成员与其最喜爱的酒店（在“[!DNL Hotels]”模式中定义）之间创建关系。

>[!IMPORTANT]
>
>要建立关系，两个架构都必须定义了主标识并为[!DNL Real-time Customer Profile]启用。 如果需要有关如何相应配置架构的指导，请参阅架构创建教程中关于[启用架构以在用户档案](./create-schema-ui.md#profile)中使用的部分。

架构关系由&#x200B;**源架构**&#x200B;中的专用字段表示，该字段引用&#x200B;**目标架构**&#x200B;中的其他字段。 在后续步骤中，“[!DNL Loyalty Members]”将作为源架构，而“[!DNL Hotels]”将作为目标架构。

出于参考目的，以下各节介绍了在定义关系之前本教程中使用的每个架构的结构。

### [!DNL Loyalty Members] 模式

源架构“[!DNL Loyalty Members]”基于[!DNL XDM Individual Profile]类，是在教程中构建的架构，用于在UI](create-schema-ui.md)中创建架构。 [它在其`_tenantId`命名空间下包含一个`loyalty`对象，该对象包含多个特定于忠诚度的字段。 其中一个字段`loyaltyId`用作[!UICONTROL Email]命名空间下架构的主标识。 如&#x200B;**[!UICONTROL 架构属性]**&#x200B;下所示，此架构已启用，可在[!DNL Real-time Customer Profile]中使用。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 模式

目标架构“[!DNL Hotels]”基于自定义“[!DNL Hotels]”类，并包含描述酒店的字段。

![](../images/tutorials/relationship/hotels.png)

要参与关系，目标架构必须具有主标识。 在此示例中， `hotelId`字段用作主标识，使用自定义“Hotel ID”标识命名空间。

![酒店主要身份](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>要了解如何创建自定义身份命名空间，请参阅[Identity Service文档](../../identity-service/namespaces.md#manage-namespaces)。

设置主标识后，必须为[!DNL Real-time Customer Profile]启用目标架构。

![为配置文件启用](../images/tutorials/relationship/hotel-profile.png)

## 创建关系架构字段组

>[!NOTE]
>
>仅当源架构没有要用作目标架构引用的专用字符串类型字段时，才需要执行此步骤。 如果源架构中已定义此字段，请跳至定义关系字段](#relationship-field)的下一步。[

要定义两个架构之间的关系，源架构必须具有一个专用字段以用作对目标架构的引用。 您可以通过创建新架构字段组将此字段添加到源架构。

首先，在&#x200B;**[!UICONTROL 字段组]**&#x200B;部分中选择&#x200B;**[!UICONTROL Add]**。

![](../images/tutorials/relationship/loyalty-add-field-group.png)

出现[!UICONTROL 添加字段组]对话框。 从此处，选择&#x200B;**[!UICONTROL 创建新字段组]**。 在显示的文本字段中，输入新字段组的显示名称和说明。 完成后，选择&#x200B;**[!UICONTROL 添加字段组]**。

![](../images/tutorials/relationship/create-field-group.png)

画布将重新显示，并在&#x200B;**[!UICONTROL 字段组]**&#x200B;部分中显示“[!DNL Favorite Hotel]”。 选择字段组名称，然后选择根级别`Loyalty Members`字段旁边的&#x200B;**[!UICONTROL 添加字段]**。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中的`_tenantId`命名空间下会显示一个新字段。 在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下，提供字段名称和显示名称，并将其类型设置为“[!UICONTROL String]”。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，选择&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的`favoriteHotel`字段显示在画布中。 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成对架构的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源架构定义关系字段 {#relationship-field}

在源架构定义了专用引用字段后，您可以将其指定为关系字段。

在画布中选择`favoriteHotel`字段，然后在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下向下滚动，直到出现&#x200B;**[!UICONTROL Relationship]**&#x200B;复选框。 选中此复选框可显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

选择&#x200B;**[!UICONTROL 引用架构]**&#x200B;的下拉列表，然后为关系选择目标架构（本示例中为“[!DNL Hotels]”）。 如果为[!DNL Profile]启用了目标架构，则会自动将&#x200B;**[!UICONTROL 引用标识命名空间]**&#x200B;字段设置为目标架构主标识的命名空间。 如果架构未定义主标识，则必须从下拉菜单中手动选择您计划使用的命名空间。 完成后，选择&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

`favoriteHotel`字段现在在画布中以关系的形式突出显示，显示目标架构的名称和引用标识命名空间。 选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过阅读本教程，您已使用[!DNL Schema Editor]成功创建了两个架构之间的一对一关系。 有关如何使用API定义关系的步骤，请参阅[上的教程，该教程使用架构注册表API](relationship-api.md)定义关系。
