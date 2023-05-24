---
keywords: Experience Platform；首頁；熱門主題；資料擷取；擷取的資料；串流；概觀；串流擷取；延遲；串流延遲；
solution: Experience Platform
title: 串流擷取概觀
description: Adobe Experience Platform的串流擷取為使用者提供一種方法，可即時從使用者端和伺服器端裝置傳送資料至Experience Platform。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# 流式摄取概述

Adobe Experience Platform的串流擷取為使用者提供一種從使用者端和伺服器端裝置傳送資料到的方法 [!DNL Experience Platform] 即時。

## 您可以使用串流擷取做什麼？

Adobe Experience Platform可讓您透過產生 [!DNL Real-Time Customer Profile] 適用於您的每位客戶。 串流擷取可讓您傳送，在建置這些設定檔時扮演關鍵角色 [!DNL Profile] 資料匯入 [!DNL Data Lake] 儘可能縮短延遲時間。

以下影片旨在協助您瞭解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 串流設定檔記錄和 [!DNL ExperienceEvents]

透過串流擷取，使用者可以串流設定檔記錄和 [!DNL ExperienceEvents] 至 [!DNL Platform] 數秒內完成，協助促進即時個人化。 所有傳送至串流獲取API的資料都會自動儲存在 [!DNL Data Lake].

請閱讀 [建立串流連線指南](../tutorials/create-streaming-connection.md) 以取得詳細資訊。

### 資料集資料流

一旦您確定您的資料是乾淨的，就可以啟用資料集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].

如需啟用資料集的詳細資訊，請參閱 [!DNL Profile] 和 [!DNL Identity Service]，請閱讀 [設定資料集指南](../../profile/tutorials/dataset-configuration.md).

## 串流擷取的預期延遲為何？ [!DNL Platform]？

| 目标 | 預期延遲 |
| --------- | ---------------- |
| 实时客户资料 | &lt; 1分鐘 |
| 資料湖 | &lt; 60 分钟 |

## 串流擷取的每秒要求(RPS)指引

下表顯示串流擷取的每秒請求數限制相關指引。

| RPS限制 | 注释 |
| --- | --- |
| 每秒1000個要求 | 使用時，這些可包含多則訊息 `/collection/batch` 端點。 |
| 每秒傳10000個別訊息 | 使用時，可將訊息分組為較少的實際請求 `/collection/batch` 端點。 |

>[!IMPORTANT]
>
>強制限制會變成 **每分鐘60個請求** 當使用同步驗證以進行偵錯時。

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform擴充功能來建立新的串流連線。 此 [!DNL Experience Platform] 擴充功能提供傳送信標的動作，格式化方式為 [!DNL Experience Data Model] (XDM)即時擷取至 [!DNL Experience Platform]. 造訪 [Experience Platform擴充功能](../../tags/extensions/client/sdk/overview.md) 說明檔案以取得詳細資訊。
