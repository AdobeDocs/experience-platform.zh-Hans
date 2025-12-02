---
title: environment
description: 标记属性当前使用的生成环境。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

`_satellite.environment`对象说明标记属性当前使用的生成环境。

```js
readonly _satellite.environment: Environment
```

## 可用字段

调用此对象时，可以使用以下字段。

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| 名称 | 类型 | 描述 |
|---|---|---|
| **`id`** | `string` | 环境的唯一标识符。 您可以通过选择标记UI中&#x200B;**[!UICONTROL Install]**&#x200B;下的[[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md)图标来查找环境ID。 |
| **`stage`** | `development \| staging \| production` | 环境类型。 |
