---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；字段；
solution: Experience Platform
title: 在UI中定义XDM字段
description: 了解如何在Experience Platform用户界面中定义XDM字段。
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 4%

---

# 在UI中定义XDM字段

利用Adobe Experience Platform用户界面中的[!DNL Schema Editor]，可在自定义体验数据模型(XDM)类和架构字段组中定义自己的字段。 本指南介绍了在UI中定义XDM字段的步骤，包括每个字段类型的可用配置选项。

## 先决条件

本指南需要对XDM系统有一定的了解。 请参阅[XDM概述](../../home.md) ，了解XDM在Experience Platform生态系统中的角色，以及[架构组合基础知识](../../schema/composition.md) ，以了解类和字段组如何为XDM架构贡献字段。

虽然本指南不是必需的，但建议您也按照[在UI](../../tutorials/create-schema-ui.md)中合成架构的教程，熟悉[!DNL Schema Editor]的各种功能。

## 选择要向{#select-resource}添加字段的资源

要在UI中定义新的XDM字段，必须首先在[!DNL Schema Editor]中打开架构。 根据[!DNL Schema Library]中当前可用的架构，您可以选择[创建新架构](../resources/schemas.md#create)或[选择现有架构以编辑](../resources/schemas.md#edit)。

打开[!DNL Schema Editor]后，使用左边栏选择要为其定义字段的类或字段组。 如果资源是您的组织定义的自定义资源，则画布中会显示用于添加或编辑字段的控件。 这些控件显示在架构名称旁边，以及在选定类或字段组下定义的任何对象类型字段。

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>如果您选择的类或字段组是Adobe提供的核心资源，则无法编辑该资源，因此将不显示上面显示的控件。 如果要将字段添加到的架构基于核心XDM类，并且不包含任何自定义字段组，则可以[创建新字段组](../resources/field-groups.md#create)以添加到架构中。

要向资源中添加新字段，请选择画布中架构名称旁边的&#x200B;**加号(+)**&#x200B;图标，或选择要在下定义字段的对象类型字段旁边的图标。

![](../../images/ui/fields/overview/plus-icon.png)

## 为资源定义字段 {#define}

选择&#x200B;**加号(+)**&#x200B;图标后，画布中会出现一个&#x200B;**[!UICONTROL 新字段]**，它位于根级别对象中，该对象与您的独特租户ID同名（在以下示例中显示为`_tenantId`）。 通过自定义类和字段组添加到架构的所有字段都会自动放置在此命名空间中，以防止与Adobe提供的类和字段组中的其他字段发生冲突。

![](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下的右边栏中，您可以配置新字段的详细信息。 每个字段都需要以下信息：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 字段名称] | 字段的唯一描述性名称。 请注意，保存架构后，无法更改字段名称。<br><br>理想情况下，该名称应使用camelCase写入。它可能包含字母数字、短划线或下划线字符，但&#x200B;**不能**&#x200B;以下划线开头。<ul><li>**正确**:  `fieldName`</li><li>**可接受：** `field_name2`、  `Field-Name`、  `field-name_3`</li><li>**错误**:  `_fieldName`</li></ul> |
| [!UICONTROL 显示名称] | 字段的人类易记名称。 |
| [!UICONTROL 类型] | 字段将包含的数据类型。 从此下拉菜单中，您可以选择XDM支持的[标准标量类型](../../schema/field-constraints.md)之一，或选择之前在[!DNL Schema Registry]中定义的多字段[数据类型](../resources/data-types.md)之一。<br><br>您还可以选择高 **[!UICONTROL 级类]** 型search以搜索和筛选现有数据类型，并更轻松地找到所需类型。 |

{style=&quot;table-layout:auto&quot;}

您还可以为字段提供可选的人类可读&#x200B;**[!UICONTROL 描述]**，以提供有关字段预期用例的更多上下文。

>[!NOTE]
>
>根据您为字段选择的&#x200B;**[!UICONTROL Type]**，其他配置控件可能会显示在右边栏中。 有关这些控件的更多信息，请参阅[类型特定字段属性](#type-specific-properties)中的部分。
>
>右边栏还提供用于指定特殊字段类型的复选框。 有关详细信息，请参阅[特殊字段类型](#special)中的部分。

配置完字段后，选择&#x200B;**[!UICONTROL Apply]**。

![](../../images/ui/fields/overview/field-details.png)

画布会更新以显示字段的名称和类型，除了列出其他属性外，右边栏现在还会列出字段的路径。

![](../../images/ui/fields/overview/field-added.png)

您可以继续按照上述步骤向架构添加更多字段。 保存架构后，如果对其进行了任何更改，也会保存其基类和字段组。

>[!NOTE]
>
>您对某个架构的字段组或类所做的任何更改都将反映在使用它们的所有其他架构中。

## 类型特定的字段属性{#type-specific-properties}

定义新字段时，可能会根据您为该字段选择的&#x200B;**[!UICONTROL Type]**&#x200B;在右边栏中显示其他配置选项。 下表概述了这些附加的字段属性及其兼容类型：

| 字段属性 | 兼容类型 | 描述 |
| --- | --- | --- |
| [!UICONTROL 默认值] | [!UICONTROL 字符串]、 [!UICONTROL 双精度类型]、 [!UICONTROL 长度]、 [!UICONTROL 整数]、 [!UICONTROL 短]、 [!UICONTROL 字节]、 [!UICONTROL 布尔值] | 一个默认值，如果在摄取期间未提供任何其他值，则将分配给此字段。 此值必须符合字段的选定类型。 |
| [!UICONTROL 图案] | [!UICONTROL 字符串] | [正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)，此字段的值必须符合该表达式，才能在摄取期间被接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字符串] | 从值必须符合的字符串的预定义格式列表中进行选择。 可用格式包括： <ul><li>[[!UICONTROL 日期时间]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 电子邮件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主机名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小长度] | [!UICONTROL 字符串] | 要在摄取期间接受值，字符串必须包含的最小字符数。 |
| [!UICONTROL 最大长度] | [!UICONTROL 字符串] | 要在摄取期间接受值，字符串必须包含的最大字符数。 |
| [!UICONTROL 最小值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最小值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，“[!UICONTROL 排他最小值]”约束必须留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最大值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，“[!UICONTROL 排他最大值]”约束必须留空。 |
| [!UICONTROL 唯一最小值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最大值。 如果摄取的值与此处输入的值完全匹配，则该值会被拒绝。 使用此约束时，“[!UICONTROL 最小值]”（非独占）约束必须留空。 |
| [!UICONTROL 唯一最大值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最大值。 如果摄取的值与此处输入的值完全匹配，则该值会被拒绝。 使用此约束时，“[!UICONTROL 最大值]”（非独占）约束必须留空。 |

{style=&quot;table-layout:auto&quot;}

## 特殊字段类型 {#special}

右边栏提供了多个复选框，用于为选定字段指定特殊角色。 其中某些选项的用例涉及与数据建模策略以及您打算如何使用下游Platform服务有关的重要考虑事项。

要了解有关这些特殊类型的更多信息，请参阅以下文档：

* [[!UICONTROL 必需]](./required.md)
* [[!UICONTROL 数组]](./array.md)
* [[!UICONTROL 枚举]](./enum.md)
* [[!UICONTROL 身份]](./identity.md) （仅适用于字符串字段）
* [[!UICONTROL 关系]](./relationship.md) （仅适用于字符串字段）

虽然从技术上讲，不是特殊字段类型，但建议您访问[定义对象类型字段](./object.md)上的指南，以了解有关在架构结构中定义嵌套子字段的更多信息。

## 后续步骤

本指南概述了如何在UI中定义XDM字段。 请记住，字段只能通过使用类和字段组添加到架构中。 要详细了解如何在UI中管理这些资源，请参阅有关创建和编辑[类](../resources/classes.md)和[字段组](../resources/field-groups.md)的指南。

有关[!UICONTROL Schema]工作区功能的更多信息，请参阅[[!UICONTROL Schema]工作区概述](../overview.md)。
