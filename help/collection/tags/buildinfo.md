---
title: buildInfo
description: 获取有关在网站上实施的标记版本的信息。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

`_satellite.buildInfo`对象包含有关已实现的标记属性生成的信息。 此对象在调试频繁的内部版本时最有用，可确保您使用的是最新版本。

```ts
readonly _satellite.buildInfo: BuildInfo
```

## 可用字段

调用此对象时，可以使用以下字段。

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **`minified`** | `boolean` | 指示库是否已缩小。 生产内部版本一般是缩小的(`true`)，而开发和暂存内部版本一般不是(`false`)。 |
| **`buildDate`** | `string (ISO-8601 datetime)` | 生成和发布JavaScript文件的日期和时间。 |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine)是Adobe的引擎，用于处理标记规则并将逻辑委派给标记扩展。 此字段包含用于发布标记属性的Turbine构建的日期和时间。 |
| **`turbineVersion`** | `string` | 用于构建和发布标记属性的Turbine版本。 |

`_satellite._container.buildInfo`中也包含类似的信息。 有关详细信息，请参阅[`_container`](container.md)。
