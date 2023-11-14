---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；字段；
solution: Experience Platform
title: 在用户界面中定义XDM字段
description: 了解如何在Experience Platform用户界面中定义XDM字段。
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 765079f084dce316d321fbac5aee9e387373ba00
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 4%

---

# 在用户界面中定义XDM字段

此 [!DNL Schema Editor] 在Adobe Experience Platform用户界面中，您可以在自定义体验数据模型(XDM)类和架构字段组中定义自己的字段。 本指南介绍在UI中定义XDM字段的步骤，包括每种字段类型的可用配置选项。

## 先决条件

本指南要求您对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [模式组合基础](../../schema/composition.md) 了解类和字段组如何向XDM架构贡献字段。

虽然本指南并非必需，但建议您也按照以下内容阅读本教程： [在UI中组合架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 选择要向其添加字段的资源 {#select-resource}

要在UI中定义新的XDM字段，您必须首先在 [!DNL Schema Editor]. 根据您在以下位置当前可用的架构： [!DNL Schema Library]，您可以选择 [创建新架构](../resources/schemas.md#create) 或 [选择要编辑的现有架构](../resources/schemas.md#edit).

一旦拥有 [!DNL Schema Editor] 打开，画布中会显示用于添加字段的控件。 这些控件显示在架构的名称旁边，以及在所选类或字段组下定义的任何对象类型字段旁边。

![](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果您尝试将字段添加到由标准字段组提供的对象，则该字段组将转换为自定义字段组，并且原始字段组将不再可用。 请参阅以下部分 [将字段添加到标准字段组](../resources/schemas.md#custom-fields-for-standard-groups) 有关更多信息，请参阅架构UI指南。

要向资源添加新字段，请选择 **加(+)** 图标（位于画布中的架构名称旁边），或位于要定义其下的字段的对象类型字段旁边。

![](../../images/ui/fields/overview/plus-icon.png)

根据您是将字段直接添加到架构还是其组成类和字段组，添加字段所需的步骤会有所不同。 本文档的其余部分侧重于如何配置字段的属性，而不管该字段在架构中的显示位置如何。 有关可向架构添加字段的不同方式的更多信息，请参阅架构UI指南中的以下部分：

* [将字段添加到字段组](../resources/schemas.md#add-fields)
* [将字段直接添加到架构](../resources/schemas.md#add-individual-fields)

## 定义字段的属性 {#define}

选择 **加(+)** 图标，一个 **[!UICONTROL 无标题的字段]** 占位符显示在画布中。

![](../../images/ui/fields/overview/new-field.png)

在右边栏中，在 **[!UICONTROL 字段属性]**，您可以配置新字段的详细信息。 每个字段都需要以下信息：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 字段名称] | 字段的唯一描述性名称。 请注意，保存架构后，无法更改字段名称。 此值用于标识和引用代码和其他下游应用程序中的字段<br><br>理想情况下，名称应以camelCase编写。 它可包含字母数字、短划线或下划线字符，但它 **可能不会** 从下划线开始。<ul><li>**正确**： `fieldName`</li><li>**可接受：** `field_name2`， `Field-Name`， `field-name_3`</li><li>**不正确**： `_fieldName`</li></ul> |
| [!UICONTROL 显示名称] | 字段的显示名称。 该名称将用于表示架构编辑器画布中的字段。 可使用将字段名称更改为显示名称 [显示名称切换](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL 类型] | 字段将包含的数据类型。 从该下拉菜单中，您可以选择以下任一项 [标准标量类型](../../schema/field-constraints.md) 受XDM或多字段之一支持 [数据类型](../resources/data-types.md) 之前在中定义的 [!DNL Schema Registry].<br><br>您还可以选择 **[!UICONTROL 高级类型搜索]** 搜索和筛选现有数据类型，并更轻松地找到所需类型。 |

{style="table-layout:auto"}

您还可以提供易于用户阅读的可选内容 **[!UICONTROL 描述]** 到字段以提供有关字段预期用例的更多上下文。

>[!NOTE]
>
>根据 **[!UICONTROL 类型]** 您为该字段选择了其他配置控件，则其他配置控件可能会显示在右边栏中。 请参阅以下部分 [特定类型的字段属性](#type-specific-properties) 以了解有关这些控件的详细信息。
>
>右边栏还提供了用于指定特殊字段类型的复选框。 请参阅以下部分 [特殊字段类型](#special) 以了解更多信息。

配置完字段后，选择 **[!UICONTROL 应用]**.

![](../../images/ui/fields/overview/field-details.png)

画布将更新以显示新添加的字段，该字段位于为您唯一租户ID命名的一个对象中(显示为 `_tenantId` （如下例所示）。 添加到架构的所有自定义字段都会自动放置在此命名空间中，以防止与Adobe提供的类和字段组中的其他字段冲突。 现在，右边栏会列出字段的路径及其其他属性。

![](../../images/ui/fields/overview/field-added.png)

您可以继续按照上述步骤向架构添加更多字段。 保存架构后，如果对其进行了任何更改，也会保存其基类和字段组。

>[!NOTE]
>
>您对一个架构的字段组或类所做的任何更改都将反映在使用这些字段组或类的所有其他架构中。

## 特定于类型的字段属性 {#type-specific-properties}

定义新字段时，其他配置选项可能会显示在右边栏中，具体取决于 **[!UICONTROL 类型]** 为字段选择。 下表概述了这些附加字段属性及其兼容类型：

| 字段属性 | 兼容类型 | 描述 |
| --- | --- | --- |
| [!UICONTROL 默认值] | [!UICONTROL 字符串]， [!UICONTROL 多次]， [!UICONTROL 长]， [!UICONTROL 整数]， [!UICONTROL 短]， [!UICONTROL 字节]， [!UICONTROL 布尔型] | 如果在摄取期间没有提供其他值，则分配给此字段的默认值。 此值必须符合字段的选定类型。<br><br>默认值在摄取时不会保存在数据集中，因为它们可能会随着时间的推移而更改。 从数据集中读取数据时，下游平台服务和应用程序会推断架构中设置的默认值。 例如，在使用查询服务查询数据时，如果属性的值为NULL，但缺省值设置为 `5` 在架构级别，查询服务应返回 `5` 而不是NULL。 请注意，此行为当前在所有AEP服务中并不一致。 |
| [!UICONTROL 模式] | [!UICONTROL 字符串] | A [正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) 此字段的值必须符合以便在摄取期间被接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字符串] | 从预定义的字符串格式列表中选取值必须符合的格式。 可用的格式包括： <ul><li>[[!UICONTROL 日期时间]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 电子邮件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主机名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小长度] | [!UICONTROL 字符串] | 字符串必须包含的最小字符数才能在摄取期间接受该值。 |
| [!UICONTROL 最大长度] | [!UICONTROL 字符串] | 字符串必须包含的最大字符数才能在摄取期间接受该值。 |
| [!UICONTROL 最小值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最小值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时， “[!UICONTROL 独占最小值]”约束必须留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最大值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时， “[!UICONTROL 独占最大值]”约束必须留空。 |
| [!UICONTROL 独占最小值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 使用此约束时， “[!UICONTROL 最小值]“（非独占）约束必须留空。 |
| [!UICONTROL 独占最大值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 使用此约束时， “[!UICONTROL 最大值]“（非独占）约束必须留空。 |

{style="table-layout:auto"}

## 特殊字段类型 {#special}

右边栏提供了多个复选框，用于为所选字段指定特殊角色。 其中一些选项的用例涉及有关数据建模策略以及如何使用下游平台服务的重要注意事项。

要了解有关这些特殊类型的更多信息，请参阅以下文档：

* [[!UICONTROL 必需]](./required.md)
* [[!UICONTROL 数组]](./array.md)
* [[!UICONTROL 枚举]](./enum.md)
* [[!UICONTROL 标识]](./identity.md) （仅适用于字符串字段）
* [[!UICONTROL 关系]](./relationship.md) （仅适用于字符串字段）

虽然从技术上讲不是特殊字段类型，但还是建议您在以下位置访问指南： [定义对象类型字段](./object.md) 了解有关在架构结构中定义嵌套子字段的更多信息。

## 后续步骤

本指南概述了如何在UI中定义XDM字段。 请记住，字段只能通过使用类和字段组添加到架构中。 要详细了解如何在UI中管理这些资源，请参阅有关创建和编辑的指南 [类](../resources/classes.md) 和 [字段组](../resources/field-groups.md).

欲知关于 [!UICONTROL 架构] 工作区，请参见 [[!UICONTROL 架构] 工作区概述](../overview.md).
