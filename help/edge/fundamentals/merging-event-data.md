---
title: 在Adobe Experience Platform Web SDK中合并事件数据
description: 了解如何合并Experience Platform Web SDK事件数据
keywords: merge;事件数据；eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise;合并Id承诺；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# 合并事件数据

>[!IMPORTANT]
>
>此功能仍在开发中。 并非所有解决方案都能如本页所述合并事件数据。

有时，并非所有数据在发生事件时都可用。 您可能希望捕获您拥有的数据，以便在用户关闭浏览器时不会丢失数据。 另一方面，您可能还会包含任何稍后将可用的数据。

在这种情况下，您可以通过将`mergeId`作为选项传递给`event`命令，将数据与先前事件合并，如下所示：

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
  },
  "mergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
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
  },
  "mergeId": "ABC123"
});
```

通过将`mergeId`选项的相同值传递给本例中的两个事件命令，将第二个事件命令中的数据增强为先前通过第一个事件命令发送的数据。 在[!DNL Experience Data Platform]中创建每个事件命令的记录，但在报告期间，使用事件合并ID将记录连接在一起，并显示为单个事件。

如果向第三方提供商发送有关特定事件的数据，则也可以包含与该数据相同的事件合并ID。 稍后，如果您选择将第三方数据导入Adobe Experience Platform,事件合并ID将用于合并因您网页上发生的离散事件而收集的所有数据。

## 生成事件合并ID

事件合并ID可以是您选择的任何字符串，但请记住，使用相同ID发送的所有事件都报告为单个事件，因此，当事件不应合并时，请务必强制实现唯一性。 如果希望SDK代表您生成唯一的事件合并ID（遵循被广泛采用的[ UUID v4规范](https://www.ietf.org/rfc/rfc4122.txt)），则可以使用`createEventMergeId`命令执行此操作。

与所有命令一样，将返回一个承诺，因为您可能在SDK完成加载之前执行该命令。 承诺将尽快使用唯一的事件合并ID解决。 您可以等待承诺得到解析，然后将数据发送到服务器，如下所示：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    },
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
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
    },
    "mergeId": results.eventMergeId
  });
});
```

如果您出于其他原因(例如，要将事件合并ID发送到第三方提供商)而希望访问该ID，请遵循相同的模式：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## 关于XDM格式的注意事项

在事件命令中，事件合并ID将代表您添加到`xdm`有效负荷中正确的位置。  如果需要，可以将事件合并ID作为`xdm`选项的一部分进行发送，如下所示：

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
    },
    "eventMergeId": "ABC123"
  }
});
```

将事件合并ID直接添加到`xdm`对象时，请注意名称`eventMergeID`是使用的，而不是`mergeId`。
