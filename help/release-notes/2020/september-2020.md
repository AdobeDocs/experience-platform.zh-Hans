---
title: Adobe Experience Platform發行說明2020年9月
description: Adobe Experience Platform 2020年9月發行說明。
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 9 月 9 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据治理](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 数据治理 {#governance}

Adobe Experience Platform資料控管是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略與技術。 它在以下方面發揮著關鍵作用 [!DNL Experience Platform] 包括目錄、資料譜系、資料使用標籤、資料存取原則，以及行銷動作資料的存取控制。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 資料集標籤UI增強功能 | 已將數個新的排序和篩選控制項新增至資料集標籤UI，以便更輕鬆地使用大型結構描述： <ul><li>根據完整結構描述路徑，依字母順序排序欄位。</li><li>對欄位路徑名稱執行部分搜尋。</li><li>篩選沒有標籤、選定標籤或標籤類別的欄位。</li></ul> |

請參閱 [資料控管概觀](../../data-governance/home.md) 以取得服務的詳細資訊。

## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| UX改良 | 使用者可以存取內嵌表格動作，以便更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 請參閱 [目的地工作區](../../destinations/ui/destinations-workspace.md) 檔案以取得詳細資訊。 |

若要進一步瞭解，請造訪 [目的地概觀](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 可讓您透過使用統計量度和事件通知來監視Adobe Experience Platform上的活動。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights] 運用Adobe I/O事件為多個Experience Platform服務建立事件通知。 通知裝載會傳送至已設定的webhook，您隨後可以使用它來自動化後續的流程。 |

請參閱 [[!DNL Observability Insights] 概觀](../../observability/home.md) 以取得服務的詳細資訊。

## [!DNL Privacy Service] {#privacy}

幾項法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。 Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 替換為 [!DNL Privacy Service]，您可以提交存取和刪除Adobe Experience Cloud應用程式中私人或個人客戶資料的請求，協助實現法律和組織隱私法規的自動合規性。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支援LGPD （巴西） | 隱私權工作現在可以在巴西的 [!DNL Lei Geral de Proteção de Dados] (LGPD)法規。 這些工作會根據法規代碼進行追蹤 `lgpd_bra`. |

請參閱 [Privacy Service概觀](../../privacy-service/home.md) 以取得服務的詳細資訊。

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 替換為 [!DNL Real-Time Customer Profile]，您可以看到結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 [!DNL Profile] 可讓您將不同的客戶資料合併成統一的檢視，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 描述 |
| ------- | ----------- |
| 設定檔檢視器 | Platform UI中的設定檔檢視器已更新，成為具有完整自訂功能的儀表板。 使用者現在可以選擇執行下列工作： <ul><li>更新基本資訊Widget中選取的標準與自訂屬性。</li><li>建立、編輯和移除自訂Widget</li><li>調整大小並重新排列Widget</li></ul> |

如需詳細資訊，請參閱 [!DNL Real-Time Customer Profile]，包括使用的教學課程和最佳實務 [!DNL Profile] 資料，請閱讀 [即時客戶個人檔案總覽](../../profile/home.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段並從 [!DNL Real-Time Customer Profile] 資料。 這些區段會集中設定並維護於 [!DNL Platform]，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 匯出工作 | 已新增旗標，以允許將區段評估為匯出作業的一部分。 因此，使用者可以在單一工作中執行細分和匯出。 |
| 合併原則 | 單一批次分段工作中可包含多個合併原則。 |

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 自動對應 | [!DNL Platform] 根據使用者選取的目標結構描述或資料集，在資料擷取工作流程期間提供自動對應的智慧型建議。 您可以手動調整彈性的自動對應規則，以符合您的使用案例。 |
| UX改良 | 使用者可以存取內嵌表格動作，以便更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 請參閱 [監控資料流](../../sources/tutorials/ui/monitor.md) 檔案以取得詳細資訊。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
