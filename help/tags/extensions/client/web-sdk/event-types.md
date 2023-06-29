---
title: Adobe Experience Platform Web SDK扩展中的事件类型
description: 了解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的事件类型。
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 2772660936444e39124a75deda6f78d97f7793f2
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 事件类型

本页介绍了由Adobe Experience Platform Web SDK标记扩展提供的Adobe Experience Platform事件类型。 这些已用于 [生成规则](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) 也不应混淆 [`eventType` xdm中的字段](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hans).

## [!UICONTROL 发送事件完成]

通常，您的资产会有一个或多个规则使用 [[!UICONTROL 发送事件] 操作](action-types.md#send-event) 将事件发送到Adobe Experience Platform Edge Network。 每次将事件发送到Edge Network时，都会向浏览器返回一个包含有用数据的响应。 不使用 [!UICONTROL 发送事件完成] 事件类型时，您将无权访问此返回的数据。

要访问返回的数据，请创建一个单独的规则，然后添加 [!UICONTROL 发送事件完成] 事件到规则。 每次从服务器收到作为响应结果而发出的成功响应时，都会触发此规则。 [!UICONTROL 发送事件] 操作。

当 [!UICONTROL 发送事件完成] 事件触发规则，它提供从服务器返回的数据，这些数据可能有助于完成某些任务。 通常，您将添加 [!UICONTROL 自定义代码] 操作(来自 [!UICONTROL 核心] 扩展名)添加到包含 [!UICONTROL 发送事件完成] 事件。 在 [!UICONTROL 自定义代码] 操作，则自定义代码将有权访问名为的变量 `event`. 此 `event` 变量将包含从服务器返回的数据。

用于处理从Edge Network返回的数据的规则可能如下所示：

![](assets/send-event-complete.png)

以下是如何使用执行某些任务的一些示例 [!UICONTROL 自定义代码] 操作。

### 手动渲染个性化内容

在处理响应数据的规则中的Custom Code操作中，您可以访问从服务器返回的个性化建议。 为此，您需要键入以下自定义代码：

```javascript
var propositions = event.propositions;
```

如果 `event.propositions` 存在，它是一个包含个性化建议对象的数组。 数组中包括的建议在很大程度上取决于将事件发送到服务器的方式。

对于第一个方案，假定您尚未检查 [!UICONTROL 渲染决策] 复选框，但未提供任何 [!UICONTROL 决策范围] 内部 [!UICONTROL 发送事件] 负责发送事件的操作。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此示例中， `propositions` 数组仅包含与事件相关的建议，这些建议符合自动渲染的条件。

此 `propositions` 数组可能与以下示例类似：

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

发送事件时， [!UICONTROL 渲染决策] 未选中复选框，因此SDK不会尝试自动渲染任何内容。 但是，SDK仍会自动检索符合自动渲染条件的内容，并在您希望手动渲染时提供该内容。 请注意，每个建议对象都有其 `renderAttempted` 属性设置为 `false`.

如果您选择的是 [!UICONTROL 渲染决策] 复选框。在发送事件时，SDK会尝试渲染任何符合自动渲染条件的建议。 因此，每个建议对象将具有其 `renderAttempted` 属性设置为 `true`. 在这种情况下，无需手动呈现这些建议。

到目前为止，您仅查看了符合自动呈现条件的个性化内容(例如，在Adobe Target可视化体验编辑器中创建的任何内容)。 检索任何个性化内容 _非_ 符合自动呈现的条件，通过使用提供决策范围来请求内容 [!UICONTROL 决策范围] 中的字段 [!UICONTROL 发送事件] 操作。 范围是一个字符串，它标识您要从服务器检索的特定建议。

此 [!UICONTROL 发送事件] 操作将如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在此示例中，如果在服务器上找到与 `salutation` 或 `discount` 范围，它们将返回并包含在 `propositions` 数组。 请注意，符合自动呈现条件的主张将继续包含在 `propositions` 阵列，无论如何配置 [!UICONTROL 渲染决策] 或 [!UICONTROL 决策范围] 中的字段 [!UICONTROL 发送事件] 操作。 此 `propositions` 在此例中，数组类似于以下示例：

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

此时，您可以按照自己认为合适的方式呈现建议内容。 在此示例中，建议与 `discount` scope是使用Adobe Target的基于表单的HTML编辑器构建的体验建议。 假设您的页面上有一个元素，其ID为 `daily-special` 并希望从呈现内容 `discount` 中的建议 `daily-special` 元素。 执行以下操作：

1. 从提取建议 `event` 对象。
1. 循环查看每个建议，寻找具有以下范围的建议： `discount`.
1. 如果您找到一个建议，请循环遍历建议中的每个项目，查找内容为HTML的项目。 (检查总比假设要好。
1. 如果找到一个包含HTML内容的项目，请找到 `daily-special` 元素，并将其HTML替换为个性化内容。

您在中的自定义代码 [!UICONTROL 自定义代码] 操作可能如下所示：

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

从Adobe Target返回的个性化内容包括 [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，其中包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 可在Adobe Target用户界面中配置响应令牌。

在处理响应数据的规则中的Custom Code操作中，您可以访问从服务器返回的个性化建议。 为此，请键入以下自定义代码：

```javascript
var propositions = event.propositions;
```

如果 `event.propositions` 存在，它是一个包含个性化建议对象的数组。 参见 [手动渲染个性化内容](#manually-render-personalized-content) ，以了解有关 `result.propositions`.

假设您要从Web SDK自动渲染的所有建议中收集所有活动名称，并将它们推入单个数组中。 然后，您可以将单个阵列发送给第三方。 在这种情况下，请将自定义代码写入 [!UICONTROL 自定义代码] 操作目标：

1. 从提取建议 `event` 对象。
1. 循环访问每个建议。
1. 确定SDK是否呈现了建议。
1. 如果是这样，则循环访问建议中的每个项目。
1. 从检索活动名称 `meta` 属性，它是一个包含响应令牌的对象。
1. 将活动名称推入数组中。
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
            activityNames.push(activityName);  
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
