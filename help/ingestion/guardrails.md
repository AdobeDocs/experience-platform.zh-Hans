---
keywords: Experience Platform；疑難排解；護欄；指南；
title: 資料擷取的護欄
description: 本檔案提供在Adobe Experience Platform中用於資料擷取的護欄相關指示
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 582f6ffdea6fa1978f6af6f0f0f92e50a12f6200
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---

# 資料擷取的護欄

護欄是臨界值，可為Adobe Experience Platform中的資料和系統使用、效能最佳化以及避免錯誤或意外結果提供指引。 護欄可指您關於授權權益的使用或資料消耗與處理方式。

本檔案提供在Adobe Experience Platform中用於資料擷取的護欄相關指示。

## 批次擷取的護欄

下表概述使用時需考慮的護欄 [批次擷取API](./batch-ingestion/overview.md) 或來源：

| 內嵌型別 | 准则 | 注释 |
| --- | --- | --- |
| 使用批次擷取API擷取資料湖 | <ul><li>您可以使用批次擷取API，每小時最多可擷取20 GB資料至資料湖。</li><li>每個批次的最大檔案數為1500。</li><li>最大批次大小為100 GB。</li><li>每列的屬性或欄位數上限為10000。</li><li>每分鐘每個使用者的批次數量上限為138。</li></ul> |
| 使用批次來源擷取資料湖 | <ul><li>您可以使用批次擷取來源（例如），每小時將最多200 GB的資料擷取至資料湖 [!DNL Azure Blob]， [!DNL Amazon S3]、和 [!DNL SFTP].</li><li>批次大小應介於256 MB和100 GB之間。</li><li>每個批次的最大檔案數為1500。</li></ul> | 請參閱 [來源概觀](../sources/home.md) 如需可用於資料內嵌的來源目錄。 |
| 批次擷取至設定檔 | <ul><li>記錄類別的大小上限為100 KB （可變）。</li><li>ExperienceEvent類別的大小上限為10 KB （可變）。</li><li>單一記錄的大小上限為1 MB。</li></ul> |
| 每天擷取的設定檔或ExperienceEvent批次數量 | **每天最多可擷取90個Profile或ExperienceEvent批次。** 這表示每天擷取的Profile和ExperienceEvent批次總數不能超過90。 擷取其他批次將會影響系統效能。 | 這是軟性限制。 雖然可能會超出軟性限制，但軟性限制會提供系統效能的建議指引。 |

## 串流擷取的護欄

下表概述使用時需考慮的護欄 [串流獲取API](./streaming-ingestion/overview.md) 或串流來源：

| 內嵌型別 | 准则 | 注释 |
| --- | --- | --- |
| 流式摄取 | <ul><li>記錄大小上限為1 MB，建議大小為10 KB。</li><li>您每秒最多可以處理2500個要求至Profile。</li><li>您可以在15分鐘內每秒最多處理20000個前往資料湖的請求。</li></ul> | 如果您需要更高的資料輸送量，請使用批次擷取API。 |
| 串流來源 | <ul><li>記錄大小上限為1 MB，建議大小為10 KB。</li><li>在建立新的來源連線時，串流來源支援每秒鐘約4000到5000個要求。 **注意**：將串流資料完全處理至Data Lake最多可能需要30分鐘。</li><li>您可以每秒處理4000到5000個至Data Lake的請求。 **注意**：將串流資料完全處理至Data Lake最多可能需要30分鐘。</li></ul> | 串流來源，例如 [!DNL Kafka]， [!DNL Azure Event Hubs]、和 [!DNL Amazon Kinesis] 請勿使用 [!DNL Data Collection Core Service] (DCCS)路由，可有不同的輸送量限制。 請參閱 [來源概觀](../sources/home.md) 如需可用於資料內嵌的來源目錄。 |

## 后续步骤

請參閱下列檔案，深入瞭解資料與Experience Platform處理護欄：

* [即時客戶個人檔案資料的護欄](../profile/guardrails.md)
* [Identity Service資料的護欄](../identity-service/guardrails.md)
