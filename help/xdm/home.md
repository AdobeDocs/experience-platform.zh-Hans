---
keywords: Experience Platform；首頁；熱門主題；XDM；XDM系統；XDM個人設定檔；XDM ExperienceEvent；XDM體驗事件；體驗事件；欄位群組；欄位群組；欄位群組；體驗事件；XDM ExperienceEvent；XDM Experienceevent；XDM Experienceevent；體驗資料模型；體驗資料模型；結構描述登入；結構描述庫；結構描述庫；結構描述；記錄時間序列
solution: Experience Platform
title: XDM系統概覽
description: 標準化和互用性是Adobe Experience Platform背後的重要概念。 體驗資料模型(XDM)以Adobe為導向，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 5%

---

# XDM 系统概述

標準化和互用性是Adobe Experience Platform背後的重要概念。 [!DNL Experience Data Model] (XDM)以Adobe為導向，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的力量。 它提供通用結構和定義，可讓任何應用程式使用來與Platform服務通訊。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作中獲得有價值的深入分析、透過區段定義客戶對象，以及針對個人化目的表達客戶屬性。

XDM是基礎架構，可讓Adobe Experience Cloud (以Experience Platform為動力)在正確的時間透過正確的頻道，將正確的訊息傳遞給正確的人。 建置Experience Platform的方法XDM系統可操作 [!DNL Experience Data Model] 供平台服務使用的結構描述。

本檔案概述XDM系統在Experience Platform中的角色。

## XDM結構描述

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在將資料內嵌至Platform之前，必須組成結構描述來說明資料結構，並對可包含在每個欄位中的資料型別提供限制。 結構描述包含一個基底類別和零個或多個結構描述欄位群組。

如需結構描述組合模型的詳細資訊，包括設計原則和最佳實務，請參閱 [結構描述組合基本概念](schema/composition.md).

### 標準XDM元件

XDM提供標準欄位群組和資料型別的強大集合，旨在擷取不同產業的共同概念和使用案例。 Experience Platform可讓您依產業篩選這些元件，讓您快速自信地建構最能支援您特定業務需求的結構描述。

在Experience PlatformUI中建構結構描述時，列出的欄位群組會顯示人氣量度。 此量度取決於其他Platform使用者在其結構描述中使用該欄位群組的頻率。 數字越高，欄位群組就越受歡迎。 依預設，會顯示從最受歡迎到最不受歡迎的結果，讓您隨時瞭解業界的資料模型化趨勢。

