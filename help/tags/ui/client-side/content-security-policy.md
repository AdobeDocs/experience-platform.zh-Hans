---
title: 內容安全性原則(CSP)支援
description: 瞭解將您的網站與Adobe Experience Platform中的標籤整合時，如何處理內容安全性原則(CSP)限制。
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 57%

---

# 內容安全性原則(CSP)支援

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

内容安全策略 (CSP) 是一项安全功能，有助于防止跨站点脚本攻击 (XSS)。當瀏覽器受到誘騙而執行似乎來自信任的來源但實際上來自其他位置的惡意內容時，就會發生這種情況。 CSP 允许浏览器（代表用户）验证脚本是否实际来自可信来源。

CSP 通过以下两种方式来实施：将 `Content-Security-Policy` HTTP 标头添加到服务器响应，或者在 HTML 文件的 `<head>` 部分中添加已配置的 `<meta>` 元素。

>[!NOTE]
>
> 有关 CSP 的更多详细信息，请参阅 [MDN Web 文档](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)。

Adobe Experience Platform中的標籤是標籤管理系統，專為動態載入網站指令碼而設計。 由于潜在的安全问题，默认的 CSP 会阻止这些动态加载的脚本。本檔案提供如何設定CSP以允許從標籤動態載入指令碼的指引。

如果您希望標籤能與CSP搭配使用，有兩個主要難題需要克服：

* **標籤程式庫的來源必須受信任。** 若不符合這項條件，瀏覽器就會封鎖標籤程式庫和其他必要的JavaScript檔案，使其無法在頁面上載入。
* **必须允许使用内联脚本。**&#x200B;如果不满足这项条件，则页面将阻止“自定义代码”规则操作，并且无法正常执行。

提高安全性需要代表內容建立者增加工作量。 如果您想要使用標籤並部署CSP，請解決這兩項問題，並妥善將其他指令碼標示為安全指令碼。 本文档的其余部分提供了有关如何实现此目标的指南。

## 將標籤新增為信任的來源

使用 CSP 时，必须在 `Content-Security-Policy` 标头值中包含任何可信域。您必須為標籤提供的值會因您使用的託管型別而異。

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

如果您使用的是 [Adobe 管理的主机](../publishing/hosts/managed-by-adobe-host.md)，则在 `assets.adobedtm.com` 上维护您的内部版本。您應指定 `self` 作為安全網域，這樣就不會破壞已載入的任何指令碼，但您也需要 `assets.adobedtm.com` 將列為安全，否則您的標籤庫不會載入頁面上。 在这种情况下，您应该使用以下配置：

**HTTP 标头**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` 标记**


有一個非常重要的先決條件：您必須載入標籤程式庫 [非同步](./asynchronous-deployment.md). 無法同步載入標籤程式庫（這會導致主控台錯誤和規則無法正確執行）。

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
>CSP規格有第三種方法，也就是使用雜湊的詳細資訊，但這種方法無法用於標籤等標籤管理系統。 如需搭配Platform中的標籤使用雜湊的限制詳細資訊，請參閱 [子資源完整性(SRI)指南](./sri.md).

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

設定標頭或HTML標籤後，您必須告訴標籤在載入內嵌指令碼時要在哪裡找到Nonce。 若要讓標籤在載入指令碼時使用Nonce，您必須：

1. 创建一个数据元素，使其引用 nonce 在数据层中的位置。
1. 配置核心扩展，并指定要使用的数据元素。
1. 发布数据元素和核心扩展更改。

>[!NOTE]
>
>上述过程只处理自定义代码的加载，而不处理自定义代码的用途。如果内联脚本包含与 CSP 不兼容的自定义代码，则优先使用 CSP。例如，如果您使用自訂程式碼，透過將內嵌指令碼附加至DOM來執行載入作業，標籤將無法正確新增Nonce，導致該特定自訂程式碼動作無法正常運作。

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

閱讀本檔案後，您現在應瞭解如何設定CSP標頭，以接受標籤程式庫檔案和內嵌指令碼。

作为一项额外的安全措施，您还可以选择使用子资源完整性 (SRI) 来验证已获取的库内部版本。不過，此功能與標籤等標籤管理系統搭配使用時有一些重大限制。 請參閱指南： [平台中的SRI相容性](./sri.md) 以取得詳細資訊。
