---
title: 移动到Web和跨域ID共享
description: 了解如何将访客ID从移动资产保留到Web资产并跨域保留
keywords: 身份；移动设备；ID；共享；域；跨域；SDK；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 移动到Web和跨域ID共享

## 概述

Adobe Experience Platform Web SDK支持访客ID共享功能，这使得客户能够在移动应用程序和移动Web内容之间以及跨域更准确地提供个性化体验。

## 用例 {#use-cases}

### 在移动应用程序和移动网站之间提供一致的个性化

一家服装公司希望根据客户的兴趣来为他们提供个性化体验，并在同时加载WebViews的移动应用程序中保持个性化的准确性。 通过使用移动到Web ID共享功能，他们可以将[!DNL ECID]传递到移动Web URL，从而确保在应用程序和移动Web内容中使用相同的访客标识符来向客户呈现最准确的优惠。

### 跨域提供一致的个性化

一家拥有多个在线商店的零售商希望根据客户兴趣对其域中的购物者体验进行个性化。 通过使用Web SDK跨域ID共享功能，零售商可以在其所有域中根据客户兴趣提供准确的优惠。

### 增强访客活动报告功能

技术零售商希望提供有关访客何时从移动应用程序移动到其移动网站或何时移动到其其他域的信息来改进其访客活动报表。 通过使用Web SDK跨域ID共享功能，营销团队可以准确地跟踪其Web资产中的访客并生成活动报表。

## 先决条件 {#prerequisites}

要使用移动到Web和跨域ID共享，您必须使用[!DNL Web SDK]版本2.11.0或更高版本。

对于Edge Network移动设备实施，从版本1.1.0(iOS和Android)开始的[Edge Network标识](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/)扩展支持此功能。

此功能还与[!DNL VisitorAPI.js]版本1.7.0或更高版本兼容。

## 移动到Web ID共享 {#mobile-to-web}

使用Edge Network[&#128279;](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables)扩展的身份中的`getUrlVariables` API将标识符检索为查询参数，并在打开[!DNL webViews]时将其附加到您的URL。

Web SDK无需其他配置即可接受查询字符串中的`ECID`值。

查询字符串参数包括：

* `MCID`：Experience CloudID (`ECID`)
* `MCORGID`：Experience Cloud`orgID`必须与[!DNL Web SDK]中配置的`orgID`匹配。
* `TS`：时间戳参数不能早于5分钟。


移动设备与Web ID共享使用`adobe_mc`参数。 当`adobe_mc`参数存在且有效时，查询字符串中的`ECID`将自动添加到向Edge Network发出的第一个请求中的标识映射。 所有后续Edge Network交互将使用该`ECID`。

有关如何将访客ID从移动应用程序传递到WebView的更多信息，请参阅有关[处理WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html?lang=zh-Hans#implementation)的文档。

## 实施跨域ID共享 {#cross-domain-sharing}

有关同时使用Web SDK标记扩展和Web SDK JavaScript库的实施说明，请参阅[`appendIdentityToUrl`](../commands/appendidentitytourl.md)命令。
