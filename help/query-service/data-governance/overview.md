---
title: 查詢服務中的資料控管
description: 此概述涵蓋Experience Platform查詢服務中資料治理的主要元素。
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 54a6f508818016df1a4ab2a217bc0765b91df9e9
workflow-type: tm+mt
source-wordcount: '2843'
ht-degree: 1%

---

# 查詢服務中的資料控管

Adobe Experience Platform將來自多個企業系統的資料彙集在一起，可讓您根據自己的需求，透過查詢服務來清理、塑形、操縱和擴充資料。 這可讓行銷人員以更好的方式識別、瞭解及吸引客戶。 確保適當的資料控管是處理個人資訊的重要方面，因為某些資料可能會受到根據組織政策和法規的使用限制。 請務必確保您擷取的資料及其相關作業符合定義的資料使用原則。

Query Service中的資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。 在確保使用原則已根據您企業定義的法規套用時，這會發揮關鍵作用。

建議定期進行資料處理的組織概述、實踐和執行這些准則，為所有使用者營造注重隱私權的環境。

下列類別有助於在使用查詢服務時遵循資料法規遵循：

1. 安全性
1. 稽核
1. 資料使用
1. 隐私
<!-- 1. Data hygiene -->

本檔案會檢視各個不同的控管領域，並示範如何在使用「查詢服務」時促進資料合規性。 請參閱 [治理、隱私權及安全性概述](../../landing/governance-privacy-security/overview.md) 以進一步瞭解Experience Platform如何讓您管理客戶資料並確保法規遵循。

## 安全性

資料安全性是保護資料免於未經授權存取的程式，並確保在整個生命週期中都能安全存取。 透過角色型存取控制和屬性型存取控制等功能應用角色和許可權，在Experience Platform中維護安全存取。 憑證、SSL和資料加密也用於確保跨平台的資料保護。

查詢服務的安全性分為下列類別：

