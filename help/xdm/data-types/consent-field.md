---
solution: Experience Platform
title: 通用同意字段数据类型
topic: overview
description: 本文档概述了通用同意字段XDM数据类型。
translation-type: tm+mt
source-git-commit: ebcd8900687b6e91d3f06690a9db0e118bbc3b58
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 2%

---


# [!UICONTROL Generic Consent Field] 数据类型

[!UICONTROL Generic Consent Field] 是一种标准XDM数据类型，用于描述客户针对特定同意首选项的选择。

>[!NOTE]
>
>此模式类型旨在用于使用[[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixin](../mixins/profile/consents.md)作为基线来自定义组织的同意的结构。

![](../images/data-types/consent-field.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `val` | 字符串 | 客户为此用例提供的同意选择。 有关已接受的值和定义，请参阅下表。 |

下表概述了`val`的已接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是 | 客户已选择同意。 换句话说，他们&#x200B;**do**&#x200B;同意使用其数据，如有关同意所示。 |
| `n` | 否 | 客户已选择不同意。 换句话说，他们&#x200B;**不**&#x200B;同意使用其数据，如有关同意所示。 |
| `p` | 待验证 | 系统尚未收到最终同意值。 这通常是需要两步核查的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意将设置为`p`，直到他们选择电子邮件中的链接以验证他们提供了正确的电子邮件地址，此时该同意将更新为`y`。<br><br>如果此同意不使用两组验证过程，则该 `p` 选择可用于指示客户尚未响应同意提示。例如，您可以在客户响应同意提示之前，在网站的第一页自动将值设置为`p`。 在不需要明确同意的司法管辖区，您还可以使用它指示客户未明确选择退出（即假定客户同意）。 |
| `u` | Unknown | 客户的同意信息未知。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的合法商业利益超过数据对个人的潜在伤害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到特定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的切身利益 | 为了保护个人的切身利益，需要为特定目的收集数据。 |
| `PI` | Public Interest | 为特定目的收集数据，是为了公共利益或行使官方权力而进行任务。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)