---
title: 使用Adobe Experience Platform Web SDK访问响应令牌
description: 了解如何使用Adobe Experience Platform Web SDK访问响应令牌。
keywords: 个性化；Target;Adobe Target;renderDecisions;sendEvent;decisionScopes;result.decisions，响应令牌；
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 访问响应令牌

从Adobe Target返回的个性化内容包括[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，这些令牌提供了有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可以与第三方工具共享或用于调试。 可以在Adobe Target用户界面中配置响应令牌。

要访问任何个性化内容，请在发送事件时提供回调函数。 SDK在收到来自服务器的成功响应后，将调用此回调。 将为您的回调提供一个`result`对象，该对象可能包含包含任何返回的个性化内容的`propositions`属性。 以下是提供回调函数的示例。

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

在此示例中， `result.propositions`（如果存在）是一个数组，其中包含与事件相关的个性化建议。 有关`result.propositions`内容的更多信息，请参阅[渲染个性化内容](../rendering-personalization-content.md) 。

假设您要收集所有由Web SDK自动呈现的主张中的所有活动名称，并将它们推送到单个数组中。 然后，您可以将单个阵列发送给第三方。 在这种情况下：

1. 从`result`对象中提取命题。
1. 回答每个建议。
1. 确定SDK是否提出了建议。
1. 如果是，则循环讨论建议中的每个项目。
1. 从`meta`属性中检索活动名称，该属性是包含响应令牌的对象。
1. 将活动名称推送到数组中。
1. 将活动名称发送给第三方。

您的代码如下所示：

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```


