---
keywords: 雲端儲存空間目的地；雲端儲存空間
title: 雲端儲存空間目的地概觀
description: Adobe Experience Platform可將您的區段以資料檔案形式傳送至您的Amazon S3、AWS Kinesis、Azure事件中樞或SFTP雲端儲存位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# 雲端儲存空間目的地概觀 {#cloud-storage-destinations}

## 概述 {#overview}

Adobe Experience Platform可將您的區段以資料檔案形式傳送至雲端儲存位置。 這可讓您透過以下專案的CSV檔案將對象及其設定檔屬性傳送至您的內部系統： [!DNL Amazon S3]， [!DNL Azure Blob]， [!DNL Azure Data Lake Storage Gen2]， [!DNL Data Landing Zone]， [!DNL Google Cloud Storage]和SFTP。 對象 [!DNL Amazon Kinesis] 和 [!DNL Azure Event Hubs] 目的地，資料會以串流方式從Experience Platform傳出 [!DNL JSON] 格式。

![Adobe雲端儲存空間目的地](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支援的雲端儲存空間目的地 {#supported-destinations}

Adobe Experience Platform支援下列雲端儲存空間目的地：

* [Amazon Kinesis連線](amazon-kinesis.md)
* [Amazon S3連線](amazon-s3.md)
* [Azure Blob連線](azure-blob.md)
* [(Beta) Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure事件中樞連線](azure-event-hubs.md)
* [(Beta)資料登陸區域](data-landing-zone.md)
* [(Beta) Google雲端儲存空間](google-cloud-storage.md)
* [sftp連線](sftp.md)

## 連線到新的雲端儲存空間目的地 {#connect-destination}

若要將區段傳送至行銷活動的雲端儲存空間目的地，Platform必須先連線至目的地。 請參閱 [目的地建立教學課程](../../ui/connect-destination.md) 以取得設定新目的地的詳細資訊。


## 使用宏在存储位置创建一个文件夹 {#use-macros}

>[!NOTE]
>
> 本節所述的功能目前適用於 [Amazon S3](amazon-s3.md) 僅限目的地。

若要在儲存位置中為每個區段檔案建立自訂資料夾，您可以在資料夾路徑輸入欄位中使用巨集。 在輸入欄位的結尾處插入巨集，如下所示。

![如何使用巨集在儲存空間中建立資料夾](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

下列範例會參考範例區段 `Luxury Audience` 包含ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**巨集1：`%SEGMENT_NAME%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience`

**巨集2：`%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**巨集3：`%SEGMENT_NAME%/%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 資料匯出型別 {#export-type}

雲端儲存空間目的地支援 **以設定檔為基礎的匯出**. 這表示您正在匯出對象中個人的詳細資訊。 個人化需要這些詳細資訊，可能包括屬性、事件、區段成員資格等。