---
title: 呈现个性化内容
seo-title: Adobe Experience Platform Web SDK渲染个性化内容
description: 了解如何使用Experience Platform Web SDK呈现个性化内容
seo-description: 了解如何使用Experience Platform Web SDK呈现个性化内容
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# 个性化选项概述

Adobe Experience Platform Web SDK支持在Adobe查询个性化解决方案，包括Adobe目标。 有两种个性化模式： 检索可自动渲染的内容和开发人员必须渲染的内容。 SDK还提供管理闪 [烁的工具](../../edge/solution-specific/target/flicker-management.md)。

## 自动呈现内容

当您将事件发送到服务器并设置为事件上的选项时，SDK `renderDecisions` 会自动 `true` 呈现个性化内容。

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
});
```

个性化内容的呈现是异步的，因此当特定内容片段是页面的一部分时，不应存在任何假设。

## 手动呈现内容

您可以使用来请求作为对命令的承诺返回决策 `event` 的列表 `scopes`。 范围是让个性化解决方案知道您需要做出哪些决策的字符串。

```javascript
alloy("sendEvent",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
    }
  })
```

这将返回一列表决策作为每个决策的JSON对象。

```javascript
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

{info}如果您使用目标作用域在服务器上变为mBoxes，则只有它们一次是所有请求，而不是单独请求。 全局mbox始终会发送。
{info}

### 检索自动内容

如果您希望包含 `result.decisions` 可渲染的自动决策，可以将 `renderDecisions` 其设置为false并包含特殊范围 `__view__`
