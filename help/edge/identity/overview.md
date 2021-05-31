---
title: 使用Adobe Experience Platform Web SDK检索Experience CloudID
description: 了解如何使用Adobe Experience Cloud Web SDK检索Adobe Experience Platform ID(ECID)。
seo-description: 了解如何获取Adobe Experience Cloud Id。
keywords: 身份；第一方身份；身份服务；第三方身份；ID迁移；访客ID；第三方身份；ThirdPartyCookiesEnabled;idMigrationEnabled;getIdentity；同步身份；sendEvent;identityMap；主；EID；身份命名空间；命名空间ID;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# 检索Adobe Experience Cloud ID

Adobe Experience Platform Web SDK利用[AdobeIdentity服务](../../identity-service/ecid.md)。 这可确保每个设备都有一个唯一标识符，该标识符会保留在设备上，以便页面之间的活动可以绑定在一起。

## 第一方身份

[!DNL Identity Service]将标识存储在第一方域的Cookie中。 [!DNL Identity Service]尝试使用域上的HTTP标头来设置Cookie。 如果操作失败， [!DNL Identity Service]将回退到通过Javascript设置Cookie。 Adobe建议您设置CNAME，以确保客户端ITP限制不会对您的Cookie设置上限。

## 第三方标识

[!DNL Identity Service]能够将ID与第三方域(demdex.net)同步，以启用跨站点的跟踪。 启用此功能后，将向demdex.net发出访客的第一个请求（例如，没有ECID的访客）。 此操作将仅在允许使用它的浏览器（如Chrome）上完成，并由配置中的`thirdPartyCookiesEnabled`参数控制。 如果要一起禁用此功能，请将`thirdPartyCookiesEnabled`设置为false。

## ID迁移

使用访客API从迁移时，您还可以迁移现有的AMCV Cookie。 要启用ECID迁移，请在配置中设置`idMigrationEnabled`参数。 ID迁移可支持以下用例：

* 当域的某些页面使用访客API，而其他页面使用此SDK时。 为支持这种情况，SDK会读取现有AMCV Cookie，并使用现有ECID写入新Cookie。 此外，SDK还会编写AMCV Cookie，以便如果首先在使用SDK分析的页面上获取ECID，则使用访客API分析的后续页面将具有相同的ECID。
* 在同时具有访客API的页面上设置Adobe Experience Platform Web SDK时。 要支持这种情况，如果未设置AMCV Cookie，SDK将在页面上查找访客API，并调用该API以获取ECID。
* 当整个网站使用Adobe Experience Platform Web SDK并且没有访客API时，迁移ECID以保留回访访客信息会非常有用。 将SDK与`idMigrationEnabled`一起部署一段时间以便迁移大多数访客Cookie后，可以关闭该设置。

## 更新迁移特征

当XDM格式化的数据被发送到Audience Manager时，迁移时需要将这些数据转换为信号。 您的特征需要更新以反映XDM提供的新键值。 使用Audience Manager创建的[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)，可以更轻松地执行此过程。

## 服务器端转发

如果您当前已启用服务器端转发并且正在使用`appmeasurement.js`。 和`visitor.js`您可以保持启用服务器端转发功能，这不会导致任何问题。 在后端，Adobe会获取任何AAM区段，并将其添加到对Analytics的调用中。 如果对Analytics的调用包含这些区段，则Analytics不会调用Audience Manager来转发任何数据，因此不会进行任何双重数据收集。 使用Web SDK时也不需要位置提示，因为后端会调用相同的分段端点。

## 检索访客ID和区域ID

如果要使用唯一访客ID，请使用`getIdentity`命令。 `getIdentity` 返回当前访客的现有ECID。对于首次没有ECID的访客，此命令会生成一个新的ECID。 `getIdentity` 也会返回访客的区域ID。有关更多信息，请参阅[Adobe Audience Manager用户指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html)。

>[!NOTE]
>
>此方法通常与需要读取[!DNL Experience Cloud] ID或需要Adobe Audience Manager位置提示的自定义解决方案一起使用。 标准实施不使用该函数。

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## 正在同步身份

>[!NOTE]
>
>除哈希功能外，版本2.1.0中还删除了`syncIdentity`方法。 如果您使用的是版本2.1.0及更高版本，并且希望同步身份，则可以直接在`sendEvent`命令的`xdm`选项中`identityMap`字段下发送它们。

此外，[!DNL Identity Service]允许您使用`syncIdentity`命令将自己的标识符与ECID同步。

>[!NOTE]
>
>强烈建议在每个`sendEvent`命令中传递所有可用的标识。 这将解锁一系列用例，包括个性化。 现在，您可以在`sendEvent`命令中传递这些标识，现在可以直接将它们放置在数据层中。

同步身份允许您使用多个身份来识别设备/用户，设置其身份验证状态并确定哪个标识符被视为主标识符。 如果未将标识符设置为`primary`，则主标识符默认为`ECID`。

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

`identityMap`中的每个属性表示属于特定[标识命名空间](../../identity-service/namespaces.md)的标识。 属性名称应该是标识命名空间符号，您可以在Adobe Experience Platform用户界面的“[!UICONTROL Identities]”下找到该符号。 属性值应该是与该标识命名空间相关的标识数组。

标识数组中的每个标识对象的结构如下所示：

### `id`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

这是您要为给定命名空间同步的ID。

### `authenticationState`

| **类型** | **必需** | **默认值** | **可能值** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| 字符串 | 是 | 模糊 | 不明确、已验证并已注销 |

ID的身份验证状态。

### `primary`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 可选 | false |

确定此标识是否应用作统一配置文件中的主片段。 默认情况下，ECID将设置为用户的主标识符。
