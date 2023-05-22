---
title: 資料管理授權權益最佳實務
description: 了解可用来借助 Adobe Experience Platform 更好地管理您的许可证权利的最佳实践和工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 225fee7e2addf5067cb13da11615f6acff62ed72
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 2%

---

# 資料管理授權權益最佳實務

Adobe Experience Platform是一個開放系統，可將您的資料轉換為健全的客戶設定檔，並即時更新，使用AI導向的深入分析來協助您跨每個管道提供正確的體驗。 您可以擷取不同型別、磁碟區和歷史資料以使用來源Experience Platform，然後迎合從細分和個人化到分析和機器學習等使用案例的資料。

Platform提供的授權可建立您可建立的設定檔數目以及可匯入的資料量。 因為有引入任何資料來源、數量或歷史記錄的容量，所以隨著資料量的增加，可能會超過您的授權權利。

本文档概述了借助 Adobe Experience Platform 更好地管理您的许可证权利需要遵循的最佳实践和可以使用的工具。

## 瞭解Adobe Experience Platform資料儲存

Experience Platform主要由兩個資料存放庫組成： [!DNL data lake] 和設定檔存放區。

此 **[!DNL data lake]** 主要用途如下：

* 充當將資料上線到Experience Platform中的中繼區域；
* 充當所有Experience Platform資料的長期資料儲存體；
* 啟用資料分析和資料科學等使用案例。

此 **設定檔存放區** 是建立客戶設定檔的位置，主要用途如下：

* 充當用來支援即時體驗之設定檔的資料儲存空間；
* 啟用分段、啟用和個人化等使用案例。

>[!NOTE]
>
>您對的存取權 [!DNL data lake] 取決於您購買的產品SKU。 如需產品SKU的詳細資訊，請洽詢您的Adobe代表。

## 许可证使用 {#license-usage}

當您授權Experience Platform時，系統會提供您隨SKU而異的授權使用權益：

**[!DNL Addressable Audience]**  — 合約上允許在Experience Platform中使用的客戶設定檔總數，包括已知和假名設定檔。

**[!DNL Profile Richness]**  — 設定檔資料在Experience Platform中的平均大小。 您可以提高 [!DNL Profile Richness] 透過購買豐富套件獲得權益。

此 [!DNL Profile Richness] 量度會依您購買的授權而有所不同。 有兩個計算 [!DNL Profile Richness] 可用：

* Adobe Real-time Customer Data Platform中儲存的所有生產資料（即即時客戶設定檔和Identity Service）在任何時間點的總和，除以 [!DNL Addressable Audience]；
* 儲存在Platform中的所有資料的總和(包括但不限於 [!DNL data lake]、Real-Time Customer Profile和Identity Service)以及過去12個月內透過Platform串流（而非儲存）的任何資料，除以 [!DNL Addressable Audience].

這些量度的可用性，以及每個量度的特定定義，會因貴組織已購買的授權而異。

## 授權使用情況儀表板

Adobe Experience Platform UI提供儀表板，您可以透過儀表板檢視貴組織適用於Platform的授權相關資料快照。 儀表板中的資料與快照拍攝時特定時間點顯示的資料完全相同。 快照既不是近似值，也不是資料範例，而且儀表板沒有即時更新。

