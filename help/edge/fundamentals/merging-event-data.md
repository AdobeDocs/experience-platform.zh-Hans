---
title: 合并事件数据
seo-title: 合并Adobe Experience Platform Web SDK活动数据
description: 了解如何合并Experience Platform Web SDK事件数据
seo-description: 了解如何合并Experience Platform Web SDK事件数据
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）合并事件数据

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

有时，并非所有数据都在发生事件时可用。 您可能希望捕获您拥有的 _数据_ ，以便在用户关闭浏览器时不会丢失数据。 另一方面，您可能还会包含任何稍后可用的数据。

在这种情况下，您可以将数据与先前事件合并，方 `eventMergeId` 法是按如下方式传递 `event` 命令：

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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

通过在本示例中向两个事件命令传递相同的事件合并ID值，第二事件命令中的数据被增强为先前通过第一事件命令发送的数据。 在Experience Data Platform中会创建每个事件命令的记录，但在报告过程中，这些记录会使用事件合并ID连接在一起，并显示为单个事件。

如果向第三方提供者发送特定事件的相关数据，则也可以包含与该数据相同的事件合并ID。 稍后，如果您选择将第三方数据导入Adobe Experience Platform，则事件合并ID将用于合并因您网页上发生的离散事件而收集的所有数据。

## 生成事件合并ID

事件合并ID值可以是您选择的任何字符串，但请记住，使用同一ID发送的所有事件都将作为单个事件报告，因此，当不应合并事件时，请务必强制执行唯一性。 如果希望SDK代表您生成唯一的事件合并ID(遵循被广泛采用的 [UUID v4规范](https://www.ietf.org/rfc/rfc4122.txt))，则可以使用 `createEventMergeId` 该命令。

与所有命令一样，将返回承诺，因为您可能在SDK完成加载之前执行该命令。 承诺将尽快通过唯一的事件合并ID得到解决。 您可以等待承诺得到解决，然后将数据发送到服务器，如下所示：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
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
    "mergeId": eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": eventMergeId
  });
});
```

如果您出于其他原因想访问活动合并ID（例如，将其发送给第三方提供商），请遵循相同的模式：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  // send event merge ID to a third-party provider
  console.log(eventMergeId);
});
```

## 关于XDM格式的注意事项

在event命令中，实际 `mergeId` 上已将其添加到有 `xdm` 效负荷。  如果需要， `mergeId` 可以作为xdm选项的一部分发送，如下所示：

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
    },
    "eventMergeId": "ABC123"
  }
});
```
