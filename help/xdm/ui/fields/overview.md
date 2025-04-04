---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；字段；
solution: Experience Platform
title: 在用户界面中定义XDM字段
description: 了解如何在Experience Platform用户界面中定义XDM字段。
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 2%

---

# 在用户界面中定义XDM字段

Adobe Experience Platform用户界面中的[!DNL Schema Editor]允许您在自定义体验数据模型(XDM)类和架构字段组中定义自己的字段。 本指南介绍在UI中定义XDM字段的步骤，包括每种字段类型的可用配置选项。

## 先决条件

本指南要求您对XDM系统有一定的了解。 请参阅[XDM概述](../../home.md)，了解XDM在Experience Platform生态系统中的角色以及[架构组合的基础知识](../../schema/composition.md)，了解类和字段组如何为XDM架构贡献字段。

虽然本指南并非必需，但建议您也学习有关[在UI](../../tutorials/create-schema-ui.md)中撰写架构的教程，以熟悉[!DNL Schema Editor]的各种功能。

## 选择要向其添加字段的资源 {#select-resource}

要在UI中定义新的XDM字段，必须首先在[!DNL Schema Editor]中打开架构。 根据[!DNL Schema Library]中您当前可用的架构，您可以选择[创建新架构](../resources/schemas.md#create)或[选择要编辑的现有架构](../resources/schemas.md#edit)。

打开[!DNL Schema Editor]后，画布中会显示用于添加字段的控件。 这些控件显示在架构的名称旁边，以及在所选类或字段组下定义的任何对象类型字段旁边。

![突出显示添加图标的架构编辑器。](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>如果您尝试将字段添加到由标准字段组提供的对象，则该字段组将转换为自定义字段组，并且原始字段组将不再可用。 有关详细信息，请参阅架构UI指南中有关[将字段添加到标准字段组](../resources/schemas.md#custom-fields-for-standard-groups)的部分。

要向资源添加新字段，请选择画布中架构名称旁边的&#x200B;**加号(+)**&#x200B;图标，或选择您想要在其下定义字段的对象类型字段旁边的图标。

![突出显示添加图标的架构编辑器。](../../images/ui/fields/overview/plus-icon.png)

根据您是将字段直接添加到架构还是其组成类和字段组，添加字段所需的步骤会有所不同。 本文档的其余部分侧重于如何配置字段的属性，而不管该字段在架构中的显示位置如何。 有关可向架构添加字段的不同方式的更多信息，请参阅架构UI指南中的以下部分：

* [将字段添加到字段组](../resources/schemas.md#add-fields)
* [将字段直接添加到架构](../resources/schemas.md#add-individual-fields)

## 定义字段的属性 {#define}

选择&#x200B;**加号(+)**&#x200B;图标后，**[!UICONTROL 无标题字段]**&#x200B;占位符将显示在画布中。

![突出显示具有新无标题字段的架构编辑器。](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下的右边栏中，您可以配置新字段的详细信息。 每个字段都需要以下信息：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 字段名称] | 字段的唯一描述性名称。 请注意，保存架构后，无法更改字段名称。 此值用于标识和引用代码和其他下游应用程序中的字段<br><br>最好以camelCase格式写入名称。 它可包含字母数字或下划线字符，但&#x200B;**不能**&#x200B;以下划线开头。<ul><li>**正确**： `fieldName`</li><li>**可接受：** `field_name2`，`fieldName_3`</li><li>**不正确**： `_fieldName`</li></ul> |
| [!UICONTROL 显示名称] | 字段的显示名称。 该名称将用于表示架构编辑器画布中的字段。 可使用[显示名称切换](../resources/schemas.md#display-name-toggle)将字段名称更改为显示名称。 |
| [!UICONTROL 类型] | 字段将包含的数据类型。 从该下拉菜单中，您可以选择XDM支持的[标准标量类型](../../schema/field-constraints.md)之一，或之前在[!DNL Schema Registry]中定义的多字段[数据类型](../resources/data-types.md)之一。<br>注意：如果选择“映射”数据类型，则会显示[!UICONTROL 映射值类型]属性。<br><br>您还可以选择&#x200B;**[!UICONTROL 高级类型搜索]**&#x200B;来搜索和筛选现有数据类型，并更轻松地找到所需类型。 |
| [!UICONTROL 映射值类型] | 如果选择[!UICONTROL 映射]作为字段的数据类型，则需要此值。 映射的可用值为[!UICONTROL 字符串]和[!UICONTROL 整数]。 从可用选项的下拉列表中选择一个值。<br>要了解有关[特定于类型的字段属性](#type-specific-properties)的更多信息，请参阅定义字段概述。 |

{style="table-layout:auto"}

您还可以选择为每个字段提供说明和注释。 使用&#x200B;**[!UICONTROL Description]**&#x200B;字段添加上下文并描述映射数据类型的功能。 这有助于提高实施的可维护性和可读性。 您还可以添加注释以补充初始描述。 这应该提供更细粒度和更具体的信息，以帮助开发人员在代码库的上下文中有效理解、维护和利用映射。 |


>[!NOTE]
>
>根据您为字段选择的&#x200B;**[!UICONTROL 类型]**，右边栏中可能会显示其他配置控件。 有关这些控件的详细信息，请参阅[特定类型的字段属性](#type-specific-properties)部分。
>
>右边栏还提供了用于指定特殊字段类型的复选框。 有关详细信息，请参阅有关[特殊字段类型](#special)的部分。

完成字段配置后，选择&#x200B;**[!UICONTROL 应用]**。

![架构编辑器的[!UICONTROL 字段属性]部分已突出显示。](../../images/ui/fields/overview/field-details.png)

画布更新以显示新添加的字段，该字段位于以您的唯一租户ID命名的对象中（如下面的示例所示`_tenantId`）。 添加到架构的所有自定义字段都会自动放置在此命名空间中，以防止与Adobe提供的类和字段组中的其他字段冲突。 现在，右边栏会列出字段的路径及其其他属性。

![架构图中的新字段及其在[!UICONTROL 字段属性]分区中的相应路径突出显示。](../../images/ui/fields/overview/field-added.png)

您可以继续按照上述步骤向架构添加更多字段。 保存架构后，如果对其进行了任何更改，也会保存其基类和字段组。

>[!NOTE]
>
>您对一个架构的字段组或类所做的任何更改都将反映在使用这些字段组或类的所有其他架构中。

## 特定于类型的字段属性 {#type-specific-properties}

定义新字段时，根据您为该字段选择的&#x200B;**[!UICONTROL 类型]**，右边栏中可能会显示其他配置选项。 下表概述了这些附加字段属性及其兼容类型：

| 字段属性 | 兼容类型 | 描述 |
| --- | --- | --- |
| [!UICONTROL 映射值类型] | [!UICONTROL 地图] | 仅当您从[!UICONTROL 类型]下拉选项中选择映射值时，[!UICONTROL 映射值类型]属性才会出现在UI中。 您可以在String和Integer值类型之间为Map选择。<br>![Schemas Editor 中类型和映射值类型字段突出显示。](../../images/ui/fields/overview/map-type.png "Schemas Editor 中类型和映射值类型字段突出显示。"){width="100" zoomable="yes"}<br>注意：任何通过API创建的映射数据类型（不是String或Integer类型）均显示为“[!UICONTROL Complex]”数据类型。 您无法通过UI创建“[!UICONTROL 复杂]”数据类型。 |
| [!UICONTROL 模式] | [!UICONTROL 字符串] | 此字段的值必须符合的[正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)才能在摄取期间被接受。 |
| [!UICONTROL 格式] | [!UICONTROL 字符串] | 从预定义的字符串格式列表中选取值必须符合的格式。 可用的格式包括： <ul><li>[[!UICONTROL 日期时间]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 电子邮件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主机名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri引用]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小长度] | [!UICONTROL 字符串] | 字符串必须包含的最小字符数才能在摄取期间接受该值。 |
| [!UICONTROL 最大长度] | [!UICONTROL 字符串] | 字符串必须包含的最大字符数才能在摄取期间接受该值。 |
| [!UICONTROL 最小值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最小值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，“[!UICONTROL 独占最小值]”约束必须留空。 |
| [!UICONTROL 最大值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最大值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 使用此约束时，“[!UICONTROL 独占最大值]”约束必须留空。 |
| [!UICONTROL 独占最小值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 使用此约束时，“[!UICONTROL 最小值]”（非独占）约束必须留空。 |
| [!UICONTROL 独占最大值] | [!UICONTROL 双精度] | 摄取期间接受的Double的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 使用此约束时，“[!UICONTROL 最大值]”（非独占）约束必须留空。 |

{style="table-layout:auto"}

## 特殊字段类型 {#special}

右边栏提供了多个复选框，用于为所选字段指定特殊角色。 其中一些选项的用例涉及有关数据建模策略以及如何使用下游Experience Platform服务的重要注意事项。

要了解有关这些特殊类型的更多信息，请参阅以下文档：

* [地图](./map.md)
* [[!UICONTROL 必需]](./required.md)
* [[!UICONTROL 数组]](./array.md)
* [[!UICONTROL 枚举]](./enum.md)
* [[!UICONTROL 标识]](./identity.md) （仅适用于字符串字段）
* [[!UICONTROL Relationship]](./relationship.md) （仅适用于字符串字段）

虽然从技术上讲不是特殊字段类型，但还建议您访问有关[定义对象类型字段](./object.md)的指南，以了解有关在架构结构中定义嵌套子字段的更多信息。

## 后续步骤

本指南概述了如何在UI中定义XDM字段。 请记住，字段只能通过使用类和字段组添加到架构中。 要详细了解如何在UI中管理这些资源，请参阅有关创建和编辑[类](../resources/classes.md)和[字段组](../resources/field-groups.md)的指南。

有关[!UICONTROL 架构]工作区的功能的更多信息，请参阅[[!UICONTROL 架构]工作区概述](../overview.md)。
