---
solution: Experience Platform
title: 通用Personalization首选项字段数据类型
description: 了解通用Personalization首选项字段XDM数据类型。
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# [!UICONTROL 通用Personalization首选项字段]数据类型

[!UICONTROL 通用Personalization首选项字段]是一个标准XDM数据类型，用于描述客户为特定个性化首选项所做的选择。

>[!NOTE]
>
>此数据类型旨在使用[[!UICONTROL 同意和偏好设置]字段组](../field-groups/profile/consents.md)作为基准自定义组织的同意架构的结构。

![](../images/data-types/personalization-field.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `val` | 字符串 | 此个性化用例的客户提供的偏好设置选择。 有关接受的值和定义，请参阅下表。 |

{style="table-layout:auto"}

下表概述了`val`的接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（选择启用） | 客户已选择加入偏好设置。 换言之，他们&#x200B;**同意**&#x200B;使用相关偏好设置所指示的数据。 |
| `n` | 否（选择退出） | 客户已选择退出偏好设置。 换言之，他们&#x200B;**不**&#x200B;同意使用相关偏好设置所指示的数据。 |
| `p` | 等待验证 | 系统尚未收到最终首选项值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，该同意将设置为`p`，直到他们在电子邮件中选择链接以验证他们提供了正确的电子邮件地址，此时同意将更新为`y`。<br><br>如果此首选项未使用两集验证流程，则可能改为使用`p`选项来指示客户尚未响应同意提示。 例如，在客户响应同意提示之前，您可以在网站的第一个页面上自动将值设置为`p`。 在不要求明确同意的司法辖区中，您还可以使用它来表示客户没有明确选择退出（换言之，假定您同意该选项）。 |
| `u` | 未知 | 客户的首选项信息未知。 |
| `dy` | 默认为“是（选择启用）” | 客户本身未提供同意值，默认情况下将视为选择加入（“是”）。 换言之，除非客户另有指示，否则将假定客户同意。<br><br>请注意，如果法律或公司隐私策略的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `dn` | 默认为“否”（选择退出） | 客户本身并未提供同意值，并默认被视为选择退出（“否”）。 换言之，客户被假定已拒绝同意，直到他们表示不同意。<br><br>请注意，如果法律或公司隐私策略的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的合法商业利益大于其对个人造成的潜在危害。 |
| `CT` | 合同 | 为特定目的收集数据是履行与个人的合同义务所必需的。 |
| `CP` | 遵守法律义务 | 为特定目的收集数据是履行企业法律义务所必需的。 |
| `VI` | 个人切身利益 | 为了保护个人的切身利益，必须收集用于特定目的的数据。 |
| `PI` | 公共利益 | 为特定目的收集数据，是为了执行一项符合公众利益或行使官方权力的任务。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
