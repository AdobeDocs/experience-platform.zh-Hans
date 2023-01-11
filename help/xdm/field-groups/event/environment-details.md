---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；环境；环境详细信息；
solution: Experience Platform
title: 环境详细信息架构字段组
description: 本文档概述了ExperienceEvent环境详细信息架构字段组。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL 环境详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 请参阅 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 环境详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获与体验事件相关的环境详细信息，如设备详细信息、浏览器信息、本地时间和其他地理信息。

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [设备](../../data-types/device.md) | 描述可跨会话（通常由Cookie跟踪）跟踪的已识别设备、应用程序或设备浏览器实例。 |
| `environment` | [环境](../../data-types/environment.md) | 描述事件观测的情境背景信息，特别是详细描述过渡信息，如网络或软件版本。 |
| `placeContext` | [放置上下文](../../data-types/place-context.md) | 描述与事件观察相关的临时情况。 示例包括特定于区域设置的信息，如天气、当地时间、流量、一周中的某天、工作日与假日以及工作时间。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
