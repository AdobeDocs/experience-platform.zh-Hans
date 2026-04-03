---
title: 跨域共享身份
description: 维护组织拥有的跨域的身份连续性，以改善个性化和报告。
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 跨域共享身份

当访客在组织拥有的域之间移动时，每个域默认将维护其自己的访客身份。 如果没有明确切换，访客从某个域单击到另一个域时，会在目标网站上被视为新的未知人员。 此类实施片段报告并重新启动个性化。

跨域身份共享可在访客点击链接或被重定向时，通过将`adobe_mc`查询字符串参数附加到目标URL来解决此问题。 此参数包含访客的[Experience Cloud ID (ECID)](./overview.md)、您的组织ID和时间戳。 当目标页面加载了有效的`adobe_mc`参数时，Web SDK会自动读取该参数，并在其第一个Edge Network请求中应用切换身份，因此两个域共享同一访客。 `adobe_mc`参数将在五分钟后过期，因此目标页面必须在重定向后立即加载。

此用例涵盖了不同域上的网站之间的身份共享。 如果要将标识从移动应用传递到WebView或移动网页，请改用[移动到Web标识共享](./mobile-to-web.md)。

## 先决条件

在开始之前，请确保您的实施满足以下要求：

* **Web SDK**： [Web SDK](/help/collection/js/js-overview.md)版本&#x200B;**2.11.0或更高版本**，或者Web SDK标记扩展安装在源域和目标域上。
* **匹配配置**：在配置Web SDK时，所有参与域都使用相同的[`orgId`](../js/commands/configure/orgid.md)。
* **URL控件**：您的代码控制域之间的链接或重定向，以便您可以将查询字符串参数附加到目标URL。

## 实施跨域共享

您必须在充当跨域切换源的每个域上配置身份共享。 如果访客可以在两个域之间双向导航，请将两个域配置为源。

>[!BEGINTABS]

>[!TAB JavaScript库]

使用[`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md)命令将`adobe_mc`参数附加到出站链接。 以下示例侦听对锚点元素的单击，并将标识附加到指向所需域的任何链接：

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Web SDK标记扩展]

使用[**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)操作将`adobe_mc`参数附加到出站链接。 您可以创建满足以下条件的规则，以获得所需的行为：

1. **事件**：将扩展设置为&#x200B;**[!UICONTROL Core]**，将事件类型设置为&#x200B;**[!UICONTROL Click]**。 在&#x200B;**[!UICONTROL Elements matching the CSS selector]**&#x200B;下，输入`a[href]`。
2. **条件**：将扩展设置为&#x200B;**[!UICONTROL Core]**，将条件类型设置为&#x200B;**[!UICONTROL Value Comparison]**。 将&#x200B;**[!UICONTROL Left Operand]**&#x200B;设置为`%this.hostname%`，将&#x200B;**[!UICONTROL Operator]**&#x200B;设置为&#x200B;**[!UICONTROL Matches Regex]**，将&#x200B;**[!UICONTROL Right Operand]**&#x200B;设置为与您的目标域匹配的正则表达式（例如，`example\.com$|example\.org$`）。
3. **操作**：将扩展设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，将操作类型设置为&#x200B;**[!UICONTROL Redirect with identity]**。

>[!ENDTABS]

## 接收目标域上的标识

目标域上不需要其他代码。 如果页面上存在Web SDK，且URL包含有效的`adobe_mc`参数，则SDK会自动提取ECID，并将其应用于访客在其第一个Edge Network请求中的身份映射。

确保目标域满足以下条件：

* Web SDK或Web SDK标记扩展已安装并使用与源域相同的[`orgId`](../js/commands/configure/orgid.md)进行配置。 您可以在域之间交替使用JavaScript库和Web SDK标记扩展，只要它们共享相同的`orgId`即可。
* 在&#x200B;**参数过期之前，页面将在重定向的** 5分钟`adobe_mc`内加载并发送其第一个Edge Network请求。
