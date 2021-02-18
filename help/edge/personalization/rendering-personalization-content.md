---
title: 使用Adobe Experience Platform Web SDK渲染个性化内容
description: 了解如何使用Adobe Experience Platform Web SDK呈现个性化内容。
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 呈现个性化内容

Adobe Experience Platform [!DNL Web SDK]支持在Adobe(包括Adobe Target)查询个性化解决方案。 有两种个性化模式：检索可自动渲染的内容和开发人员必须渲染的内容。 SDK还提供了用于[管理闪烁](../personalization/manage-flicker.md)的工具。

## 自动呈现内容

当您向服务器发送事件并将`renderDecisions`设置为`true`作为事件上的选项时，SDK会自动呈现个性化内容。

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

呈现个性化内容是异步的，因此当特定内容片段是页面的一部分时，不应该有任何假设。

## 手动呈现内容

您可以通过指定`decisionScopes`选项，请求将决策作为`sendEvent`命令的承诺返回的列表。 范围是一个字符串，它让个性化解决方案知道您需要做出哪些决策。

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

这将返回一列表决策，作为每个决策的JSON对象。

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
> 如果使用[!DNL Target]，作用域将变为服务器上的mBoxes，则只一次请求它们，而不是单独请求它们。 全局mbox始终被发送。

### 检索自动内容

如果希望`result.decisions`包含自动可渲染决策，并且NOT have Alloy自动渲染它们，则可以将`renderDecisions`设置为`false`，并包含特殊范围`__view__`。
