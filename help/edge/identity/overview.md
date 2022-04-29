---
title: 平台Web SDK中的身份数据
description: 了解如何使用Adobe Experience Cloud Web SDK检索和管理Adobe Experience Platform ID(ECID)。
keywords: 身份；第一方身份；身份服务；第三方身份；ID迁移；访客ID；第三方身份；ThirdPartyCookiesEnabled;idMigrationEnabled;getIdentity；同步身份；sendEvent;identityMap；主；EID；身份命名空间；命名空间ID;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 85ff35e0e7f7e892de5252e8f3ad069eff83aa15
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 1%

---

# 平台Web SDK中的身份数据

Adobe Experience Platform Web SDK利用 [Adobe Experience Cloud ID(ECID)](../../identity-service/ecid.md) 来跟踪访客行为。 使用ECID，您可以确保每个设备都具有一个唯一标识符，该标识符可以跨多个会话保留，从而将在Web会话期间和跨Web会话发生的所有点击与特定设备相关联。

本文档概述了如何使用平台Web SDK管理ECID。

## 使用SDK跟踪ECID

Platform Web SDK通过使用Cookie分配和跟踪ECID，以及使用多种可用方法配置这些Cookie的生成方式。

当新用户到达您的网站时，Adobe Experience Cloud Identity服务会尝试为该用户设置设备标识Cookie。 对于首次访客，会在Adobe Experience Platform边缘网络的首次响应中生成并返回ECID。 对于重复访客，将从 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie和Edge Network添加到有效负载中。

设置包含ECID的Cookie后，Web SDK生成的每个后续请求都将在 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie。

使用Cookie进行设备标识时，您有两个选项可与边缘网络进行交互：

1. 将数据直接发送到边缘网络域 `adobedc.net`. 此方法称为 [第三方数据收集](#third-party).
1. 在您自己的域上创建指向 `adobedc.net`. 此方法称为 [第一方数据收集](#first-party).

如以下各节所述，您选择使用的数据收集方法会直接影响各种浏览器的Cookie生命周期。

### 第三方数据收集 {#third-party}

第三方数据收集涉及将数据直接发送到边缘网络域 `adobedc.net`.

近年来，Web浏览器在处理第三方设置的Cookie时越来越受限。 默认情况下，某些浏览器会阻止第三方Cookie。 如果您使用第三方Cookie来识别网站访客，则这些Cookie的生命周期几乎总是比使用第一方Cookie时可能提供的生命周期短。 在某些情况下，第三方Cookie的过期时间最少为七天。

此外，当使用第三方数据收集时，某些广告拦截器会将流量限制为完全Adobe数据收集端点。

### 第一方数据收集 {#first-party}

第一方数据收集涉及在您自己的域上通过CNAME设置Cookie，该CNAME指向 `adobedc.net`.

虽然浏览器长期以来处理由CNAME端点设置的Cookie的方式与由站点拥有的端点设置的方式类似，但浏览器实施的最新更改在处理CNAME Cookie的方式上有所区别。 虽然默认情况下没有阻止第一方CNAME Cookie的浏览器，但某些浏览器会将使用CNAME设置的Cookie的生命周期限制为仅7天。

### Cookie生命周期对Adobe Experience Cloud应用程序的影响 {#lifespans}

无论您选择是第一方还是第三方数据收集，Cookie可持续的时长都会直接影响Adobe Analytics和Customer Journey Analytics中的访客计数。 此外，当在网站上使用Adobe Target或Offer decisioning时，最终用户可能会遇到不一致的个性化体验。

例如，假设您创建了一个个性化体验，如果用户在过去七天中查看了任何项目三次，则该体验会将其提升到主页。

如果最终用户一周内访问三次，但七天内没有返回网站，则当他们返回网站时，该用户可能会被视为新用户，因为浏览器策略可能已删除了其Cookie（具体取决于他们访问网站时使用的浏览器）。 如果出现这种情况，您的Analytics工具会将访客视为新用户，即使他们在七天多一点前访问了网站。 此外，将再次开始为用户个性化体验的任何工作。

### 第一方设备ID

要考虑如上所述Cookie生命周期的影响，您可以选择设置并管理您自己的设备标识符。 请参阅 [第一方设备ID](./first-party-device-ids.md) 以了解更多信息。

## 检索当前用户的ECID和区域

要检索当前访客的唯一ECID，请使用 `getIdentity` 命令。 对于首次没有ECID的访客，此命令会生成一个新的ECID。 `getIdentity` 也会返回访客的区域ID。

>[!NOTE]
>
>此方法通常与需要读取 [!DNL Experience Cloud] ID或需要Adobe Audience Manager的位置提示。 标准实施不使用该函数。

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

## 使用 `identityMap`

使用XDM [`identityMap` 字段](../../xdm/schema/composition.md#identityMap)，您可以使用多个标识来识别设备/用户，设置其身份验证状态，并确定哪个标识符被视为主标识符。 如果未将标识符设置为 `primary`，则主要默认为 `ECID`.

`identityMap` 字段将使用 `sentEvent` 命令。

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

中的每个属性 `identityMap` 表示属于特定 [标识命名空间](../../identity-service/namespaces.md). 属性名称应该是身份命名空间符号，您可以在Adobe Experience Platform用户界面的“ ”下找到该符号[!UICONTROL 标识]&quot; 属性值应该是与该标识命名空间相关的标识数组。

标识数组中的每个标识对象都包含以下属性：

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | **（必需）** 要为给定命名空间设置的ID。 |
| `authenticationState` | 字符串 | **（必需）** ID的身份验证状态。 可能的值为 `ambiguous`, `authenticated`和 `loggedOut`. |
| `primary` | 布尔型 | 确定此标识是否应用作配置文件中的主片段。 默认情况下，ECID将设置为用户的主标识符。 如果忽略，则此值默认为 `false`. |

## 从访客API迁移到ECID

使用访客API从迁移时，您还可以迁移现有的AMCV Cookie。 要启用ECID迁移，请将 `idMigrationEnabled` 参数。 ID迁移可支持以下用例：

* 当域的某些页面使用访客API，而其他页面使用此SDK时。 为支持这种情况，SDK会读取现有AMCV Cookie，并使用现有ECID写入新Cookie。 此外，SDK还会编写AMCV Cookie，以便如果首先在使用SDK分析的页面上获取ECID，则使用访客API分析的后续页面将具有相同的ECID。
* 在同时具有访客API的页面上设置Adobe Experience Platform Web SDK时。 要支持这种情况，如果未设置AMCV Cookie，SDK将在页面上查找访客API，并调用该API以获取ECID。
* 当整个网站使用Adobe Experience Platform Web SDK并且没有访客API时，迁移ECID以保留回访访客信息会非常有用。 在将SDK部署为 `idMigrationEnabled` 一段时间后，该设置便可关闭，以便迁移大部分访客cookie。

### 更新迁移特征

当XDM格式化的数据被发送到Audience Manager时，迁移时需要将这些数据转换为信号。 您的特征需要更新以反映XDM提供的新键值。 使用 [BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) Audience Manager创建的。

## 在事件转发中使用

如果您当前 [事件转发](../../tags/ui/event-forwarding/overview.md) 已启用且正在使用 `appmeasurement.js` 和 `visitor.js`，则可以保持启用事件转发功能，这不会导致任何问题。 在后端，Adobe会获取任何AAM区段，并将其添加到对Analytics的调用中。 如果对Analytics的调用包含这些区段，则Analytics不会调用Audience Manager来转发任何数据，因此不会进行任何双重数据收集。 使用Web SDK时也不需要位置提示，因为后端会调用相同的分段端点。
