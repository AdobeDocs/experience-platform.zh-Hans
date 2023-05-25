---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；iab；tcf；同意；
solution: Experience Platform
title: 事件架构的IAB TCF 2.0同意字段组
description: 本文档概述了XDM ExperienceEvent类的IAB TCF 2.0同意架构字段组。
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0同意] 事件架构的字段组

>[!IMPORTANT]
>
>本文档涵盖 [!UICONTROL IAB TCF 2.0同意] xdm ExperienceEvent类的架构字段组。 仅当您打算跟踪一段时间内同意更改事件时，才应使用此字段组。
>
>请注意，在事件数据中记录的同意值不遵循自动实施工作流程。 为了进行自动实施，同意值必须被摄取到XDM个人配置文件类中，并为实时客户配置文件启用。
>
>有关用于XDM Individual Profile类的字段组，请参阅以下内容 [文档](../profile/iab.md) 而是。

[!UICONTROL IAB TCF 2.0同意] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获带有时间戳的系列IAB同意字符串，以跟踪随时间变化的同意更改模式。

![](../../images/field-groups/iab-event.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `consentStrings` | 数组 [同意字符串](../../data-types/consent-string.md) | 与事件关联的同意字符串值的数组。 |

{style="table-layout:auto"}

请参阅指南，网址为 [平台中的IAB TCF 2.0支持](../../../landing/governance-privacy-security/consent/iab/overview.md) 有关此字段组用例的更多信息。 有关字段组本身的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
