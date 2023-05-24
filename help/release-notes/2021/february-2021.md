---
title: Adobe Experience Platform發行說明2021年2月
description: Adobe Experience Platform 2021年2月版本注意事項。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 2 月 24 日**

Adobe Experience Platform中的新功能：

- [(Beta)控制面板](#dashboards)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta)控制面板 {#dashboards}

Adobe Experience Platform提供多個控制面板，您可檢視有關組織資料的重要資訊，這些資訊是在每日快照期間擷取的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 設定檔、區段、目的地和授權使用儀表板（測試版） | **注意：控制面板功能目前為測試版，並非所有使用者都可使用。 文档和功能可能会发生变化。**<br/><br/>&#x200B;控制面板提供組織資料的現成報告，並直接內建於Platform內的行銷人員工作流程中。 這些儀表板不需要額外的IT支援，也不需要透過其他資料倉儲設計與實作匯出及處理資料所需的時間和精力。 |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧，從您的資料建立深入分析。 Data Science Workspace已整合至Adobe Experience Platform，可協助您跨多個Adobe解決方案使用您的內容和資料資產進行預測。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| JupyterLab EDA筆記本 | 探索性資料分析(EDA) Python筆記型電腦現在可在Jupyterlab中使用。 此筆記型電腦的設計目的，是協助您探索資料模式、檢查資料健全度，以及彙總預測性模型的相關資料。 請參閱教學課程，位置如下： [探索預測性模型的網頁型資料](../../data-science-workspace/jupyterlab/eda-notebook.md) 以取得詳細資訊。 |

如需資料科學工作區的詳細一般資訊，請參閱 [資料科學工作區概觀](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform中，資料會從各種來源擷取、在Experience Platform中分析，並啟用至各種目的地。 Platform藉由提供資料流透明度，讓追蹤這種潛在非線性資料流的程式變得更輕鬆。

数据流是跨平台移动数据的数据作业的表示方法。這些資料流是跨不同服務設定的，有助於將資料從來源聯結器移至目標資料集，然後由使用 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最終啟用之前 [!DNL Destinations].

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 新的監視儀表板 | 您現在可以使用監視儀表板來確保跨服務透明度，並針對來源資料擷取提供可操作的深入分析。 新的監控儀表板提供處理自的資料的完整檢視 [!DNL Data Lake] 至 [!DNL Identity Service] 和 [!DNL Profile]，也可讓您監視擷取率、成功和失敗。 請參閱教學課程，位置如下： [在UI中監控來源資料流](../../dataflows/ui/monitor-sources.md) 以取得詳細資訊。 |

如需資料流的詳細一般資訊，請參閱 [資料流概觀](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 此 [!DNL LinkedIn Matched Audiences] 連線可讓您在中啟用對象 [!DNL LinkedIn] 社交平台。 |

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

標準化和互用性是背後的重要概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)以Adobe為導向，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的力量。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 已升級搜尋UI | 改善的搜尋功能現在可在 [!UICONTROL 瀏覽] 索引標籤中的 [!UICONTROL 結構描述] 工作區與結構描述欄位群組選擇對話方塊 [!DNL Schema Editor].<br><br>先前搜尋辭彙時，結果將僅包含名稱符合搜尋查詢的XDM資源。 現在，除了名稱符合查詢的資源外，也會包含符合字詞的個別屬性資源。 這可讓您根據XDM資源包含的屬性而不是資源名稱來搜尋這些資源。<br><br>檢視檔案： [探索XDM資源](../../xdm/ui/explore.md) 和 [管理結構描述](../../xdm/ui/resources/schemas.md) （在UI中）以取得詳細資訊。 |

如需XDM的一般資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使情況更困難，導致每個個別客戶似乎有多個「身分」。

Adobe Experience Platform [!DNL Identity Service] 透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更好地瞭解客戶及其行為。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 身分圖表檢視器 | 身分圖表檢視器可讓您驗證和視覺化UI中拼接在一起的身分，進而改善偵錯和透明度。 請參閱 [身分圖表檢視器檔案](../../identity-service/ui/identity-graph-viewer.md) 以取得詳細資訊。 |

如需更多一般資訊，請參閱 [!DNL Identity Service]，請參閱 [Identity Service概觀](../../identity-service/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 [!DNL Profile] 可讓您將客戶資料合併成統一的檢視，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 計算屬性(Alpha) | ***注意：此功能目前為Alpha版，並非所有使用者都可使用。 文档和功能可能会发生变化。*** <br/><br/>計算屬性是用來將事件層級資料彙總到設定檔層級屬性的函式。 然後，您就可以在分段、啟動和個人化中使用彙總。 這些函式的一些範例包括count、sum、average、min、max、true/false。 計算屬性目前只能透過API使用。 |

如需即時客戶個人檔案的詳細資訊，包括使用的教學課程和最佳實務 [!DNL Profile] 資料，請先閱讀 [即時客戶個人檔案總覽](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新來源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Google PubSub] | 您現在可以連線 [!DNL Google PubSub] 至 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 請參閱 [[!DNL Google PubSub] 聯結器概述](../../sources/connectors/cloud-storage/google-pubsub.md) 以取得詳細資訊。 |
| [!DNL Oracle Object Storage] | 您現在可以連線 [!DNL Oracle Object Storage] 至 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 請參閱 [[!DNL Oracle Object Storage] 聯結器概述](../../sources/connectors/cloud-storage/oracle-object-storage.md) 以取得詳細資訊。 |

如需來源的一般詳細資訊，請參閱 [來源概觀](../../sources/home.md).
