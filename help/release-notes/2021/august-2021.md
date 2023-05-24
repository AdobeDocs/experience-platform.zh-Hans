---
title: Adobe Experience Platform發行說明2021年8月
description: Adobe Experience Platform的2021年8月發行說明。
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 8 月 25 日**

Adobe Experience Platform 现有功能的更新包括：

- [目标](#destinations)
- [可观察性洞察](#observability)
- [实时客户资料](#profile)
- [源](#sources)

## 目标 {#destinations}

目的地是預先建立的與目的地平台的整合，可無縫地從Adobe Experience Platform啟用資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | 「飛艇屬性」目的地（先前為測試版）現已正式推出。 |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 飛艇標籤目的地（先前為測試版）現已正式推出。 |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze目的地（先前為測試版）現已正式推出。 |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | 透過Pinterest客戶清單目的地，您可以從客戶清單、造訪過您網站的人或已在Pinterest上與您的內容互動的人中建立受眾。 |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | 在Twitter中鎖定您現有的追隨者和客戶，並透過啟用Adobe Experience Platform中建立的對象來建立相關的再行銷活動。 |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX是彙總的Verizon Media/Yahoo基礎架構，其中託管各種元件，讓Verizon Media/Yahoo能夠以安全、自動化及可擴充的方式與外部合作夥伴交換資料。 |

**新增功能**

| 功能 | 描述 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK是一套設定API，可讓您根據您選擇的資料和驗證格式，設定Experience Platform的目的地整合模式，以傳送對象和設定檔資料至您的端點。 設定儲存在Experience Platform中，並可透過API擷取以取得其他更新。 |
| [目的地的可用性改善](../../destinations/ui/activation-overview.md) | 目的地的可用性改良可讓行銷人員順暢地啟用現有目的地的區段。 |

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 可观察性洞察 {#observability}

「可觀察性深入分析」可讓您透過使用統計量度和事件通知來監控Platform活動。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 警报 | 您現在可以訂閱與Platform上執行的工作流程相關的重要警示。 訂閱特定警報規則後，當發生重要生命週期事件（例如成功的資料擷取）或發生需要您注意的問題（例如擷取流程失敗或區段作業耗時超過預期）時，您將會收到UI內通知和電子郵件。 如需詳細資訊，請參閱 [警報概觀](../../observability/alerts/overview.md). |

請參閱 [可觀察性深入分析概觀](../../observability/home.md) 以取得服務的詳細資訊。

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 設定檔可讓您將客戶資料整合到統一的檢視中，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 描述 |
| ------- | ----------- |
| 依合併原則或身分瀏覽設定檔 | 在Experience Platform中瀏覽設定檔時，您現在可以按合併原則瀏覽，以根據所選的合併原則預覽20個範例設定檔。 您也可以依身分瀏覽，以使用身分名稱空間和相關身分值搜尋特定設定檔。 如需詳細資訊，請參閱 [Real-Time Customer Profile UI指南](../../profile/ui/user-guide.md). |

若要進一步瞭解即時客戶個人檔案，包括使用個人檔案資料的教學課程和最佳實務，請先閱讀 [即時客戶個人檔案總覽](../../profile/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| ------- | ----------- |
| 本機檔案上傳來源聯結器 | 檔案擷取類別已重新命名為本機系統，好讓您可以使用本機檔案上傳聯結器將本機檔案直接引進Platform。 透過此聯結器擷取的資料可透過監控儀表板進行監控。 請參閱 [本機檔案上傳來源概觀](../../sources/connectors/local-system/local-file-upload.md) 以取得詳細資訊。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
