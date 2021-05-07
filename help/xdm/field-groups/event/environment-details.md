---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；体验事件；字段；模式;模式;模式设计；字段组；字段组；环境;环境详细信息；
solution: Experience Platform
title: 环境详细信息模式字段组
topic-legacy: overview
description: 此文档概述了ExperienceEvent环境详细信息模式字段组。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---


# [!UICONTROL Environment Details] 模式字段组

>[!NOTE]
>
>多个模式字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL Environment Details] 是类的标准模式字段组，用 [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) 于捕获与体验事件相关的环境详细信息（如设备详细信息、浏览器信息、本地时间和其他地理信息）。

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [设备](../../data-types/device.md) | 描述可跨会话跟踪（通常由cookies跟踪）的已识别设备、应用程序或设备浏览器实例。 |
| `environment` | [环境](../../data-types/environment.md) | 描述事件观测的情境情境，特别是详细描述网络或软件版本等暂时信息。 |
| `placeContext` | [放置上下文](../../data-types/place-context.md) | 描述与事件观测相关的暂态情况。 示例包括特定于区域设置的信息，如天气、当地时间、流量、一周中的某天、工作日与假日以及工作时间。 |

有关字段组的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
