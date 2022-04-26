---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；字段；
solution: Experience Platform
title: 在UI中定义XDM字段
description: 了解如何在Experience Platform用户界面中定义XDM字段。
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 1d4eba9f566dc1926afd7886c6ad2808ed91ea13
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 4%

---

# 在UI中定义XDM字段

的 [!DNL Schema Editor] 在Adobe Experience Platform用户界面中，您可以在自定义体验数据模型(XDM)类和架构字段组中定义自己的字段。 本指南介绍了在UI中定义XDM字段的步骤，包括每个字段类型的可用配置选项。

## 先决条件

本指南需要对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [架构组合基础知识](../../schema/composition.md) 了解类和字段组如何为XDM模式贡献字段。

虽然本指南不是必需的，但建议您也要遵循 [在UI中合成架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 选择要将字段添加到的资源 {#select-resource}

要在UI中定义新的XDM字段，您必须先在 [!DNL Schema Editor]. 根据您当前在 [!DNL Schema Library]，您可以选择 [创建新模式](../resources/schemas.md#create) 或 [选择要编辑的现有架构](../resources/schemas.md#edit).

在您 [!DNL Schema Editor] 打开后，用于添加或编辑字段的控件将显示在画布中。 这些控件显示在架构名称旁边，以及在选定类或字段组下定义的任何对象类型字段。

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果尝试将字段添加到标准字段组提供的对象，则该字段组将转换为自定义字段组，并且原始字段组将不再可用。 请参阅 [向标准字段组添加字段](../resources/schemas.md#custom-fields-for-standard-groups) 有关更多信息，请参阅架构UI指南。

要向资源添加新字段，请选择 **加号(+)** 图标（位于画布中架构名称的旁边）或要在下定义字段的object-type字段旁边。

![](../../images/ui/fields/overview/plus-icon.png)

根据您是直接将字段添加到架构还是其组成类和字段组，添加该字段的所需步骤会有所不同。 本文档的其余部分重点介绍如何配置字段的属性，而不管该字段在架构中的显示位置。 有关字段可添加到架构的不同方式的更多信息，请参阅架构UI指南中的以下部分：

* [向字段组添加字段](../resources/schemas.md#add-fields)
* [将字段直接添加到架构](../resources/schemas.md#add-individual-fields)

## 定义字段的属性 {#define}

选择 **加号(+)** 图标， **[!UICONTROL 新建字段]** 显示在画布中，它位于与您的独特租户ID同名的对象中(显示为 `_tenantId` )。 添加到架构的所有自定义字段都会自动放置在此命名空间内，以防止与Adobe提供的类和字段组中的其他字段发生冲突。

![](../../images/ui/fields/overview/new-field.png)

在右边栏的 **[!UICONTROL 字段属性]**，则可以配置新字段的详细信息。 每个字段都需要以下信息：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 字段名称] | 字段的唯一描述性名称。 请注意，保存架构后，无法更改字段名称。<br><br>理想情况下，该名称应使用camelCase写入。 它可能包含字母数字、短划线或下划线字符，但 **不能** 以下划线开头。<ul><li>**正确**: `fieldName`</li><li>**可接受：** `field_name2`, `Field-Name`, `field-name_3`</li><li>**错误**: `_fieldName`</li></ul> |
| [!UICONTROL 显示名称] | 字段的人类易记名称。 |
| [!UICONTROL 类型] | 字段将包含的数据类型。 从此下拉菜单中，您可以选择 [标准标量类型](../../schema/field-constraints.md) 受XDM或多字段之一支持 [数据类型](../resources/data-types.md) 之前在 [!DNL Schema Registry].<br><br>您还可以选择 **[!UICONTROL 高级类型搜索]** 搜索和筛选现有数据类型，并更轻松地找到所需类型。 |

{style=&quot;table-layout:auto&quot;}

您还可以提供可选的可供用户读取的 **[!UICONTROL 描述]** 到字段以提供更多有关字段预期用例的上下文。

>[!NOTE]
>
>根据 **[!UICONTROL 类型]** 您为字段选择了，其他配置控件可能会显示在右边栏中。 请参阅 [类型特定的字段属性](#type-specific-properties) 以了解有关这些控件的更多信息。
>
>右边栏还提供用于指定特殊字段类型的复选框。 请参阅 [特殊字段类型](#special) 以了解更多信息。

配置完字段后，选择 **[!UICONTROL 应用]**.

![](../../images/ui/fields/overview/field-details.png)

画布会更新以显示字段的名称和类型，除了列出其他属性外，右边栏现在还会列出字段的路径。

![](../../images/ui/fields/overview/field-added.png)

您可以继续按照上述步骤向架构添加更多字段。 保存架构后，如果对其进行了任何更改，也会保存其基类和字段组。

>[!NOTE]
>
>您对某个架构的字段组或类所做的任何更改都将反映在使用它们的所有其他架构中。

## 类型特定的字段属性 {#type-specific-properties}

定义新字段时，其他配置选项可能会显示在右边栏中，具体取决于 **[!UICONTROL 类型]** 选择字段。 下表概述了这些附加的字段属性及其兼容类型：

| 字段属性 | 兼容类型 | 描述 |
| --- | --- | --- |
| [!UICONTROL 默认值] | [!UICONTROL 字符串], [!UICONTROL 双精度], [!UICONTROL 长], [!UICONTROL 整数], [!UICONTROL 短], [!UICONTROL 字节], [!UICONTROL 布尔值] | 一个默认值，如果在摄取期间未提供任何其他值，则将分配给此字段。 此值必须符合字段的选定类型。 |
| [!UICONTROL 图案] | [!UICONTROL 字符串] | A [正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) 此字段的值必须符合，才能在摄取期间接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字符串] | 从值必须符合的字符串的预定义格式列表中进行选择。 可用格式包括： <ul><li>[[!UICONTROL 日期时间]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 电子邮件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主机名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小长度] | [!UICONTROL 字符串] | 要在摄取期间接受值，字符串必须包含的最小字符数。 |
| [!UICONTROL 最大长度] | [!UICONTROL 字符串] | 要在摄取期间接受值，字符串必须包含的最大字符数。 |
| [!UICONTROL 最小值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最小值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，[!UICONTROL 唯一最小值]“ constraint必须留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最大值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，[!UICONTROL 唯一最大值]“ constraint必须留空。 |
| [!UICONTROL 唯一最小值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最大值。 如果摄取的值与此处输入的值完全匹配，则该值会被拒绝。 使用此约束时，[!UICONTROL 最小值]“（非独占）约束必须留空。 |
| [!UICONTROL 唯一最大值] | [!UICONTROL 双精度] | 在摄取期间接受的双精度类型的最大值。 如果摄取的值与此处输入的值完全匹配，则该值会被拒绝。 使用此约束时，[!UICONTROL 最大值]“（非独占）约束必须留空。 |

{style=&quot;table-layout:auto&quot;}

## 特殊字段类型 {#special}

右边栏提供了多个复选框，用于为选定字段指定特殊角色。 其中某些选项的用例涉及与数据建模策略以及您打算如何使用下游Platform服务有关的重要考虑事项。

要了解有关这些特殊类型的更多信息，请参阅以下文档：

* [[!UICONTROL 必需]](./required.md)
* [[!UICONTROL 数组]](./array.md)
* [[!UICONTROL 枚举]](./enum.md)
* [[!UICONTROL 身份]](./identity.md) （仅适用于字符串字段）
* [[!UICONTROL 关系]](./relationship.md) （仅适用于字符串字段）

虽然从技术上讲，它不是特殊字段类型，但建议您访问 [定义对象类型字段](./object.md) 以了解有关在架构结构中定义嵌套子字段的更多信息。

## 后续步骤

本指南概述了如何在UI中定义XDM字段。 请记住，字段只能通过使用类和字段组添加到架构中。 要详细了解如何在UI中管理这些资源，请参阅有关创建和编辑的指南 [类](../resources/classes.md) 和 [字段组](../resources/field-groups.md).

有关 [!UICONTROL 模式] 工作区，请参阅 [[!UICONTROL 模式] 工作区概述](../overview.md).
