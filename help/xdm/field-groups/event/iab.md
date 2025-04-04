---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；iab；tcf；同意；
solution: Experience Platform
title: IAB TCF 2.0事件架构的同意字段组
description: 了解XDM ExperienceEvent类的IAB TCF 2.0同意架构字段组。
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# 事件架构的[!UICONTROL IAB TCF 2.0同意]字段组

>[!IMPORTANT]
>
>本文档介绍XDM ExperienceEvent类的[!UICONTROL IAB TCF 2.0 Consent]架构字段组。 仅当要跟踪一段时间内同意更改事件时，才应使用此字段组。
>
>请注意，在事件数据中记录的同意值不遵循自动实施工作流。 为了进行自动实施，必须将同意值引入XDM个人配置文件类并为实时客户配置文件启用。
>
>有关用于XDM个人资料类的字段组，请改为参阅以下[文档](../profile/iab.md)。

[!UICONTROL IAB TCF 2.0同意]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于捕获带有时间戳的系列IAB同意字符串，以跟踪一段时间内同意更改的模式。

![](../../images/field-groups/iab-event.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `consentStrings` | [同意字符串的数组](../../data-types/consent-string.md) | 与事件关联的同意字符串值的数组。 |

{style="table-layout:auto"}

有关此字段组用例的更多信息，请参阅Experience Platform](../../../landing/governance-privacy-security/consent/iab/overview.md)中支持[IAB TCF 2.0的指南。 有关字段组本身的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
