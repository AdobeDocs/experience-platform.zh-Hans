---
title: Web SDK中的身份数据
description: 了解如何使用Adobe Experience Platform Web SDK检索和管理Adobe Experience Cloud ID (ECID)。
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: b8c38108e7481a5c4e94e4122e0093fa6f00b96c
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 0%

---

# Web SDK中的身份数据

Adobe Experience Platform Web SDK使用[Adobe Experience Cloud ID (ECID)](../../identity-service/features/ecid.md)来跟踪访客行为。 通过使用ECID，您可以确保每个设备都有一个唯一标识符，该标识符可以跨多个会话持续存在，从而将特定设备在Web会话期间和之间发生的所有点击绑定在一起。

本文档概述了如何使用Platform Web SDK管理ECID。

## 使用SDK跟踪ECID

Platform Web SDK通过使用Cookie分配和跟踪ECID，以及使用多种可用方法来配置这些Cookie的生成方式。

当新用户访问您的网站时，Adobe Experience Cloud Identity服务会尝试为该用户设置设备识别Cookie。 对于首次访问的访客，会在首次从Adobe Experience PlatformEdge Network响应中生成并返回ECID。 对于回访访客，ECID将从`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie中检索，并由Edge Network添加到有效负载中。

设置包含ECID的Cookie后，Web SDK生成的每个后续请求都在`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie中包含编码的ECID。

使用Cookie进行设备识别时，可通过两个选项与Edge Network交互：

