---
title: Adobe Experience Platform發行說明2020年12月
description: Adobe Experience Platform的2020年12月發行說明。
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**發行日期： 2020年12月9日**

Adobe Experience Platform中的新功能：

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

数据流是跨平台移动数据的数据作业的表示方法。這些資料流會在不同的服務之間設定，有助於將資料從來源聯結器移至目標資料集、身分和設定檔服務以及目的地。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 資料流程的透明度 | 您可以監視來源和目的地的資料流。 如需詳細資訊，請閱讀 [監控來源的教學課程](../../dataflows/ui/monitor-sources.md) 或 [監控目的地的教學課程](../../dataflows/ui/monitor-destinations.md). |

若要進一步瞭解資料流，請閱讀 [資料流概觀](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 Data Science Workspace已整合至Adobe Experience Platform，可協助您跨多個Adobe解決方案使用您的內容和資料資產進行預測。

**主要功能**

| 功能 | 描述 |
| --- | ---|
| Adobe Experience Platform Intelligence套件附加元件 | Adobe Experience Platform Intelligence套件附加元件是資料科學工作區升級，可解鎖其他重要功能，例如： <li> UI導向的模型實驗與評估。</li><li> 能夠透過排程的培訓和推斷工作來部署及操作模型。</li><li> 支援Tensorflow模型（GPU運算）的深度學習。</li><li> 以Spark為基礎的分散式計算，可針對大型資料集（10MM +列）進行訓練和評分。</li><li>及更多內容</li> |

若要深入瞭解Adobe Experience Platform Intelligence套件附加元件，請參閱以下檔案： [資料科學工作區存取與功能](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新串流來源的帳戶和連線詳細資料 | 您現在可以使用更新現有串流連線的名稱、說明和認證 [!DNL Flow Service] API和UI。 如需詳細資訊，請參閱以下教學課程： [使用API更新連線](../../sources/tutorials/api/update.md) 和 [使用UI編輯帳戶詳細資料](../../sources/tutorials/ui/monitor.md). |
| 刪除資料流 | 現在可以使用刪除包含錯誤或變得不必要的串流資料流 [!DNL Flow Service] API和UI。 如需詳細資訊，請參閱以下教學課程： [使用API刪除資料流](../../sources/tutorials/api/delete-dataflows.md) 和 [使用UI刪除資料流](../../sources/tutorials/ui/delete.md). |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