* [存取控制](#access-control)：存取權可透過角色和許可權控制，包括資料集和欄層級的許可權。
* 透過以下方式保護資料 [連線能力](#connectivity)：藉由使用即將到期的憑證或不即將到期的憑證達成有限的連線，透過Platform和外部使用者端來保護資料。
* 透過以下方式保護資料 [加密和系統層級的金鑰](#encryption)：資料閒置時，可透過加密確保資料安全性。

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### 访问控制 {#access-control}

Adobe Experience Platform中的存取控制可讓您使用 [Adobe Admin Console](https://adminconsole.adobe.com/) 使用角色型許可權來管理對查詢服務功能的存取。 同樣地，您可以透過結構描述和資料欄位的標籤管理，控制特定資料屬性的存取權。

本節概述使用者必須具備的存取控制許可權，才能充分利用查詢服務功能。 檢視檔案： [管理許可權](../../access-control/ui/permissions.md) 和 [管理使用者](../../access-control/ui/users.md) 以取得關於指派存取權給產品設定檔的詳細指示。

#### 相關許可權

相關存取控制許可權會根據其範圍層級在下表中定義。

**查詢執行許可權**

若要在Query Service中執行查詢，必須為使用者指派具有以下許可權的角色：

| 权限 | 描述 |
|---|---|
| [!UICONTROL 管理查詢] | 此許可權可讓使用者執行資料探索和批次查詢，以便讀取現有資料集或寫入資料集上的資料。 這包括兩者 `CREATE TABLE AS SELECT` (`CTAS`)和 `INSERT INTO AS SELECT` (`ITAS`)個查詢。 |

**資料集許可權**

本節提供透過查詢服務查詢資料時，存取資料集所需的資源型存取指南。

透過許可權介面，您可以為資料集和結構描述定義資源型存取控制，並具有下列許可權：

| 权限 | 描述 |
|---|---|
| [!UICONTROL 管理資料集] | 此許可權提供結構描述的唯讀存取權，並允許讀取、建立、編輯和刪除資料集，以與查詢服務搭配使用。 |
| [!UICONTROL 查看数据集] | 此許可權允許對搭配查詢服務使用的資料集和結構描述進行唯讀存取。 |

#### 欄/欄位的存取控制

以屬性為基礎的存取控制功能可讓Query Service使用者限制對關鍵使用者資料的存取。 可以根據指派給角色的許可權來授與或限制存取權。 使用者對個別欄的存取權由相關資料使用標籤和套用至指派給使用者的角色的許可權集控制。

使用資料使用標籤來標籤結構描述欄位群組和類別，會將資料使用限制套用至具有相同欄位群組和類別的所有結構描述。 請參閱以下文章的概觀： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得此功能的完整資訊。

此功能可讓您將機密欄的存取權授與您所選的使用者群組。 欄上的存取控制可限制特定使用者型別的讀取和寫入功能。

欄的存取控制可在架構層級套用於標準和臨時架構。 將資料使用標籤套用至XDM結構描述，以限制存取一或多個欄。 資料標籤會一致地套用，即使是透過查詢服務建立的資料集，只要使用預先定義的結構描述或在CTAS作業中產生的臨時結構描述即可。

一旦使用標籤和角色套用了適當的存取層級，當使用者嘗試存取無法存取的資料時，就會出現以下系統行為：

1. 如果拒絕使用者存取結構描述中的其中一個資料行，也會拒絕使用者讀取或寫入受限制資料行的許可權。 這種情況適用於下列常見案例：

   * **案例1**：當使用者嘗試執行僅影響受限欄的查詢時，系統會擲回該欄不存在錯誤。
   * **案例2**：當使用者嘗試執行具有多個欄（包括受限欄）的查詢時，系統僅為所有非受限欄傳回輸出。

1. 如果使用者嘗試存取計算欄位，使用者需要存取構成中使用的所有欄位，或系統也拒絕存取計算欄位。

#### 檢視的存取控制

「查詢服務」提供將標準ANSI SQL用於 [`CREATE VIEW`](../sql/syntax.md#create-view) 陳述式。 對於高度敏感的資料工作流程，您必須在建立檢視時實施適當的控制項。

此 `CREATE VIEW` 關鍵字定義查詢的檢視，但檢視並未實際具體化。 而是每次在查詢中參考檢視時都執行查詢。 當使用者從資料集建立檢視時，父資料集的角色和屬性型存取控制規則為 **not** 階層式套用。 因此，在建立檢視時，您必須明確設定每個欄的許可權。

#### 對加速的資料集建立欄位式存取限制 {#create-field-based-access-restrictions-on-accelerated-datasets}

使用 [屬性型存取控制功能](../../access-control/abac/overview.md) 您可以在下列位置定義事實和維度資料集的組織或資料使用範圍： [加速存放區](../data-distiller/query-accelerated-store/send-accelerated-queries.md). 這可讓管理員管理特定區段的存取權，並更好地管理授予使用者或使用者群組的存取權。

若要針對加速資料集建立欄位式存取限制，您可以使用查詢服務CTAS查詢來建立加速資料集，並根據現有的XDM結構描述或臨時結構描述來建構這些資料集。 然後，管理員可以 [新增和編輯結構描述的資料使用標籤](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) 或 [臨時結構描述](./ad-hoc-schema-labels.md#edit-governance-labels). 您可以從以下位置套用、建立及編輯方案標籤： [!UICONTROL 標籤] 工作區在 [!UICONTROL 結構描述] UI。

資料使用標籤也可以是 [已直接套用或編輯至資料集](../../data-governance/labels/user-guide.md#add-labels) 透過資料集UI，或透過存取控制建立 [!UICONTROL 標籤] 工作區。 請參閱操作方法指南 [建立新標籤](../../access-control/abac/ui/labels.md) 以取得詳細資訊。

接著，就可以透過附加的資料使用標籤以及套用至指派給使用者的角色的許可權集，來控制使用者對個別欄的存取權。

### 連線能力 {#connectivity}

查詢服務可透過Platform UI或透過與外部相容使用者端建立連線來存取。 存取所有可用前端是由一組認證所控制。

#### 透過外部使用者端的連線

使用協力廠商使用者端存取查詢服務需要認證才能獲得授權。 若要使用任何相容的外部使用者端存取查詢服務，這些認證是必要的。 您可以使用下列任一方式連線至外部使用者端： [即將到期的認證](#expiring-credentials) 或 [不會到期的認證](#non-expiring-credentials).

#### 透過到期認證的連線時間有限 {#expiring-credentials}

[即將到期的認證](../ui/credentials.md) 允許使用者與外部使用者端建立暫時連線。 這組認證僅在24小時內有效。 這些型別的認證的到期日會與認證索引標籤一起顯示在查詢服務儀表板中。

![「查詢服務」工作區中的「認證」索引標籤中反白了即將過期的認證。](../images/data-governance/overview/expiring-credentials.png)

#### 不會到期的認證 {#non-expiring-credentials}

[不會到期的認證](../ui/credentials.md#non-expiring-credentials) 可讓您與外部使用者端建立永久連線，讓您無需手動密碼即可輕鬆連線至查詢服務。

若要啟用產生不會到期的認證的選項，您必須遵循下列步驟 [必要的工作流程](../ui/credentials.md#prerequisites). 在此程式中，您的組織管理員需要設定產品設定檔的許可權，讓管理員控制哪些帳戶有權使用不會到期的認證。

允許具有不會到期認證的技術使用者帳戶可以指派角色，根據其職責和需求定義其讀取和寫入存取權的範圍，以確保適當的資料治理。 請參閱上一節關於 [透過存取控制使用角色型許可權](#access-control) 以管理對查詢服務的存取。

先決條件工作流程完成後，授權使用者現在可以 [產生所需的連線認證](../ui/credentials.md#generate-credentials).

#### SSL資料加密

為了提高安全性，Query Service為SSL連線提供原生支援，以加密使用者端/伺服器通訊。 Platform支援各種SSL選項，以符合您的資料安全性需求，並平衡加密和金鑰交換的處理開銷。

請參閱可用指南 [第三方使用者端連線至查詢服務的SSL選項](../clients/ssl-modes.md) 如需詳細資訊，包括如何使用 `verify-full` SSL引數值。

### 加密 {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

加密是使用演演算法程式，將資料轉換為已編碼和無法讀取的文字，以確保資訊受到保護且無法存取，而不需要解密金鑰。

Query Service資料相容性可確保資料一律加密。 傳輸中的資料一律符合HTTPS規範，靜態資料會使用系統層級的金鑰在Azure Data Lake存放區中加密。 請參閱以下說明檔案： [如何在Adobe Experience Platform中加密資料](../../landing/governance-privacy-security/encryption.md) 以取得詳細資訊。 如需如何在Azure Data Lake Storage中加密閒置資料的詳細資訊，請參閱 [Azure官方檔案](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## 稽核 {#audit}

查詢服務會記錄使用者活動，並將該活動分類為不同的記錄型別。 記錄提供資訊於 **誰** 已執行 **什麼** 動作，以及 **時間**. 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

Platform使用者可視需要請求任何記錄類別。 本節提供為「查詢服務」擷取的資訊型別，以及此資訊的存取位置的詳細資訊。

### 查詢記錄 {#query-logs}

查詢記錄UI可讓您監視和檢閱已透過查詢編輯器或查詢服務API執行的所有查詢的執行詳細資訊。 這可讓查詢服務活動透明化，讓您檢查中繼資料 **全部** 已跨查詢服務執行的查詢。 它包含所有型別的查詢，無論是探索、批次或排程的查詢。

查詢記錄檔可透過以下位置的Platform UI存取： [!UICONTROL 記錄檔] 的標籤 [!UICONTROL 查詢] 工作區。

![「查詢記錄」索引標籤中會反白顯示詳細資訊面板。](../images/data-governance/overview/queries-log.png)

### 审核日志 {#audit-logs}

稽核記錄包含比查詢記錄更詳細的資訊，並可讓您根據屬性（例如使用者、日期、查詢型別等）篩選記錄。 除了查詢記錄UI中提供的詳細資訊之外，稽核記錄還會儲存個別使用者的詳細資訊，及其工作階段資料或與協力廠商使用者端的連線。

稽核軌跡可提供使用者動作的確切記錄，有助於疑難排解問題，並幫助您的企業有效遵守公司資料管理政策和法規要求。 稽核記錄提供所有Platform活動的記錄。 使用稽核記錄，您可以稽核與查詢執行、範本和已排程查詢相關的使用者動作，以提高查詢服務中使用者所執行動作的透明度和可見度。

下表指出稽核記錄所擷取的查詢類別及其所記錄的動作型別：

| 类别 | 動作型別 |
|---|---|
| 查询 | Execute |
| 查詢範本 | 建立、刪除、更新 |
| 排定的查詢 | 建立、刪除、更新 |

以下是三個延伸伺服器記錄檔的清單，其中包含的詳細資訊多於查詢記錄檔中的詳細資訊。 可在稽核記錄查詢類別中找到擴充記錄：

1. **中繼查詢記錄**：執行查詢時，會執行各種相關聯的後端子查詢（例如剖析）。 這些型別的查詢稱為「中繼資料」查詢。 您可以在稽核記錄檔中找到它們的相關詳細資料。
1. **工作階段記錄**：系統會在使用者登入查詢服務時為其建立工作階段專案記錄，不論使用者是否執行查詢。
1. **協力廠商使用者端連線記錄**：當使用者成功將查詢服務連線至協力廠商使用者端時，會產生連線稽核記錄。

請參閱 [稽核記錄概觀](../../landing/governance-privacy-security/audit-logs/overview.md) 有關稽核記錄如何協助您的組織處理資料合規性的詳細資訊。

## 資料使用 {#data-usage}

Platform的資料控管架構提供統一方式，可讓您負責地使用所有Adobe解決方案、服務和平台中的資料。 它協調在整個的Adobe Experience Cloud中擷取、通訊和使用中繼資料的系統方法。 這進而可協助資料控管單位根據所需的行銷動作，以及這些預期行銷動作對該資料所設的限制，來標籤資料。 請參閱以下文章的概觀： [資料使用標籤](../../data-governance/labels/overview.md) 瞭解資料控管如何讓您將資料使用標籤套用至資料集和欄位的詳細資訊。

最佳實務是在資料歷程的每個階段致力於資料合規性。 為此，使用臨時結構描述的衍生資料集應在資料控管框架中適當地加上標籤。 查詢服務形成的衍生資料集有兩種型別：使用標準結構的資料集和使用臨時結構的資料集。

>[!NOTE]
>
>使用查詢服務建立的資料集稱為「衍生資料集」。

由於臨時結構描述是由個別使用者出於特定目的所建立，因此XDM結構描述欄位會為該特定資料集建立名稱空間，而不是打算用於不同的資料集。 因此，預設情況下，臨時結構描述不會顯示在Experience PlatformUI中。 雖然在標準與臨時結構描述之間應用資料使用標籤並無差異，但查詢服務為加上標籤而建立的臨時結構描述必須首先顯示在Platform UI中。 請參閱指南： [在Platform UI中探索臨時結構描述](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) 以取得更多詳細資料。

存取結構描述後，您可以 [將標籤套用至個別欄位](../../xdm/tutorials/labels.md). 在結構描述加上標籤後，衍生自該結構描述的所有資料集都會繼承這些標籤。 從這裡，您可以設定資料使用原則，以限制將具有特定標籤的資料啟用至特定目的地。 如需詳細資訊，請參閱以下文章的概觀： [資料使用原則](../../data-governance/policies/overview.md).

## 隐私 {#privacy}

[Privacy Service](../../privacy-service/home.md) 協助您根據法律隱私權法規，管理客戶存取和刪除其資料的請求。 其做法是搜尋資料中預先存在的識別碼，並根據請求的隱私權工作存取或刪除該資料。 資料必須正確加上標籤，服務才能在隱私權工作期間決定要存取或刪除哪些欄位。 受隱私權請求限制的資料必須包含客戶身分資訊，才能將不同的資料片段與隱私權請求適用的個人連結。 查詢服務可透過唯一識別碼擴充其使用的資料，以滿足隱私權工作的需求。

隱私權請求可以傳送至Data Lake或設定檔資料存放區。 從Data Lake中刪除的記錄不會導致從這些記錄中建立的設定檔刪除。 此外，從Data Lake刪除個人資訊的隱私權工作不會刪除其設定檔，因此在隱私權工作完成後，擷取的任何資訊（包含該設定檔ID）都會正常更新該設定檔。 這再次說明必須正確識別臨時結構描述中使用的資料。

請參閱Privacy Service檔案以取得以下專案的詳細資訊： [隱私權請求的身分資料](../../privacy-service/identity-data.md) 以及如何設定資料作業並運用Adobe技術，有效擷取適合客戶隱私權請求的身分資訊。

資料控管的查詢服務功能可簡化及簡化資料分類程式，以及遵守資料使用規範。 識別資料後，查詢服務可讓您在所有輸出資料集上配置主要身分。 您 **必須** 將身分新增至資料集，以利資料隱私權請求，並努力符合資料規範。

透過Platform UI，可將結構描述資料欄位設定為身分欄位，而查詢服務也可讓您 [使用SQL命令&#39;ALTER TABLE&#39;標籤主要身分](../sql/syntax.md#alter-table). 使用設定身分 `ALTER TABLE` 命令在使用SQL建立資料集時特別有用，而不是直接透過平台UI從結構描述建立。 請參閱檔案以瞭解如何操作的說明 [在UI中定義身分欄位](../../xdm/ui/fields/identity.md) 使用標準結構描述時。

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
