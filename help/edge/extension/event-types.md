---
title: Adobe Experience Platform Web SDK扩展中的事件类型
description: 了解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的事件类型。
solution: Experience Platform
feature: Web SDK
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 1%

---

# 事件类型

本页介绍Adobe Experience Platform Web SDK标记扩展提供的Adobe Experience Platform事件类型。 这些规则用于[生成规则](https://experienceleague.adobe.com/docs/launch-learn/tutorials/fundamentals/building-rules-in-launch.html)，不应与XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hans)中的[`eventType`字段混淆。

## [!UICONTROL 发送事件结束]

通常，您的资产将具有一个或多个使用[[!UICONTROL Send event]操作](action-types.md#send-event)将事件发送到Adobe Experience Platform边缘网络的规则。 每次将事件发送到边缘网络时，都会向浏览器返回一个包含有用数据的响应。 如果没有[!UICONTROL Send event complete]事件类型，您将无权访问返回的数据。

要访问返回的数据，请创建单独的规则，然后向规则中添加[!UICONTROL Send event complete]事件。 每次由于[!UICONTROL Send event]操作而从服务器收到成功响应时，都会触发此规则。

当[!UICONTROL 发送事件complete]事件触发规则时，它会提供从服务器返回的数据，这些数据对于完成某些任务可能非常有用。 通常，您会将[!UICONTROL Custom code]操作（来自[!UICONTROL Core]扩展）添加到包含[!UICONTROL Send event complete]事件的相同规则中。 在[!UICONTROL Custom code]操作中，您的自定义代码将有权访问名为`event`的变量。 此`event`变量将包含从服务器返回的数据。

用于处理从边缘网络返回的数据的规则可能如下所示：

![](./assets/send-event-complete.png)

以下是如何使用此规则中的[!UICONTROL Custom code]操作执行某些任务的一些示例。

### 手动渲染个性化内容

在用于处理响应数据的规则中的自定义代码操作中，您可以访问从服务器返回的个性化建议。 为此，您需要键入以下自定义代码：

```javascript
var propositions = event.propositions;
```

如果存在`event.propositions`，则它是一个包含个性化建议对象的数组。 该阵列中包含的命题在很大程度上取决于事件如何发送到服务器。

对于第一种情景，假定您尚未选中[!UICONTROL Render decisions]复选框，并且在[!UICONTROL Send event]操作中未提供任何负责发送事件的[!UICONTROL 决策范围]。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此示例中，`propositions`数组仅包含与事件相关的命题，这些命题符合自动渲染的条件。

`propositions`数组可能与以下示例类似：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

发送事件时，未选中[!UICONTROL 渲染决策]复选框，因此SDK不会尝试自动渲染任何内容。 但是，SDK仍会自动检索符合自动渲染条件的内容，并将其提供给您以在您愿意的情况下手动渲染。 请注意，每个命题对象的`renderAttempted`属性都设置为`false`。

如果您在发送事件时改为选中了[!UICONTROL 渲染决策]复选框，则SDK将尝试渲染任何符合自动渲染条件的主张。 因此，每个命题对象的`renderAttempted`属性都将设置为`true`。 在这种情况下，无需手动呈现这些建议。

迄今为止，您仅查看了符合自动渲染条件的个性化内容(例如，在Adobe Target的可视化体验编辑器中创建的任何内容)。 要检索符合自动渲染条件的任何个性化内容&#x200B;_不_，请使用[!UICONTROL Send event]操作中的[!UICONTROL Decision scopes]字段提供决策范围，以请求内容。 范围是一个字符串，用于标识要从服务器检索的特定主张。

[!UICONTROL Send event]操作如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在本例中，如果在与`salutation`或`discount`范围匹配的服务器上找到命题，则会返回这些命题并将其包含在`propositions`阵列中。 请注意，符合自动渲染条件的主题将继续包含在`propositions`数组中，无论您如何在[!UICONTROL Send event]操作中配置[!UICONTROL Render decisions]或[!UICONTROL Decision scopes]字段。 在本例中，`propositions`数组类似于以下示例：

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

此时，您可以根据自己的需求渲染建议内容。 在此示例中，与`discount`范围匹配的命题是使用Adobe Target基于表单的体验编辑器构建的HTML命题。 假设您的页面上有一个ID为`daily-special`的元素，并希望将`discount`命题中的内容渲染到`daily-special`元素中。 执行以下操作：

1. 从`event`对象中提取命题。
1. 回顾每个命题，寻找范围`discount`的命题。
1. 如果您找到一个建议，请循环查看建议中的每个项目，并查找HTML内容的项目。 （检查好过假设。）
1. 如果找到包含HTML内容的项目，请在页面上找到`daily-special`元素，并将其HTML替换为个性化内容。

[!UICONTROL Custom code]操作中的自定义代码可能如下所示：

```javascript
var propositions = event.propositions;

var discountProposition;
if (propositions) {
  // Find the discount proposition, if it exists.
  for (var i = 0; i < propositions.length; i++) {
    var proposition = propositions[i]; 
    if (proposition.scope === "discount") {
      discountProposition = proposition;
      break;
    }
  }
}

var discountHtml;
if (discountProposition) {
  // Find the item from proposition that should be rendered.
  // Rather than assuming there a single item that has HTML
  // content, find the first item whose schema indicates
  // it contains HTML content.
  for (var j = 0; j < discountProposition.items.length; j++) {
    var discountPropositionItem = discountProposition.items[i]; 
    if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
      discountHtml = discountPropositionItem.data.content;
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### 访问Adobe Target响应令牌

从Adobe Target返回的个性化内容包括[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，这些令牌提供了有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可以与第三方工具共享或用于调试。 可以在Adobe Target用户界面中配置响应令牌。

在用于处理响应数据的规则中的自定义代码操作中，您可以访问从服务器返回的个性化建议。 为此，请键入以下自定义代码：

```javascript
var propositions = event.propositions;
```

如果存在`event.propositions`，则它是一个包含个性化建议对象的数组。 有关`result.propositions`内容的更多信息，请参阅[手动渲染个性化内容](#manually-render-personalized-content) 。

假设您希望收集所有由Web SDK自动呈现的主张中的所有活动名称，并将它们推送到单个数组中。 然后，您可以将单个阵列发送给第三方。 在这种情况下，在[!UICONTROL Custom code]操作中写入自定义代码，以：

1. 从`event`对象中提取命题。
1. 回答每个建议。
1. 确定SDK是否提出了建议。
1. 如果是，则循环讨论建议中的每个项目。
1. 从`meta`属性中检索活动名称，该属性是包含响应令牌的对象。
1. 将活动名称推送到数组中。
1. 将活动名称发送给第三方。

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(item.meta);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```





