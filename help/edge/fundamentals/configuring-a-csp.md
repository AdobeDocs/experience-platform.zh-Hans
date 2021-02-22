---
title: 配置CSP
seo-title: 为Adobe Experience Platform Web SDK配置CSP
description: 了解如何为Experience Platform Web SDK配置CSP
seo-description: 了解如何为Experience Platform Web SDK配置CSP
keywords: 配置；配置；SDK；边缘；Web SDK；配置；上下文；Web；设备；环境;Web SDK设置；内容安全策略；
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# 配置CSP

使用[内容安全策略](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy)(CSP)来限制浏览器允许使用的资源。 CSP还可以限制脚本和样式资源的功能。 Adobe Experience Platform Web SDK不需要CSP，但添加一个CSP可以减少攻击表面以防止恶意攻击。

CSP需要反映如何部署和配置[!DNL Platform Web SDK]。 以下CSP显示SDK正常工作可能需要哪些更改。 可能需要其他CSP设置，具体取决于您的特定环境。

## 内容安全策略示例

以下示例说明如何配置CSP。

### 允许访问边缘域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上例中，`EDGE-DOMAIN`应替换为第一方域。 第一方域配置为[edgeDomain](configuring-the-sdk.md#edge-domain)设置。 如果尚未配置第一方域，应将`EDGE-DOMAIN`替换为`*.adobedc.net`。 如果使用[idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled)打开访客迁移，则`connect-src`指令还需要包含`*.demdex.net`。

### 使用NONCE允许内联脚本和样式元素

[!DNL Platform Web SDK] 可以修改页面内容，必须批准才能创建内联脚本和样式标记。为此，Adobe建议对[default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指令使用nonce。 nonce是服务器生成的加密强随机令牌，每个唯一页面视图生成一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，CSPnonce需要作为属性添加到[!DNL Platform Web SDK] [基本代码](installing-the-sdk.md#adding-the-code)脚本标签。 [!DNL Platform Web SDK] 然后，在将内联脚本或样式标签添加到页面时，将立即使用该选项：

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用nonce，则另一个选项是将`unsafe-inline`添加到`script-src`和`style-src` CSP指令：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe **不**&#x200B;建议指定`unsafe-inline`，因为它允许在页面上运行任何脚本，这限制了CSP的优势。
