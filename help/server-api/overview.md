---
title: 边缘网络服务器API概述
description: 了解什么是 Edge Network Server API 以及如何使用它。
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: 数据收集；Adobe Experience Platform Edge Network；服务器API;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 5%

---

# 边缘网络服务器API概述 {#overview}

Adobe Experience Platform Edge Network为客户提供了一种与任何Adobe Experience Cloud或Adobe Experience Platform Edge服务进行交互的优化方式。

的 [!DNL Edge Network Server API] 可用于各种数据收集、个性化、广告和营销用例。 的 [!DNL Server API] 可在服务器上使用， [!DNL IoT] 设备、机顶盒和各种其他设备。

自 [!DNL Server API] 它不依赖任何库来加载，它提供了一种以闪电般的速度与Adobe Experience Platform边缘网络及受支持的解决方案进行交互的方式。

的好处 [!DNL Server API] 架构包括：

* 缩短了页面加载时间
* 改进了延迟
* 第一方数据收集
* 简化的服务端通信

的 [!DNL Server API] 通过两个专用端点支持交互式和批量数据收集：

1. 交互式端点支持与Adobe Experience Platform和Adobe Experience Cloud服务的通信，这些服务支持高级分段、个性化和其他营销用例。
2. 批处理端点将允许在需要载入数据时批量发送请求，而不会收到来自正在调用的应用程序的响应。

的 [!DNL Server API] 支持以下类型的请求：

* 通过验证的请求 [Adobe I/O](https://developer.adobe.com/)，使用新 `server.adobedc.net` 端点。
* 通过的未验证请求 `edge.adobedc.net` 端点。

这允许根据贵组织的隐私政策，安全地收集经过身份验证的敏感数据。 除了身份验证之外，服务器API还支持标记数据流以仅接受通过API进行的经过身份验证的通信。

请观看以下视频，以简化服务器API的概述。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
