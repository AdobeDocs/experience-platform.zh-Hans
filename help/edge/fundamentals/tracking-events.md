---
title: 跟踪事件
seo-title: 跟踪Adobe Experience Platform Web SDK事件
description: 了解如何跟踪Experience Platform Web SDK事件
seo-description: 了解如何跟踪Experience Platform Web SDK事件
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# 跟踪事件

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

要将活动数据发送到Adobe Experience Cloud，请使用该命 `event` 令。 该命 `event` 令是将数据发送到Experience Cloud以及检索个性化内容、身份和受众目标的主要方式。

发送到Adobe Experience Cloud的数据分为两类：

* XDM数据
* 非XDM数据（当前不支持）

## 发送XDM数据

XDM数据是一个对象，其内容和结构与您在Adobe Experience Platform中创建的架构相匹配。 [了解有关如何创建架构的更多信息。](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)

您希望成为分析、个性化、受众或目标的一部分的任何XDM数据都应使用此选项进行发 `xdm` 送。

```javascript
alloy("event", {
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

### 发送非XDM数据

当前，不支持发送与XDM架构不匹配的数据。 支持计划在将来某个日期提供。

### 设置 `eventType`

在XDM体验事件中，有一个字 `eventType` 段。 它保存记录的主要事件类型。 此选项可作为选项的一部分传 `xdm` 入。

```javascript
alloy("event", {
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

或者，也可 `eventType` 以使用选项将该命令传递到事件命 `type` 令中。 在后台，这会添加到XDM数据中。 使用作 `type` 为选项可以更轻松地设置，而 `eventType` 无需修改XDM有效负荷。

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 启动视图

当视图启动时，务必通过在命令中设置来通知 `viewStart` SDK `true``event` 。 这表明，SDK应检索和呈现个性化内容。 即使您目前不使用个性化，它也极大地简化了以后启用个性化或其他功能，因为您无需修改页面代码。 此外，在收集数据后查看分析报告时，跟踪视图也有益。

视图的定义取决于上下文。

* 在常规网站中，每个网页通常被视为一个唯一视图。 在这种情况下，应 `viewStart` 在页 `true` 面顶部尽快执行设置为的事件。
* 在单页应用程序\(SPA\)中，视图定义较少。 它通常意味着用户已在应用程序中导航，并且大部分内容已更改。 对于熟悉单页应用程序技术基础的用户，这通常是在应用程序加载新路径时。 每当用户移动到新视图时，但您选择定义视 _图_，应执行设 `viewStart` 置为 `true` 的事件。

设置为 `viewStart` 的活 `true` 动是向Adobe Experience Cloud发送数据并从Adobe Experience Cloud请求内容的主要机制。 以下是如何开始视图：

```javascript
alloy("event", {
  "viewStart": true,
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

发送数据后，服务器会响应个性化内容等。 此个性化内容会自动呈现到您的视图中。 链接处理函数也会自动附加到新视图的内容。

## 使用sendBeacon API

在网页用户导航离开之前发送事件数据可能很棘手。 如果请求过长，浏览器可能会取消请求。 某些浏览器已实现了一个调用的Web标 `sendBeacon` 准API，以便在此期间更轻松地收集数据。 使用时， `sendBeacon`浏览器会在全局浏览上下文中发出Web请求。 这意味着浏览器在后台发出信标请求，并且不会保留页面导航。 要告知Adobe Experience Platform Web SDK使用， `sendBeacon`请将该选项添 `"documentUnloading": true` 加到event命令。  示例如下：

```javascript
alloy("event", {
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

浏览器对一次可发送的数据量设 `sendBeacon` 置了限制。 在许多浏览器中，限制为64K。 如果浏览器因为负载过大而拒绝该事件，Adobe Experience Platform Web SDK会回退到使用其常规传输方法（例如，提取）。

## 处理来自事件的响应

如果要处理某个事件的响应，可以通知您成功或失败，如下所示：

```javascript
alloy("event", {
  "viewStart": true,
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
}).then(function() {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## 全局修改事件 {#modifying-events-globally}

如果要全局添加、删除或修改活动中的字段，则可以配置回调 `onBeforeEventSend` 。  每次发送事件时都会调用此回调。  此回调在带字段的事件对象中传 `xdm` 递。  修改 `event.xdm` 以更改在活动中发送的数据。

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

`xdm` 字段按以下顺序设置：

1. 作为选项传入事件命令的值 `alloy("event", { xdm: ... });`
2. 自动收集的值。  (请参阅 [自动信息](../reference/automatic-information.md)。)
3. 在回调中所做的 `onBeforeEventSend` 更改。

如果回 `onBeforeEventSend` 调引发异常，则仍会发送该事件；但是，回调中所做的所有更改都不会应用于最终事件。

## 潜在可操作错误

发送事件时，如果发送的数据过大（完整请求的数据量超过32KB），可能会引发错误。 在这种情况下，您需要减少发送的数据量。

启用调试时，服务器同步验证针对所配置的XDM架构发送的事件数据。 如果数据与架构不匹配，则服务器会返回有关不匹配的详细信息并引发错误。 在这种情况下，请修改数据以匹配架构。 当未启用调试时，服务器异步验证数据，因此不会引发相应的错误。
