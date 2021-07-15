---
solution: Experience Platform
title: 通用营销首选项字段数据类型
topic-legacy: overview
description: 本文档概述了通用营销首选项字段XDM数据类型。
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---

# [!UICONTROL 通用营销首选项字] 段数据类型

[!UICONTROL 通用营销首] 选项字段是一个标准XDM数据类型，用于描述客户对特定营销首选项的选择。

>[!NOTE]
>
>此数据类型旨在用于使用[[!UICONTROL 同意和首选项]字段组](../field-groups/profile/consents.md)作为基线来自定义组织同意架构的结构。
>
>如果您需要特定营销首选项字段的`subscriptions`映射，则必须改用[营销字段来提供订阅数据类型](./marketing-field-subscriptions.md)。

![](../images/data-types/marketing-field.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `reason` | 字符串 | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |
| `time` | DateTime | 营销首选项更改时的ISO 8601时间戳（如果适用）。 |
| `val` | 字符串 | 客户为此营销用例提供的首选项选择。 有关接受的值和定义，请参阅下表。 |

{style=&quot;table-layout:auto&quot;}

下表概述了`val`的接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是 | 客户已选择使用该首选项。 换言之，他们&#x200B;**do**&#x200B;同意使用其数据，如相关首选项所示。 |
| `n` | 否 | 客户已选择退出该首选项。 换言之，他们&#x200B;**不**&#x200B;同意使用其数据，如相关首选项所示。 |
| `p` | 待验证 | 系统尚未收到最终的偏好值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意将设置为`p`，直到他们选择电子邮件中的链接来验证他们是否提供了正确的电子邮件地址，此时同意将更新为`y`。<br><br>如果此首选项不使用两套验证过程，则 `p` 可以使用选择来指示客户尚未响应同意提示。例如，您可以在客户响应同意提示之前，在网站的首页上自动将值设置为`p`。 在不需要明确同意的司法管辖区中，您还可以使用它来指示客户未明确选择退出（换言之，假设同意）。 |
| `u` | Unknown | 客户的首选项信息未知。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的正当商业利益，超过了这些数据对个人的潜在损害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到指定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的重大利益 | 为了保护个人的重大利益，需要为特定目的收集数据。 |
| `PI` | 公共利益 | 为特定目的收集数据是为了公共利益或行使官方权力而执行一项任务所必需的。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
