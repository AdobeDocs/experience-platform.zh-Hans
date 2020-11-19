---
title: 检索Experience CloudID
seo-title: Adobe Experience PlatformWeb SDK检索Experience CloudID
description: 了解如何获得Adobe Experience CloudID。
seo-description: 了解如何获得Adobe Experience CloudID。
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---


# 标识——检索Experience CloudID

Adobe Experience PlatformWeb SDK利用 [Adobe标识服务](../../identity-service/ecid.md)。 这可确保每个设备都有一个唯一标识符，该标识符会保留在设备上，以便页面之间的活动可以绑定在一起。

## 第一方身份

该标 [!DNL Identity Service] 识存储在第一方域的cookie中。 尝 [!DNL Identity Service] 试使用域上的HTTP头设置cookie。 如果失败， [!DNL Identity Service] 将返回到通过Javascript设置Cookie。 Adobe建议您设置CNAME，以确保您的Cookie不受客户端ITP限制的限制。

## 第三方身份

该 [!DNL Identity Service] 软件能够将ID与第三方域(demdex.net)同步，以启用跨站点跟踪。 启用此功能后，将向demdex.net发出对访客（例如，某个没有ECID的人）的第一个请求。 此操作将仅在允许其使用的浏览器（如Chrome）上完成，并由配置中 `thirdPartyCookiesEnabled` 的参数控制。 如果您希望全部禁用此功能，请将其 `thirdPartyCookiesEnabled` 设置为false。

## ID迁移

从使用访客API迁移时，您还可以迁移现有AMCV cookie。 要启用ECID迁移，请在配 `idMigrationEnabled` 置中设置参数。 ID迁移可启用以下用例：

* 当域的某些页面使用访客API，而其他页面使用此SDK时。 为支持此情况，SDK会读取现有AMCV cookie，并使用现有ECID写入新cookie。 此外，SDK会编写AMCV cookies，这样，如果ECID是首先在使用SDK进行指令的页面上获得的，则使用访客API指令的后续页面具有相同的ECID。
* 当Adobe Experience PlatformWeb SDK设置在同时具有访客API的页面上时。 为支持此情况，如果未设置AMCV cookie,SDK将在页面上查找访客API并调用它以获取ECID。
* 当整个站点使用Adobe Experience PlatformWeb SDK且没有访客API时，迁移ECID以便保留返回的访客信息很有用。 在将SDK部署到某 `idMigrationEnabled` 段时间以便迁移大多数访客cookie后，可关闭该设置。

## 检索访客ID

如果要使用此唯一ID，请使用该命 `getIdentity` 令。 `getIdentity` 返回当前访客的现有ECID。 对于尚未具有ECID的首次访客，此命令将生成新ECID。

>[!NOTE]
>
>此方法通常用于需要读取ID的自定义解决 [!DNL Experience Cloud] 方案。 标准实施不使用该函数。

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log(result.identity.ECID);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## 同步身份

>[!NOTE]
>
>除了 `syncIdentity` 散列功能外，在版本2.1.0中也删除了该方法。 如果您使用版本2.1.0+并且希望同步身份，则可以直接在命令的选项( `xdm` 位于字 `sendEvent` 段下)中发送 `identityMap` 它们。

此外，该 [!DNL Identity Service] 命令还允许您使用命令将您自己的标识符与ECID `syncIdentity` 同步。

>[!NOTE]
>
>强烈建议在每个命令上传递所有可用 `sendEvent` 身份。 这将解锁包括个性化在内的一系列使用案例。 现在，您可以在命令中传递 `sendEvent` 这些标识，它们可以直接放置在DataLayer中。

同步标识允许您使用多个标识来标识设备／用户，设置其身份验证状态，并确定哪个标识符被视为主标识符。 如果未将标识符设置 `primary`为，则主标识符默认为 `ECID`。

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

内的每个属 `identityMap` 性表示属于特定身份命名空间 [的身份](../../identity-service/namespaces.md)。 属性名称应为标识命名空间符号，您可以在“标识”下的Adobe Experience Platform用户界面中找到该[!UICONTROL 符号]。 属性值应该是与该标识命名空间相关的标识数组。

标识数组中的每个标识对象按以下方式进行结构化：

### `id`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

这是您要为给定命名空间同步的ID。

### `authenticationState`

| **类型** | **必需** | **默认值** | **可能值** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 字符串 | 是 | 模糊 | 不明确、已验证和已注销 |

ID的身份验证状态。

### `primary`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 可选 | false |

确定是否应将此标识用作统一用户档案中的主片段。 默认情况下，ECID设置为用户的主标识符。
