---
title: 检索Experience CloudID
seo-title: Adobe Experience PlatformWeb SDK检索Experience CloudID
description: 了解如何获得Adobe Experience CloudID。
seo-description: 了解如何获得Adobe Experience CloudID。
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 9%

---


# 标识——检索Experience CloudID

Adobe Experience Platform [!DNL Web SDK] 利用 [Adobe标识服务](../../identity-service/ecid.md)。 这可确保每个设备都有一个唯一标识符，该标识符会保留在设备上，以便页面之间的活动可以绑定在一起。

## 第一方身份

该标 [!DNL Identity Service] 识存储在第一方域的cookie中。 尝 [!DNL Identity Service] 试使用域上的HTTP头设置cookie。 如果失败， [!DNL Identity Service] 将返回到通过Javascript设置Cookie。 Adobe建议您设置CNAME，以确保您的Cookie不受客户端ITP限制的限制。

## 第三方身份

该 [!DNL Identity Service] 软件能够将ID与第三方域(demdex.net)同步，以启用跨站点跟踪。 启用此功能后，将向demdex.net发出对访客（例如，某个没有ECID的人）的第一个请求。 此操作将仅在允许其使用的浏览器（如Chrome）上完成，并由配置中 `thirdPartyCookiesEnabled` 的参数控制。 如果您希望全部禁用此功能，请将其 `thirdPartyCookiesEnabled` 设置为false。

## 检索访客ID

如果要使用此唯一ID，请使用该命 `getIdentity` 令。 `getIdentity` 返回当前访客的现有ECID。 对于尚未具有ECID的首次访客，此命令将生成新ECID。

>[!NOTE]
>
>此方法通常用于需要读取ID的自定义解决 [!DNL Experience Cloud] 方案。 标准实施不使用该函数。

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

此外，该 [!DNL Identity Service] 命令还允许您使用命令将您自己的标识符与ECID `syncIdentity` 同步。

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

对象的键是标识 [命名空间符](../../identity-service/namespaces.md) 。 您可以在“身份”下的Adobe Experience Platform用户界面中找到此 [!UICONTROL 列表]。

#### `id`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

这是您要为给定命名空间同步的ID。

#### `authenticationState`

| **类型** | **必需** | **默认值** | **可能值** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 字符串 | 是 | 模糊 | 不明确、已验证和已注销 |

ID的身份验证状态。

#### `primary`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 可选 | false |

确定是否应将此标识用作统一用户档案中的主片段。 默认情况下，ECID设置为用户的主标识符。

#### `hashEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 可选 | false |

如果启用，它将使用SHA256哈希对标识进行哈希处理。
