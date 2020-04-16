---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 受众管理器映射字段
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# 受众管理器映射字段

下表包含Adobe受众管理器数据(实时、载入和用户档案数据)中的字段与其对应的XDM字段之间的映射。

有关每个XDM字 [段的更多信息](../../../xdm/schema/field-dictionary.md) ，请参阅XDM字段词典。

## 实时数据

类型：实时数据

| 实时数据字段 | XDM字段 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *仅适用于endUserId中存在的命名空间，且仅适用于第一个值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds —— 仅适 *用于endUserId中存在的命名空间，且仅适用于第一个值。* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType→类型</li><li>制造商→制造商</li><li>marketingName→model</li><li>modelNumber→模型</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country→countryCode</li><li>d_state→stateProvince</li><li>d_city→城市</li><li>d_postal→postalCode</li><li>d_lat→纬度</li><li>d_longitude→经度</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent→userAgent</li><li>h_accept-language→acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name→ os名称 </li><li>d_os_version→os_version</li></ul> |
| `Signals` | ExperienceEvent.signals |

## 入站数 **据（已弃用）**

类型：ExperienceEvent

| 入站字段 | XDM字段 |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] 入站字段计划在将来的版本中弃用。

## 用户档案数据

类型：用户档案XDM

| 用户档案字段 | XDM字段 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
