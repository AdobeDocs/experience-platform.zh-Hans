---
title: Edge Network Server API總覽
description: 了解什么是 Edge Network Server API 以及如何使用它。
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: 資料收集；收集；Adobe Experience Platform Edge Network；伺服器api；
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 15%

---

# Edge Network Server API總覽 {#overview}

Adobe Experience Platform Edge Network 为客户提供了与任何 Adobe Experience Cloud 或 Adobe Experience Platform Edge 服务交互的优化方式。

此 [!DNL Edge Network Server API] 可用於各種資料收集、個人化、廣告和行銷使用案例。 此 [!DNL Server API] 可用於伺服器， [!DNL IoT] 裝置、機上盒和其他各種裝置。

由於 [!DNL Server API] 不依賴任何程式庫載入，而是提供極快速的方式與Adobe Experience Platform Edge Network和支援的解決方案互動。

的優點 [!DNL Server API] 架構包括：

* 縮短頁面載入時間
* 改善延遲
* 第一方資料收集
* 簡化服務之間的伺服器端通訊

此 [!DNL Server API] 透過兩個專用端點，支援互動式和批次資料收集：

1. 互動式端點支援與Adobe Experience Platform和Adobe Experience Cloud服務的通訊，這些服務支援進階細分、個人化和其他行銷使用案例。
2. 當需要上線資料時，批次端點將允許批次傳送請求，而不會收到來自被呼叫的應用程式的回應。

此 [!DNL Server API] 支援下列型別的請求：

* 已驗證的請求，透過 [Adobe I/O](https://developer.adobe.com/)，使用新的 `server.adobedc.net` 端點。
* 透過的未驗證請求 `edge.adobedc.net` 端點。

如此一來，即可根據貴組織的隱私權政策，啟用允許收集敏感資料且經過驗證的安全使用案例。 除了驗證以外，伺服器API支援標籤資料串流，以僅接受透過API的驗證通訊。

觀看以下影片，瞭解Server API的簡化概觀。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
