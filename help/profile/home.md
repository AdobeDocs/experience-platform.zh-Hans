---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp；XDM圖形
title: 即時客戶個人檔案概述
description: Real-Time Customer Profile可合併來自各種來源的資料，並以個別客戶設定檔和相關時間序列事件的形式提供對該資料的存取權。 此功能可讓行銷人員跨多個管道與其受眾推動協調、一致且相關的體驗。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 概述

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 替換為 [!DNL Real-Time Customer Profile]，您可以透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 [!DNL Profile] 可讓您將客戶資料合併成統一的檢視，針對每個客戶互動提供可採取行動且附有時間戳記的說明。 此概覽可協助您瞭解的角色和使用 [!DNL Real-Time Customer Profile] 在 [!DNL Experience Platform].

## [!DNL Profile] 在Experience Platform中

下圖會強調即時客戶設定檔與Experience Platform內其他服務之間的關係：

![即時客戶設定檔與Adobe Experience Platform中其他服務之間的關係。 此圖表顯示設定檔是Adobe Experience Platform的核心元件之一。](images/profile-overview/profile-in-platform.png)

## 瞭解設定檔

[!DNL Real-Time Customer Profile] 合併來自各種企業系統的資料，然後以客戶個人檔案與相關時間序列事件的形式提供對該資料的存取權。 此功能可讓行銷人員跨多個管道與其受眾推動協調、一致且相關的體驗。 以下章節著重說明您必須瞭解的一些核心概念，才能在Platform內有效建置和維護設定檔。

### 設定檔實體組合

即時客戶個人檔案由一個主要實體組成，稱為 **主要實體**&#x200B;和各種支援實體。 在Experience Platform內容中，主要實體通常是 **設定檔實體**，由個人特徵、行為和區段會籍組成。 其他實體可讓細分引擎利用設定檔主要實體以外的資料，並包括下列專案：

- **維度實體**：用於簡化跨事件或設定檔記錄共用資訊的資料模型化程式的實體。 這也稱為查詢實體或分類實體。
- **B2B實體**：說明設定檔與企業對企業帳戶和商機關係的實體。

