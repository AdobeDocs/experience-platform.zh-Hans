---
title: 使用Adobe Experience Platform Web SDK跟踪事件
seo-description: 了解如何跟踪Adobe Experience Platform Web SDK事件。
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;文档卸载；onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---


# 跟踪事件

要将事件数据发送到Adobe Experience Cloud，请使用`sendEvent`命令。 `sendEvent`命令是向[!DNL Experience Cloud]发送数据以及检索个性化内容、身份和受众目标的主要方式。

发送到Adobe Experience Cloud的数据分为两个类别:

* XDM数据
* 非XDM数据（当前不支持）

## 发送XDM数据

XDM模式是一个内容和结构与您在Adobe Experience Platform中创建的数据相匹配的对象。 [了解有关如何创建模式的更多信息。](../../xdm/tutorials/create-schema-ui.md)

您希望成为分析、个性化、受众或目标的一部分的任何XDM数据都应使用`xdm`选项发送。


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

在执行`sendEvent`命令和将数据发送到服务器之间（例如，如果Web SDK库尚未完全加载或尚未收到同意）可能会有一段时间。 如果要在执行`sendEvent`命令后修改`xdm`对象的任何部分，强烈建议在&#x200B;_执行`sendEvent`命令之前克隆`xdm`对象_。 例如：

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

在此示例中，通过将数据层序列化为JSON，然后反序列化来克隆数据层。 接下来，克隆结果将传递到`sendEvent`命令中。 这样做可确保`sendEvent`命令具有数据层的快照，就像执行`sendEvent`命令时一样，这样以后对原始数据层对象的修改不会反映在发送到服务器的数据中。 如果您使用事件驱动的数据层，克隆数据可能已自动处理。 例如，如果您使用[Adobe客户端数据层](https://github.com/adobe/adobe-client-data-layer/wiki)，则`getState()`方法将提供所有先前更改的计算的克隆快照。 如果您使用Adobe Experience Platform Launch中的Adobe Experience Platform Web SDK扩展，也会自动为您处理此问题。

>[!NOTE]
>
>在XDM字段的每个事件中可以发送的数据有32 KB的限制。

### 发送非XDM数据

当前，不支持发送与XDM模式不匹配的数据。 支持计划在将来某个日期提供。

### 设置 `eventType`

在XDM体验事件中，有一个可选的`eventType`字段。 它保存记录的主事件类型。 设置事件类型可以帮助您区分要发送的不同事件。 XDM提供了几种可供您使用的预定义事件类型，或者您始终可以为您的使用案例创建自己的自定义事件类型。 以下是XDM提供的所有预定义事件类型的列表。 [阅读XDM公开回购协议中的更多内容](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)。


| **事件类型:** | **定义:** |
| ---------------------------------- | ------------ |
| advertising.completes | 指示是否观看了某个定时媒体资产的完成 — 这不一定表示查看者观看了整个视频；查看器可能已跳过 |
| advertising.timePlayed | 描述用户在特定定时媒体资产上所花费的时间 |
| advertising.federated | 指示是否通过数据联盟创建体验事件（客户之间的数据共享） |
| advertising.clicks | 广告上的单击操作 |
| advertising.conversions | 客户预定义的操作，触发事件进行绩效评估 |
| advertising.firstQuartiles | 数字视频广告以正常速度播放了25%的持续时间 |
| advertising.impressions | 广告给具有被观看潜力的最终用户的印象 |
| advertising.midpoints | 数字视频广告以正常速度播放了50%的持续时间 |
| advertising.starts | 数字视频广告已开始播放 |
| advertising.thirdQuartiles | 数字视频广告以正常速度播放了75%的持续时间 |
| web.webpagedetails.pageViews | 视图网页 |
| web.webinteraction.linkClicks | 已单击Web链接 |
| commerce.checkouts | 在产品列表的结帐过程中的操作，如果结帐过程中有多个步骤，则可能有多个结帐事件。 如果有多个步骤，则事件时间信息和引用的页面或体验将用于标识按顺序表示的各个事件的步骤 |
| commerce.productListAdds | 将产品添加到产品列表。 Example a product is added to a shopping cart |
| commerce.productListOpens | 新产品列表的初始化。 Example a shopping cart is created |
| commerce.productListRemovals | 从产品列表中删除产品条目。 Example a product is removed from a shopping cart |
| commerce.productListReopens | 用户已重新激活不再可访问（已放弃）的产品列表。 通过再营销活动 |
| commerce.productListViews | 视图产品列表 |
| commerce.productViews | 产品视图已发生 |
| commerce.purchases | 已接受命令。 购买是商务转化中唯一必需的操作。 购买必须引用产品列表 |
| commerce.saveForLaters | 产品列表保存以备将来使用。 产品需求示例列表 |
| delivery.feedback | 针对投放的反馈事件。 电子邮件事件的反馈投放示例 |


如果使用Adobe Experience Platform Launch扩展，这些事件类型将显示在下拉列表中，或者您始终可以在不Experience Platform Launch的情况下传入它们。 它们可以作为`xdm`选项的一部分传入。


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

或者，可以使用`type`选项将`eventType`传递到事件命令中。 在后台，这会添加到XDM数据中。 将`type`作为选项可让您更轻松地设置`eventType`，而无需修改XDM有效负荷。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆盖数据集ID

在某些情况下，您可能希望将事件发送到配置UI中配置的数据集以外的数据集。 为此，您需要在`sendEvent`命令上设置`datasetId`选项：


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 添加身份信息

自定义身份信息也可以添加到事件。 请参阅[检索Experience CloudID](../identity/overview.md)。

## 使用sendBeacon API

在网页用户离开之前发送事件数据可能很棘手。 如果请求过长，浏览器可能会取消该请求。 一些浏览器已实现了一个名为`sendBeacon`的Web标准API，以便在此期间更轻松地收集数据。 使用`sendBeacon`时，浏览器在全局浏览上下文中发出Web请求。 这意味着浏览器在后台发出信标请求，并且不会保留页面导航。 要告诉Adobe Experience Platform [!DNL Web SDK]使用`sendBeacon`，请将选项`"documentUnloading": true`添加到事件命令。  示例如下：


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

浏览器已对一次可与`sendBeacon`一起发送的数据量施加了限制。 在许多浏览器中，限制为64K。 如果浏览器因负载过大而拒绝事件,Adobe Experience Platform [!DNL Web SDK]将回退到使用其常规传输方法（例如，提取）。

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

## 全局修改事件{#modifying-events-globally}

如果要从事件全局添加、删除或修改字段，可以配置`onBeforeEventSend`回调。  每次发送事件时都会调用此回调。  此回调在具有`xdm`字段的事件对象中传递。  修改`event.xdm`以更改在事件中发送的数据。


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

`xdm` 按此顺序设置字段：

1. 作为选项传入的值传递给事件命令`alloy("sendEvent", { xdm: ... });`
2. 自动收集的值。  （请参阅[自动信息](../data-collection/automatic-information.md)。）
3. 在`onBeforeEventSend`回调中所做的更改。

如果`onBeforeEventSend`回调引发异常，则仍会发送事件;但是，在回调中所做的任何更改都不会应用于最终事件。

## 可能的可操作错误

发送事件时，如果发送的数据太大（完整请求超过32KB），可能会引发错误。 在这种情况下，您需要减少发送的数据量。

启用调试时，服务器同步验证正在针对所配置的XDM模式发送的事件数据。 如果模式不匹配，则服务器会返回有关不匹配的详细信息，并引发错误。 在这种情况下，请修改数据以匹配模式。 当未启用调试时，服务器将异步验证数据，因此不会引发相应的错误。
