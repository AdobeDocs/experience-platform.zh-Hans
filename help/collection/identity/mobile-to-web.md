---
title: 将标识从移动应用程序共享到移动Web/WebViews
description: 将标识从移动应用程序传递到移动Web内容或WebView中，以便报表和个性化可在Web上下文中继续。
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 将标识从移动应用程序共享到移动Web/WebViews

当访客从移动应用程序移至WebView或移动网页时，应用程序和Web上下文将分别维护各自的身份。 如果没有明确切换，则Web体验会将访客视为新的未知人员，这会分割报表并重新启动个性化。

移动到Web身份共享可通过[查询字符串参数将访客的](./overview.md)Experience Cloud ID (ECID)`adobe_mc`从移动应用程序传递到Web目标，从而解决此问题。 参数包含ECID、您的Experience Cloud组织ID和时间戳。 当Web目标加载有效的`adobe_mc`参数时，Web SDK会自动读取该参数，并在其第一个Edge Network请求中应用切换身份，因此两个上下文共享同一访客。

当您的移动应用程序打开由组织控制的WebView或移动网页，并且您希望应用程序活动和Web活动保持绑定到同一访客时，请使用此模式。 如果您的目标是不同域上的网站之间的标识连续性，请改用[跨域共享](cross-domain-sharing.md)。

## 先决条件

在开始之前，请确保您的实施满足以下要求：

* **移动设备应用程序**： Adobe Experience Platform移动设备SDK，具有[Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/)扩展版本&#x200B;**1.1.0或更高版本** （iOS和Android）的标识。
* **Web目标**： [Web SDK](/help/collection/js/js-overview.md)版本&#x200B;**2.11.0或更高版本**，或Web SDK标记扩展。
* **URL控件**：您的代码控制应用程序传递给WebView或浏览器的URL，以便您可以向其附加查询字符串参数。
* **匹配配置**：在移动和Web实施中配置了相同的Experience Cloud组织ID。

## 从移动设备应用程序中检索身份 {#retrieve-identity}

使用Edge Network Identity扩展中的[`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) API以查询字符串形式检索访客身份。 然后，您可以在打开WebView或浏览器之前将该字符串附加到URL中。

返回的字符串包含以下URL编码的参数：

| 参数 | 描述 |
| --- | --- |
| `MCID` | Experience Cloud ID (ECID)。 |
| `MCORGID` | 您的Experience Cloud组织ID。 此参数必须与目标页面上的Web SDK中配置的组织匹配。 |
| `TS` | 时间戳。 目标必须在&#x200B;**5分钟**&#x200B;内收到此值，否则切换被拒绝。 |

以下代码示例显示了切换在您的移动应用程序中可能显示的内容：

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB 科特林(Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## 在Web端接收身份 {#receive-identity}

Web目标上不需要其他代码。 如果页面上存在Web SDK，且URL包含有效的`adobe_mc`参数，则SDK会自动提取ECID，并将其应用于首次Edge Network请求中的访客身份映射。

如果您的Web目标使用Web SDK标记扩展，并且需要在保留身份的同时将访客重定向到其他页面，请使用带有身份的[重定向](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)操作将`adobe_mc`参数转发到下一页。

>[!NOTE]
>
>`adobe_mc`参数将在&#x200B;**5分钟**&#x200B;后过期。 确保Web目标在打开URL后立即加载并发送其第一个Edge Network请求。