![欄位群組人氣](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform提供使用者介面和RESTful API，您可以從中檢視和管理Experience Platform中所有結構描述相關的資源 **[!DNL Schema Library]**. 此 [!DNL Schema Library] 包含您依Adobe可使用的標準XDM元件，以及來自您使用之應用程式的Experience Platform合作夥伴和廠商的資源。

使用 [!DNL Schema Registry API] 或 [!UICONTROL 結構描述] 工作區，您也可以建立和管理組織專屬的新方案和資源。

如需如何在Platform中管理方案並與之互動的詳細資訊，請參閱下列檔案：

* [XDM UI指南](./ui/overview.md)
* [Schema Registry API指南](./api/overview.md)

## XDM系統中的資料行為 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="数据行为"
>abstract="Experience Platform 中使用的数据分为三种行为类型：记录、时间序列和临时。记录架构提供有关主体属性的信息，时间序列架构在执行操作时捕获系统的快照。临时架构捕获作为仅由单个数据集使用的命名空间的字段。有关 Platform 中的数据行为的更多信息，请参阅文档。"

Experience Platform專用資料分為三種行為型別：

* **記錄**：提供主旨屬性的相關資訊。 主體可以是組織或個人。
* **時間序列**：提供記錄主體直接或間接執行動作時的系統快照。
* **臨機**：擷取已名稱空間的欄位，以供單一資料集使用。 臨機結構用於各種資料擷取工作流程中以進行Experience Platform，包括擷取CSV檔案和建立特定型別的來源連線。

所有XDM結構描述都可歸類為記錄或時間序列的資料。 結構描述的資料行為由結構描述的類別定義，該類別在首次建立時指派給結構描述。 XDM類別說明結構描述必須包含的最小屬性數量，才能代表特定的資料行為。

雖然您能在 [!DNL Schema Registry]，建議您使用標準類別 **[!UICONTROL XDM個別設定檔]** 和 **[!UICONTROL XDM ExperienceEvent]** 分別用於記錄和時間序列資料。 這些類別在下文中會有更詳細的說明。

>[!NOTE]
>
>沒有基於臨機行為的標準類別。 臨時結構會由平台程式自動產生，這些程式會使用這些臨時結構描述，但也可以使用 [使用結構描述登入API手動建立](./tutorials/ad-hoc.md).

### [!UICONTROL XDM 个人资料] {#xdm-individual-profile}

[!UICONTROL XDM個別設定檔] 是以記錄為基礎的類別，可形成已識別和部分識別之主體的屬性的單一表示法。 高度識別的設定檔可用於個人通訊或目標參與，並可包含詳細的個人資訊，例如姓名、性別、出生日期、地點和聯絡資訊（包括電話號碼和電子郵件地址）。

識別較少的設定檔可能僅由匿名行為訊號（如瀏覽器Cookie）組成。 在這種情況下，會使用稀疏設定檔資料來建立資訊庫，匿名設定檔的興趣和偏好設定會整理並儲存於此資訊庫中。 隨著主體註冊接收通知、訂閱、購買等，這些識別碼可能會隨著時間而變得更加詳細。 設定檔屬性的這種增加最終可能會導致識別的主題，並允許更高程度的目標參與。

隨著個人檔案持續成長，它會成為個人個人資訊、身分資訊、聯絡詳細資料和通訊偏好設定的強大存放庫。

請參閱 [[!UICONTROL XDM個別設定檔] 參考指南](./classes/individual-profile.md) 有關類別所提供欄位的結構和使用案例的詳細資訊。

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一種以時間序列為基礎的類別，用來擷取發生事件（或一組事件）時的系統狀態，包括相關主體的時間點和身分。 體驗事件是指在該時間點所發生之事情的不可變、真實記錄，代表未彙總或詮釋時所發生之事。 它們對於時間網域分析至關重要，因為它們可用於分析指定時段內發生的變化，並比較多個時段之間的差異以追蹤趨勢。

體驗事件可以是明確或隱含的。 明確事件是指在歷程中某個時間點發生的直接可觀察的人類行為。 隱含事件是在沒有直接人類動作的情況下引發，但仍與個人相關的事件。 隱含事件的範例包括排程傳送電子郵件電子報或電池電壓達到特定臨界值。

雖然並非所有事件都可輕鬆跨所有資料來源分類，但儘可能將類似事件協調為類似型別以進行處理，這極為重要。

![ExperienceEvent客戶歷程](images/overview/experience-event-journey.png)

請參閱 [[!UICONTROL XDM ExperienceEvent] 參考指南](./classes/experienceevent.md) 有關類別所提供欄位的結構和使用案例的詳細資訊。

## XDM結構描述和Experience Platform服務

Experience Platform與結構描述無關，這表示符合XDM標準的任何結構描述都可供Platform服務使用。 下文將更詳細地說明不同Platform服務使用結構描述的方式。

### 目錄服務、資料擷取和Data Lake

目錄服務是Experience Platform資產及其相關結構描述的記錄系統。 目錄並不包含實際的資料檔案或目錄，而是包含這些檔案和目錄的中繼資料和說明。

目錄資料會儲存在Data Lake中，這是高度精細的資料存放區，包含Platform管理的所有資料，無論來源或檔案格式為何。

若要開始將資料擷取至Experience Platform，您可以使用目錄服務建立資料集。 資料集參考的XDM結構描述描述了要擷取的資料結構。 如果在沒有結構描述的情況下建立資料集，Experience Platform會透過檢查所擷取資料欄位的型別和內容來衍生「觀察到的結構描述」。 然後，資料集會在目錄中受到追蹤，並與資料集所根據的結構描述和觀察到的結構描述一起儲存在資料湖中。

如需有關目錄的詳細資訊，請參閱 [目錄服務概觀](../catalog/home.md). 如需Adobe Experience Platform資料擷取的詳細資訊，請參閱 [資料擷取概觀](../ingestion/home.md).

### 查询服务

Adobe Experience Platform查詢服務可讓您使用標準SQL來查詢Experience Platform資料，以支援許多不同的使用案例。

在撰寫結構描述並建立參考該結構描述的資料集後，系統就會擷取資料並儲存在Data Lake中。 使用查詢服務，您可以聯結Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或擷取到即時客戶設定檔中。

請參閱 [查詢服務總覽](../query-service/home.md) 以取得服務的詳細資訊。

### 实时客户资料

Real-Time Customer Profile提供集中式消費者設定檔，用於針對性和個人化的體驗管理。 每個設定檔都包含彙總所有系統的資料，以及在您用於Experience Platform的任何系統中發生的涉及個人之事件的可操作時間戳記帳戶。

即時客戶設定檔會根據以下專案使用結構描述格式化的資料： [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 類別，並根據該資料回應查詢。 設定檔不支援根據其他類別使用結構描述。

系統會維護每個客戶設定檔的執行個體，將資料合併在一起，形成個人的「單一信任來源」。 此統一資料使用所謂的「聯合結構描述」（有時稱為「聯合檢視」）表示。 聯合結構描述會將實施相同類別的所有結構描述的欄位彙總到單一結構描述中。  使用UI或API構成結構描述時，您可以啟用結構描述以與即時客戶個人檔案搭配使用，並標籤它以包含在聯合中。 然後，標籤的結構描述將參與饋送至設定檔的結構描述定義。

作為 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 資料會擷取至Data Lake，即時客戶設定檔會擷取任何已啟用以供使用的資料。 內嵌的互動和詳細資訊越多，個別設定檔就越健全。

[!UICONTROL XDM個別設定檔] 資料可協助您針對任何管道或Adobe產品整合提供資訊並強化動作。 搭配豐富的行為和互動資料歷程記錄時，此資料可用於推動機器學習。 Real-Time Customer Profile API也可用來擴充協力廠商解決方案、CRM和專有解決方案的功能。

請參閱 [即時客戶個人檔案總覽](../profile/home.md) 以取得詳細資訊。

### 数据科学工作区

Adobe Experience Platform Data Science Workspace使用機器學習和人工智慧，從Experience Platform中儲存的資料獲得深入見解。 Data Science Workspace可讓資料科學家根據以下專案建立配方 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 有關客戶及其活動的資料，有助於進行預測，例如購買傾向和個人可能欣賞和使用的建議選件。

藉由Data Science Workspace，資料科學家可以輕鬆建立由機器學習提供支援的智慧型服務API。 這些服務可搭配其他Adobe解決方案(包括Adobe Target和Adobe Analytics Cloud)運作，協助您自動個人化、目標定位的數位體驗。

如需使用Experience Platform資料強化深入分析的詳細資訊，請參閱 [資料科學工作區概觀](../data-science-workspace/home.md).

## 後續步驟和其他資源

現在您已透過Experience Platform更瞭解結構描述的作用，您已準備好開始撰寫自己的結構描述。

若要瞭解構成要與Experience Platform搭配使用的結構描述的設計原則和最佳實務，請從閱讀 [結構描述組合基本概念](schema/composition.md). 如需如何建立方案的逐步指示，請參閱建立方案教學課程 [使用API](tutorials/create-schema-api.md) 或 [使用使用者介面](tutorials/create-schema-ui.md).

加強您對「 」的瞭解 [!DNL XDM System] 在Experience Platform中，觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
