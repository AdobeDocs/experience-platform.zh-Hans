---
keywords: Experience Platform；首頁；熱門主題；日期範圍
title: 標準警報規則
description: 本檔案說明Experience Platform提供的預先定義警示規則。
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 6650894c145fd1f42731fd5ed8aeb6e38062aa61
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# 標準警報規則

Adobe Experience Platform提供數個預先定義的警報規則，您可以為組織啟用這些規則。 本檔案說明這些Adobe提供的警報規則的詳細資料。 如需Experience Platform中警示的一般詳細資訊，請參閱 [警報概觀](./overview.md).

時間 [在Platform UI中檢視警報規則](./ui.md)，您可以個別訂閱每個規則。 透過訂閱警報時 [I/O事件通知](./subscribe.md)不過，警報規則會整理成不同的訂閱套件。 下表顯示每個規則及其對應的I/O事件訂閱名稱。

## 数据引入

下列警示規則專屬於 [資料擷取](../../ingestion/home.md) 和  [來源](../../sources/home.md)：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 來源流程執行資訊 | 來源流程執行開始 | 當來源連線開始處理資料時，就會觸發此警報。 |
| 來源流程執行資訊 | 來源資料流執行成功 | 成功從來源連線擷取資料時，就會觸發此警報。 |
| 來源流程執行延遲、失敗和錯誤 | 來源流程執行失敗 | 從來源連線擷取資料時發生錯誤，就會觸發此警報。 |
| 來源流程執行延遲、失敗和錯誤 | 擷取延遲 | 批次擷取流程執行需要超過150分鐘的處理時間時，就會觸發此警報。 |
| 來源流程執行延遲、失敗和錯誤 | 擷取失敗 | 當失敗記錄與所有記錄的比率超過0.5%的臨界值時，就會觸發此警報。 |

{style="table-layout:auto"}

如果您先前已訂閱下列警示型別，則不會再收到警示，因為此警示已過時：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 來源流程執行延遲、失敗和錯誤 | 缺乏內嵌 | 如果內嵌延遲超過7小時且沒有資料內嵌到Platform，此警報會傳送訊息給您。 |

{style="table-layout:auto"}

## Identity Service

下列警示規則專屬於 [Identity Service](../../identity-service/home.md)：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 身分擷取資訊 | Identity服務流程執行開始 | 當Identity Service流程執行開始處理資料時，就會觸發此警報。 換句話說，擷取的資料正從Data Lake載入至Identity Service。 |
| 身分擷取資訊 | Identity服務流程執行成功 | 當資料成功從Data Lake載入到Identity Service時，就會觸發此警報。 |
| 身分擷取延遲、失敗和錯誤 | Identity服務流程執行延遲 | 當Identity服務流程執行需要超過150分鐘的處理時間時，就會觸發此警報。 |
| 身分擷取延遲、失敗和錯誤 | 識別服務流程執行失敗 | 將資料擷取至Identity Service時發生錯誤，就會觸發此警報。 |

{style="table-layout:auto"}

## 实时客户资料

下列警示規則專屬於 [即時客戶個人檔案](../../profile/home.md)：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 設定檔擷取資訊 | 設定檔流程執行開始 | 設定檔流程執行開始處理資料時，就會觸發此警報。 |
| 設定檔擷取資訊 | 設定檔流程執行成功 | 當資料成功從資料湖載入設定檔時，就會觸發此警報。 |
| 設定檔擷取延遲、失敗和錯誤 | 設定檔流程執行延遲 | 從資料湖載入資料至設定檔時，若處理時間超過150分鐘，就會觸發此警報。 |
| 設定檔擷取延遲、失敗和錯誤 | 設定檔流程執行失敗 | 將資料擷取至設定檔時發生錯誤，就會觸發此警報。 |

{style="table-layout:auto"}

## 区段

下列警示規則專屬於 [細分服務](../../segmentation/home.md)：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 區段評估工作資訊 | 區段工作開始 | 當區段評估工作開始處理資料時，就會觸發此警報。 |
| 區段評估工作資訊 | 區段工作成功 | 當區段評估工作成功完成時，就會觸發此警報。 |
| 區段評估工作延遲、失敗和錯誤 | 區段工作延遲 | 當區段評估工作需要超過150分鐘才能完成時，就會觸發此警報。 <br> 將會出現下列其中一種狀態： <br> — 引發 — 已符合失敗或延遲的條件（將其視為使用中）。 <br> — 非使用中 — 條件未滿足或未解決（將其考慮為已解決狀態）。 |
| 區段評估工作延遲、失敗和錯誤 | 區段作業失敗 | 當區段評估工作導致錯誤時，就會觸發此警報。 |
| 區段評估工作延遲、失敗和錯誤 | 區段定義已停用 | 此警報會在區段定義因內部錯誤而停用時觸發。 這會自動觸發戰場，讓Adobe工程團隊調查此問題。 此警報僅供參考，不需要您採取任何動作。 |

{style="table-layout:auto"}

## 目标

下列警示規則專屬於 [目的地](../../destinations/home.md)：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 目的地流程執行資訊 | 目的地流程執行開始 | 目的地流程執行開始啟用區段時，就會觸發此警報。 |
| 目的地流程執行資訊 | 目的地流程執行成功 | 成功將區段啟用至目的地時，就會觸發此警報。 |
| 目的地流程執行延遲、失敗和錯誤 | 目的地資料流執行延遲 | 目的地流程執行需要超過150分鐘的時間來啟動區段時，就會觸發此警報。 |
| 目的地流程執行延遲、失敗和錯誤 | 目的地流程執行失敗 | 將區段啟用至目的地時發生錯誤，就會觸發此警報。 |
| 目的地流程執行延遲、失敗和錯誤 | 略過率超過臨界值 | 略過的ID與總ID的比率超過臨界值時，就會觸發此警報。 |

{style="table-layout:auto"}

## 查询服务

下列警示規則專屬於 [查詢服務](../../query-service/home.md)：

| I/O事件訂閱 | 警示規則 | 描述 |
| --- | --- | --- |
| 查詢服務排定的查詢資訊 | 查詢服務已排程查詢開始 | 排定的查詢開始執行時會觸發此警報。 |
| 查詢服務排定的查詢資訊 | 查詢服務已排程查詢成功 | 排定的查詢工作順利完成時，就會觸發此警報。 |
| 查詢服務已排程查詢延遲、失敗和錯誤 | 查詢服務排程查詢失敗 | 排定的查詢作業失敗時，就會觸發此警報。 |

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
