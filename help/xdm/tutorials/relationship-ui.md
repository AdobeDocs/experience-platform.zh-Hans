---
keywords: Experience Platform；主页；热门主题；UI;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；创建；关系；参考；引用；
solution: Experience Platform
title: 使用模式编辑器定义两个模式之间的关系
description: 本文档提供了一个教程，用于使用Experience Platform用户界面中的架构编辑器定义两个架构之间的关系。
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 0%

---

# 使用 [!DNL Schema Editor]

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="架构关系"
>abstract="属于不同类的架构可以通过关系字段根据上下文进行链接，从而允许您构建更复杂的分段规则。 有关架构关系的更多信息，请参阅此文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="参考模式"
>abstract="选择要与之建立关系的架构。 此架构可以是与当前架构不同的类。 有关架构关系的更多信息，请参阅此文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="引用标识命名空间"
>abstract="引用架构的主标识字段的命名空间（类型）。 引用架构必须具有已建立的主标识字段才能参与关系。 有关架构关系的更多信息，请参阅此文档。"

了解客户之间的关系以及客户与品牌在各种渠道中的交互是Adobe Experience Platform的重要组成部分。 在 [!DNL Experience Data Model] (XDM)模式允许您对客户数据进行复杂的分析。

而架构关系可以通过使用并集架构和 [!DNL Real-time Customer Profile]，这仅适用于共享同一类的架构。 要在属于不同类的两个架构之间建立关系，必须将专用关系字段添加到源架构中，该源架构引用目标架构的标识。

本文档提供了一个教程，用于使用 [!DNL Experience Platform] 用户界面。 有关使用API定义架构关系的步骤，请参阅 [使用模式注册表API定义关系](relationship-api.md).

>[!NOTE]
>
>有关如何在Real-time Customer Data Platform B2B Edition中创建多对一关系的步骤，请参阅 [创建B2B关系](./relationship-b2b.md).

## 快速入门

本教程需要对 [!DNL XDM System] 和模式编辑器 [!DNL Experience Platform] UI。 在开始使用本教程之前，请查阅以下文档：

* [XDM系统在Experience Platform](../home.md):XDM及其在 [!DNL Experience Platform].
* [架构组合的基础知识](../schema/composition.md):介绍XDM模式的构建基块。
* [使用创建架构 [!DNL Schema Editor]](create-schema-ui.md):一个教程，其中介绍了使用 [!DNL Schema Editor].

## 定义源架构和目标架构

您应该已经创建了将在关系中定义的两个架构。 出于演示目的，本教程将创建组织忠诚度计划(在[!DNL Loyalty Members]“模式”和他们最喜爱的酒店(在“[!DNL Hotels]“架构”)。

>[!IMPORTANT]
>
>要建立关系，两个架构都必须定义了主标识，并启用 [!DNL Real-time Customer Profile]. 请参阅 [启用模式以在用户档案中使用](./create-schema-ui.md#profile) 在架构创建教程中，如果您需要有关如何相应地配置架构的指导。

架构关系由 **源模式** 是指 **目标架构**. 在后续步骤中，“[!DNL Loyalty Members]“ ”将是源架构，而“[!DNL Hotels]“ ”将用作目标架构。

出于参考目的，以下各节介绍了在定义关系之前本教程中使用的每个架构的结构。

### [!DNL Loyalty Members] 模式

源架构“[!DNL Loyalty Members]“ ”基于 [!DNL XDM Individual Profile] 类，是在教程中构建的架构 [在UI中创建架构](create-schema-ui.md). 它包括 `loyalty` 对象 `_tenantId` 命名空间，其中包含多个特定于忠诚度的字段。 其中一个领域， `loyaltyId`，用作下架构的主标识 [!UICONTROL 电子邮件] 命名空间。 如 **[!UICONTROL 架构属性]**，此架构已启用，可在中使用 [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 模式

目标架构“[!DNL Hotels]“ ”基于自定义“[!DNL Hotels]“类”，并包含描述酒店的字段。

![](../images/tutorials/relationship/hotels.png)

要参与关系，目标架构必须具有主标识。 在本例中， `hotelId` 字段用作主标识，并使用自定义“Hotel ID”标识命名空间。

![酒店主要身份](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>要了解如何创建自定义身份命名空间，请参阅 [Identity Service文档](../../identity-service/namespaces.md#manage-namespaces).

设置主标识后，必须为 [!DNL Real-time Customer Profile].

![为配置文件启用](../images/tutorials/relationship/hotel-profile.png)

## 创建关系架构字段组

>[!NOTE]
>
>仅当源架构没有要用作目标架构引用的专用字符串类型字段时，才需要执行此步骤。 如果此字段已在源架构中定义，请跳转到的下一步 [定义关系字段](#relationship-field).

要定义两个架构之间的关系，源架构必须具有一个专用字段以用作对目标架构的引用。 您可以通过创建新架构字段组将此字段添加到源架构。

首先选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 字段组]** 中。

![](../images/tutorials/relationship/loyalty-add-field-group.png)

的 [!UICONTROL 添加字段组] 对话框。 从此处选择 **[!UICONTROL 创建新字段组]**. 在显示的文本字段中，输入新字段组的显示名称和说明。 选择 **[!UICONTROL 添加字段组]** 完成。

![](../images/tutorials/relationship/create-field-group.png)

画布将重新显示为“[!DNL Favorite Hotel]&quot; **[!UICONTROL 字段组]** 中。 选择字段组名称，然后选择 **[!UICONTROL 添加字段]** 根级别旁边 `Loyalty Members` 字段。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中的 `_tenantId` 命名空间。 在 **[!UICONTROL 字段属性]**，提供字段名称和显示名称，并将其类型设置为“[!UICONTROL 字符串]&quot;

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，选择 **[!UICONTROL 应用]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

已更新 `favoriteHotel` 字段。 选择 **[!UICONTROL 保存]** 以完成对架构所做的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源架构定义关系字段 {#relationship-field}

在源架构定义了专用引用字段后，您可以将其指定为关系字段。

>[!NOTE]
>
>以下步骤涵盖如何使用画布中的右边栏控件定义关系字段。 如果您有权访问Real-Time CDP B2B Edition，则还可以使用 [同一对话框](./relationship-b2b.md#relationship-field) 与创建多对一关系时一样。

选择 `favoriteHotel` 字段，然后向下滚动到 **[!UICONTROL 字段属性]** 直到 **[!UICONTROL 关系]** 复选框。 选中此复选框可显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

选择的下拉菜单 **[!UICONTROL 参考模式]** 并选择关系的目标架构(&quot;[!DNL Hotels]”)。 如果为 [!DNL Profile], **[!UICONTROL 引用标识命名空间]** 字段自动设置为目标架构主标识的命名空间。 如果架构未定义主标识，则必须从下拉菜单中手动选择您计划使用的命名空间。 选择 **[!UICONTROL 应用]** 完成。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

的 `favoriteHotel` 字段现在作为关系在画布中突出显示，用于显示目标架构的名称和引用标识命名空间。 选择 **[!UICONTROL 保存]** 以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过阅读本教程，您已使用 [!DNL Schema Editor]. 有关如何使用API定义关系的步骤，请参阅 [使用模式注册表API定义关系](relationship-api.md).
