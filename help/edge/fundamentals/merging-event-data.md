---
title: 合并事件数据
seo-title: 合并Adobe Experience Platform Web SDK事件数据
description: 了解如何合并Experience Platform Web SDK事件数据
seo-description: 了解如何合并Experience Platform Web SDK事件数据
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# 合并事件数据

>[!IMPORTANT]
>
>此功能仍在开发中，因此并非所有解决方案都能够合并此数据。

有时，并非所有数据在发生事件时都可用。 您可能希望捕获您拥 _有的_ 数据，以便在用户关闭浏览器时不会丢失数据。 另一方面，您可能还会包含以后将可用的任何数据。

在这种情况下，您可以将事件作为选项传递给 `eventMergeId` 以下命令，从而 `event` 将数据与先前的合并：

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

通过在本例中将相同的事件合并ID值传递给两个事件命令，将第二个事件命令中的数据增强为先前在第一个事件命令上发送的数据。 每个事件命令的记录都在Experience Data Platform中创建，但在报告期间，这些记录使用事件合并ID连接在一起并显示为单个事件。

如果要将特定事件的相关数据发送给第三方提供商，您也可以将同一事件合并ID与该数据包含在一起。 稍后，如果您选择将第三方数据导入Adobe Experience Platform,事件合并ID将用于合并因您网页上发生的离散事件而收集的所有数据。

## 生成事件合并ID

事件合并ID值可以是您选择的任何字符串，但请记住，使用同一ID发送的所有事件都报告为单个事件，因此，当事件不应合并时，请务必强制唯一性。 如果希望SDK代表您生成唯一的事件合并ID(遵循广泛采用的 [UUID v4规范](https://www.ietf.org/rfc/rfc4122.txt))，可以使用 `createEventMergeId` 该命令执行此操作。

与所有命令一样，将返回承诺，因为您可能在SDK完成加载之前执行该命令。 承诺将尽快用唯一的事件合并ID解决。 您可以等待承诺得到解决，然后将数据发送到服务器，如下所示：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});
```

如果您出于其他原因想要访问事件合并ID（例如，将其发送给第三方提供商），请遵循相同的模式：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## 关于XDM格式的注释

在事件命令中， `mergeId` 实际将添加到有 `xdm` 效负荷。  如果需要， `mergeId` 可以将其作为xdm选项的一部分进行发送，如下所示：

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
