---
title: 检索Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK检索Experience Cloud ID
description: 了解如何获取Adobe Experience Cloud Id。
seo-description: 了解如何获取Adobe Experience Cloud Id。
translation-type: tm+mt
source-git-commit: 9bd6feb767e39911097bbe15eb2c370d61d9842a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 7%

---


# （测试版）检索Experience Cloud ID

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform Web SDK利用Adobe [Identity Service](../../identity-service/ecid.md)。 这可确保每个设备都有一个唯一标识符，该标识符会保留在设备上，以便页面之间的活动可以绑定在一起。

## 第一方身份

ID服务将标识存储在第一方域的cookie中。 如果ID服务失败，则ID服务将尝试使用域上的HTTP头设置cookie，而ID服务将回退到通过Javascript设置cookie。 Adobe建议您设置CNAME，以确保您的Cookie不受客户端ITP限制的限制。

## 第三方身份

ID服务能够将ID与第三方域(demdex.net)同步，以启用跨站点跟踪。 启用此功能后，将向demdex.net发出对访客（例如，某个没有ECID的人）的第一个请求。 此操作将仅在允许其使用的浏览器（如Chrome）上完成，并由配置中 `thirdPartyCookiesEnabled` 的参数控制。 如果您要全部禁用此功能，请将其 `thirdPartyCookiesEnabled` 设置为false。

## 检索访客ID

如果要使用此唯一ID，请使用该命 `getIdentity` 令。 `getIdentity` 返回当前访客的现有ECID。 对于尚未具有ECID的首次访客，此命令将生成新ECID。

>[!NOTE]
>
>此方法通常用于需要读取Experience Cloud ID的自定义解决方案。 标准实施不使用它。

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## 同步身份

此外，Identity Service允许您使用命令将您自己的标识符与ECID同 `syncIdentity` 步。

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### 同步身份选项

#### 身份命名空间符号

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

对象的键是标识 [命名空间符](../../identity-service/namespaces.md) 。 您可以在Adobe Experience Platform UI的“身份”下找到此列表。

#### `id`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

这是您要为给定命名空间同步的ID。

#### `primary`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 可选 | false |

此标识是否应用作统一用户档案中的主片段。 默认情况下，ECID设置为用户的主标识符。

#### `hashEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 可选 | false |

如果启用，它将使用SHA256哈希对标识进行哈希处理。