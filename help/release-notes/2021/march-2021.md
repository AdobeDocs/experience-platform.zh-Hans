---
title: Adobe Experience Platform發行說明2021年3月
description: Adobe Experience Platform 2021年3月發行說明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2021 年 3 月 31 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

| 功能 | 描述 |
| ------- | ----------- |
| `add_to_array` 函数 | 更新支援陣列作為引數的功能。 |
| `to_array` 函数 | 更新支援物件作為引數的功能。 |

如需詳細資訊，請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段並從 [!DNL Real-Time Customer Profile] 資料。 這些區段會集中設定並維護於 [!DNL Platform]，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| (Beta)邊緣細分 | Edge區段會即時評估區段，以允許相同頁面和下一頁個人化使用案例。 有關邊緣細分的更多資訊可在以下網址找到： [區段UI總覽](../../segmentation/ui/overview.md). |
| (Beta)增量細分 | 將批次分段中評估之現有區段定義的時效性提高至最多一小時。 |

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| ------- | ----------- |
| Beta版來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 壓縮檔案擷取的API支援 | 您現在可以使用雲端儲存空間來源，預覽及擷取壓縮的JSON或分隔檔案。 如需詳細資訊，請參閱以下教學課程： [使用API收集雲端儲存空間資料](../../sources/tutorials/api/collect/cloud-storage.md). |
| UI支援遞回檔案上傳 | 您現在可以在使用雲端儲存空間來源時遞回擷取整個資料夾。 擷取整個資料夾時，您必須確保其內容共用相同的結構描述。 如需詳細資訊，請參閱以下教學課程： [在UI中為雲端儲存聯結器設定資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
