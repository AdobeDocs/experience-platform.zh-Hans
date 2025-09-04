---
title: sendPushSubscription
description: 在Adobe Experience Platform中注册推送通知订阅。
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
> Web SDK的推送通知当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会更改。

`sendPushSubscription`命令向Adobe Experience Platform注册推送通知订阅。 此命令处理从浏览器检索推送订阅详细信息并将它们发送到您配置的数据流。

## 先决条件 {#prerequisites}

在使用`sendPushSubscription`之前，请确保您具有：

1. **已配置推送通知**：使用您的VAPID公钥设置[`pushNotifications`](configure/pushnotifications.md)配置属性
2. **用户权限**：用户必须已授予通知权限(`Notification.permission === "granted"`)
3. **服务工作进程**：您的网站上必须有已注册的服务工作进程
4. **推送管理器支持**：浏览器必须支持推送通知并且具有PushManager API

## 使用Web SDK标记扩展注册推送订阅 {#register-push-subscription-tag-extension}

在Adobe Experience Platform数据收集标记界面的规则中，将发送推送订阅数据作为一项操作执行。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送推送订阅]**。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库注册推送订阅 {#register-push-subscription-javascript}

调用Web SDK的配置实例时运行`sendPushSubscription`命令。 确保在调用[`configure`](configure/overview.md)命令之前配置推送通知并调用`sendPushSubscription`命令。

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## 建议的执行频率 {#recommended-execution-frequency}

为获得最佳的推送通知功能，Adobe建议每天执行`sendPushSubscription`命令&#x200B;**一次**。 这可确保：

- Adobe Experience Platform中的订阅详细信息保持最新
- 捕获对推送令牌或订阅状态所做的任何更改
- 用户的配置文件会与最新的推送通知首选项保持更新

您可以使用与以下方法类似的方法实施此方法：

```js
// Check if we've sent subscription data today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## 工作原理 {#how-it-works}

`sendPushSubscription`命令执行以下操作：

1. **验证先决条件**：验证是否已配置推送通知并授予用户权限
2. **等待标识**：等待用户的ECID可用
3. **检索订阅**：使用配置的VAPID密钥从Service Worker获取活动推送订阅
4. **检查更改**：将当前的订阅详细信息与缓存的值（ECID +订阅详细信息）进行比较。 如果订阅详细信息未更改，该命令将记录一条信息消息并返回，而不发出网络请求
5. **发送到数据流**：如果检测到更改，则将订阅数据传输到您配置的Adobe Experience Platform数据流
6. **更新缓存**：存储新的订阅详细信息以供将来比较

## 错误处理 {#error-handling}

常见错误情况及其消息：

| 错误 | 原因 |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | pushNotifications配置缺失或无效 |
| `"Service workers are not supported in this browser."` | 浏览器不支持服务工作程序 |
| `"Push notifications are not supported in this browser."` | 浏览器不支持推送通知或通知API |
| `"The user has not given permission to send push notifications."` | 用户尚未授予通知权限 |
| `"No service worker registration was found."` | 没有为当前源注册服务工作程序 |
| `"No VAPID public key was provided."` | 配置中缺少VAPID公钥 |

## 数据有效负载 {#data-payload}

该命令会以下列格式发送推送通知数据：

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## 相关文档

- [配置推送通知](configure/pushnotifications.md)
- [Web推送API规范](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
