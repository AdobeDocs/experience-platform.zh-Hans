---
title: 在Web SDK中管理显示事件
description: 本文介绍了什么是显示事件以及如何在Web SDK中使用它们。
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# 在Web SDK中管理显示事件

当页面上显示特定的个性化内容时，Web SDK会使用显示事件来通知您的个性化或分析服务。

发送显示事件可提高个性化量度的准确性，并让您准确大致了解用户在您的页面上看到的内容。

Web SDK允许您通过两种方式发送显示事件：

* [自动](#send-automatically)，紧跟在页面上呈现个性化内容之后。 请参阅有关如何执行操作的文档 [呈现个性化内容](rendering-personalization-content.md) 以了解更多信息。
* [手动](#send-sendEvent-calls)，通过后续的 `sendEvent` 呼叫。

>[!NOTE]
>
>在调用时，不会自动发送显示事件 `applyPropositions` 函数。

## 自动发送显示事件 {#send-automatically}

发送显示事件会自动提供更准确的分析量度，因为事件会在个性化加载后立即发送。 此实施还具有更简化的实施方法。

要在页面上呈现个性化内容后自动发送显示事件，必须配置以下参数：

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` 或未指定

在任何个性化作为的结果呈现后，Web SDK会立即发送显示事件。 `sendEvent` 呼叫。

## 在后续sendEvent调用中发送显示事件 {#send-sendEvent-calls}

比较对象 [自动](#send-automatically) 发送显示事件（当在后续操作中包含这些事件时） `sendEvent` 调用您还有机会在调用中包含有关页面加载的更多信息。 这可能是额外的信息，在请求个性化内容时不可用。

此外，发送显示事件于 `sendEvent` 使用Adobe Analytics时，调用可将跳出率错误降至最低。

>[!IMPORTANT]
>
>使用手动渲染的建议时，仅支持显示事件，途径为 `sendEvent` 呼叫。 在这种情况下，您无法自动发送显示事件。

### 为自动呈现的建议发送显示事件 {#auto-rendered-propositions}

要为自动呈现的建议发送显示事件，您必须在 `sendEvent` 调用：

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` 对于页面点击顶部

要发送显示事件，请调用 `sendEvent` 替换为 `personalization.includePendingDisplayNotifications: true`

### 发送手动呈现的建议的显示事件 {#manually-rendered-propositions}

要为手动呈现的建议发送显示事件，您必须将它们包含在中 `_experience.decisioning.propositions` XDM字段，包括 `id`， `scope`、和 `scopeDetails` 字段。

此外，设置 `include _experience.decisioning.propositionEventType.display` 字段至 `1`.