如需詳細資訊，請參閱以下指南： [在Platform UI上使用授權使用儀表板](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## 資料管理最佳實務

以下各節概述要遵循的最佳實務，以便更好地管理您的資料。

### 瞭解您的資料

並非所有資料在Adobe Experience Platform中都是相同的。 有些資料可能密集，但數值低，而其他資料可能稀疏，但數值高。 有些資料在產生後可能會立即失去價值，而其他資料則可能在數月（如果不是數年）內有價值。

在瞭解資料的值時，需要考量三個維度：

| 维度 | 描述 | 示例 |
| --- | --- | --- |
| 数量 | 代表所擷取的資料數量和總數。 | 網路點按 — 高音量和中等逼真度。 值可能會迅速減少。 |
| 時間跨度 | 代表內嵌資料持續發揮價值的時間長度。 | 離線購買 — 在數量和保真度上較為適度，但可能在較長時間內很有價值。 |
| 逼真度 | 代表資料中資訊的豐富程度。 | 客戶帳戶 — 數量低但保真度高。 在客戶的生命週期之外仍可發揮寶貴的作用。 |

### 資料管理工具 {#data-management-tools}

在確保您的資料使用量保持在授許可權制內時，請考慮兩種主要情況：

### 要將哪些資料帶入Platform？

資料可內嵌至Platform的一或多個系統中，即 [!DNL data lake] 和/或設定檔存放區。 這表示兩個系統中可以針對不同的使用案例存在不同的資料。 例如，您可能想要將歷史資料儲存在 [!DNL data lake]，但不在設定檔存放區中。 您可以啟用設定檔擷取的資料集，以選取要傳送至設定檔存放區的資料。

>[!NOTE]
>
>您對的存取權 [!DNL data lake] 取決於您購買的產品SKU。 如需產品SKU的詳細資訊，請洽詢您的Adobe代表。

### 要保留哪些資料？

您可以同時套用資料擷取篩選器和到期規則，以移除已因使用案例而過時的資料。 通常，行為資料（例如Analytics資料）使用的儲存空間會比記錄資料（例如CRM資料）多很多。 例如，相較於記錄資料，許多Platform使用者有超過90%的設定檔僅由行為資料填入。 因此，管理您的行為資料對於確保授權權益內的合規性至關重要。

您可以善用許多工具來保持您的授權使用權益：

* [擷取篩選器](#ingestion-filters)
* [設定檔存放區](#profile-service)

### 擷取篩選器 {#ingestion-filters}

內嵌篩選器可讓您僅匯入使用案例所需的資料，並篩選出所有不需要的事件。

| 擷取篩選器 | 描述 |
| --- | --- |
| Adobe Audience Manager來源篩選 | 建立Adobe Audience Manager來源連線時，您可以挑選要帶入的區段和特徵 [!DNL data lake] 和即時客戶個人檔案，而不是擷取整個Audience Manager資料。 請參閱指南： [建立Audience Manager來源連線](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 以取得詳細資訊。 |
| Adobe Analytics資料準備 | 您可以使用 [!DNL Data Prep] 功能來建立Analytics來源連線，以篩選掉使用案例不需要的資料。 到 [!DNL Data Prep]，您可以定義哪些屬性/欄需要發佈至設定檔。 您也可以提供條件陳述式，通知Platform資料應該發佈至設定檔，還是僅發佈至 [!DNL data lake]. 請參閱指南： [建立Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以取得詳細資訊。 |
| 支援設定檔的啟用/停用資料集 | 若要將資料內嵌至即時客戶個人檔案，您必須啟用資料集以用於個人檔案存放區。 如此一來，會將新增至 [!DNL Addressable Audience] 和 [!DNL Profile Richness] 權益。 一旦客戶設定檔使用案例不再需要資料集，您可以停用該資料集與設定檔的整合，以確保您的資料符合授權規範。 請參閱指南： [為設定檔啟用和停用資料集](../../catalog/datasets/enable-for-profile.md) 以取得詳細資訊。 |
| Web SDK和Mobile SDK資料排除 | Web和Mobile SDK收集的資料有兩種型別：自動收集的資料以及開發人員明確收集的資料。 若要更妥善地管理授權法規遵循，您可以透過內容設定，在SDK的設定中停用自動資料收集。 您的開發人員也可以移除或設定自訂資料。 請參閱指南： [設定SDK基礎知識](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) 以取得詳細資訊。 |
| 伺服器端轉送資料排除 | 如果您使用伺服器端轉送來傳送資料至Platform，可以移除規則動作中的對應以在所有事件中排除該資料，或是將條件新增至規則，讓資料僅針對特定事件引發，藉此排除傳送的資料。 請參閱以下說明檔案： [事件和條件](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) 以取得詳細資訊。 |
| 在來源層級篩選資料 | 在建立連線和內嵌資料至Experience Platform之前，您可以使用邏輯和比較運運算元來篩選來源中的列層級資料。 如需詳細資訊，請閱讀以下指南： [篩選來源的列層級資料，使用 [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### 設定檔存放區 {#profile-service}

設定檔存放區由下列元件組成：

| 設定檔存放區元件 | 描述 |
| --- | --- |
| 設定檔片段 | 每個客戶設定檔都由多個組成 **設定檔片段** 已合併的單一檢視，形成該客戶的單一檢視。 例如，如果客戶透過數個管道與您的品牌互動，您的組織將擁有多個 **設定檔片段** 和出現在多個資料集中的單一客戶有關。 將這些片段內嵌至Platform時，會使用身分圖表將它們彙整在一起，以為該客戶建立單一設定檔。 **設定檔片段** 由身分名稱空間組成，做為識別碼，並具有關聯的記錄資料和/或時間序列資料。 |
| 記錄資料（屬性） | 設定檔是主體、組織或個人的表示法，由許多部分組成 **屬性** (也稱為 **記錄資料**)。 例如，產品的設定檔可能包含SKU和說明，而人員的設定檔包含名字、姓氏和電子郵件地址等資訊。 **記錄資料** 量通常較低/中等，但長時間而言很有價值。 |
| 時間序列資料（行為） | **時間序列資料** 提供有關使用者行為的資訊。 由標準結構描述類別Experience Data Model (XDM)表示 [!DNL ExperienceEvent]，時間序列資料可說明事件，例如要新增至購物車的專案、要點按的連結和已檢視的視訊。 行為的價值可能會隨著時間而降低。 |
| 身分名稱空間（身分） | 當客戶資料彙集一起時，會透過使用將其合併到單一設定檔中 **身分名稱空間**，以及隨著更多使用者相關資訊浮出水面時將這些身分識別貼合在一起的能力。 請參閱 [身分名稱空間概觀](../../identity-service/namespaces.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

#### 設定檔存放區構成報表

有許多報表可協助您瞭解設定檔存放區的組成。 這些報告可協助您針對如何及到哪裡設定體驗事件有效期，做出明智的決策，以更能最佳化您的授權使用情況：

* **資料集重疊報表API**：公開對可定址對象貢獻最大的資料集。 您可以使用此報告來識別哪些 [!DNL ExperienceEvent] 要設定到期日的資料集。 請參閱教學課程，位置如下： [產生資料集重疊報表](../../profile/tutorials/dataset-overlap-report.md) 以取得詳細資訊。
* **身分重疊報表API**：公開對可定址對象貢獻最大的身分名稱空間。 請參閱教學課程，位置如下： [產生身分重疊報表](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 以取得詳細資訊。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### 假名設定檔資料有效期 {#pseudonymous-profile-expirations}

此功能可讓您自動從設定檔存放區中移除過時的假名設定檔。 如需有關此功能的詳細資訊，請閱讀 [假名設定檔資料到期概觀](../../profile/pseudonymous-profiles.md).

#### 體驗事件有效期 {#event-expirations}

此功能可讓您從已啟用設定檔的資料集中自動移除對您的使用案例不再有用的行為資料。 請參閱以下文章的概觀： [體驗事件有效期](../../profile/event-expirations.md) 瞭解此程式在資料集啟用後如何運作。

## 授權使用合規性最佳實務摘要 {#best-practices}

以下是您可以遵循的一些建議最佳實務清單，以確保更符合您的授權使用權益：

* 使用 [授權使用量儀表板](../../dashboards/guides/license-usage.md) 以追蹤及監控客戶使用趨勢。 這可讓您搶先瞭解可能發生的潛在使用過量。
* 設定 [擷取篩選器](#ingestion-filters) 識別細分和個人化使用案例所需的事件。 這可讓您僅傳送使用案例所需的重要事件。
* 確保您只有 [為設定檔啟用資料集](#ingestion-filters) 區段和個人化使用案例所需的資訊。
* 設定 [體驗事件有效期](#event-expirations) 和 [假名設定檔資料有效期](#pseudonymous-profile-expirations) 例如網頁資料等高頻資料。
* 定期檢查 [設定檔構成報表](#profile-store-composition-reports) 以瞭解您的設定檔存放區構成。 這可讓您瞭解對授權使用量消耗貢獻最大的資料來源。

## 功能摘要和可用性 {#feature-summary}

本檔案概述的最佳實務和工具將幫助您在Adobe Experience Platform中更好地管理您的授權權益使用情況。 此檔案將會隨著發行其他功能而更新，以協助向所有Experience Platform客戶提供可見度和控制力。

下表概述您目前可使用的功能清單，以便更好地管理您的授權使用權益。

| 功能 | 描述 |
| --- | --- |
| [啟用/停用設定檔的資料集](../../catalog/datasets/user-guide.md) | 啟用或停用將資料集擷取至Real-Time Customer Profile。 |
| [體驗事件有效期](../../profile/event-expirations.md) | 為擷取到已啟用設定檔的資料集中的所有事件套用到期時間。 請聯絡您的Adobe客戶團隊或客戶服務，以啟用此功能。 |
| [Adobe Analytics資料準備篩選器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 套用 [!DNL Kafka] 用於從內嵌中排除不必要資料的篩選器 |
| [Adobe Audience Manager來源聯結器篩選器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 套用Audience Manager來源連線篩選器以從擷取中排除不必要的資料 |
| [Alloy SDK資料篩選器](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | 套用Alloy篩選器以從擷取中排除不必要的資料 |
| [事件轉送資料篩選器](../../tags/ui/event-forwarding/overview.md) | 套用伺服器端 [!DNL Kafka] 篩選條件來排除內嵌中不必要的資料。  請參閱以下說明檔案： [標籤規則](../../tags/ui/managing-resources/rules.md) 以取得其他資訊。 |
| [授權使用量控制面板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 檢視貴組織的授權相關資料快照以供Experience Platform |
| [資料集重疊報表API](../../profile/tutorials/dataset-overlap-report.md) | 輸出對可定址對象貢獻最大的資料集 |
| [身分重疊報表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 輸出對可定址對象貢獻最大的身分名稱空間 |

{style="table-layout:auto"}
