---
title: 配置CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: 了解如何为Experience Platform Web SDK配置CSP
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: 配置；配置；SDK；edge；Web SDK；配置；上下文；Web；设备；环境；Web SDK设置；内容安全策略；
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 配置CSP

[内容安全策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP)用于限制浏览器可以使用的资源。 CSP还可以限制脚本和样式资源的功能。 Adobe Experience Platform Web SDK不需要CSP，但添加一个CSP可减少攻击面，以防止恶意攻击。

CSP需要反映[!DNL Experience Platform Web SDK]的部署和配置方式。 以下CSP显示了SDK正常运行可能需要进行的更改。 根据您的特定环境，可能需要其他CSP设置。

## 内容安全策略示例

以下示例显示如何配置CSP。

### 允许访问边缘域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上例中，`EDGE-DOMAIN`应替换为第一方域。 第一方域配置为[edgeDomain](../js/commands/configure/edgedomain.md)设置。 如果尚未配置第一方域，则应将`EDGE-DOMAIN`替换为`*.adobedc.net`。 如果使用[idMigrationEnabled](../js/commands/configure/idmigrationenabled.md)启用访客迁移，则`connect-src`指令也需要包含`*.demdex.net`。

### 使用NONCE允许内联脚本和样式元素

[!DNL Experience Platform Web SDK]可以修改页面内容，必须获得批准才能创建内联脚本和样式标记。 为此，Adobe建议对[default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指令使用nonce。 nonce是服务器生成的加密性强随机令牌，每个唯一页面查看生成一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，需要将CSP nonce作为属性添加到[!DNL Experience Platform Web SDK] [基础代码](../js/install/library.md)脚本标记中。 然后，[!DNL Experience Platform Web SDK]将在向页面添加内联脚本或样式标记时使用该nonce：

```html
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用nonce，则另一个选项是将`unsafe-inline`添加到`script-src`和`style-src` CSP指令中：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe不&#x200B;**建议**&#x200B;指定`unsafe-inline`，因为它允许在该页面上运行任何脚本，这限制了CSP的优势。

## 为应用程序内消息传送配置CSP {#in-app-messaging}

在配置Web应用程序内消息传送时，必须在CSP中包含以下指令：

```
default-src  blob:;
```
