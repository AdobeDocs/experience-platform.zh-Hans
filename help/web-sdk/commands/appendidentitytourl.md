---
title: appendIdentityToUrl
description: 在应用程序、Web和跨域之间更准确地交付个性化体验。
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# `appendIdentityToUrl`

此 `appendIdentityToUrl` 命令用于将用户标识符作为查询字符串添加到URL中。 通过此操作，您可以在域之间携带访客身份，从而防止同时包含域或渠道的数据集出现重复访客计数。 它在Web SDK版本2.11.0或更高版本上可用。

生成并附加到URL的查询字符串是 `adobe_mc`. 如果Web SDK找不到ECID，则会调用 `/acquire` 端点以生成一个。

>[!NOTE]
>
>如果未提供同意，则此方法的URL将保持不变。 此命令会立即运行；它不会等待同意更新。

## 使用Web SDK扩展将身份附加到URL {#extension}

将身份附加到URL可作为Adobe Experience Platform数据收集标记界面中的规则中的操作执行。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 带标识的重定向]**.
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

此命令通常与监听点击并检查所需域的特定规则一起使用。

+++规则事件条件

当具有的锚标记时触发 `href` 属性被单击。

* **[!UICONTROL 扩展名]**：核心
* **[!UICONTROL 事件类型]**：单击
* **[!UICONTROL 当用户单击]**：特定元素
* **[!UICONTROL 匹配CSS选择器的元素]**： `a[href]`

![规则事件](../assets/id-sharing-event-configuration.png)

+++

+++规则条件

仅在所需的域上触发。

* **[!UICONTROL 逻辑类型]**：常规
* **[!UICONTROL 扩展名]**：核心
* **[!UICONTROL 完成情况类型]**：值比较
* **[!UICONTROL 左操作数]**： `%this.hostname%`
* **[!UICONTROL 运算符]**：匹配Regex
* **[!UICONTROL 右操作数]**：匹配所需域的正则表达式。 例如：`adobe.com$|behance.com$`

![规则条件](../assets/id-sharing-condition-configuration.png)

+++

+++规则操作

将标识附加到URL。

* **[!UICONTROL 扩展名]**：Adobe Experience Platform Web SDK
* **[!UICONTROL 操作类型]**：使用标识重定向

![规则操作](../assets/id-sharing-action-configuration.png)

+++

## 使用Web SDK JavaScript库将身份附加到URL

运行 `appendIdentityToUrl` 命令并将URL作为参数。 此方法会返回一个标识符作为查询字符串附加的URL。

```js
alloy("appendIdentityToUrl",document.location);
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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## 响应对象

如果您决定 [处理响应](command-responses.md) 使用此命令，响应对象将包含 **`url`**，包含身份信息的新URL被添加为查询字符串参数。
