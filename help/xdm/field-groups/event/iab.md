---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；iab;tcf；同意；
solution: Experience Platform
title: 事件架构的IAB TCF 2.0同意字段组
topic-legacy: overview
description: 本文档概述了XDM ExperienceEvent类的IAB TCF 2.0同意架构字段组。
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0同意] 事件架构的字段组

>[!IMPORTANT]
>
>本文档涵盖 [!UICONTROL IAB TCF 2.0同意] XDM ExperienceEvent类的架构字段组。 仅当您打算跟踪一段时间内的同意更改事件时，才应使用此字段组。
>
>请注意，在自动执行工作流中，不接受事件数据中记录的同意值。 要自动执行，必须将同意值摄取到XDM个人用户档案类中，并启用“实时客户用户档案”。
>
>对于用于XDM个人用户档案类的字段组，请参阅以下内容 [文档](../profile/iab.md) 中。

[!UICONTROL IAB TCF 2.0同意] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获带有时间戳的系列IAB同意字符串，以便跟踪随时间推移的同意更改模式。

![](../../images/field-groups/iab-event.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `consentStrings` | 数组 [同意字符串](../../data-types/consent-string.md) | 与事件关联的同意字符串值数组。 |

{style=&quot;table-layout:auto&quot;}

请参阅 [平台中的IAB TCF 2.0支持](../../../landing/governance-privacy-security/consent/iab/overview.md) 有关此字段组用例的详细信息。 有关字段组本身的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
