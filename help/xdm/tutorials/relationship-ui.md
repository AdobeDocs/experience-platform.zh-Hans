---
keywords: Experience Platform；主页；热门主题；UI；UI；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；创建；关系；引用；引用；
solution: Experience Platform
title: 使用架构编辑器定义两个架构之间的关系
description: 本文档提供了一个教程，介绍如何使用Experience Platform用户界面中的架构编辑器定义两个架构之间的关系。
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 9%

---

# 使用以下方式定义两个架构之间的一对一关系 [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="架构关系"
>abstract="可以通过关系字段对属于不同类的架构进行上下文链接，从而构建更复杂的分段规则。有关架构关系的更多信息，请参阅文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="参考架构"
>abstract="选择要与之建立关系的架构。此架构可以是与当前架构不同的类。有关架构关系的更多信息，请参阅文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="参考标识命名空间"
>abstract="参考架构的主要标识字段的命名空间（类型）。参考架构必须有一个建立的主要标识字段才能参与关系。有关架构关系的更多信息，请参阅文档。"

能够了解客户之间的关系以及客户在不同渠道中与您的品牌的互动是Adobe Experience Platform的重要组成部分。 在的结构中定义这些关系 [!DNL Experience Data Model] (XDM)架构允许您对客户数据获得复杂的见解。

虽然可以通过使用合并架构和来推断架构关系 [!DNL Real-Time Customer Profile]，这仅适用于共享相同类的架构。 要在属于不同类的两个架构之间建立关系，必须在源架构中添加一个专用关系字段，该字段引用其他相关架构的标识。

本文档提供了一个教程，介绍如何使用中的架构编辑器定义两个架构之间的关系。 [!DNL Experience Platform] 用户界面。 有关使用API定义架构关系的步骤，请参阅以下教程： [使用架构注册表API定义关系](relationship-api.md).

>[!NOTE]
>
>有关如何在Adobe Real-time Customer Data Platform B2B版本中创建多对一关系的步骤，请参阅以下指南中的 [创建B2B关系](./relationship-b2b.md).

## 快速入门

本教程需要您实际了解 [!DNL XDM System] 和中的架构编辑器 [!DNL Experience Platform] UI。 在开始本教程之前，请查看以下文档：

* [Experience Platform中的XDM系统](../home.md)：XDM及其在中的实施概述 [!DNL Experience Platform].
* [模式组合基础](../schema/composition.md)：XDM架构的构建块简介。
* [使用创建架构 [!DNL Schema Editor]](create-schema-ui.md)：涵盖使用的基础知识的教程 [!DNL Schema Editor].

## 定义源和引用架构

您应已创建将在关系中定义的两个架构。 出于演示目的，本教程会在组织的忠诚度计划(在“[!DNL Loyalty Members]”架构)和他们最喜爱的酒店(在“[!DNL Hotels]”架构)。

>[!IMPORTANT]
>
>为了建立关系，两个架构都必须定义主身份并启用 [!DNL Real-Time Customer Profile]. 请参阅以下部分： [启用架构以在配置文件中使用](./create-schema-ui.md#profile) 模式创建教程中，如果您需要有关如何相应地配置模式的指导。

架构关系由 **源架构** 指向内的另一个字段 **引用模式**. 在接下来的步骤中， ”[!DNL Loyalty Members]“ ”将是源架构，而“[!DNL Hotels]”将用作参考模式。

以下各节介绍在定义关系之前本教程中使用的每个架构的结构。

### [!DNL Loyalty Members] 架构

源架构»[!DNL Loyalty Members]”基于 [!DNL XDM Individual Profile] 类，包含描述忠诚度计划成员的字段。 其中一个领域， `personalEmail.addess`，用作下的架构的主要标识 [!UICONTROL 电子邮件] 命名空间。 如下所见 **[!UICONTROL 架构属性]**，此架构已支持用于 [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 架构

引用架构»[!DNL Hotels]“基于自定义”[!DNL Hotels]“ ”类，并包含描述酒店的字段。 为了参与关系，引用架构还必须定义并启用主标识 [!UICONTROL 个人资料]. 在这个案例中， `_tenantId.hotelId`充当架构的主要标识，使用自定义&quot;[!DNL Hotel ID]”身份命名空间。

![为配置文件启用](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>要了解如何创建自定义身份命名空间，请参阅 [Identity Service文档](../../identity-service/namespaces.md#manage-namespaces).

## 创建关系字段组

>[!NOTE]
>
>仅当源架构没有专用字符串类型字段用作引用架构主要标识的指针时，才需要执行此步骤。 如果此字段已在源架构中定义，请跳至的下一步 [定义关系字段](#relationship-field).

为了定义两个架构之间的关系，源架构必须有一个专用字段来指示引用架构的主要身份。 您可以通过创建新架构字段组或扩展现有架构字段组，将此字段添加到源架构中。

对于 [!DNL Loyalty Members] 架构，新 `preferredHotel` 将添加字段以指示忠诚度会员访问公司的首选酒店。 首先，选择加号图标(**+**)。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中将显示一个新的字段占位符。 下 **[!UICONTROL 字段属性]**，为字段提供字段名称和显示名称，并将其类型设置为&quot;[!UICONTROL 字符串]“。 下 **[!UICONTROL 分配给]**，选择要扩展的现有字段组，或键入唯一名称以创建新字段组。 在本例中，是新的“[!DNL Preferred Hotel]已创建“ ”字段组。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，选择 **[!UICONTROL 应用]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

已更新 `preferredHotel` 字段显示在画布中，位于 `_tenantId` 对象，因为它是自定义字段。 选择 **[!UICONTROL 保存]** 以完成对架构的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源架构定义关系字段 {#relationship-field}

一旦您的源架构定义了专用引用字段，您就可以将其指定为关系字段。

>[!NOTE]
>
>以下步骤介绍了如何使用画布中的右边栏控件定义关系字段。 如果您有权访问Real-Time CDP B2B版本，还可以使用 [相同对话框](./relationship-b2b.md#relationship-field) 在创建多对一关系时也是如此。

选择 `preferredHotel` 字段，然后向下滚动到 **[!UICONTROL 字段属性]** 直到 **[!UICONTROL 关系]** 复选框。 选中此复选框以显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

选择以下项的下拉列表 **[!UICONTROL 引用架构]** 并为关系选择引用架构(&quot;[!DNL Hotels]在本例中)。 下 **[!UICONTROL 引用身份命名空间]**，选择引用架构的标识字段的命名空间(在本例中， ”[!DNL Hotel ID]“)。 选择 **[!UICONTROL 应用]** 完成后。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

此 `preferredHotel` 字段现在以画布中的关系突出显示，显示引用架构的名称。 选择 **[!UICONTROL 保存]** 以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过阅读本教程，您已使用成功创建了两个架构之间的一对一关系。 [!DNL Schema Editor]. 有关如何使用API定义关系的步骤，请参阅 [使用架构注册表API定义关系](relationship-api.md).
