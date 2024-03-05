---
title: getIdentity
description: 在不发送事件数据的情况下获取访客身份。
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

此 `getIdentity` 命令允许您在不发送事件数据的情况下获取访客ID。 当您运行 `sendEvent` 命令中，如果访客的身份尚不存在，则Web SDK会自动获取该访客的身份。

如果您需要单独的调用来生成访客ID并发送数据，则可以使用此命令。

## 使用Web SDK标记扩展获取身份

Web SDK标记扩展不会通过标记扩展UI提供此命令。 使用JavaScript库语法使用自定义代码编辑器。

## 使用Web SDK JavaScript库获取身份

运行 `getIdentity` 命令。 配置此命令时，可以使用以下选项：

* **`namespaces`**：命名空间数组。 默认值为 `["ECID"]`。有效值包括 `["ECID"]`， `null`，或 `undefined`.
* **`edgeConfigOverrides`**：一个 [数据流配置覆盖对象](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## 响应对象

如果您决定 [处理响应](command-responses.md) 使用此命令，响应对象中提供了以下属性：

* **`identity.ECID`**：包含访客ECID的字符串。
* **`edge.regionID`**：一个整数，表示在获取身份时浏览器点击的Edge Network区域。 它与旧版Audience Manager位置提示相同。
