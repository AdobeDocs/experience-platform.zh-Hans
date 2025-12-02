---
title: getIdentity
description: 在不发送事件数据的情况下获取访客身份。
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---

# `getIdentity`

运行[`sendEvent`](sendevent/overview.md)命令时，Web SDK会自动获取访客身份（如果尚未获取）。 `getIdentity`命令允许您在不发送事件数据的情况下获取访客ID。 如果您需要单独的调用来生成访客ID并发送数据，则可以使用此命令。

`getIdentity`命令将按照以下流程检索`ECID`。

1. 您使用Web SDK调用`getIdentity`或[`appendIdentityToUrl`](appendidentitytourl.md)。
1. Web SDK会等待您提供同意信息。
1. Web SDK检查调用中是否请求了`ECID`命名空间。 默认情况下，`ECID`命名空间始终包括在内。
1. Web SDK读取`kndctr` Cookie并将其值返回为`ECID`（如果存在）。 这仅返回`ECID`值，但不返回`regionId`。
1. 如果未设置`kndctr`标识Cookie，或已请求`"CORE"`命名空间，则Web SDK会向Edge Network发出请求。
1. Edge Network同时返回`ECID`和`regionId`（如果请求，还返回`CORE ID`）。

调用Web SDK的配置实例时运行`getIdentity`命令。 配置此命令时，可以使用以下选项：

* **`namespaces`**：命名空间数组。 默认值为 `["ECID"]`。其他支持的值包括：
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  您可以同时请求`"ECID"`和`"CORE ID"`。 示例：`"namespaces": ["ECID","CORE"]`。

* **`edgeConfigOverrides`**： [数据流配置覆盖对象](configure/edgeconfigoverrides.md)。

```js
alloy("getIdentity",{
  // This command retrieves both ECID and CORE IDs
  "namespaces": ["ECID","CORE"] 
});
```

## 响应对象

如果您决定使用此命令[处理响应](command-responses.md)，则响应对象中提供了以下属性：

* **`identity.ECID`**：包含访客ECID的字符串。
* **`identity.CORE`**：包含访客核心ID的字符串。
* **`edge.regionID`**：一个整数，表示在获取标识时浏览器点击的Edge Network区域。 它与旧版Audience Manager位置提示相同。

```js
// Get the visitor's ECID
alloy('getIdentity').then(result => {
  console.log(result.identity.ECID);
});
```

## 使用Web SDK标记扩展获取身份

Web SDK标记扩展不会通过标记扩展UI提供此命令。 使用JavaScript库语法使用自定义代码编辑器。
