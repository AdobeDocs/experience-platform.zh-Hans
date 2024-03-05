---
title: 配置CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: 了解如何为Experience PlatformWeb SDK配置CSP
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: 配置；配置；SDK；边缘；Web SDK；配置；上下文；Web；设备；环境；Web SDK设置；内容安全策略；
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 配置CSP

A [内容安全策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP)用于限制浏览器可以使用的资源。 CSP还可以限制脚本和样式资源的功能。 Adobe Experience Platform Web SDK不需要CSP，但添加一个CSP可以减少攻击面，以防止恶意攻击。

CSP需要反映以下情况 [!DNL Platform Web SDK] 已部署和配置。 以下CSP显示了使SDK正常运行可能需要进行的更改。 根据您的特定环境，可能需要其他CSP设置。

## 内容安全策略示例

以下示例显示如何配置CSP。

### 允许访问边缘域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上例中， `EDGE-DOMAIN` 应替换为第一方域。 第一方域配置用于 [edgeDomain](../commands/configure/edgedomain.md) 设置。 如果未配置第一方域， `EDGE-DOMAIN` 应替换为 `*.adobedc.net`. 如果使用打开访客迁移 [idMigrationEnabled](../commands/configure/idmigrationenabled.md)， `connect-src` 指令还需要包括 `*.demdex.net`.

### 使用NONCE允许内联脚本和样式元素

[!DNL Platform Web SDK] 可以修改页面内容，并且必须获得批准才能创建内联脚本和样式标记。 要完成此操作，Adobe建议对 [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指令。 nonce是服务器生成的加密性强随机令牌，每个唯一页面查看生成一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，需要将CSP nonce作为属性添加到 [!DNL Platform Web SDK] [基础代码](../install/library.md) 脚本标记。 [!DNL Platform Web SDK] 之后，将该nonce用于向页面添加内联脚本或样式标记：

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用随机数，则另一个选项是添加 `unsafe-inline` 到 `script-src` 和 `style-src` CSP指令：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe会 **非** 建议指定 `unsafe-inline` 因为它允许任何脚本在页面上运行，这限制了CSP的好处。

## 为应用程序内消息传送配置CSP {#in-app-messaging}

配置时 [Web应用程序内消息传递](../personalization/web-in-app-messaging.md)中，必须在CSP中包含以下指令：

```
default-src  blob:;
```
