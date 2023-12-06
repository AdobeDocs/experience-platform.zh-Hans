---
title: Edge Network服务器API概述
description: 了解什么是 Edge Network Server API 以及如何使用它。
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---


# Edge Network服务器API概述 {#overview}

Adobe Experience Platform Edge Network为客户提供了与任何Adobe Experience Cloud或Adobe Experience Platform Edge服务交互的优化方式。

此 [!DNL Edge Network Server API] 可用于各种数据收集、个性化、广告和营销用例。 此 [!DNL Server API] 可以在服务器上使用， [!DNL IoT] 设备、机顶盒和其他各种设备。

由于 [!DNL Server API] 它不依赖任何库来加载，提供了与Adobe Experience Platform Edge Network及支持的解决方案进行交互的快速方式。

的好处 [!DNL Server API] 架构包括：

* 缩短页面加载时间
* 改善延迟
* 第一方数据收集
* 服务之间简化的服务器端通信

此 [!DNL Server API] 支持通过两个专用端点进行交互式和批量数据收集：

1. 交互式端点支持与Adobe Experience Platform和Adobe Experience Cloud服务的通信，这些服务支持高级分段、个性化和其他营销用例。
2. 批处理端点允许在必须载入数据时批量发送请求，而不会收到来自所调用应用程序的响应。

此 [!DNL Server API] 支持以下类型的请求：

* 已通过身份验证的请求 [Adobe Developer](https://developer.adobe.com/)，使用 `server.adobedc.net` 端点。
* 通过进行的未经身份验证的请求 `edge.adobedc.net` 端点。

这样可根据贵组织的隐私政策，启用允许安全、经过身份验证的敏感数据收集的使用案例。 除了身份验证之外，服务器API支持标记数据流以仅接受通过API的经过身份验证的通信。

请观看以下视频，以大致了解服务器API。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
