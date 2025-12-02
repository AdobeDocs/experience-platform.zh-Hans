---
title: 公司
description: 获取有关拥有已实施的标记属性的IMS组织的信息。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

`_satellite.company`对象显示有关拥有标记属性的IMS组织的信息。

```ts
readonly _satellite.company: Company
```

## 可用字段

调用此对象时，可以使用以下字段：

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **`orgId`** | `string` | 标记属性的IMS组织ID。 |
| **`dynamicCdnEnabled`** | `boolean` | 确定标记属性是否使用Adobe的动态CDN切换功能。 如果设置为`true`，它将根据访客的位置自动切换访客请求您标记的CDN。 |
| **`cdnAllowList`** | `string[]` | 从中加载标记属性的允许CDN。 |

`_satellite._container.company`中也包含类似的信息。 有关详细信息，请参阅[`_container`](container.md)。
