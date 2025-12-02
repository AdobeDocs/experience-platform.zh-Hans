---
title: getVisitorId
description: 检索Experience Cloud访客ID服务标记扩展实例。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# `getVisitorId()`

`_satellite.getVisitorId()`方法会在您的标记属性[if](https://experienceleague.adobe.com/en/docs/id-service/using/home)中返回&#x200B;**Adobe Experience Cloud ID服务**&#x200B;的实例，您已安装并发布ID服务扩展。 当您希望直接访问访客ID实例以在自定义代码块、高级数据元素配置或访客身份问题疑难解答中使用时，此方法非常有用。

>[!IMPORTANT]
>
>此方法仅适用于包含独立Experience Cloud ID服务标签扩展的资产。 它不适用于Web SDK标记扩展中可用的隐式ID服务功能。 如果需要使用Web SDK的隐式ID服务功能获取访客身份，请参阅[`getIdentity`](/help/collection/js/commands/getidentity.md)命令。

如果在安装并发布ID服务扩展的情况下调用此方法，则将返回一个对象，该对象类似于在调用[`Visitor.getInstance()`](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/getinstance)方法后获得的对象。 如果未安装或发布ID服务扩展时调用此方法，则该方法返回`null`。

```ts
_satellite.getVisitorId(): Visitor | null
```

## 可用字段和方法

请参阅Experience Cloud访客ID服务文档中的Experience Cloud ID服务[方法](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/get-set)，以查看您可以使用哪些字段和方法。

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
