---
title: 跟踪事件
seo-title: 跟踪Adobe Experience PlatformWeb SDK事件
description: 了解如何跟踪Experience PlatformWeb SDK事件
seo-description: 了解如何跟踪Experience PlatformWeb SDK事件
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 0%

---


# 跟踪事件

要将事件数据发送到Adobe Experience Cloud，请使用 `sendEvent` 命令。 该 `sendEvent` 命令是将数据发送到并检索个 [!DNL Experience Cloud]性化内容、身份和受众目标的主要方式。

发送到Adobe Experience Cloud的数据分为两个类别:

* XDM数据
* 非XDM数据（当前不支持）

## 发送XDM数据

XDM数据是一个对象，其内容和结构与您在Adobe Experience Platform内创建的模式相匹配。 [进一步了解如何创建模式。](../../xdm/tutorials/create-schema-ui.md)

您希望成为分析、个性化、受众或目标的一部分的任何XDM数据都应使用此选项进 `xdm` 行发送。


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
>
>在XDM字段的每个事件中发送的数据有32 KB的限制。

### 发送非XDM数据

当前，不支持发送与XDM模式不匹配的数据。 支持计划在将来某个日期提供。

### 设置 `eventType`

在XDM体验事件中，有一个可选 `eventType` 字段。 它保存记录的主事件类型。 设置事件类型可以帮助您区分要发送的不同事件。 XDM提供了多种可供您使用的预定义事件类型，或者您始终可以为您的使用案例创建自己的自定义事件类型。 以下是XDM提供的所有预定义事件类型的列表。 [在XDM公共回购协议中阅读更多内容](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)。


| **事件类型:** | **定义:** |
| ---------------------------------- | ------------ |
| advertising.completes | 指示是否已观看完某个定时媒体资产——这并不一定表示查看器已观看整个视频；查看器可能已跳过 |
| advertising.timePlayed | 描述用户在特定定时媒体资产上所花费的时间 |
| advertising.federated | 指示是否通过数据联盟创建体验事件（客户之间的数据共享） |
| advertising.clicks | 广告上的单击操作 |
| advertising.conversions | 客户预定义的操作，其触发事件进行绩效评估 |
| advertising.firstQuartiles | 数字视频广告以正常速度播放了25%的持续时间 |
| advertising.impressions | 广告对有可能被观看的最终用户的印象 |
| advertising.midpoints | 数字视频广告以正常速度播放了50%的持续时间 |
| advertising.starts | 数字视频广告已开始播放 |
| advertising.thirdQuartiles | 数字视频广告以正常速度播放了75%的持续时间 |
| web.webpagedetails.pageViews | 网页视图已发生 |
| web.webinteraction.linkClicks | 已单击Web链接 |
| commerce.checkouts | 在产品列表的结帐过程中执行的操作，如果结帐过程中有多个步骤，则可能有多个结帐事件。 如果有多个步骤，则事件时间信息和引用的页面或体验将用于标识按顺序表示的各个事件的步骤 |
| commerce.productListAdds | 将产品添加到产品列表。 示例将产品添加到购物车 |
| commerce.productListOpens | 新产品列表的初始化。 Example a shopping cart is created |
| commerce.productListRemovals | 从产品列表删除产品条目。 Example a product is removed from a shopping cart |
| commerce.productListReopens | 用户已重新激活不再可访问（已放弃）的产品列表。 通过再营销活动实例 |
| commerce.productListViews | 产品视图已发生 |
| commerce.productViews | 视图已发生 |
| commerce.purchases | 已接受命令。 购买是商务转换中唯一的必需操作。 购买必须引用产品列表 |
| commerce.saveForLaters | 保存产品列表供将来使用。 示例产品需求列表 |
| delivery.feedback | 投放的反馈事件。 电子邮件事件的反馈投放示例 |


如果使用Adobe Experience Platform Launch扩展，这些事件类型将显示在下拉菜单中，或者您始终可以不Experience Platform Launch地传递它们。 它们可以作为选项的一部分传 `xdm` 入。


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

### 覆盖数据集ID

在某些用例中，您可能希望将事件发送到配置UI中配置的数据集以外的数据集。 为此，您需要设置命 `datasetId` 令上的选 `sendEvent` 项：


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 添加身份信息

自定义身份信息也可以添加到事件。 请参 [阅检索Experience CloudID](../identity/overview.md)。

## 使用sendBeacon API

在网页用户导航离开之前发送事件数据可能很棘手。 如果请求过长，浏览器可能会取消请求。 某些浏览器已实现一个调用的Web标 `sendBeacon` 准API，以便在此期间更轻松地收集数据。 使用时， `sendBeacon`浏览器在全局浏览上下文中发出Web请求。 这意味着浏览器在后台发出信标请求，并且不保留页面导航。 要告诉Adobe Experience Platform [!DNL Web SDK] 使用 `sendBeacon`，请将选项添加 `"documentUnloading": true` 到事件命令。  示例如下：


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

浏览器已对一次可发送的数据量 `sendBeacon` 施加限制。 在许多浏览器中，限制为64K。 如果浏览器由于有效负荷过大而拒绝事件，则 [!DNL Web SDK] Adobe Experience Platform将回退到使用其常规传输方法（例如，提取）。

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
2. 自动收集的值。  (请参阅 [自动信息](../data-collection/automatic-information.md)。)
3. 回调中所做的 `onBeforeEventSend` 更改。

如果回 `onBeforeEventSend` 调引发异常，仍会发送事件;但是，回调中所做的任何更改都不会应用于最终事件。

## 可能的可操作错误

发送事件时，如果所发送的数据过大（完整请求的数据量超过32KB），则可能会引发错误。 在这种情况下，您需要减少所发送的数据量。

启用调试时，服务器同步验证针对所配置的XDM事件发送的模式数据。 如果模式与数据不匹配，则服务器会返回有关不匹配的详细信息并引发错误。 在这种情况下，请修改数据以匹配模式。 当未启用调试时，服务器将异步验证数据，因此不会引发相应的错误。
