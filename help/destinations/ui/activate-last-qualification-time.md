---
title: 使用新Beta版雲端儲存空間目的地中的上次資格取得時間XDM屬性
description: 瞭解如何在新的Beta版雲端儲存目的地中使用上次資格取得時間XDM屬性
hidefromtoc: y
hide: y
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 使用新Beta版雲端儲存空間目的地中的上次資格取得時間XDM屬性 {#last-qualification-time}

>[!IMPORTANT]
> 
>本頁說明測試版中的功能。 功能和檔案可能會有所變更。 如果您想要存取此Beta版計畫，請聯絡您的Adobe代表或客戶服務。

## 先决条件 {#prerequisites}

若要使用上次合格時間(`lastQualificationTime`) XDM屬性，您必須註冊 [Beta版計畫](/help/release-notes/2022/october-2022.md#destinations) 使用改良的檔案匯出功能，並將資料匯出至六項功能之一 [beta雲端儲存空間目的地](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)， [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)， [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)， [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))。 如果您能在目錄中看到雲端儲存空間目的地的新Beta版卡，請註冊，如下所示 [!DNL Amazon S3].

![顯示新Amazon S3 Beta卡的影像](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## 如何使用最後合格時間XDM屬性 {#how-to-use}

如果您使用六個新Cloud Storage Beta聯結器之一，則可以在中使用最後資格取得時間XDM屬性 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 啟動工作流程的資訊，以在匯出的檔案中建立欄，且最新時間戳記為設定檔符合區段資格的時間。 這可協助您處理某些測量或分析使用案例，也可讓您更清楚瞭解何時啟用某些對象。

請注意，若要新增 `lastQualificationTime` 在檔案匯出中，您目前需要手動插入值 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 放入來源欄位中，如下所示。 您也可以將目標欄位編輯為 `lastQualificationTime` 或您想要命名此欄的任何其他值。 請注意，由於這是測試版功能，因此其 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 值未來可能會變更。

![熒幕錄製，顯示將XDM屬性貼入對應步驟的最後合格時間](/help/destinations/ui/last-qualification-time.gif)

## 更多信息 {#more-information}

如需將資料啟用至檔案型目的地的詳細資訊，包括工作流程中的所有步驟和必要許可權，請參閱 [啟用檔案型目的地教學課程](/help/destinations/ui/activate-batch-profile-destinations.md).
