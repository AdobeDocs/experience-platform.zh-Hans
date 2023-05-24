---
title: Adobe Experience Platform發行說明2022年1月
description: Adobe Experience Platform的2022年1月發行說明。
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 3%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 1 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [分段服务](#segmentation)
- [源](#sources)

## 警报 {#alerts}

Experience Platform可讓您訂閱各種Platform活動的事件型警報。 您可以透過以下方式訂閱不同的警報規則： [!UICONTROL 警報] 索引標籤中，並可選擇在UI本身或透過電子郵件通知接收警示訊息。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新警報規則 | 與資料擷取、身分、設定檔、細分和啟用相關的工作流程，現在提供幾個新的警報規則。 請參閱以下文章的概觀： [警示規則](../../observability/alerts/rules.md) 以取得更新的警示型別清單。 |
| 來源資料流的內容感知警報 | 您現在可以訂閱在擷取工作流程期間接收有關資料流狀態的警報訊息。 如需詳細資訊，請參閱以下指南： [在UI中訂閱來源警示](../../sources/tutorials/ui/alerts.md). |

如需Platform警示的詳細資訊，請參閱 [警報概觀](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個儀表板，您可以透過這些儀表板檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

| 功能 | 描述 |
| --- | --- |
| 智能字幕 | 機器學習演演算法會自動提供您設定檔和受眾資料的深入分析，並說明30-90天或12個月期間的模式和趨勢。 註解包含的相關資訊 <ul><li>整體形狀和統計資料</li><li>趨勢和突然變化</li><li>季節性模式</li><li>未預期的異常</li></ul> 如需詳細資訊，請參閱 [設定檔控制面板](../../dashboards/guides/profiles.md#profiles-count-trend) 和 [區段控制面板](../../dashboards/guides/segments.md#audience-size-trend) 說明檔案。 |
| 控制面板詳細目錄 | 在集中位置存取預先設定的設定檔、區段和目的地儀表板報表，包括任何已安裝的整合，例如PowerBI。 如需詳細資訊，請參閱 [[!DNL Dashboards] 詳細目錄檔案](../../dashboards/inventory.md). |
| PowerBI報表範本 | 使用新的PowerBI圖表，從設定檔、區段和目的地報表資料模型建立、自訂或擴充量度。 自動化安裝工作流程可讓您在PowerBI環境中，跨組織分享行銷分析。 如需詳細資訊，請參閱 [PowerBI報表範本檔案](../../dashboards/integrations/power-bi.md). |

如需詳細資訊，請參閱 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概觀](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 整合的對應體驗 | Platform UI中新的對應介面為您提供一致的對應體驗，以利用智慧型對應建議、手動設定對應規則，以及對對應集發生的任何錯誤進行偵錯。 如需詳細資訊，請參閱 [[!DNL Data Prep] UI指南](../../data-prep/ui/mapping.md). |

如需詳細資訊，請參閱 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 相同頁面和下一頁個人化 | 此 [相同頁面和下一頁個人化功能](../../destinations/ui/configure-personalization-destinations.md) 為Experience Edge上的應用程式提供共用、可定位的使用者檢視，以確保行銷和客戶管道之間的一致性。 此個人化可透過 [Adobe Target連線](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md). 若要設定相同頁面或下一頁個人化行銷活動，請參閱 [專屬教學課程](../../destinations/ui/configure-personalization-destinations.md). |
| 批次目的地監控和區段層級量度 | 目的地監控功能現已從串流目的地擴充至同時包含批次目的地和啟用資料流程的區段層級量度。 如需詳細資訊，請閱讀 [監視目的地儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)， [監控區段作業儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard)、和 [區段層級檢視](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| 排程在UI中編輯現有批次啟用資料流 | 此版本引進了將現有啟動資料流排程編輯到批次目的地的選項。 如需詳細資訊，請閱讀 [將設定檔資料啟用至批次設定檔目的地](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo目的地增強功能 | 使用Marketo Engage的Experience Platform客戶可以透過將全新個人記錄從Experience Platform推送到Marketo Engage的新功能，將其Marketo資料庫發揮到極致。 [Marketo目的地聯結器](/help/destinations/catalog/adobe/marketo-engage.md). <br> 將受眾區段從Experience Platform傳送至Marketo Engage時，區段內尚未存在於Marketo Engage資料庫中的人員可以自動新增至該區段。 如需詳細資訊，請閱讀 [將Adobe Experience Platform區段推送至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (教學課程中的步驟9會說明如何將新進人員記錄推送至Marketo)。 |

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [Adobe Target連線](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target應用程式可在跨網站、行動應用程式等的所有傳入客戶互動中提供即時的AI支援個人化和實驗。 Adobe Target是Adobe Experience Platform中的個人化連線。 |
| [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md) | 此個人化連線提供一種方法，可讓您從Adobe Experience Platform將區段資訊擷取到外部個人化平台、內容管理系統、廣告伺服器，以及在客戶網站上執行的其他應用程式。 |

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 查询服务 {#query-service}

[!DNL Query Service] 可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從以下位置聯結任何資料集： [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或內嵌至即時客戶個人檔案。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 匿名區塊 | 匿名區塊SQL建構可讓您將查詢服務中的大型資料準備工作分解為較小的工作，然後重複使用並依序執行它們，以載入增量資料。 如需詳細資訊，請參閱 [匿名區塊檔案的範例查詢](../../query-service/essential-concepts/anonymous-block.md). |
| 資料集組織 | 提供一致的邏輯資料結構，可隨著沙箱內的資料資產數量成長，組織您的資料資產以與查詢服務搭配使用。 如需詳細資訊，請參閱 [組織資料資產檔案](../../query-service/best-practices/organize-data-assets.md). |

如需詳細資訊，請參閱 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概觀](../../query-service/home.md).

## 沙盒 {#sandboxes}

Adobe Experience Platform的設計目的，是為了在全球範圍內豐富數位體驗應用程式。 公司通常會同時執行多個數位體驗應用程式，並且需要滿足這些應用程式的開發、測試和部署，同時確保營運合規性。 為了滿足此需求，Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的沙箱，以協助開發及改進數位體驗應用程式。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 沙箱UI增強功能 | 沙箱指標現在已整合到所有Platform UI應用程式的標頭中。 沙箱指示器會顯示沙箱名稱、區域和型別，也可讓您存取下拉式選單以在沙箱之間切換。 如需詳細資訊，請參閱 [沙箱UI指南](../../sandboxes/ui/user-guide.md). |

如需沙箱的詳細資訊，請參閱 [沙箱總覽](../../sandboxes/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 區段比對 | 區段比對是一項資料共同作業服務，可讓兩名或以上Platform使用者根據通用識別碼，以安全、受管且隱私權友好的方式交換資料。 區段比對會使用Platform隱私權標準和個人識別碼，例如雜湊電子郵件、雜湊電話號碼，以及裝置識別碼，例如IDFA和GAID。 如需詳細資訊，請參閱 [區段比對概觀](../../segmentation/ui/segment-match/overview.md). |

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| --- | --- |
| Beta版來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] 來源增強功能 | 此 [!DNL Event Hubs] source現在支援非根SAS金鑰型別的驗證，以連線並建立來源連線。 如需詳細資訊，請參閱 [[!DNL Event Hubs] 概觀](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] 來源增強功能 | 此 [!DNL SFTP] source現在可讓您建立資料流可用於連線至SFTP伺服器的最大並行連線數量。 如需詳細資訊，請參閱 [[!DNL SFTP] 概觀](../../sources/connectors/cloud-storage/sftp.md). |
