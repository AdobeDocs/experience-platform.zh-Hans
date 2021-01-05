---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field;
solution: Experience Platform
title: 在UI中定义XDM字段
description: 了解如何在Experience Platform用户界面中定义XDM字段。
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 4%

---


# 在UI中定义XDM字段

Adobe Experience Platform用户界面中的[!DNL Schema Editor]允许您在自定义体验数据模型(XDM)类和混合中定义自己的字段。 本指南介绍在UI中定义XDM字段的步骤，包括每个字段类型的可用配置选项。

## 先决条件

本指南要求对XDM系统有有效的了解。 有关XDM在Experience Platform生态系统中的作用的介绍，请参阅[XDM概述](../../home.md)，以及[模式合成基础知识](../../schema/composition.md)，了解类和混合如何将字段贡献给XDM模式。

虽然本指南不是必需的，但建议您还要按照[在UI](../../tutorials/create-schema-ui.md)中编写模式的教程来熟悉[!DNL Schema Editor]的各种功能。

## 选择要向{#select-resource}添加字段的资源

要在UI中定义新的XDM字段，必须首先在[!DNL Schema Editor]中打开模式。 根据[!DNL Schema Library]中当前可用的模式，您可以选择[创建新模式](../resources/schemas.md#create)或[选择现有模式来编辑](../resources/schemas.md#edit)。

打开[!DNL Schema Editor]后，使用左边栏选择要为其定义字段的类或混音。 如果资源是由您的组织定义的自定义资源，则用于添加或编辑字段的控件将显示在画布中。 这些控件显示在模式的名称旁边，以及在选定类或混合下定义的任何对象类型字段。

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>如果您选择的类或混音是Adobe提供的核心资源，则无法编辑它，因此将不显示上面显示的控件。 如果要向其添加字段的模式基于核心XDM类，并且不包含任何自定义混音，则可以[创建新的混音](../resources/mixins.md#create)以添加到模式。

要向资源添加新字段，请在画布中模式名称旁选择&#x200B;**加号(+)**&#x200B;图标，或在要定义字段的对象类型字段旁边选择。

![](../../images/ui/fields/overview/plus-icon.png)

## 为资源{#define}定义字段

在选择&#x200B;**加号(+)**&#x200B;图标后，画布中将显示一个&#x200B;**[!UICONTROL 新字段]**，该字段位于根级对象中，该对象与您的唯一租户ID同名（在以下示例中显示为`_tenantId`）。 通过自定义类和混音添加到模式的所有字段都会自动放置在此命名空间中，以防止与Adobe提供的类和混音中的其他字段发生冲突。

![](../../images/ui/fields/overview/new-field.png)

在&#x200B;**[!UICONTROL 字段属性]**&#x200B;下的右边栏中，可以配置新字段的详细信息。 每个字段都需要以下信息：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 字段名称] | 字段的唯一描述性名称。 请注意，保存模式后，无法更改字段的名称。<br><br>最好用camelCase写入该名称。它可能包含字母数字、短划线或下划线字符，但&#x200B;**不能**&#x200B;带下划线的开始。<ul><li>**正确**:  `fieldName`</li><li>**可接受** `field_name2`: `Field-Name`、  `field-name_3`</li><li>**不正确**:  `_fieldName`</li></ul> |
| [!UICONTROL 显示名称] | 这个田地的人性化名称。 |
| [!UICONTROL 类型] | 字段将包含的数据类型。 从此下拉菜单中，可以选择XDM支持的[标准标量类型](../../schema/field-constraints.md)中的一种，或选择之前在[!DNL Schema Registry]中定义的多字段[数据类型](../resources/data-types.md)中的一种。<br><br>您还可以选择高 **[!UICONTROL 级类]** 型搜索来搜索和筛选现有数据类型，并更轻松地查找所需类型。 |

您还可以为字段提供可选的人可读&#x200B;**[!UICONTROL 说明]**，以提供有关字段预期用例的更多上下文。

>[!NOTE]
>
>根据您为字段选择的&#x200B;**[!UICONTROL 类型]**，其他配置控件可能显示在右边栏中。 有关这些控件的详细信息，请参见[类型特定字段属性](#type-specific-properties)一节。
>
>右边栏还提供用于指定特殊字段类型的复选框。 有关详细信息，请参见[特殊字段类型](#special)一节。

配置完字段后，选择&#x200B;**[!UICONTROL 应用]**。

![](../../images/ui/fields/overview/field-details.png)

画布将更新以显示字段的名称和类型，除了其他属性，右边栏现在还列表字段的路径。

![](../../images/ui/fields/overview/field-added.png)

您可以继续执行上述步骤，向模式添加更多字段。 保存模式后，如果对其进行了任何更改，也会保存其基类和混合。

>[!NOTE]
>
>您对某个模式的混音或类所做的任何更改将反映在使用它们的所有其他模式中。

## 类型特定字段属性{#type-specific-properties}

定义新字段时，根据您为字段选择的&#x200B;**[!UICONTROL 类型]**，其他配置选项可能显示在右边栏中。 下表概述了这些附加字段属性及其兼容类型：

| 字段属性 | 兼容类型 | 描述 |
| --- | --- | --- |
| [!UICONTROL 默认值] | [!UICONTROL 字符串] [!UICONTROL 、多次]、长 [!UICONTROL 、整数]、短 、、字节   [!UICONTROL 、、布尔值] | 在摄取期间未提供其他值时将分配给此字段的默认值。 此值必须与字段的选定类型一致。 |
| [!UICONTROL 图案] | [!UICONTROL 字符串] | 一个[常规表达式符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)，该字段的值必须符合该符号，才能在摄取过程中被接受。 |
| [!UICONTROL Format] | [!UICONTROL 字符串] | 从预定义格式列表中选择值必须符合的字符串。 可用格式包括： <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 电子邮件]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 主机名]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 最小长度] | [!UICONTROL 字符串] | 字符串必须包含的最少字符数，才能在摄取过程中接受该值。 |
| [!UICONTROL 最大长度] | [!UICONTROL 字符串] | 字符串必须包含的最大字符数，才能在摄取过程中接受该值。 |
| [!UICONTROL 最小值] | [!UICONTROL 双精度] | 在摄取过程中接受的多次的最小值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 |
| [!UICONTROL 最大值] | [!UICONTROL 双精度] | 在摄取过程中接受多次的最大值。 如果摄取的值与此处输入的值完全匹配，则接受该值。 |
| [!UICONTROL 独占最小值] | [!UICONTROL 双精度] | 在摄取过程中接受多次的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 |
| [!UICONTROL 独占最大值] | [!UICONTROL 双精度] | 在摄取过程中接受多次的最大值。 如果摄取的值与此处输入的值完全匹配，则该值将被拒绝。 |

## 特殊字段类型{#special}

右边栏提供了多个复选框，用于为所选字段指定特殊角色。 其中一些选项的使用案例涉及有关数据建模策略以及您打算如何使用下游平台服务的重要考虑事项。

要进一步了解这些特殊类型，请参阅以下文档：

* [[!UICONTROL 必需]](./required.md)
* [[!UICONTROL 阵列]](./array.md)
* [[!UICONTROL 枚举]](./enum.md)
* [[!UICONTROL 标识]](./identity.md) （仅适用于字符串字段）
* [[!UICONTROL 关系]](./relationship.md) （仅适用于字符串字段）

虽然从技术上讲不是特殊字段类型，但还建议您访问[定义对象类型字段](./object.md)的指南，进一步了解如果模式结构，定义嵌套子字段。

## 后续步骤

本指南概述了如何在UI中定义XDM字段。 请记住，字段只能通过使用类和混音来添加到模式。 要进一步了解如何在UI中管理这些资源，请参阅有关创建和编辑[类](../resources/classes.md)和[mixins](../resources/mixins.md)的指南。

有关[!UICONTROL 模式]工作区功能的详细信息，请参阅[[!UICONTROL 模式]工作区概述](../overview.md)。