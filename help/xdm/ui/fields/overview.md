---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；字段；
solution: Experience Platform
title: 在UI中定义XDM字段
description: 了解如何在Experience Platform用户界面中定义XDM字段。
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 3%

---

# 在UI中定义XDM字段

Adobe Experience Platform用户界面中的[!DNL Schema Editor]允许您在自定义体验数据模型(XDM)类和混合中定义自己的字段。 本指南介绍了在UI中定义XDM字段的步骤，包括每个字段类型的可用配置选项。

## 先决条件

本指南要求对XDM系统有充分的了解。 有关Experience Platform生态系统中XDM角色的介绍，请参阅[XDM概述](../../home.md)以及模式合成](../../schema/composition.md)基础知识[，了解类和混合如何将字段贡献给XDM模式。

虽然本指南不是必需的，但建议您也要按照有关在UI](../../tutorials/create-schema-ui.md)中编写模式的教程来熟悉[!DNL Schema Editor]的各种功能。[

## 选择要向{#select-resource}添加字段的资源

要在UI中定义新的XDM字段，必须首先在[!DNL Schema Editor]中打开模式。 根据[!DNL Schema Library]中当前可用的模式，您可以选择[创建新模式](../resources/schemas.md#create)或[选择现有模式以编辑](../resources/schemas.md#edit)。

打开[!DNL Schema Editor]后，使用左边栏选择要为其定义字段的类或混音。 如果资源是您的组织定义的自定义资源，则用于添加或编辑字段的控件将显示在画布中。 这些控件显示在模式名称旁边，以及在选定类或混合下定义的任何对象类型字段。

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>如果您选择的类或混音是Adobe提供的核心资源，则无法编辑它，因此将不显示上面显示的控件。 如果要向中添加字段的模式基于核心XDM类，并且不包含任何自定义混音，则可以[创建新的混音](../resources/mixins.md#create)以添加到模式。

要向资源添加新字段，请在画布中模式名称旁边或要定义字段的对象类型字段旁边选择加号(+)**图标。**

![](../../images/ui/fields/overview/plus-icon.png)

## 为资源{#define}定义字段

在选择&#x200B;**加号(+)**&#x200B;图标后，画布中会出现一个&#x200B;**[!UICONTROL New field]**，它位于根级对象中，该对象与您的唯一租户ID同名（在以下示例中显示为`_tenantId`）。 通过自定义类和混合添加到模式的所有字段将自动放置在此命名空间中，以防止与Adobe提供的类和混合中的其他字段发生冲突。

![](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL Field properties]**&#x200B;下的右边栏中，您可以配置新字段的详细信息。 每个字段都需要以下信息：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL Field name] | 字段的唯一描述性名称。 请注意，保存模式后，无法更改字段的名称。<br><br>最好用camelCase写入该名称。它可能包含字母数字、短划线或下划线字符，但&#x200B;**不能**&#x200B;带下划线的开始。<ul><li>**正确**:  `fieldName`</li><li>**可接受** `field_name2`: `Field-Name`、  `field-name_3`</li><li>**不正确**:  `_fieldName`</li></ul> |
| [!UICONTROL Display name] | 这个领域的人性化名称。 |
| [!UICONTROL Type] | 字段将包含的数据类型。 从此下拉菜单中，您可以选择XDM支持的[标准标量类型](../../schema/field-constraints.md)之一，或之前在[!DNL Schema Registry]中定义的多字段[数据类型](../resources/data-types.md)之一。<br><br>您还可以选择以 **[!UICONTROL Advanced type search]** 搜索和筛选现有数据类型，并更轻松地查找所需类型。 |

您还可以为字段提供可选的人可读&#x200B;**[!UICONTROL Description]**，以提供有关字段预期用例的更多上下文。

>[!NOTE]
>
>根据您为字段选择的&#x200B;**[!UICONTROL Type]**，其他配置控件可能会显示在右边栏中。 有关这些控件的详细信息，请参见[类型特定字段属性](#type-specific-properties)的部分。
>
>右边栏还提供用于指定特殊字段类型的复选框。 有关详细信息，请参阅[特殊字段类型](#special)一节。

配置完字段后，选择&#x200B;**[!UICONTROL Apply]**。

![](../../images/ui/fields/overview/field-details.png)

画布会更新以显示字段的名称和类型，除了其他属性，右边栏现在还列表字段的路径。

![](../../images/ui/fields/overview/field-added.png)

您可以继续执行上述步骤，向模式添加更多字段。 保存模式后，如果对基类和混合进行了任何更改，也会保存它们。

>[!NOTE]
>
>您对某个模式的混音或类所做的任何更改将反映在雇佣它们的所有其他模式中。

## 类型特定字段属性{#type-specific-properties}

定义新字段时，根据您为该字段选择的&#x200B;**[!UICONTROL Type]**，其他配置选项可能显示在右边栏中。 下表概述了这些附加字段属性及其兼容类型：

| 字段属性 | 兼容类型 | 描述 |
| --- | --- | --- |
| [!UICONTROL Default value] | [!UICONTROL String], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Integer], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolean] | 一个默认值，如果在摄取期间未提供其他值，则将分配给此字段。 此值必须与字段的选定类型一致。 |
| [!UICONTROL Pattern] | [!UICONTROL String] | 一个[常规表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)，该字段的值必须符合它，才能在摄取期间被接受。 |
| [!UICONTROL Format] | [!UICONTROL String] | 从列表预定义格式中选择值必须符合的字符串。 可用格式包括： <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | 字符串必须包含的最小字符数，才能在摄取过程中接受该值。 |
| [!UICONTROL Maximum length] | [!UICONTROL String] | 字符串必须包含的最大字符数，才能在摄取过程中接受该值。 |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | 在摄取期间接受的多次的最小值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，“[!UICONTROL Exclusive minimum value]”约束必须留空。 |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | 在摄取期间接受的多次的最大值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，“[!UICONTROL Exclusive maximum value]”约束必须留空。 |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | 在摄取期间接受的多次的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 使用此约束时，“[!UICONTROL Minimum value]”（非独占）约束必须留空。 |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | 在摄取期间接受的多次的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 使用此约束时，“[!UICONTROL Maximum value]”（非独占）约束必须留空。 |

## 特殊字段类型{#special}

右边栏提供了多个复选框，用于为选定字段指定特殊角色。 其中一些选项的使用案例涉及有关数据建模策略以及您打算如何使用下游平台服务的重要考虑事项。

要进一步了解这些特殊类型，请参阅以下文档：

* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) （仅适用于字符串字段）
* [[!UICONTROL Relationship]](./relationship.md) （仅适用于字符串字段）

虽然从技术上讲不是特殊字段类型，但还建议您访问[定义对象类型字段](./object.md)的指南，进一步了解如果您的模式结构，定义嵌套子字段。

## 后续步骤

本指南概述了如何在UI中定义XDM字段。 请记住，只能通过使用类和混合将字段添加到模式。 要进一步了解如何在UI中管理这些资源，请参阅有关创建和编辑[类](../resources/classes.md)和[mixins](../resources/mixins.md)的指南。

有关[!UICONTROL Schemas]工作区功能的详细信息，请参阅[[!UICONTROL Schemas]工作区概述](../overview.md)。
