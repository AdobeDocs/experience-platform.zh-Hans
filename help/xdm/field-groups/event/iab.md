---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；iab;tcf；同意；
solution: Experience Platform
title: IAB TCF 2.0同意架构字段组
topic-legacy: overview
description: 本文档概述了XDM ExperienceEvent类的IAB TCF 2.0同意架构字段组。
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# [!UICONTROL IAB TCF 2.0同意] 架构字段组

>[!IMPORTANT]
>
>本文档介绍XDM ExperienceEvent类的[!UICONTROL IAB TCF 2.0 Consent]架构字段组。 仅当您打算跟踪一段时间内的同意更改事件时，才应使用此字段组。
>
>请注意，在自动执行工作流中，不接受事件数据中记录的同意值。 要自动执行，必须将同意值摄取到XDM个人用户档案类中，并启用“实时客户用户档案”。
>
>对于用于XDM个人配置文件类的字段组，请改为参阅以下[document](../profile/iab.md)。

[!UICONTROL IAB TCF 2.0同意] 是类的标准架构字段组，用 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 于捕获带有时间戳的系列IAB同意字符串，以跟踪随时间推移的同意更改模式。

![](../../images/field-groups/iab-event.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `consentStrings` | [同意字符串](../../data-types/consent-string.md)的数组 | 与事件关联的同意字符串值数组。 |

{style=&quot;table-layout:auto&quot;}

有关此字段组用例的更多信息，请参阅Platform](../../../landing/governance-privacy-security/consent/iab/overview.md)中[IAB TCF 2.0支持指南。 有关字段组本身的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
