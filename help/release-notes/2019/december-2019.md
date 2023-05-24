---
title: Adobe Experience Platform發行說明2019年12月
description: Adobe Experience Platform的2019年12月發行說明。
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**發行日期： 2019年12月11日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段並從 [!DNL Real-Time Customer Profile] 資料。 這些區段會集中設定並維護於 [!DNL Platform]，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 「合併的對象」索引標籤位於 [!DNL Segment Builder] | 此 [!UICONTROL 區段] 和 [!UICONTROL 受眾] 索引標籤 [!DNL Segment Builder] 已合併到單一 [!UICONTROL 受眾] 標籤。 此索引標籤可讓您瀏覽及搜尋現有對象，然後將其拖放至規則產生器畫布中以建立新的區段定義。 參照對象可將下列規則邏輯集合之一新增至新的區段定義：對象成員資格如規則，定義參照對象的完整規則邏輯集合。 |
| 合併原則選擇器的新位置 | 中合併原則選擇器的位置 [!DNL Segment Builder] 已變更。 若要選取區段定義的合併原則，請選取 **[!UICONTROL 欄位]** 標籤，然後使用 **[!UICONTROL 合併原則]** 下拉式選單，以選取您要使用的合併原則。 |

**已知问题**

* None

如需詳細資訊，請參閱 [Segmentation Service概述](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 提供以程式設計方式、聰明地從特定個人的一組可用選項中選取「下一個最佳體驗」的功能，將其傳送至任何管道或應用程式，以及執行報告和分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 排名函式 | 設定檔的優惠方案順序現在透過排名函式衍生，而不是所有設定檔的固定優惠方案集。 |

**已知问题**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe解決方案、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證儲存系統和CRM服務、設定擷取執行時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 串流連線 | 串流擷取可讓您從使用者端和伺服器端裝置傳送資料至 [!DNL Experience Platform] 即時。 此版本包含新的串流連線使用者介面。 |
| 的聯結器支援 [!DNL Google Cloud Store] | 支援從收集資料 [!DNL Google Cloud Store]. |

**已知问题**

* None.

如需來源的詳細資訊，請參閱 [來源概觀](../../sources/home.md).

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互用性是背後的重要概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)以Adobe為導向，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的力量。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 改善的結構描述驗證 | 新檢查可確保參考按預期解析為其他欄位。 新增其他檢查至定義為物件陣列的欄位，以確保物件已完全定義。 改善錯誤訊息，以協助識別及修正問題。 |

**错误修复**

* 與存取控制和沙箱相關的維護和改善。
* 支援 `eTag` 的 `/descriptors` 中的端點 [!DNL Schema Registry] API。

**已知问题**

* None

若要進一步瞭解如何使用XDM [!DNL Schema Registry] API和 [!DNL Schema Editor] 使用者介面，請閱讀 [XDM系統檔案](../../xdm/home.md).
