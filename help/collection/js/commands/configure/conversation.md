---
title: 对话
description: 配置Brand Concierge聊天设置。
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 4%

---

# `conversation`

>[!AVAILABILITY]
>
>适用于Web SDK的Brand Concierge当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会发生更改。

`conversation`对象包含Brand Concierge聊天会话的配置选项。 Web SDK 2.31.0或更高版本支持此对象。

## 属性

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| **`stickyConversationSession`** | `boolean` | 确定Web SDK是否设置会话Cookie来跨页面加载保留Brand Concierge聊天会话。 默认为`false`。 如果忽略或设置为`false`，Brand Concierge Chat会在每次页面加载时启动新会话。 |

## 示例

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    stickyConversationSession: true
  }
});
```

## 使用Web SDK标记扩展配置对话设置

可以使用[Brand Concierge设置](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md)在Web SDK标记扩展中配置这些设置。
