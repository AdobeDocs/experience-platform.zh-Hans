---
title: getIdentity
description: 在不发送事件数据的情况下获取访客身份。
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

`getIdentity`命令允许您在不发送事件数据的情况下获取访客ID。 运行`sendEvent`命令时，如果访客的标识尚不存在，则Web SDK会自动获取该访客的标识。

如果您需要单独的调用来生成访客ID并发送数据，则可以使用此命令。

## 使用Web SDK标记扩展获取身份

Web SDK标记扩展不会通过标记扩展UI提供此命令。 使用JavaScript库语法使用自定义代码编辑器。

## 使用Web SDK JavaScript库获取身份

调用Web SDK的配置实例时运行`getIdentity`命令。 配置此命令时，可以使用以下选项：

* **`namespaces`**：命名空间数组。 默认值为 `["ECID"]`。有效值包括`["ECID"]`、`null`或`undefined`。
* **`edgeConfigOverrides`**： [数据流配置覆盖对象](datastream-overrides.md)。

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## 响应对象

如果您决定使用此命令[处理响应](command-responses.md)，则响应对象中提供了以下属性：

* **`identity.ECID`**：包含访客ECID的字符串。
* **`edge.regionID`**：一个整数，表示在获取标识时浏览器点击的Edge Network区域。 它与旧版Audience Manager位置提示相同。
