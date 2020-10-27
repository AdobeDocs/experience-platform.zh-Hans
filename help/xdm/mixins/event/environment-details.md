---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: 环境详细信息混合
topic: overview
description: 此文档概述了ExperienceEvent环境详细信息混合。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---


# [!UICONTROL 环境详细信息] （混合）

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请 [参阅混合名称](../name-updates.md) 更新文档。

[!UICONTROL 环境详细信] 息是类的标准混合 [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) ，用于捕获与体验事件相关的环境详细信息，如设备详细信息、浏览器信息、本地时间和其他地理信息。

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [设备](../../data-types/device.md) | 描述可跨会话跟踪的已识别设备、应用程序或设备浏览器实例，通常由cookie跟踪。 |
| `environment` | [环境](../../data-types/environment.md) | 描述事件观察的情境信息，特别是详细描述诸如网络或软件版本等暂时性信息。 |
| `placeContext` | [放置上下文](../../data-types/place-context.md) | 描述与事件观测相关的瞬态情况。 示例包括特定于区域设置的信息，如天气、当地时间、流量、一周中的某天、工作日与假日以及工作时间。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
