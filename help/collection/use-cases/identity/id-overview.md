---
title: Web SDK中的身份数据
description: 了解如何使用Adobe Experience Platform Web SDK检索和管理Adobe Experience Cloud ID (ECID)。
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# Web SDK中的身份数据

Adobe Experience Platform Web SDK使用[Adobe Experience Cloud ID (ECID)](/help/identity-service/features/ecid.md)来跟踪访客行为。 通过使用[!DNL ECIDs]，您可以确保每个设备都有一个唯一标识符，该标识符可以跨多个会话持续存在，从而将特定设备在Web会话期间和跨这些会话发生的所有点击绑定在一起。

本文档概述了如何使用Web SDK管理[!DNL ECIDs]和[!DNL CORE IDs]。

## 使用Web SDK跟踪ECID {#tracking-ecids-web-sdk}

Web SDK使用Cookie分配和跟踪[!DNL ECIDs]，并使用多种可用方法来配置这些Cookie的生成方式。

当新用户访问您的网站时，[Adobe Experience Cloud Identity服务](/help/identity-service/home.md)将尝试为该用户设置设备识别Cookie。

* 对于首次访问的访客，在首次从Experience Platform Edge Network响应中生成并返回[!DNL ECID]。
* 对于回访访客，将从[!DNL ECID] Cookie中检索`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`，并将其添加到Edge Network的请求有效负载中。

设置包含[!DNL ECID]的Cookie后，Web SDK生成的每个后续请求在[!DNL ECID] Cookie中包含编码的`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`。

使用Cookie进行设备识别时，可通过两种方式与Edge Network交互：

