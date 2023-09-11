---
title: 移动到Web和跨域ID共享
description: 了解如何将访客ID从移动资产保留到Web资产并跨域保留
keywords: 身份；移动设备；ID；共享；域；跨域；SDK；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 移动到Web和跨域ID共享

## 概述

Adobe Experience Platform Web SDK支持访客ID共享功能，这使得客户能够在移动应用程序和移动Web内容之间以及跨域更准确地提供个性化体验。

## 用例 {#use-cases}

### 在移动应用程序和移动网站之间提供一致的个性化

一家服装公司希望根据客户的兴趣来为他们提供个性化体验，并在同时加载WebViews的移动应用程序中保持个性化的准确性。 通过使用移动到Web ID共享功能，他们可以确保在应用程序和移动Web内容中使用相同的访客标识符，通过传递 [!DNL ECID] 到移动Web URL。

### 跨域提供一致的个性化

一家拥有多个在线商店的零售商希望根据客户兴趣对其域中的购物者体验进行个性化。 通过使用Web SDK跨域ID共享功能，零售商可以在其所有域中根据客户兴趣提供准确的优惠。

### 增强访客活动报告功能

技术零售商希望提供有关访客何时从移动应用程序移动到其移动网站或何时移动到其其他域的信息来改进其访客活动报表。 通过使用Web SDK跨域ID共享功能，营销团队可以准确地跟踪其Web资产中的访客并生成活动报表。

## 先决条件 {#prerequisites}

要使用移动到Web和跨域ID共享，您必须使用 [!DNL Web SDK] 版本2.11.0或更高版本。

对于Edge Network移动设备实施，支持此功能的 [边缘网络的标识](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) 扩展从版本1.1.0(iOS和Android)开始。

此功能还与 [!DNL VisitorAPI.js] 版本1.7.0或更高版本。

## 移动到Web ID共享 {#mobile-to-web}

使用 `getUrlVariables` 来自的API [边缘网络的标识](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) 扩展名，用于将标识符检索为查询参数，并在打开时将其附加到您的URL [!DNL webViews].

Web SDK无需其他配置即可接受 `ECID` 查询字符串中的值。

查询字符串参数包括：

* `MCID`：Experience CloudID (`ECID`)
* `MCORGID`：Experience Cloud `orgID` 必须匹配 `orgID` 在中配置 [!DNL Web SDK].
* `TS`：时间戳参数不能早于5分钟。


移动设备与Web ID共享会使用 `adobe_mc` 参数。 当 `adobe_mc` 参数存在且有效， `ECID` 中的标识映射，在向Edge Network发出的第一个请求中，自动添加到查询字符串中。 所有后续的Edge Network交互都将使用 `ECID`.

有关如何将访客ID从移动应用程序传递到WebView的更多信息，请参阅此文档位于 [处理WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 跨域标识共享 {#cross-domain-sharing}

对于跨域ID共享，Web SDK版本2.11.0添加了对 `appendIdentityToUrl` 命令。 使用此命令时，将生成 `adobe_mc` 查询字符串参数。

该命令接受具有一个属性的对象， `url`，并返回具有属性的对象 `url`.

此命令不等待任何同意更新。 如果未提供同意，则返回的URL将保持不变。

如果 `ECID` 未提供，则 `/acquire` 将调用端点以生成 `ECID`.

以下示例介绍了客户如何在其网站上实施跨域ID共享。

此代码会为页面上的所有点击添加一个事件侦听器，如果点击位于指向匹配域的链接上（在本例中为） `adobe.com` 或 `behance.com`)，将标识添加到URL并将用户重定向到该处。

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## 使用标记扩展 {#tags-extension}

与使用 [!DNL Web SDK]中，无需其他配置 [!DNL Tags] 扩展，用于使用通过URL传递的身份。

要通过Tags扩展使用移动到Web和跨域ID共享，您必须使用Tags扩展版本2.12.0或更高版本。

要将当前页面中的标识共享给其他域，需在 [!DNL Web SDK] [!DNL Tags] 扩展。 此操作设计为与 **[!UICONTROL 核心 — 单击]** 事件类型和值比较条件。

按照描述的步骤操作 [此处](../../tags/ui/managing-resources/rules.md) 创建具有以下配置的规则：

* [!UICONTROL 事件配置]：
   * **[!UICONTROL 扩展：核心]**
   * **[!UICONTROL 事件类型：单击]**
   * 选择 **[!UICONTROL 当用户单击>特定元素时]**
   * 键入 **[!UICONTROL 选择器]**： `a[href]`. 只要在页面上单击锚点标记，此事件就会触发。 `href` 属性。

     ![显示具有上述设置的事件配置的UI图像](assets/id-sharing-event-configuration.png)

* [!UICONTROL 条件配置]
   * **[!UICONTROL 逻辑类型]**： [!UICONTROL 常规]
   * **[!UICONTROL 扩展名]**： [!UICONTROL 核心]
   * **[!UICONTROL 完成情况类型]**： [!UICONTROL Value Comparison]
   * **[!UICONTROL 左操作数]**： [!UICONTROL `%this.hostname%`]. 这是一个与配合使用的特殊数据元素 [!UICONTROL 核心 — 单击] 事件并解析为所单击链接的主机名。
   * **[!UICONTROL 运算符]**： [!UICONTROL 匹配Regex]
   * **[!UICONTROL 右操作数]**：键入与要与其共享标识的域匹配的正则表达式。 例如，匹配主机名以结尾的链接 `adobe.com` 或 `behance.com`，请使用此正则表达式： `behance.com$|adobe.com$`. 链接的页面需要具有 [!DNL Web SDK] 或 [!DNL Visitor ID] 安装以接受身份。

     ![显示具有上述设置的条件配置的用户界面图像](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 操作配置]
   * **[!UICONTROL 扩展名]**： [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL 操作类型]**： [!UICONTROL 带标识的重定向]
   * **[!UICONTROL 实例]**：选择您的实例。 在大多数情况下，您只会配置一个实例。 如果您有多个实例，请选择具有您要共享的标识的实例。

     ![显示具有上述设置的操作配置的用户界面图像](assets/id-sharing-action-configuration.png)

此 **[!UICONTROL 带标识的重定向]** 操作将阻止浏览器导航到链接。 然后，它将调用 `appendIdentityToUrl` 上的方法 [!DNL Web SDK] 实例。

最后，它会将用户重定向到 [!DNL URL] 使用 `adobe_mc` 已附加查询字符串参数。
