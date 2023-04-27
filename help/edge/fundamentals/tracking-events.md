---
title: 使用Adobe Experience Platform Web SDK跟踪事件
description: 了解如何跟踪Adobe Experience Platform Web SDK事件。
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon；发送信标；documentUnloading；文档卸载；onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 跟踪事件

要将事件数据发送到Adobe Experience Cloud，请使用 `sendEvent` 命令。 的 `sendEvent` 命令是将数据发送到 [!DNL Experience Cloud]，以及检索个性化内容、身份和受众目标。

发送到Adobe Experience Cloud的数据分为两类：

* XDM数据
* 非XDM数据

## 发送XDM数据

XDM数据是一个对象，其内容和结构与您在Adobe Experience Platform中创建的架构相匹配。 [详细了解如何创建模式。](../../xdm/tutorials/create-schema-ui.md)

您希望成为分析、个性化、受众或目标一部分的任何XDM数据都应使用 `xdm` 选项。


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

在 `sendEvent` 命令，并且数据被发送到服务器时（例如，如果Web SDK库尚未完全加载或尚未收到同意），将执行该命令。 如果您打算修改 `xdm` 对象 `sendEvent` 命令，强烈建议您克隆 `xdm` 对象 _之前_ 执行 `sendEvent` 命令。 例如：

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

在此示例中，数据层通过序列化到JSON并反序列化来克隆。 接下来，克隆的结果将传递到 `sendEvent` 命令。 这样做可确保 `sendEvent` 命令具有数据层的快照，该快照与 `sendEvent` 命令，以便以后对原始数据层对象的修改不会反映在发送到服务器的数据中。 如果您使用事件驱动的数据层，则克隆数据可能已经自动处理。 例如，如果您使用 [Adobe客户端数据层](https://github.com/adobe/adobe-client-data-layer/wiki), `getState()` 方法提供所有先前更改的计算克隆快照。 如果您使用Adobe Experience Platform Web SDK标记扩展，也会自动为您处理此问题。

>[!NOTE]
>
>在XDM字段中，每个事件中可发送的数据均受32 KB的限制。


## 发送非XDM数据

与XDM架构不匹配的数据应使用 `data` 的 `sendEvent` 命令。 Web SDK版本2.5.0及更高版本支持此功能。

如果您需要更新Adobe Target配置文件或发送Target Recommendations属性，此操作将非常有用。 [阅读有关这些Target功能的更多信息。](../personalization/adobe-target/target-overview.md#single-profile-update)

将来，您将能够在 `data` ，并将其映射到XDM服务器端。

**如何将用户档案和Recommendations属性发送到Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### 设置 `eventType` {#event-types}

在XDM ExperienceEvent架构中，有一个可选 `eventType` 字段。 它保存记录的主事件类型。 设置事件类型可以帮助您区分要发送的不同事件。 XDM提供了多种预定义事件类型，您可以使用这些类型，也可以始终为用例创建自己的自定义事件类型。 有关 [所有预定义事件类型的列表](../../xdm/classes/experienceevent.md#eventType).

如果使用标记扩展，则这些事件类型将显示在下拉菜单中，或者您始终可以在不使用标记的情况下传递它们。 它们可以作为 `xdm` 选项。


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

或者， `eventType` 可以使用 `type` 选项。 在后台，会将其添加到XDM数据中。 拥有 `type` 作为选项，您可以更轻松地设置 `eventType` 无需修改XDM有效负载。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆盖数据集ID

>[!IMPORTANT]
>
>的 `datasetId` 选项受支持 `sendEvent` 命令已弃用。 要覆盖数据集ID，请使用 [配置覆盖](../datastreams/overrides.md) 中。

在某些用例中，您可能希望将事件发送到配置UI中配置的数据集以外的数据集。 为此，您需要将 `datasetId` 选项 `sendEvent` 命令：



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 添加身份信息

也可以将自定义身份信息添加到事件中。 请参阅 [检索Experience CloudID](../identity/overview.md).

## 使用sendBeacon API

在网页用户导航离开之前发送事件数据可能会比较困难。 如果请求过长，浏览器可能会取消该请求。 某些浏览器实施了名为的Web标准API `sendBeacon` 以便在此期间更轻松地收集数据。 使用 `sendBeacon`，则浏览器会在全局浏览上下文中发出web请求。 这意味着浏览器在后台发出信标请求，并且不会保留页面导航。 告诉Adobe Experience Platform [!DNL Web SDK] 使用 `sendBeacon`，添加选项 `"documentUnloading": true` 命令。  示例如下：


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

浏览器对可随之发送的数据量施加了限制 `sendBeacon` 一次。 在许多浏览器中，限制为64K。 如果浏览器由于负载过大而拒绝该事件，则Adobe Experience Platform [!DNL Web SDK] 回退到使用其正常传输方法（例如，获取）。

## 处理来自事件的响应

如果要处理来自事件的响应，可通知您成功或失败，如下所示：


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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### 的 `result` 对象

的 `sendEvent` 命令返回通过 `result` 对象。 的 `result` 对象包含以下属性：

**命题**:访客符合条件的个性化选件。 [进一步了解建议。](../personalization/rendering-personalization-content.md#manually-rendering-content)

**决策**:此属性已弃用。 请改用 `propositions`。

**目标**:可与外部个性化平台、内容管理系统、广告服务器以及客户网站上运行的其他应用程序共享的Adobe Experience Platform区段。 [进一步了解目标。](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` 目前处于测试阶段。 文档和功能可能会发生更改。

## 全局修改事件 {#modifying-events-globally}

如果要全局添加、删除或修改事件中的字段，可以配置 `onBeforeEventSend` 回调。  每次发送事件时都会调用此回调。  此回调在事件对象中通过 `xdm` 字段。  修改 `content.xdm` 更改随事件发送的数据。


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 按以下顺序设置字段：

1. 作为选项传递到事件命令的值 `alloy("sendEvent", { xdm: ... });`
2. 自动收集的值。  (请参阅 [自动信息](../data-collection/automatic-information.md).)
3. 在 `onBeforeEventSend` 回调。

关于 `onBeforeEventSend` 回调：

* 可以在回调期间修改事件XDM。 返回回调后，随事件发送content.xdm和content.data对象的任何修改字段和值。

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 如果回调引发异常，则会中断对事件的处理，并且不会发送事件。
* 如果回调返回布尔值 `false`，则事件处理将中断，且没有错误，并且不会发送事件。 此机制允许通过检查事件数据并返回来轻松忽略某些事件 `false` 如果不应发送该事件。

   >[!NOTE]
   >应当注意避免在页面上的第一个事件时返回false。 在第一个事件中返回false可能会对个性化造成负面影响。

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

除布尔值之外的任何返回值 `false` 将允许该事件在回调后处理和发送。

* 可以通过检查事件类型来过滤事件(请参阅 [事件类型](#event-types)):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## 潜在可操作错误

发送事件时，如果发送的数据过大（完整请求的数据大于32 KB），可能会引发错误。 在这种情况下，您需要减少发送的数据量。
