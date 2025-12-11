---
title: 内容安全策略(CSP)支持
description: 了解在将您的网站与Adobe Experience Platform中的标记集成时，如何处理内容安全策略(CSP)限制。
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 56%

---

# 内容安全策略(CSP)支持

内容安全策略 (CSP) 是一项安全功能，有助于防止跨站点脚本攻击 (XSS)。这种攻击是指浏览器受到欺骗，运行似乎来自可靠来源但实际上来自其他来源的恶意内容。 CSP 允许浏览器（代表用户）验证脚本是否实际来自可信来源。

CSP 通过以下两种方式来实施：将 `Content-Security-Policy` HTTP 标头添加到服务器响应，或者在 HTML 文件的 `<head>` 部分中添加已配置的 `<meta>` 元素。

>[!NOTE]
>
> 有关 CSP 的更多详细信息，请参阅 [MDN Web 文档](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)。

Adobe Experience Platform中的标记是一个标记管理系统，旨在动态地在您的网站上加载脚本。 由于潜在的安全问题，默认的 CSP 会阻止这些动态加载的脚本。本文档提供了有关如何配置CSP以允许从标记动态加载脚本的指南。

如果您希望标记与CSP配合使用，则需要克服两个主要挑战：

* **标记库的来源必须可信。**&#x200B;如果不满足这项条件，则浏览器将阻止标记库和其他必需的JavaScript文件，并且不会在页面上加载。
* **必须允许使用内联脚本。**&#x200B;如果不满足这项条件，则页面将阻止“自定义代码”规则操作，并且无法正常执行。

提高安全性需要增加内容创建者的工作量。 如果要使用标记并实施CSP，则您必须解决这两个问题，而又不能将其他脚本错误地标记为安全。 本文档的其余部分提供了有关如何实现此目标的指南。

## 将标记添加为可信来源

使用 CSP 时，必须在 `Content-Security-Policy` 标头值中包含任何可信域。您必须为标记提供的值因您使用的托管类型而异。

### 自托管

如果您[自托管](../publishing/hosts/self-hosting-libraries.md)库，则内部版本的来源可能是您自己的域。您可以使用以下配置将主机域指定为安全来源：

**HTTP 标头**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>` 标记**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Adobe 管理的主机

如果您使用的是 [Adobe 管理的主机](../publishing/hosts/managed-by-adobe-host.md)，则在 `assets.adobedtm.com` 上维护您的内部版本。您应该将`self`指定为安全域，以便不会破坏已经加载的脚本，但同时您还需要将`assets.adobedtm.com`列为安全，否则您的标记库将不会加载到页面上。 在这种情况下，您应该使用以下配置：

**HTTP 标头**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` 标记**


有一个非常重要的先决条件：必须异步加载标记库[](./asynchronous-deployment.md)。 同步加载标记库行不通（因为会导致控制台错误和规则无法正确执行）。

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

您应该将 `self` 指定为安全域，以便已经加载的脚本可继续正常运行，但您还需要将 `assets.adobedtm.com` 列为安全，否则您的库内部版本将不会加载到页面上。

## 内联脚本

默认情况下，CSP 不允许使用内联脚本，因此必须手动配置以允许使用这些脚本。要允许使用内联脚本，您有两种选项：

* [允许特定场合使用](#nonce)（安全性良好）
* [允许使用所有内联脚本](#unsafe-inline)（最不安全）

>[!NOTE]
>
>CSP规范包含第三个选项“使用哈希”的详细信息，但是这种方法在搭配使用标记等标记管理系统时不可行。 有关对Experience Platform中的标记使用哈希的限制的更多信息，请参阅[子资源完整性(SRI)指南](./sri.md)。

### 允许特定场合使用 {#nonce}

此方法包括生成加密 nonce 并将其添加到 CSP 和网站上的每个内联脚本中。浏览器在收到加载带有 nonce 的内联脚本的指令时，会将 nonce 值与 CSP 标头内包含的值进行比较。如果二者匹配，则会加载脚本。在每次加载新页面时，这个 nonce 值会发生更改。

>[!IMPORTANT]
>
>要使用此方法，必须异步加载内部版本。同步加载内部版本时，这种方法不起作用，而且会导致控制台错误和规则无法正确执行。有关更多信息，请参阅[异步部署](./asynchronous-deployment.md)指南。

以下示例显示如何将 nonce 添加到 Adobe 管理的主机的 CSP 配置中。如果您使用自托管，则可以排除 `assets.adobedtm.com`。

**HTTP 标头**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>` 标记**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

配置标题或HTML标记后，在加载内联脚本时，必须告诉标记在何处查找nonce。 对于要在加载脚本时使用nonce的标记，您必须：

1. 创建一个数据元素，使其引用 nonce 在数据层中的位置。
1. 配置核心扩展，并指定要使用的数据元素。
1. 发布数据元素和核心扩展更改。

>[!NOTE]
>
>上述过程只处理自定义代码的加载，而不处理自定义代码的用途。如果内联脚本包含与 CSP 不兼容的自定义代码，则优先使用 CSP。例如，如果您使用自定义代码，通过将代码附加到DOM来加载内联脚本，那么标记将无法正确添加nonce，进而导致特定的自定义代码操作无法按预期执行。

### 允许使用所有内联脚本 {#unsafe-inline}

如果使用 nonce 这个选项不适合您，您可以将 CSP 配置为允许使用所有内联脚本。这是最不安全的选项，但它却相对更加易于实施和维护。

以下示例显示如何在 CSP 标头中允许使用所有内联脚本。

#### 自托管

如果您使用自托管，请使用以下配置：

**HTTP 标头**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>` 标记**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Adobe 管理的主机

如果您使用 Adobe 管理的主机，请使用以下配置：

**HTTP 标头**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>` 标记**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## 后续步骤

通过阅读本文档，您现在应该了解如何将CSP标头配置为接受标记库文件并允许使用内联脚本。

作为一项额外的安全措施，您还可以选择使用子资源完整性 (SRI) 来验证已获取的库内部版本。但是，当与标记等标记管理系统一起使用时，这项功能存在一些主要限制。 有关详细信息，请参阅Experience Platform[中有关](./sri.md)SRI兼容性的指南。
