---
title: Adobe Experience Platform Web SDK扩展中的事件类型
description: 了解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的事件类型。
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 666e8c6fcccf08d0841c5796677890409b22d794
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 0%

---

# 事件类型

本页介绍由Adobe Experience Platform Web SDK标记扩展提供的Adobe Experience Platform事件类型。 它们用于[生成规则](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=zh-Hans)，不应与[`xdm`对象](/help/web-sdk/commands/sendevent/xdm.md)中的`eventType`字段混淆。

## [!UICONTROL 发送事件完成]

通常，您的属性将有一个或多个使用[[!UICONTROL 发送事件]操作](action-types.md#send-event)将事件发送到Adobe Experience PlatformEdge Network的规则。 每次将事件发送到Edge Network时，系统都会向浏览器返回包含有用数据的响应。 如果没有[!UICONTROL 发送事件完成]事件类型，您将无法访问此返回的数据。

要访问返回的数据，请创建一个单独的规则，然后向该规则添加一个[!UICONTROL 发送事件结束]事件。 每次通过[!UICONTROL 发送事件]操作从服务器收到成功响应时，都会触发此规则。

当[!UICONTROL 发送事件完成]事件触发规则时，它会提供从服务器返回的数据，这些数据可能有助于完成某些任务。 通常，您将向包含[!UICONTROL 发送事件完成]事件的同一规则添加[!UICONTROL 自定义代码]操作（来自[!UICONTROL Core]扩展）。 在[!UICONTROL 自定义代码]操作中，您的自定义代码将有权访问名为`event`的变量。 此`event`变量将包含从服务器返回的数据。

用于处理从Edge Network返回的数据的规则可能如下所示：

![](assets/send-event-complete.png)

以下是如何使用此规则中的[!UICONTROL Custom code]操作执行某些任务的示例。

### 手动呈现个性化内容

在处理响应数据的规则中的Custom Code操作中，您可以访问从服务器返回的个性化建议。 为此，您需要键入以下自定义代码：

```javascript
var propositions = event.propositions;
```

如果`event.propositions`存在，则它是一个包含个性化建议对象的数组。 数组中包括的建议在很大程度上取决于事件发送到服务器的方式。

对于第一个方案，假设您未选中[!UICONTROL 渲染决策]复选框，并且未在负责发送事件的[!UICONTROL 发送事件]操作中提供任何[!UICONTROL 决策范围]。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此示例中，`propositions`数组仅包含与事件相关的建议，这些建议适用于自动渲染。

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

发送事件时，未选中[!UICONTROL 渲染决策]复选框，因此SDK不会尝试自动渲染任何内容。 但是，SDK仍会自动检索符合自动渲染条件的内容，并在需要时为您提供该内容以手动渲染。 请注意，每个建议对象的`renderAttempted`属性均设置为`false`。

如果您在发送事件时选中了[!UICONTROL 渲染决策]复选框，则SDK会尝试渲染任何符合自动渲染条件的建议。 因此，每个建议对象的`renderAttempted`属性都将设置为`true`。 在这种情况下，无需手动呈现这些建议。

到目前为止，您仅查看了符合自动呈现条件的个性化内容(例如，在Adobe Target可视化体验编辑器中创建的任何内容)。 要检索任何个性化内容&#x200B;_不_&#x200B;适合自动呈现，请使用[!UICONTROL 发送事件]操作中的[!UICONTROL 决策范围]字段提供决策范围，以请求该内容。 范围是一个字符串，它标识您要从服务器检索的特定建议。

[!UICONTROL 发送事件]操作如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在此示例中，如果在与`salutation`或`discount`范围匹配的服务器上找到建议，则将返回这些建议并将其包含在`propositions`数组中。 请注意，符合自动呈现条件的建议将继续包含在`propositions`数组中，无论您如何在[!UICONTROL 发送事件]操作中配置[!UICONTROL 呈现决策]或[!UICONTROL 决策范围]字段。 在这种情况下，`propositions`数组将与以下示例类似：

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

此时，您可以根据需要呈现建议内容。 在此示例中，与`discount`范围匹配的建议是使用Adobe Target的基于表单的HTML编辑器构建的体验建议。 假设您的页面上有一个ID为`daily-special`的元素，并希望将`discount`建议中的内容渲染到`daily-special`元素中。 执行以下操作：

1. 从`event`对象提取建议。
1. 循环遍历每个建议，查找范围为`discount`的建议。
1. 如果您找到一个建议，请循环遍历建议中的每个项目，查找包含HTML内容的项目。 （检查总比假设要好。 ）
1. 如果找到一个包含HTML内容的项目，请在页面上找到`daily-special`元素，并将其HTML替换为个性化内容。

您在[!UICONTROL Custom code]操作中的自定义代码可能如下所示：

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

从Adobe Target返回的Personalization内容包括[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，这些令牌包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 响应令牌可在Adobe Target用户界面中配置。

在处理响应数据的规则中的Custom Code操作中，您可以访问从服务器返回的个性化建议。 为此，请键入以下自定义代码：

```javascript
var propositions = event.propositions;
```

如果`event.propositions`存在，则它是一个包含个性化建议对象的数组。 有关`result.propositions`内容的更多信息，请参阅[手动渲染个性化内容](#manually-render-personalized-content)。

假设您想从Web SDK自动渲染的所有建议中收集所有活动名称，并将它们推入单个数组中。 然后，您可以将单个阵列发送给第三方。 在这种情况下，请在[!UICONTROL Custom code]操作中将自定义代码写入：

1. 从`event`对象提取建议。
1. 循环访问每个建议。
1. 确定SDK是否呈现建议。
1. 如果是，则循环遍历建议中的每个项目。
1. 从`meta`属性中检索活动名称，该属性是包含响应令牌的对象。
1. 将活动名称推入数组。
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

## [!UICONTROL 订阅规则集项] {#subscribe-ruleset-items}

**[!UICONTROL 订阅规则集项]**&#x200B;事件类型允许您为表面订阅Adobe Journey Optimizer内容卡。 无论何时评估规则集，提供给此命令的回调都会接收一个结果对象，该结果对象具有保存内容卡数据的建议。

![显示Experience Platform规则集项目事件类型的Subscribe Tags用户界面图像。](assets/subscribe-ruleset-items.png)

此事件类型支持以下可配置的属性：

* **[!UICONTROL 架构]**：要订阅内容卡的架构数组。 您可以手动输入架构，也可以通过提供数据元素来输入架构。
* **[!UICONTROL Surfaces]**：要订阅内容卡片的表面数组。 可以手动输入曲面，也可以通过提供数据元素来输入曲面。