1. 在您自己的域上创建一个指向`adobedc.net`的CNAME。 此方法称为[第一方数据收集](#first-party)。
1. 将数据直接发送到Edge Network域`adobedc.net`。 此方法称为[第三方数据收集](#third-party)。

如下面的部分所述，您选择使用的数据收集方法会直接影响所有浏览器的Cookie生命周期。

## 使用Web SDK跟踪核心标识 {#tracking-coreid-web-sdk}

使用启用了第三方Cookie的Google Chrome且未设置`kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Cookie时，第一个Edge Network请求将通过`demdex.net`域，该域将设置Demdex Cookie。 此Cookie包含[!DNL CORE ID]。 这是与[!DNL ECID]不同的唯一用户ID。

根据您的实施，您可能希望[访问 [!DNL CORE ID]](#retrieve-coreid)。

### 第一方数据收集 {#first-party}

第一方数据收集涉及通过您自己的域上指向`CNAME`的`adobedc.net`设置Cookie。

虽然浏览器长期以来以与站点拥有的端点所设置类似的方式处理由`CNAME`端点设置的Cookie，但浏览器最近实施的更改在如何处理`CNAME` Cookie方面造成了一种差异。 虽然默认情况下没有浏览器当前阻止第一方`CNAME` Cookie，但某些浏览器将使用`CNAME`设置的Cookie的生命周期限制为仅七天。

### 第三方数据收集 {#third-party}

第三方数据收集涉及将数据直接发送到Edge Network域`adobedc.net`。

近年来，Web浏览器在处理第三方设置的Cookie时受到的限制日益严格。 默认情况下，某些浏览器会阻止第三方Cookie。 如果您使用第三方Cookie来识别网站访客，则这些Cookie的生命周期几乎总是比使用第一方Cookie时可用的生命周期更短。 有时，第三方Cookie在短短7天后过期。

此外，在使用第三方数据收集时，一些广告拦截器会完全限制到Adobe数据收集端点的流量。

### Cookie生命周期对Adobe Experience Cloud应用程序的影响 {#lifespans}

无论您选择第一方还是第三方数据收集，Cookie可以保留的时间长短都会直接影响[Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics)和[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/customer-journey-analytics)中的访客计数。 此外，在网站上使用[Adobe Target](https://experienceleague.adobe.com/en/docs/target)或[Offer Decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision)时，最终用户可能会遇到不一致的个性化体验。

例如，假定您创建了一个个性化体验，如果用户在过去七天内查看了任何项目三次，则会将任何项目提升到主页。

如果最终用户一周访问三次，然后七天未返回网站，则该用户可能在返回网站时被视为新用户，因为其Cookie可能已被浏览器策略删除（具体取决于他们在访问网站时所使用的浏览器）。 如果发生这种情况，您的Analytics工具会将该访客视为新用户，即使他们仅在7天多一点前访问过该网站。 此外，任何为用户个性化体验的努力都会再次开始。

### 第一方设备ID (FPID) {#fpid}

如上所述，要考虑Cookie生命周期的影响，您可以选择设置和管理自己的设备标识符。 有关详细信息，请参阅[第一方设备ID](./first-party-device-ids.md)上的指南。

## 检索当前用户的ECID和区域 {#retrieve-ecid}

根据您的用例，有两种方法可以访问[!DNL ECID]：

* [通过数据准备检索 [!DNL ECID] 以进行数据收集](#retrieve-ecid-data-prep)：建议您使用此方法。
* [通过 [!DNL ECID] 命令检索`getIdentity()`](#retrieve-ecid-getidentity)：仅在您需要客户端上的[!DNL ECID]信息时使用此方法。

### 通过数据准备检索[!DNL ECID]以进行数据收集 {#retrieve-ecid-data-prep}

使用数据收集[的](/help/datastreams/data-prep.md)数据准备将[!DNL ECID]映射到[!DNL XDM]字段。 这是访问[!DNL ECID]的推荐方法。

为此，请将源字段设置为以下路径：

```js
xdm.identityMap.ECID[0].id
```

然后，将目标字段设置为字段类型为`string`的XDM路径。

![数据流映射屏幕快照](/help/tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### 通过[!DNL ECID]命令检索`getIdentity()` {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>只有在客户端需要`getIdentity()`时，才应通过[!DNL ECID]命令检索ECID。 如果只想将ECID映射到XDM字段，请改用[为数据收集准备数据](#retrieve-ecid-data-prep)。

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

## 检索当前用户的核心ID {#retrieve-coreid}

要检索用户的核心ID，可以使用[`getIdentity()`](/help/collection/js/commands/getidentity.md)命令，如下所示。

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```

## 使用`identityMap` {#using-identitymap}

使用XDM [`identityMap`字段](/help/xdm/schema/composition.md#identityMap)，您可以使用多个标识来识别设备/用户，设置其身份验证状态，并确定哪个标识符被视为主要标识符。 如果未将标识符设置为`primary`，则主标识符默认为`ECID`。

使用`identityMap`命令更新了`sentEvent`字段。

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

`identityMap`中的每个属性都表示属于特定[标识命名空间](/help/identity-service/features/namespaces.md)的标识。 属性名称应该是身份命名空间符号，您可以在Adobe Experience Platform用户界面的“[!UICONTROL Identities]”下找到该符号。 属性值应为与该身份命名空间相关的身份数组。

>[!IMPORTANT]
>
>`identityMap`中传递的命名空间ID区分大小写。 请确保使用正确的命名空间ID，以避免不完整的数据收集。

标识数组中的每个标识对象包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | **（必需）**&#x200B;要为给定的命名空间设置的ID。 |
| `authenticatedState` | 字符串 | **（必需）** ID的身份验证状态。 可能的值为`ambiguous`、`authenticated`和`loggedOut`。 |
| `primary` | 布尔值 | 确定是否应当将此标识用作配置文件中的主片段。 默认情况下，会将ECID设置为用户的主要标识符。 如果忽略，此值将默认为`false`。 |

使用`identityMap`字段识别设备或用户产生的结果与使用[`setCustomerIDs`中的](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) [!DNL ID Service API]方法产生的结果相同。 有关详细信息，请参阅[ID服务API文档](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html)。

## 从访客API迁移到ECID {#migrating-visitor-api-ecid}

从使用访客API进行迁移时，您还可以迁移现有AMCV Cookie。 要启用ECID迁移，请在配置中设置`idMigrationEnabled`参数。 ID迁移支持以下用例：

* 当域的某些页面使用访客API，而其他页面使用此SDK时。 为了支持这种情况，SDK会读取现有AMCV Cookie并使用现有ECID写入新的Cookie。 此外，SDK会写入AMCV Cookie，这样如果首先在通过SDK检测的页面上获取ECID，则通过访客API检测的后续页面将具有相同的ECID。
* 在也具有访客API的页面上设置Adobe Experience Platform Web SDK时。 为了支持这种情况，如果未设置AMCV Cookie，SDK会在页面上查找访客API，并调用它以获取ECID。
* 当整个网站都在使用Adobe Experience Platform Web SDK并且没有访客API时，迁移ECID以便保留返回的访客信息会很有用。 在将SDK与`idMigrationEnabled`一起部署以便迁移大多数访客Cookie后，可以关闭此设置。

### 更新迁移特征

将XDM格式的数据发送到Audience Manager时，迁移时必须将此数据转换为信号。 必须更新您的特征以反映XDM提供的新密钥。 通过使用Audience Manager创建的[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)，此过程变得更轻松。

## 在事件转发中使用

如果您当前启用了[事件转发](/help/tags/ui/event-forwarding/overview.md)，并且使用的是`appmeasurement.js`和`visitor.js`，则可以保持事件转发功能已启用，这不会导致任何问题。 在后端，Adobe会获取所有AAM区段，并将它们添加到对Analytics的调用。 如果对Analytics的调用包含这些区段，则Analytics不会调用Audience Manager来转发任何数据，因此不存在任何双重数据收集。 使用Web SDK时也不需要位置提示，因为后端会调用相同的分段端点。
