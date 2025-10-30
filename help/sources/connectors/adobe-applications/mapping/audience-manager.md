---
keywords: Experience Platform；主页；热门主题；Audience Manager映射；audience manager映射
solution: Experience Platform
title: Adobe Audience Manager Source连接器的映射字段
description: 了解如何将Adobe Audience Manager数据（实时、已载入和配置文件数据）映射到Audience Manager源连接器的相应Experience Data Model (XDM)字段。
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Audience Manager字段映射

下表包含Adobe Audience Manager数据（实时、已载入和配置文件数据）中的字段与其对应的XDM字段之间的映射。

有关每个XDM字段的更多信息，请参阅[XDM字段字典](../../../../xdm/schema/field-dictionary.md)。

## 实时数据

类型：实时数据

| 实时数据字段 | XDM字段 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *仅适用于endUserIds中存在的命名空间和第一个值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *仅适用于endUserIds中存在的命名空间和第一个值。* |
| `trait[]` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType→类型</li><li>制造商→制造商</li><li>marketingName →模型</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state→stateProvidle</li><li>d_city → city</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent→userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name →操作系统名称 </li><li>d_os_version → os_version</li></ul> |

{style="table-layout:auto"}

## 配置文件数据

类型：配置文件XDM

| 配置文件字段 | XDM字段 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style="table-layout:auto"}
