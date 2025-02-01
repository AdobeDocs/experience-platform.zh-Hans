---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；环境；环境详细信息；
solution: Experience Platform
title: 环境详细信息架构字段组
description: 了解ExperienceEvent环境详细信息架构字段组。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 2%

---


# [!UICONTROL 环境详细信息]架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../name-updates.md)的文档。

[!UICONTROL 环境详细信息]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于捕获与体验事件相关的环境详细信息信息，如设备详细信息、浏览器信息、本地时间和其他地理信息。

![](../../images/field-groups/environment-details.png){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [设备](../../data-types/device.md) | 描述通常可通过Cookie跨会话跟踪的已识别设备、应用程序或设备浏览器实例。 |
| `environment` | [环境](../../data-types/environment.md) | 描述有关事件观察的情境上下文的信息，特别是详细说明网络或软件版本等临时信息。 |
| `placeContext` | [放置上下文](../../data-types/place-context.md) | 描述与事件观察相关的瞬态情况。 示例包括特定于区域设置的信息，例如天气、当地时间、交通、星期几、工作日与假期以及工作时间。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
