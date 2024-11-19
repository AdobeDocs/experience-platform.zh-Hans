---
title: 在Web SDK中管理显示事件
description: 本文介绍了什么是显示事件以及如何在Web SDK中使用它们。
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# 在Web SDK中管理显示事件

当页面上显示特定的个性化内容时，Web SDK会使用显示事件来通知您的个性化或分析服务。

发送显示事件可提高个性化量度的准确性，并让您准确大致了解用户在您的页面上看到的内容。

Web SDK允许您通过两种方式发送显示事件：

* [自动](#send-automatically)，紧跟个性化内容在页面上呈现之后。 有关详细信息，请参阅有关如何[渲染个性化内容](rendering-personalization-content.md)的文档。
* [手动](#send-sendEvent-calls)，通过后续`sendEvent`调用。

>[!NOTE]
>
>调用`applyPropositions`函数时不会自动发送显示事件。

## 自动发送显示事件 {#send-automatically}

发送显示事件会自动提供更准确的分析量度，因为事件会在个性化加载后立即发送。 此实施还具有更简化的实施方法。

要在页面上呈现个性化内容后自动发送显示事件，必须配置以下参数：

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true`或未指定

Web SDK在作为`sendEvent`调用的结果呈现任何个性化设置后立即发送显示事件。

## 在后续sendEvent调用中发送显示事件 {#send-sendEvent-calls}

与[自动](#send-automatically)发送显示事件相比，当您将其包含在后续`sendEvent`调用中时，您还有机会在调用中包含有关页面加载的更多信息。 这可能是额外的信息，在请求个性化内容时不可用。

此外，在使用Adobe Analytics时，在`sendEvent`调用中发送显示事件可最大限度地减少跳出率错误。

>[!IMPORTANT]
>
>使用手动渲染的建议时，仅通过`sendEvent`调用支持显示事件。 在这种情况下，您无法自动发送显示事件。

### 为自动呈现的建议发送显示事件 {#auto-rendered-propositions}

要为自动呈现的建议发送显示事件，必须在`sendEvent`调用中配置以下参数：

* `renderDecisions: true`
* 页面点击顶部的`personalization.sendDisplayEvent: false`

若要发送显示事件，请使用`personalization.includeRenderedPropositions: true`调用`sendEvent`

### 发送手动呈现的建议的显示事件 {#manually-rendered-propositions}

要发送手动呈现建议中的显示事件，您必须将其包含在`_experience.decisioning.propositions` XDM字段中，包括建议中的`id`、`scope`和`scopeDetails`字段。

此外，将`include _experience.decisioning.propositionEventType.display`字段设置为`1`。