![說明設定檔實體組成的圖表。](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>由於維度和B2B實體僅存在於主要實體之外，因此它們僅用於批次分段。

維度和B2B實體透過連結至主要實體 **結構描述關係**. 如需詳細資訊，請參閱下列檔案：

- [為查閱實體建立一對一的結構描述關係](../xdm/tutorials/relationship-ui.md)
- [為B2B實體建立多對一結構描述關係](../xdm/tutorials/relationship-b2b.md)

### 設定檔資料存放區

雖然 [!DNL Real-Time Customer Profile] 處理擷取的資料並使用Adobe Experience Platform [!DNL Identity Service] 若要透過身分對應來合併相關資料，它會將自己的資料維護在 [!DNL Profile] 資料存放區。 此 [!DNL Profile] 存放區與Data Lake中的目錄資料分開，且 [!DNL Identity Service] 身分圖表中的資料。

設定檔存放區使用Microsoft Azure Cosmos DB基礎結構，而Platform Data Lake使用Microsoft Azure Data Lake儲存空間。

### 輪廓護欄

Experience Platform提供了一系列護欄，幫助您避免建立 [體驗資料模型(XDM)結構描述](../xdm/home.md) 哪些Real-Time Customer Profile不支援。 這包括會導致效能降低的軟性限制，以及會導致錯誤和系統中斷的硬性限制。 如需詳細資訊，包括指引清單和使用案例範例，請閱讀 [輪廓護欄](guardrails.md) 說明檔案。

### 設定檔儀表板 {#profile-dashboard}

Experience PlatformUI提供一個儀表板，您可以透過它檢視關於即時客戶個人檔案資料的重要資訊，如每日快照期間所擷取。 若要瞭解如何存取和使用 [!DNL Profile] UI中的控制面板，以及有關控制面板中顯示的量度的詳細資訊，請參閱 [設定檔控制面板UI指南](ui/profile-dashboard.md).

### 設定檔片段與合併的設定檔 {#profile-fragments-vs-merged-profiles}

每個個別客戶設定檔都由多個設定檔片段組成，這些片段已合併以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織將有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 將這些片段內嵌至Platform時，會合併在一起，以便為該客戶建立單一設定檔。

換言之，設定檔片段代表唯一的主要身分和對應的 [記錄](#record-data) 或 [事件](#time-series-events) 指定資料集中該ID的資料。

當來自多個資料集的資料衝突時（例如，一個片段將客戶列為「單身」，而另一個片段將客戶列為「已婚」）， [合併原則](#merge-policies) 決定個人設定檔中要優先處理並包括哪些資訊。 因此，Platform內的設定檔片段總數可能一律高於合併的設定檔總數，因為每個設定檔通常是由多個資料集中的多個片段組成。

### 記錄資料 {#record-data}

設定檔是主體、組織或個人的表示法，由許多屬性（也稱為記錄資料）組成。 例如，產品的設定檔可能包含SKU和說明，而人員的設定檔包含名字、姓氏和電子郵件地址等資訊。 使用 [!DNL Experience Platform]，您可以自訂設定檔，以使用與業務相關的特定資料。 標準 [!DNL Experience Data Model] (XDM)類別， [!DNL XDM Individual Profile]，是描述客戶記錄資料時用來建立結構的偏好類別，並會提供Platform服務之間許多互動不可或缺的資料。 如需在中使用結構描述的詳細資訊 [!DNL Experience Platform]，請先閱讀 [XDM系統總覽](../xdm/home.md).

### 時間序列事件 {#time-series-events}

時間序列資料提供主體直接或間接執行動作時的系統快照，以及詳細說明事件本身的資料。 以標準結構描述類別XDM ExperienceEvent表示，時間序列資料可說明事件，例如要新增至購物車的專案、被點按的連結和檢視的視訊。 時間序列資料可用於建立分段規則的基礎，而事件可在設定檔的情境中個別存取。

### 标识

每個企業都希望以個人化的方式與客戶溝通。 然而，為客戶提供相關數位體驗的挑戰之一，就是瞭解如何將分散在平板電腦、行動電話和筆記型電腦等不同數位頻道中的中斷連線資料連結在一起。 [!DNL Identity Service] 可讓您連結來自多個頻道的身分，並為每個客戶建立身分圖表，藉此拼合客戶的完整面貌。 造訪 [Identity Service概觀](../identity-service/home.md) 以取得詳細資訊。

### 合併原則

將多個來源的資料片段彙整在一起並加以合併，以便檢視每個個別客戶的完整檢視時，合併原則是指 [!DNL Platform] 使用來決定資料的優先順序以及將使用哪些資料來建立客戶設定檔。

當多個資料集中的資料發生衝突時，合併原則會決定該資料應如何處理，以及應使用哪個值。 透過RESTful API或使用者介面，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。

若要進一步瞭解合併原則及其在Experience Platform中的角色，請先閱讀 [合併原則概觀](merge-policies/overview.md).

### 聯合結構描述 {#profile-fragments-and-union-schemas}

的主要功能之一 [!DNL Real-Time Customer Profile] 是統一多管道資料的能力。 時間 [!DNL Real-Time Customer Profile] 用於存取實體，可為您提供該實體跨資料集的所有設定檔片段的合併檢視，稱為「聯合檢視」，並可透過稱為聯合結構描述的方式實現。

若要進一步瞭解聯合結構描述，包括如何在UI中存取聯合結構描述，請造訪 [聯合結構描述UI指南](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## 設定檔和區段

Adobe Experience Platform [!DNL Segmentation Service] 會產生支援個別客戶體驗所需的對象。 建立受眾區段時，該區段的ID會新增至所有合格設定檔的區段會籍清單中。 區段規則建立並套用至 [!DNL Real-Time Customer Profile] 使用RESTful API和區段產生器使用者介面的資料。 若要深入瞭解細分，請先閱讀 [Segmentation Service概述](../segmentation/home.md).

### 串流擷取和串流細分

即時輸入可透過稱為串流擷取的程式實現。 擷取設定檔和時間序列資料時， [!DNL Real-Time Customer Profile] 在將區段與現有資料合併並更新聯合檢視之前，會透過稱為串流區段的持續程式自動決定從區段包含或排除該資料。 因此，您可以即時執行計算並作出決定，在客戶與您的品牌互動時，向客戶傳遞增強、個人化的體驗。 擷取資料時，也會進行驗證，以確保資料可正確擷取，並符合資料集所依據的結構描述。 如需有關內嵌期間所完成驗證的詳細資訊，請先閱讀 [資料擷取品質概觀](../ingestion/quality/overview.md).

## 邊緣投影

為了即時跨多個管道為您的客戶推動協調、一致和個人化的體驗，需要隨時提供正確的資料，並隨著變更持續更新。 Adobe Experience Platform透過使用所謂的edge功能，實現資料的即時存取。 Edge是地理位置上放置的伺服器，可儲存資料並讓應用程式輕鬆存取資料。 例如，Adobe Target和Adobe Campaign等Adobe應用程式會使用Edge來即時提供個人化客戶體驗。 資料會透過投影路由至邊緣，投影目的地定義資料將傳送至的邊緣，投影組態定義可在邊緣上使用的特定資訊。 若要瞭解更多並開始使用投影，請使用 [!DNL Real-Time Customer Profile] API，請參閱 [邊緣投影端點導引線](api/edge-projections.md).

## 擷取資料至 [!DNL Profile]

[!DNL Platform] 可將記錄與時間序列資料設定為傳送至 [!DNL Profile]，支援即時串流擷取和批次擷取。 如需詳細資訊，請參閱教學課程，概述如何 [新增資料至即時客戶個人檔案](tutorials/add-profile-data.md).

>[!NOTE]
>
>透過Adobe解決方案收集的資料，包括 [!DNL Analytics Cloud]， [!DNL Marketing Cloud]、和 [!DNL Advertising Cloud]，流入 [!DNL Experience Platform] 和已內嵌至 [!DNL Profile].

### 設定檔擷取量度

可觀察性深入分析可讓您在Adobe Experience Platform中公開關鍵量度。 除了 [!DNL Experience Platform] 各種使用情況統計資料和績效指標 [!DNL Platform] 功能方面，我們提供特定的個人資料相關量度，讓您深入瞭解傳入的請求率、成功的擷取率、擷取的記錄大小等。 若要進一步瞭解，請先閱讀 [Observability Insights API概述](../observability/api/overview.md)和如需即時客戶個人檔案量度的完整清單，請參閱以下檔案： [可用量度](../observability/api/metrics.md#available-metrics).

## 更新設定檔存放區資料

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 這可以透過批次擷取完成，並需要設定檔啟用的資料集，以更新插入標籤。 如需如何設定屬性更新資料集的詳細資訊，請參閱的教學課程 [為設定檔和更新插入啟用資料集](../catalog/datasets/enable-upsert.md).

## 資料控管和 [!DNL Privacy]

資料控管是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略與技術。

由於資料控管與存取資料有關，因此在 [!DNL Experience Platform] 在不同層級：

- 資料使用標籤
- 資料存取原則
- 行銷動作資料的存取控制

資料控管需在數個時間點進行管理。 其中包括決定要擷取哪些資料 [!DNL Platform] 以及擷取後指定的行銷動作可存取哪些資料。 如需詳細資訊，請先閱讀 [資料控管概觀](../data-governance/home.md).

### 處理選擇退出和資料隱私權請求

[!DNL Experience Platform] 可讓您的客戶傳送與其資料的使用和儲存相關的選擇退出請求。 [!DNL Real-Time Customer Profile]. 如需如何處理選擇退出請求的詳細資訊，請參閱以下說明檔案： [接受選擇退出請求](../segmentation/consents.md).

## 後續步驟和其他資源

若要進一步瞭解如何使用Experience PlatformUI或設定檔API處理即時客戶設定檔資料，請從閱讀 [設定檔UI指南](ui/user-guide.md) 或 [API開發人員指南](api/overview.md)（分別）。
