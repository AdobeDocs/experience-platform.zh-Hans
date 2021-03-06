---
keywords: Experience Platform；主页；热门主题；Audience Manager映射；受众管理器映射
solution: Experience Platform
title: Adobe Audience Manager源连接器的映射字段
topic-legacy: overview
description: 了解如何将Adobe Audience Manager数据(实时、载入和用户档案数据)映射到Audience Manager源连接器的相应体验数据模型(XDM)字段。
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Audience Manager字段映射

下表包含Adobe Audience Manager数据(实时、载入和用户档案数据)中的字段与其对应的XDM字段之间的映射。

有关每个XDM字段的详细信息，请参阅[ XDM字段词典](../../../../xdm/schema/field-dictionary.md)。

## 实时数据

类型：实时数据

| 实时数据字段 | XDM字段 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *仅适用于endUserId中存在的命名空间，且仅适用于第一个值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *仅适用于endUserId中存在的命名空间，且仅适用于第一个值。* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType →类型</li><li>制造商→制造商</li><li>marketingName →模型</li><li>modelNumber →模型</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city→ city</li><li>d_postal →邮政编码</li><li>d_lat →纬度</li><li>d_longitue →经</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os名称 </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 用户档案数据

类型：用户档案 XDM

| 用户档案字段 | XDM字段 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