1. 将数据直接发送到Edge Network域`adobedc.net`。 此方法称为[第三方数据收集](#third-party)。
1. 在您自己的域上创建一个指向`adobedc.net`的CNAME。 此方法称为[第一方数据收集](#first-party)。

如下面的部分所述，您选择使用的数据收集方法会直接影响所有浏览器的Cookie生命周期。

### 第三方数据收集 {#third-party}

第三方数据收集涉及将数据直接发送到Edge Network域`adobedc.net`。

近年来，Web浏览器在处理第三方设置的Cookie时越来越严格。 默认情况下，某些浏览器会阻止第三方Cookie。 如果您使用第三方Cookie来识别网站访客，则这些Cookie的生命周期几乎总是比使用第一方Cookie时可用的生命周期更短。 有时，第三方Cookie在短短7天后过期。

此外，当使用第三方数据收集时，一些广告拦截器会完全将流量限制在Adobe数据收集端点。

### 第一方数据收集 {#first-party}

第一方数据收集涉及通过您自己的域上指向`adobedc.net`的CNAME设置Cookie。

虽然浏览器长期以来以与站点拥有的端点所设置的方法类似的方式处理由CNAME端点设置的Cookie，但浏览器最近实施的更改在处理CNAME Cookie方面造成了一种差异。 虽然当前没有浏览器默认阻止第一方CNAME Cookie，但某些浏览器将使用CNAME设置的Cookie的生命周期限制为仅七天。

### Cookie生命周期对Adobe Experience Cloud应用程序的影响 {#lifespans}

无论您是选择第一方还是第三方数据收集，Cookie可以保留的时间长短都会直接影响Adobe Analytics和Customer Journey Analytics中的访客计数。 此外，在网站上使用Adobe Target或Offer decisioning时，最终用户可能会遇到不一致的个性化体验。

例如，假定您创建了一个个性化体验，如果用户在过去七天内查看了任何项目三次，则会将任何项目提升到主页。

如果最终用户一周访问三次，然后七天未返回网站，则该用户可能在返回网站时被视为新用户，因为其Cookie可能已被浏览器策略删除（具体取决于他们在访问网站时所使用的浏览器）。 如果发生这种情况，您的Analytics工具会将该访客视为新用户，即使他们仅在7天多一点前访问过该网站。 此外，任何为用户个性化体验的努力都会再次开始。

### 第一方设备Id

如上所述，要考虑Cookie生命周期的影响，您可以选择设置和管理自己的设备标识符。 有关详细信息，请参阅[第一方设备ID](./first-party-device-ids.md)上的指南。

## 检索当前用户的ECID和区域 {#retrieve-ecid}

根据您的用例，有两种方法可以访问[!DNL ECID]：

* [通过数据准备检索 [!DNL ECID] 以进行数据收集](#retrieve-ecid-data-prep)：建议您使用此方法。
* [通过`getIdentity()`命令检索 [!DNL ECID] ](#retrieve-ecid-getidentity)：仅在您需要客户端上的[!DNL ECID]信息时使用此方法。

### 通过数据准备检索[!DNL ECID]以进行数据收集 {#retrieve-ecid-data-prep}

使用数据收集](../../datastreams/data-prep.md)的[数据准备将[!DNL ECID]映射到[!DNL XDM]字段。 这是访问[!DNL ECID]的推荐方法。

为此，请将源字段设置为以下路径：

```js
xdm.identityMap.ECID[0].id
```

然后，将目标字段设置为字段类型为`string`的XDM路径。

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### 通过`getIdentity()`命令检索[!DNL ECID] {#retrieve-ecid-getidentity}


>[!IMPORTANT]
>
>只有在客户端需要[!DNL ECID]时，才应通过`getIdentity()`命令检索ECID。 如果只想将ECID映射到XDM字段，请改用[为数据收集准备数据](#retrieve-ecid-data-prep)。

要检索当前访客的唯一ECID，请使用`getIdentity`命令。 对于尚无[!DNL ECID]的首次访客，此命令将生成新的[!DNL ECID]。 `getIdentity`还返回访客的区域ID。

>[!NOTE]
>
>此方法通常用于需要读取[!DNL Experience Cloud] ID或需要Adobe Audience Manager位置提示的自定义解决方案。 标准实施不使用该函数。

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

## 使用`identityMap` {#using-identitymap}

使用XDM [`identityMap`字段](../../xdm/schema/composition.md#identityMap)，您可以使用多个标识来识别设备/用户，设置其身份验证状态，并确定哪个标识符被视为主要标识符。 如果未将标识符设置为`primary`，则主标识符默认为`ECID`。

使用`sentEvent`命令更新了`identityMap`字段。

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe建议将代表个人的命名空间（如`CRMID`）作为主要身份发送。


`identityMap`中的每个属性都表示属于特定[标识命名空间](../../identity-service/features/namespaces.md)的标识。 属性名称应为标识命名空间符号，您可以在Adobe Experience Platform用户界面的“[!UICONTROL 标识]”下找到该符号。 属性值应为与该身份命名空间相关的身份数组。

>[!IMPORTANT]
>
>`identityMap`中传递的命名空间ID区分大小写。 请确保使用正确的命名空间ID，以避免不完整的数据收集。

标识数组中的每个标识对象包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | **（必需）**&#x200B;要为给定的命名空间设置的ID。 |
| `authenticationState` | 字符串 | **（必需）** ID的身份验证状态。 可能的值为`ambiguous`、`authenticated`和`loggedOut`。 |
| `primary` | 布尔值 | 确定是否应当将此标识用作配置文件中的主片段。 默认情况下，会将ECID设置为用户的主要标识符。 如果忽略，此值将默认为`false`。 |

使用`identityMap`字段识别设备或用户产生的结果与使用[!DNL ID Service API]中的[`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html)方法产生的结果相同。 有关详细信息，请参阅[ID服务API文档](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html)。

## 从访客API迁移到ECID

从使用访客API进行迁移时，您还可以迁移现有AMCV Cookie。 要启用ECID迁移，请在配置中设置`idMigrationEnabled`参数。 ID迁移支持以下用例：

* 当域的某些页面使用访客API，而其他页面使用此SDK时。 为了支持这种情况，SDK会读取现有AMCV Cookie并使用现有ECID写入新的Cookie。 此外，SDK还会写入AMCV Cookie，以便如果首先在通过SDK进行检测的页面上获取ECID，则通过访客API进行检测的后续页面将具有相同的ECID。
* 在同时具有访客API的页面上设置Adobe Experience Platform Web SDK时。 为了支持这种情况，如果未设置AMCV Cookie，SDK将在页面上查找访客API并调用它以获取ECID。
* 当整个网站都在使用Adobe Experience Platform Web SDK并且没有访客API时，迁移ECID以便保留返回的访客信息会很有用。 在与`idMigrationEnabled`一起部署SDK以便迁移大多数访客Cookie后，可以关闭此设置。

### 更新迁移特征

将XDM格式的数据发送到Audience Manager时，迁移时必须将此数据转换为信号。 必须更新您的特征以反映XDM提供的新密钥。 通过使用Audience Manager创建的[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)，此流程变得更加容易。

## 在事件转发中使用

如果您当前启用了[事件转发](../../tags/ui/event-forwarding/overview.md)，并且使用的是`appmeasurement.js`和`visitor.js`，则可以保持事件转发功能已启用，这不会导致任何问题。 在后端，Adobe获取所有AAM区段并将它们添加到对Analytics的调用。 如果对Analytics的调用包含这些区段，则Analytics不会调用Audience Manager来转发任何数据，因此不存在任何双重数据收集。 使用Web SDK时也不需要位置提示，因为后端会调用相同的分段端点。
