---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用設定檔；啟用設定檔
title: 新增資料至即時客戶個人檔案
type: Tutorial
description: 本教學課程概述將資料新增至即時客戶設定檔的必要步驟。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 新增資料至 [!DNL Real-Time Customer Profile]

本教學課程概述新增資料至的必要步驟 [!DNL Real-Time Customer Profile].

## 啟用結構描述 [!DNL Real-Time Customer Profile]

正在擷取的資料 [!DNL Experience Platform] 供使用 [!DNL Real-Time Customer Profile] 必須符合 [!DNL Experience Data Model] (XDM)結構描述已啟用 [!DNL Profile]. 若要為設定檔啟用結構描述，它必須實作 [!DNL XDM Individual Profile] 或 [!DNL XDM ExperienceEvent] 類別。

您可以啟用結構描述以用於 [!DNL Real-Time Customer Profile] 使用 [!DNL Schema Registry] API或 [!DNL Schema Editor] 使用者介面。 若要開始使用，請遵循的教學課程 [使用API建立結構描述](../../xdm/tutorials/create-schema-api.md) 或 [使用結構描述編輯器UI建立結構描述](../../xdm/tutorials/create-schema-ui.md).

## 使用批次擷取新增資料

所有資料已上傳至 [!DNL Platform] 使用批次擷取會上傳至個別資料集。 在可以使用此資料之前， [!DNL Real-Time Customer Profile]，相關資料集必須經過專門設定。 如需完整的指示，請參閱以下教學課程： [為設定檔和Identity服務設定資料集](dataset-configuration.md).

設定資料集後，您就可以開始將資料內嵌到其中。 請參閱 [批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md) 以取得有關如何上傳不同格式檔案的詳細步驟。

## 使用串流擷取新增資料

任何符合「 」的串流擷取資料 [!DNL Profile]-enabled XDM結構描述會自動新增或覆寫中的適當記錄 [!DNL Real-Time Customer Profile]. 如果記錄中提供了多個身分，或使用了時間序列資料，則這些身分將會在身分圖表中對應，而無需額外的設定。 請參閱 [串流擷取開發人員指南](../../ingestion/tutorials/streaming-record-data.md) 以深入瞭解。

## 確認上傳成功

首次將資料上傳到新資料集時，或是在涉及新ETL或資料來源的程式過程中，建議仔細檢查資料，以確保資料已正確上傳。

使用 [!DNL Real-Time Customer Profile] 存取API，您可以在批次資料載入資料集時擷取該資料。 如果您無法擷取任何您預期的實體，您的資料集可能不會啟用 [!DNL Profile]. 確認您的資料集已啟用後，請確定來源資料格式和識別碼支援您的期望。

有關如何使用存取實體的詳細說明 [!DNL Real-Time Customer Profile] API，請參閱 [實體端點指南](../api/entities.md)，也稱為「[!DNL Profile Access] API」。

## 更新設定檔存放區資料

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 這可以透過批次擷取完成，並需要設定檔啟用的資料集，以更新插入標籤。 如需如何設定屬性更新資料集的詳細資訊，請參閱的教學課程 [為設定檔和更新插入啟用資料集](../../catalog/datasets/enable-upsert.md).
