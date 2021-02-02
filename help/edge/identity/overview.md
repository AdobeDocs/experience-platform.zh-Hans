---
title: 检索Experience CloudID
seo-title: Adobe Experience PlatformWeb SDK检索Experience CloudID
description: 了解如何获得Adobe Experience CloudID。
seo-description: 了解如何获得Adobe Experience CloudID。
keywords: 身份；第一方身份；身份服务；第三方身份；身份迁移；访客ID；第三方身份；第三方身份；第三方CookiesEnabled;idMigrationEnabled;getIdentity；同步身份；syncIdentity;sendEvent;identityMap；主；ecid；身份命名空间；身份验证状态；hashEnabled;
translation-type: tm+mt
source-git-commit: 60945f7f3a87568b82d968692cc7a6e07593fa01
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 3%

---


# 标识——检索Experience CloudID

Adobe Experience PlatformWeb SDK利用[Adobe标识服务](../../identity-service/ecid.md)。 这可确保每个设备都有一个唯一标识符，该标识符会保留在设备上，以便页面之间的活动可以绑定在一起。

## 第一方身份

[!DNL Identity Service]将标识存储在第一方域的cookie中。 [!DNL Identity Service]尝试使用域上的HTTP头设置cookie。 如果失败，[!DNL Identity Service]将返回至通过Javascript设置cookie。 Adobe建议您设置CNAME，以确保您的Cookie不受客户端ITP限制的限制。

## 第三方身份

[!DNL Identity Service]能够将ID与第三方域(demdex.net)同步，以启用跨站点跟踪。 启用此功能后，将向demdex.net发出对访客（例如，某个没有ECID的人）的第一个请求。 此操作仅在允许其使用的浏览器（如Chrome）上完成，并由配置中的`thirdPartyCookiesEnabled`参数控制。 如果您希望全部禁用此功能，请将`thirdPartyCookiesEnabled`设置为false。

## ID迁移

从使用访客API迁移时，您还可以迁移现有AMCV cookie。 要启用ECID迁移，请在配置中设置`idMigrationEnabled`参数。 ID迁移可启用以下用例：

* 当域的某些页面使用访客API，而其他页面使用此SDK时。 为支持此情况，SDK会读取现有AMCV cookie，并使用现有ECID写入新cookie。 此外，SDK会编写AMCV cookies，这样，如果ECID是首先在使用SDK进行指令的页面上获得的，则使用访客API指令的后续页面具有相同的ECID。
* 当Adobe Experience PlatformWeb SDK设置在同时具有访客API的页面上时。 为支持此情况，如果未设置AMCV cookie,SDK将在页面上查找访客API并调用它以获取ECID。
* 当整个站点使用Adobe Experience PlatformWeb SDK且没有访客API时，迁移ECID以便保留返回的访客信息很有用。 在将SDK与`idMigrationEnabled`一起部署一段时间后，大多数访客cookie都被迁移，该设置可以关闭。

## 更新迁移特征

当XDM格式化数据被发送到Audience Manager时，迁移时需要将这些数据转换为信号。 您的特征需要更新以反映XDM提供的新密钥。 通过使用Audience Manager已创建的[BAAAM工具](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)，可以简化此过程。

## 服务器端转发

如果您当前启用了服务器端转发，并且正在使用`appmeasurement.js`。 和`visitor.js`，您可以保持服务器端转发功能处于启用状态，这不会导致任何问题。 在后端，Adobe获取任何AAM细分并将其添加到对Analytics的调用中。 如果对Analytics的调用包含这些区段，则Analytics将不会呼叫Audience Manager转发任何数据，因此不会收集任何多次数据。 使用Web SDK时，也不需要位置提示，因为后端调用了相同的分段端点。

## 检索访客ID

如果要使用此唯一ID，请使用`getIdentity`命令。 `getIdentity` 返回当前访客的现有ECID。对于尚未具有ECID的首次访客，此命令将生成新ECID。

>[!NOTE]
>
>此方法通常用于需要读取[!DNL Experience Cloud] ID的自定义解决方案。 标准实施不使用该函数。

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
>除散列功能外，版本2.1.0中还删除了`syncIdentity`方法。 如果您使用版本2.1.0+并希望同步标识，则可以直接在`sendEvent`命令的`xdm`选项中的`identityMap`字段下发送这些标识。

此外，[!DNL Identity Service]允许您使用`syncIdentity`命令将您自己的标识符与ECID同步。

>[!NOTE]
>
>强烈建议在每个`sendEvent`命令上传递所有可用标识。 这将解锁包括个性化在内的一系列使用案例。 现在，您可以在`sendEvent`命令中传递这些标识，它们可以直接放置在DataLayer中。

同步标识允许您使用多个标识来标识设备／用户，设置其身份验证状态，并确定哪个标识符被视为主标识符。 如果未将标识符设置为`primary`，则主默认值为`ECID`。

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

`identityMap`中的每个属性表示属于特定[标识命名空间](../../identity-service/namespaces.md)的标识。 属性名称应为标识命名空间符号，您可以在Adobe Experience Platform用户界面的“[!UICONTROL Identities]”下找到该符号。 属性值应该是与该标识命名空间相关的标识数组。

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
