---
title: 設定CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: 瞭解如何為Experience PlatformWeb SDK設定CSP
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: 設定；設定；SDK；邊緣；Web SDK；設定；上下文；Web；裝置；環境；Web SDK設定；內容安全性原則；
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# 設定CSP

A [內容安全性原則](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP)可用來限制瀏覽器可使用的資源。 CSP也可限制指令碼和樣式資源的功能。 Adobe Experience Platform Web SDK不需要CSP，但新增一個CSP可減少攻擊面，以防止惡意攻擊。

CSP必須反映如何進行 [!DNL Platform Web SDK] 已部署和設定。 下列CSP顯示SDK可能需要哪些變更才能正常運作。 視您的特定環境而定，可能需要其他CSP設定。

## 內容安全性原則範例

以下範例說明如何設定CSP。

### 允許存取邊緣網域

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

在上述範例中， `EDGE-DOMAIN` 應取代為第一方網域。 第一方網域是針對 [edgeDomain](configuring-the-sdk.md#edge-domain) 設定。 如果尚未設定第一方網域， `EDGE-DOMAIN` 應取代為 `*.adobedc.net`. 如果使用開啟訪客移轉 [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled)，則 `connect-src` 指示詞也需要包含 `*.demdex.net`.

### 使用NONCE可允許內嵌指令碼和樣式元素

[!DNL Platform Web SDK] 可以修改頁面內容，且必須獲得核准才能建立內嵌指令碼和樣式標籤。 若要完成此操作，Adobe建議使用Nonce [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP指令。 Nonce是伺服器產生的強密碼隨機權杖，每個唯一頁面檢視產生一次。

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

此外，CSP Nonce必須新增為 [!DNL Platform Web SDK] [基底程式碼](installing-the-sdk.md#adding-the-code) 指令碼標籤。 [!DNL Platform Web SDK] 然後會在將內嵌指令碼或樣式標籤新增至頁面時，使用該Nonce：

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

如果未使用Nonce，則另一個選項是新增 `unsafe-inline` 至 `script-src` 和 `style-src` CSP指示：

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe會 **not** 建議指定 `unsafe-inline` 因為它允許任何指令碼在頁面上執行，這會限制CSP的優點。
