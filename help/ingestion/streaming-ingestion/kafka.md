---
keywords: Experience Platform；首頁；熱門主題；kafka；kafka聯結器；Kafka；
solution: Experience Platform
title: Kafka聯結器
description: Adobe Experience Platform的串流聯結器以Apache Kafka Connect為基礎。 此資料庫可用於將資料中心內Kafka主題的JSON事件直接串流到即時Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform的聯結器

Adobe Experience Platform的資料流聯結器是根據 [!DNL Apache Kafka Connect]. 此程式庫可用於將JSON事件從以下來源串流： [!DNL Kafka] 資料中心中的主題直接傳送至 [!DNL Experience Platform] 即時。

串流聯結器是接收器（單向）聯結器，從傳送資料 [!DNL Kafka] 主題至已註冊的端點： [!DNL Experience Platform]. 若要使用此聯結器，您必須下載程式庫，並將其新增至您現有的 [!DNL Kafka] 部署，並設定 [!DNL Kafka] Adobe串流HTTP URL的主題。 其他程式碼為 **not** 必填。 聯結器支援下列功能：

- 已驗證的資料彙集
- 批次處理訊息以減少網路呼叫並提高輸送量

如需詳細資訊，請參閱 [!DNL Kafka] 聯結器，包括如何設定聯結器的說明，請閱讀 [快速入門手冊](https://github.com/adobe/experience-platform-streaming-connect). 如需更詳細的工作流程，請閱讀 [開發人員指南](https://www.adobe.com/go/kafka-connector-developer-guide).
