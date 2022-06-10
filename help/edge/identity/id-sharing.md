---
title: 移动到Web和跨域ID共享
description: 了解如何在移动设备属性和跨域保留访客ID
keywords: 身份；移动设备；ID；共享；域；跨域；SDK；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# 移动到Web和跨域ID共享

## 概述

Adobe Experience Platform Web SDK支持访客ID共享功能，这些功能使客户能够在移动应用程序和移动Web内容之间以及跨域之间更准确地提供个性化体验。

## 用例 {#use-cases}

### 在移动设备应用程序和移动设备网站之间提供一致的个性化

一家服装公司希望根据客户兴趣对其体验进行个性化，并在同时加载WebViews的移动应用程序中保持准确的个性化。 通过使用移动设备到Web ID共享功能，他们可以通过传递 [!DNL ECID] 到移动Web URL。

### 跨域提供一致的个性化

具有多个在线商店的零售商希望根据客户兴趣，在其域中个性化购物者体验。 通过使用Web SDK跨域ID共享功能，零售商可以根据客户的兴趣跨其所有域提供准确的选件。

### 增强访客活动报表功能

技术零售商希望使用以下信息来改进其访客活动报表：访客何时从移动应用程序移动到其移动网站，或何时移至其他域。 使用Web SDK跨域ID共享功能，营销团队可以准确跟踪访客在其Web属性中的访客并生成活动报表。

## 先决条件 {#prerequisites}

要使用移动到Web和跨域ID共享，您必须使用 [!DNL Web SDK] 版本2.11.0或更高版本。

对于边缘网络移动实施， [边缘网络的标识](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 扩展，以版本1.1.0(iOS和Android)开始。

此功能还与 [!DNL VisitorAPI.js] 版本1.7.0或更高版本。

## 移动到Web ID共享 {#mobile-to-web}

使用 `getUrlVariables` 来自的API [边缘网络的标识](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) 扩展，以在打开 [!DNL webViews].

Web SDK无需其他配置即可接受 `ECID` 值。

查询字符串参数包括：

* `MCID`:Experience CloudID(`ECID`)
* `MCORGID`:Experience Cloud `orgID` 必须与 `orgID` 在 [!DNL Web SDK].
* `TS`:时间戳参数不能早于五分钟。


移动到Web ID共享使用 `adobe_mc` 参数。 当 `adobe_mc` 参数存在且有效， `ECID` 在向边缘网络发出的第一个请求中，查询字符串中的自动添加到标识映射。 所有后续边缘网络交互都将使用该 `ECID`.

有关如何将访客ID从移动设备应用程序传递到WebView的更多信息，请参阅 [处理WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 跨域ID共享 {#cross-domain-sharing}

对于跨域ID共享，Web SDK版本2.11.0增加了对 `appendIdentityToUrl` 命令。 使用时，此命令会生成 `adobe_mc` 查询字符串参数。

该命令接受具有一个属性的对象， `url`，并返回具有属性的对象 `url`.

此命令不会等待任何同意更新。 如果未提供同意，则返回的URL将保持不变。

如果 `ECID` 未提供， `/acquire` 将调用端点以生成 `ECID`.

以下是客户如何在其网站上实施跨域ID共享的示例。

此代码会为页面上的所有点击添加事件侦听器，如果点击位于指向匹配域的链接上（在本例中为） `adobe.com` 或 `behance.com`)，会将身份添加到URL并重定向用户。

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

与使用 [!DNL Web SDK]，则无需在 [!DNL Tags] 扩展，以使用通过URL传递的身份。

要通过“标记”扩展使用移动到Web和跨域ID共享，您必须使用“标记”扩展的版本2.12.0或更高版本。

要将当前页面的标识共享到其他域，请在 [!DNL Web SDK] [!DNL Tags] 扩展。 此操作旨在与 **[!UICONTROL 核心 — 单击]** 事件类型和值比较条件。

按照描述的步骤操作 [此处](../../tags/ui/managing-resources/rules.md) 要创建具有以下配置的规则，请执行以下操作：

* [!UICONTROL 事件配置]:
   * **[!UICONTROL 扩展：核心]**
   * **[!UICONTROL 事件类型：单击]**
   * 选择 **[!UICONTROL 用户单击>特定元素时]**
   * 键入 **[!UICONTROL 选择器]**: `a[href]`. 每当在具有 `href` 属性。

      ![显示使用上述设置的事件配置的UI图像](assets/id-sharing-event-configuration.png)

* [!UICONTROL 条件配置]
   * **[!UICONTROL 逻辑类型]**: [!UICONTROL 常规]
   * **[!UICONTROL 扩展]**: [!UICONTROL 核心]
   * **[!UICONTROL 条件类型]**: [!UICONTROL 值比较]
   * **[!UICONTROL 左操作数]**: [!UICONTROL `%this.hostname%`]. 这是一个与 [!UICONTROL 核心 — 单击] 事件并解析为已单击链接的主机名。
   * **[!UICONTROL 运算符]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL 右操作数]**:键入一个与要与其共享身份的域匹配的正则表达式。 例如，要匹配主机名以结尾的链接 `adobe.com` 或 `behance.com`，请使用此正则表达式： `behance.com$|adobe.com$`. 链接的页面需要具有 [!DNL Web SDK] 或 [!DNL Visitor ID] 已安装以接受身份。

      ![使用上述设置显示条件配置的UI图像](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 操作配置]
   * **[!UICONTROL 扩展]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL 操作类型]**: [!UICONTROL 通过标识重定向]
   * **[!UICONTROL 实例]**:选择您的实例。 在大多数情况下，您将只配置一个实例。 如果您有多个实例，请选择要共享的具有身份的实例。

      ![显示使用上述设置的操作配置的UI图像](assets/id-sharing-action-configuration.png)

的 **[!UICONTROL 通过标识重定向]** 操作将阻止浏览器导航到链接。 然后，它将调用 `appendIdentityToUrl` 方法 [!DNL Web SDK] 实例。

最后，它会将用户重定向到 [!DNL URL] 和 `adobe_mc` 附加了查询字符串参数。
