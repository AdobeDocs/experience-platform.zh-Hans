---
title: pushNotifications
description: 配置Web SDK的推送通知以启用基于浏览器的推送消息。
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>Web SDK的推送通知当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会发生更改。

`pushNotifications`属性允许您为Web应用程序配置推送通知。 此功能允许您的Web应用程序接收从服务器推送的消息，即使该网站当前未加载到浏览器中也是如此。

## 先决条件 {#prerequisites}

在配置推送通知之前，请确保您具有：

1. **用户权限**：用户必须明确授予通知权限
2. **服务工作进程**：推送通知需要注册的服务工作进程才能正常工作
3. **VAPID密钥**：生成用于安全通信的VAPID（自愿应用程序服务器标识）密钥
4. **应用程序ID**：在Adobe Journey Optimizer中保存VAPID密钥时使用的应用程序ID ->渠道 — >推送设置 — >推送凭据
5. **跟踪数据集ID**：名称为“AJO推送跟踪体验事件数据集”的系统数据集的ID。 从Adobe Journey Optimizer ->数据集获取此项

## 生成VAPID密钥 {#generate-vapid-keys}

要生成VAPID密钥，请安装`web-push` NPM包并运行：

```bash
npm install web-push -g
web-push generate-vapid-keys
```

此操作生成公钥和私钥对。 在Web SDK配置中使用公钥，并在Adobe Journey Optimizer推送通知渠道中存储私钥。

## 安装Service Worker

必须从与网站相同的域提供Service Worker代码。 从Adobe的CDN下载Service Worker代码，并从您自己的服务器上托管JavaScript文件。 可以使用以下URL结构获取Web SDK服务工作进程代码：

- **缩小**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

以下是如何安装Service Worker的示例：

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## 实施

运行`pushNotifications`命令时设置`configure`对象：

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## 属性 {#properties}

| 属性 | 类型 | 必需 | 描述 |
|---|---|---|---|
| **`vapidPublicKey`** | 字符串 | 是 | 用于推送订阅的VAPID公钥。 必须为Base64编码的字符串。 |
| **`applicationId`** | 字符串 | 是 | 与VAPID公钥关联的应用程序ID。 |
| **`trackingDatasetId`** | 字符串 | 是 | 用于推送通知跟踪的系统数据集ID。 |

## 重要注意事项 {#important-considerations}

- **安全性**：推送订阅绑定到订阅期间使用的特定VAPID公钥。 如果您更改VAPID密钥，现有订阅将自动取消订阅并使用新密钥重新创建。
- **缓存**： Web SDK通过将当前ECID和订阅详细信息与缓存的值进行比较，自动管理订阅更新。 仅在检测到更改时发送订阅数据。
- **Service Worker要求**：推送通知需要注册的Service Worker。 确保您的Service Worker已正确配置为处理推送事件。

## 使用Web SDK标记扩展配置推送通知 {#configure-push-notifications-tag-extension}

配置该扩展时，与此属性等效的Web SDK标记扩展是[[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md)部分。

## 后续步骤 {#next-steps}

配置推送通知后，使用[sendPushSubscription](../sendpushsubscription.md)命令在Adobe Experience Platform中注册推送订阅。
