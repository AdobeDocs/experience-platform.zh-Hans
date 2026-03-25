---
title: 对话
description: 配置Brand Concierge聊天设置。
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# `conversation`

>[!AVAILABILITY]
>
>适用于Web SDK的Brand Concierge当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会发生更改。

`conversation`对象包含Brand Concierge聊天会话的配置选项。 Web SDK 2.31.0或更高版本支持此对象。

## 属性

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| **`collectSources`** | `boolean` | 确定Web SDK是否读取`adobe_brand_concierge_source`查询字符串参数并将其包含在`xdm.channel.referringSource`中。 默认为`false`。 |
| **`stickyConversationSession`** | `boolean` | 确定Web SDK是否设置会话Cookie来跨页面加载保留Brand Concierge聊天会话。 默认为`false`。 如果忽略或设置为`false`，Brand Concierge Chat会在每次页面加载时启动新会话。 |

## 示例

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## 使用Web SDK标记扩展配置对话设置

可以使用[Brand Concierge设置](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md)在Web SDK标记扩展中配置这些设置。
