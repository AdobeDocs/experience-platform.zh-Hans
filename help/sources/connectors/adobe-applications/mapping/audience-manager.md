---
keywords: Experience Platform;home;popular topics;Audience Manager mapping;audience manager mapping
solution: Experience Platform
title: Audience Manager映射字段
topic: overview
description: 下表包含Adobe Audience Manager数据(实时、载入和用户档案数据)中的字段与其对应的XDM字段之间的映射。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Audience Manager映射字段

下表包含Adobe Audience Manager数据(实时、载入和用户档案数据)中的字段与其对应的XDM字段之间的映射。

有关每个XDM [字段的详细信息](../../../../xdm/schema/field-dictionary.md) ，请参阅XDM字段字典。

## 实时数据

类型：实时数据

| 实时数据字段 | XDM字段 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *仅适用于endUserId中存在的命名空间，且仅适用于第一个值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserId —— 仅 *适用于endUserId中存在的命名空间，且仅适用于第一个值。* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType→类型</li><li>制造商→制造商</li><li>marketingName→模型</li><li>modelNumber→model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country→countryCode</li><li>d_state→stateProvince</li><li>d_city→城市</li><li>d_postal→postalCode</li><li>d_lat→ latitude</li><li>d_longitude→经度</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent→ userAgent</li><li>h_accept-language→ acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name→ os名称 </li><li>d_os_version→ os_version</li></ul> |

## 用户档案数据

类型：用户档案XDM

| 用户档案字段 | XDM字段 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
