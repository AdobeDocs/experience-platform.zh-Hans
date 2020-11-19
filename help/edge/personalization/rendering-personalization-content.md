---
title: 呈现个性化内容
seo-title: Adobe Experience PlatformWeb SDK渲染个性化内容
description: 了解如何使用Experience PlatformWeb SDK呈现个性化内容
seo-description: 了解如何使用Experience PlatformWeb SDK呈现个性化内容
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# 个性化选项概述

Adobe Experience Platform [!DNL Web SDK] 支持在包括Adobe Target在内的Adobe查询个性化解决方案。 有两种个性化模式：检索可自动渲染的内容和开发人员必须渲染的内容。 SDK还提供管理闪 [烁的工具](../personalization/manage-flicker.md)。

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

呈现个性化内容是异步的，因此当特定内容是页面的一部分时，不应存在任何假设。

## 手动呈现内容

通过指定选项，您可以请求作为对命令的承诺返回 `sendEvent` 的决策列表 `decisionScopes` 。 范围是让个性化解决方案知道您需要做出哪些决策的字符串。

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

这将返回一列表决策作为每个决策的JSON对象。

```json
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

>[!TIP]
>
> 如果您使 [!DNL Target]用，范围将变为服务器上的mBoxes，只一次请求它们，而不是单独请求它们。 全局mbox始终会发送。

### 检索自动内容

如果您希望包含自 `result.decisions` 动可渲染决策并且“不具有合金”(Not Have Alloy)自动渲染它们，可以将其设 `renderDecisions` 置 `false`为，并包括特殊范围 `__view__`。
