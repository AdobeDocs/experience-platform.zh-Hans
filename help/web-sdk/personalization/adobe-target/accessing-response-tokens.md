---
title: 使用Adobe Experience Platform Web SDK访问响应令牌
description: 了解如何使用Adobe Experience Platform Web SDK访问响应令牌。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；decisionScopes；result.decisions，响应令牌；
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 访问响应令牌

从Adobe Target返回的个性化内容包括 [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，其中包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 响应令牌可在Adobe Target用户界面中配置。

要访问任何个性化内容，请在发送事件时提供回调函数。 SDK收到来自服务器的成功响应后，将调用此回调。 将为您的回调提供 `result` 对象，其中可能包含 `propositions` 包含任何返回的个性化内容的属性。 以下是提供回调函数的示例。

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

在此示例中， `result.propositions`如果存在，则是一个数组，其中包含与事件相关的个性化建议。 请参阅 [呈现个性化内容](../rendering-personalization-content.md) ，以了解有关 `result.propositions`.

假设您要从Web SDK自动渲染的所有建议中收集所有活动名称，并将它们推入单个数组中。 然后，您可以将单个阵列发送给第三方。 在本例中：

1. 从提取建议 `result` 对象。
1. 循环访问每个建议。
1. 确定SDK是否呈现建议。
1. 如果是，则循环遍历建议中的每个项目。
1. 从检索活动名称 `meta` 属性，是包含响应令牌的对象。
1. 将活动名称推入数组。
1. 将活动名称发送给第三方。

您的代码将如下所示：

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
