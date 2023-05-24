---
title: Adobe Experience Platform發行說明2022年3月
description: Adobe Experience Platform的2022年3月發行說明。
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 3 月 30 日**

Adobe Experience Platform中的新功能：

- [审核日志](#audit-logs)
- [Real-Time CDP B2B版本中的相關帳戶](#related-accounts)

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [資料彙集](#data-collection)
- [[!DNL Query Service]](#query-service)
- [源](#sources)

## 审核日志 {#audit-logs}

Experience Platform可讓您稽核各種服務和功能的使用者活動。 稽核記錄會提供有關誰做了哪些事、何時做的資訊。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 資料集、結構、類別、欄位群組、資料型別、沙箱、目的地、區段、合併原則、計算屬性、產品設定檔和帳戶(Adobe)的稽核記錄 | 這些是由稽核記錄檔記錄的資源。 如果啟用此功能，將會在活動發生時自動收集稽核記錄。 您无需手动启用日志收集。 |
| 匯出稽核記錄 | 稽核記錄可下載為 `CSV` 或 `JSON` 檔案。 產生的檔案會直接儲存至您的電腦。 |

{style="table-layout:auto"}

如需Platform稽核記錄的詳細資訊，請參閱 [稽核記錄概觀](../../landing/governance-privacy-security/audit-logs/overview.md).

## Real-Time CDP B2B版本中的相關帳戶 {#related-accounts}

>[!NOTE]
>
>「相關帳戶」功能僅適用於Real-Time CDP B2B版本的客戶。

B2B企業通常將其客戶資訊儲存在多個系統中，每個系統僅包含相同真實世界商業實體的部分或甚至衝突資料。 這造成了一個巨大的挑戰，即難以準確瞭解客戶，進而降低了他們的B2B行銷和銷售工作的效率和成效。 隨著相關帳戶的發行， [!DNL Real-Time CDP B2B] 現在會顯示與您瀏覽的帳戶類似的帳戶清單。 您可以在區段定義中加入相關帳戶，以擴大您的業務範圍，或在區段中套用更廣的標準。

請在下列檔案頁面中進一步瞭解此功能：

- [Real-Time CDP B2B版本中的相關帳戶概觀](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帳戶設定檔UI指南中的相關帳戶標籤](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在區段定義中使用相關科目](../../rtcdp/segmentation/b2b.md#related-accounts)

若要進一步瞭解Real-Time CDP B2B版本，請參閱 [概觀](../../rtcdp/overview.md).

## 警报 {#alerts}

Experience Platform可讓您訂閱各種Platform活動的事件型警報。 您可以透過以下方式訂閱不同的警報規則： [!UICONTROL 警報] 索引標籤中，並可選擇在UI本身或透過電子郵件通知接收警示訊息。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新警報規則 | 兩個新警報規則現在可用於與資料擷取相關的來源。 請參閱以下文章的概觀： [警示規則](../../observability/alerts/rules.md) 以取得更新的警示型別清單。 |

{style="table-layout:auto"}

如需Platform警示的詳細資訊，請參閱 [警報概觀](../../observability/alerts/overview.md).

## 仪表板 {#dashboards}

Adobe Experience Platform提供多個 [!DNL dashboards] 您可以透過它檢視有關您組織資料的重要資訊，如每日快照期間所擷取。

### 設定檔儀表板

設定檔儀表板會顯示貴組織在Experience Platform的設定檔存放區中擁有的屬性（記錄）資料快照。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 未分段的設定檔Widget | Widget會提供未附加至任何區段的所有設定檔總數。 產生的數字自上次快照以來都是準確的，代表您組織內個人資料啟用的機會。 請參閱 [設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得詳細資訊。 |
| 未分段的設定檔趨勢Widget | 此小部件为给定时间段内未附加到任何区段的配置文件数量提供了一个折线图说明。趨勢可以視覺化呈現超過30天、90天和12個月期間。 請參閱 [設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得詳細資訊。 |
| 依身分Widget區分的未分段設定檔 | 此小部件按其唯一标识符对未分段配置文件的总数进行分类。資料會以長條圖呈現。 請參閱 [設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得詳細資訊。 |
| 單一身分設定檔Widget | 此Widget提供貴組織設定檔的計數，這些設定檔只有一種ID型別（電子郵件或ECID）可建立其身分識別。 請參閱 [設定檔標準Widget檔案](../../dashboards/guides/profiles.md#standard-widgets) 以取得詳細資訊。 |

{style="table-layout:auto"}

如需「設定檔」儀表板的詳細資訊，請參閱 [設定檔儀表板概觀](../../dashboards/guides/profiles.md).

### 目的地儀表板

目的地儀表板會顯示貴組織在Experience Platform中啟用的目的地的快照。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 目的地計數Widget | Widget提供可在系統中啟用及傳送對象的可用端點總數。 此数目包含活动目标数和非活动目标数。請參閱 [目的地標準Widget檔案](../../dashboards/guides/destinations.md#standard-widgets) 以取得詳細資訊。 |

{style="table-layout:auto"}

如需Platform中「目的地」儀表板的詳細資訊，請參閱 [目的地儀表板概觀](../../dashboards/guides/destinations.md).

## 資料彙集 {#data-collection}

Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 全域資料流設定 | 您現在可以在設定資料流時設定數個新的全域設定：地理位置、第一方ID Cookie和協力廠商ID同步。 請參閱以下小節： [設定資料串流](../../edge/datastreams/overview.md#create) 如需詳細資訊，請參閱資料串流UI指南。 |
| [边缘网络服务器 API](../../server-api/overview.md) | 伺服器API可讓客戶使用新的、經過驗證的端點與Experience Platform邊緣網路互動，以支援各種資料收集、個人化、廣告和行銷使用案例。 |

如需Platform資料收集的詳細資訊，請參閱 [資料彙集概觀](../../collection/home.md).

## 查询服务 {#query-service}

[!DNL Query Service] 可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從以下位置聯結任何資料集： [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或內嵌至即時客戶個人檔案。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `table_exists` | 新特徵指令用於確認表格目前是否存在於系統中。 該命令會傳回布林值： `true` 如果表格 **會** 存在，和 `false` 如果表格有 **not** 存在。 請參閱 [SQL語法檔案](../../query-service/sql/syntax.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

如需可用功能的詳細資訊，請參閱 [查詢服務總覽](../../query-service/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理整個過程中的資料擷取。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新來源現在可用於B2B使用 | 您現在可以針對B2B使用案例使用Platform上所有可用的來源。 請參閱 [來源目錄](../../sources/home.md) 以取得可用來源的完整清單。 |
| 全面推出新功能 [!DNL Oracle Eloqua] source | 您現在可以使用 [!DNL Oracle Eloqua] 從您的網站順暢擷取資料的來源 [!DNL Oracle Eloqua] 執行個體（帳戶、行銷活動、連絡人）到Platform。 請參閱以下說明檔案： [建立 [!DNL Oracle Eloqua] 來源連線](../../sources/connectors/marketing-automation/oracle-eloqua.md) 以取得詳細資訊。 |
| 的API增強功能 [!DNL Data Landing Zone] | 此 [!DNL Data Landing Zone] 來源現在支援在使用時自動偵測檔案屬性 [!DNL Flow Service] API。 請參閱以下說明檔案： [建立 [!DNL Data Landing Zone] 來源連線](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
