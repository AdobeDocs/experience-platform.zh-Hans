---
title: appendIdentityToUrl
description: 在应用程序、Web和跨域之间更准确地交付个性化体验。
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

`appendIdentityToUrl`命令允许您向URL添加用户标识符作为查询字符串。 通过此操作，您可以在域之间携带访客身份，从而防止同时包含域或渠道的数据集出现重复访客计数。 它在Web SDK版本2.11.0或更高版本上可用。

生成并附加到URL的查询字符串是`adobe_mc`。 如果Web SDK找不到ECID，它将调用`/acquire`端点以生成一个ECID。

>[!NOTE]
>
>如果未提供同意，则此方法的URL将保持不变。 此命令会立即运行；它不会等待同意更新。

以URL作为参数运行`appendIdentityToUrl`命令。 此方法会返回一个标识符作为查询字符串附加的URL。

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

您可以为页面上收到的所有点击添加事件侦听器，并检查URL是否与任何所需的域匹配。 如果超过100次，则将身份附加到URL并重定向用户。

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

此命令支持[`edgeConfigOverrides`](configure/edgeconfigoverrides.md)对象。

## 响应对象

使用此命令[处理响应](command-responses.md)时，响应对象包含&#x200B;**`url`**，新URL具有作为查询字符串参数添加的标识信息。

## 使用Web SDK标记扩展将身份附加到URL

与此命令等效的Web SDK标记扩展是[带有标识](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)的重定向操作。
