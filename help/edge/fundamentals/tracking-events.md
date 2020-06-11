---
title: 跟踪事件
seo-title: 跟踪Adobe Experience Platform Web SDK事件
description: 了解如何跟踪Experience Platform Web SDK事件
seo-description: 了解如何跟踪Experience Platform Web SDK事件
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 跟踪事件

要将事件数据发送到Adobe Experience Cloud，请使用该命 `sendEvent` 令。 该 `sendEvent` 命令是将数据发送到Experience Cloud以及检索个性化内容、身份和受众目标的主要方式。

发送到Adobe Experience Cloud的数据分为两个类别:

* XDM数据
* 非XDM数据（当前不支持）

## 发送XDM数据

XDM数据是一个内容和结构与您在Adobe Experience Platform中创建的模式相匹配的对象。 [进一步了解如何创建模式。](../../xdm/tutorials/create-schema-ui.md)

您希望成为分析、个性化、受众或目标一部分的任何XDM数据都应使用此选项进 `xdm` 行发送。

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

>[!NOTE]
>在XDM字段的每个事件中发送的数据有32 KB的限制。

### 发送非XDM数据

当前，不支持发送与XDM模式不匹配的数据。 支持计划在将来某个日期提供。

### 设置 `eventType`

在XDM体验事件中，有一个 `eventType` 字段。 它保存记录的主事件类型。 这可以作为选项的一部分传 `xdm` 入。

```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

或者，也 `eventType` 可以使用选项将事件命令传 `type` 入。 在后台，这会添加到XDM数据中。 使用 `type` 作为选项，您无需修改XDM负 `eventType` 载即可更轻松地设置。

```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

## 使用sendBeacon API

在网页用户导航离开之前发送事件数据可能很棘手。 如果请求过长，浏览器可能会取消请求。 某些浏览器已实现一个调用的Web标 `sendBeacon` 准API，以便在此期间更轻松地收集数据。 使用时， `sendBeacon`浏览器在全局浏览上下文中发出Web请求。 这意味着浏览器在后台发出信标请求，并且不保留页面导航。 要告知Adobe Experience Platform Web SDK使用 `sendBeacon`，请将该选项 `"documentUnloading": true` 添加到事件命令。  示例如下：

```javascript
alloy("sendEvent", {
  "documentUnloading": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

浏览器已对一次可发送的数据量 `sendBeacon` 施加限制。 在许多浏览器中，限制为64K。 如果浏览器由于负载过大而拒绝事件，则Adobe Experience Platform Web SDK将回退到使用其常规传输方法（例如，提取）。

## 处理来自事件的响应

如果要处理事件的响应，可以通知您成功或失败，如下所示：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## 全局修改事件 {#modifying-events-globally}

如果要从事件全局添加、删除或修改字段，可以配置回 `onBeforeEventSend` 调。  每次发送事件时都会调用此回调。  此回调在带字段的事件对象中 `xdm` 传递。  修 `event.xdm` 改以更改在事件中发送的数据。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 字段按此顺序设置：

1. 作为选项传递到事件命令的值 `alloy("sendEvent", { xdm: ... });`
2. 自动收集的值。  (请参阅 [自动信息](../reference/automatic-information.md)。)
3. 回调中所做的 `onBeforeEventSend` 更改。

如果回 `onBeforeEventSend` 调引发异常，仍会发送事件; 但是，回调中所做的任何更改都不会应用于最终事件。

## 可能的可操作错误

发送事件时，如果所发送的数据过大（完整请求的数据量超过32KB），则可能会引发错误。 在这种情况下，您需要减少所发送的数据量。

启用调试时，服务器同步验证针对所配置的XDM事件发送的模式数据。 如果模式与数据不匹配，则服务器会返回有关不匹配的详细信息并引发错误。 在这种情况下，请修改数据以匹配模式。 当未启用调试时，服务器将异步验证数据，因此不会引发相应的错误。
