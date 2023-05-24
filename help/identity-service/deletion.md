---
title: Identity Service中的刪除
description: 本檔案概述您可以在Experience Platform中刪除身分資料的各種機制，並說明身分圖表可能受到哪些影響。
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 1%

---

# Identity Service中的刪除

Adobe Experience Platform Identity Service會透過決定性地連結個人跨裝置和系統的身分來產生身分圖表。 在同一資料列中收到兩個或多個標籤的身分時，會建立身分圖表連結。

即時客戶個人檔案會利用身分圖表來建立客戶屬性和行為的全面且單一檢視，讓您即時向人員而非裝置提供具影響力的個人數位體驗。

本檔案概述您可以在Experience Platform中刪除身分資料的各種機制，並說明身分圖表可能受到哪些影響。

## 快速入门

以下檔案參考下列Experience Platform功能：

* [Identity Service](home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
   * [身分圖表](./ui/identity-graph-viewer.md)：身分圖表是特定客戶不同身分之間的關係地圖，可讓您以視覺化方式呈現客戶如何跨不同管道與您的品牌互動。
   * [身分名稱空間](namespaces.md)：身分識別名稱空間是Identity Service的元件，用途是作為身分識別相關內容的指標。 例如，它們區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。
* [目錄服務](../catalog/home.md)：探索Data Lake中的資料譜系、中繼資料、檔案說明、目錄和資料集。
* [資料衛生](../hygiene/home.md)：排程自動化資料集有效期，或從單一資料集或所有資料集中刪除個別記錄，藉此管理您儲存的消費者資料。
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md)：管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [即時客戶個人檔案](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。

## 單一身分刪除

單一身分刪除請求可讓您刪除圖表中的身分，進而刪除與身分名稱空間相關聯的單一使用者身分相關聯的連結。 您可以使用以下提供的機制 [Privacy Service](../privacy-service/home.md) 若是客戶要求刪除資料和遵守一般資料保護規範(GDPR)等隱私權法規等使用案例。

以下各節會概述您可以在Experience Platform中用於單一身分刪除請求的機制。

### Privacy Service中的單一身分刪除

Privacy Service會根據一般資料保護規範(GDPR)和加州消費者隱私保護法(CCPA)等隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 透過Privacy Service，您可以使用API或UI提交工作請求。 當Experience Platform收到來自Privacy Service的刪除請求時，平台會向Privacy Service傳送確認訊息，確認已收到請求且受影響的資料已標示為刪除。 個人身分的刪除是根據提供的名稱空間和/或ID值。 此外，刪除也會針對與指定組織相關聯的所有沙箱進行。 如需詳細資訊，請閱讀以下指南： [Identity Service中的隱私權請求處理](privacy.md).

下表提供Privacy Service中單一身分刪除的劃分資訊：

| 單一身分刪除 | Privacy Service |
| --- | --- |
| 接受的使用案例 | 僅限資料隱私權請求(GDPR、CCPA)。 |
| 預估延遲 | 數天至數週 |
| 受影響的服務 | Privacy Service中的單一身分刪除可讓您選擇資料將會從Identity Service、即時客戶設定檔或資料湖中刪除。 |
| 刪除模式 | 從Identity Service刪除身分。 |

{style="table-layout:auto"}

## 資料集刪除

以下各節概述可用來刪除Experience Platform中的資料集和相關聯的身分連結的機制。

### 目錄服務中的資料集刪除

您可以使用目錄服務來提交資料集刪除請求。 如需如何使用目錄服務刪除資料集的詳細資訊，請閱讀以下指南： [使用目錄服務API刪除物件](../catalog/api/delete-object.md). 或者，您可以使用Platform UI來提交資料集刪除請求。 如需詳細資訊，請閱讀 [資料集使用手冊](../catalog/datasets/user-guide.md#delete-a-dataset).

### 資料衛生中的資料集有效期

此 [[!UICONTROL 資料衛生] 工作區](../hygiene/ui/overview.md) Adobe Experience Platform UI中的可讓您排程資料集的到期時間。 當資料集到達其到期日時，Data Lake、Identity Service和Real-Time Customer Profile會開始個別程式，從各自的服務中移除資料集的內容。 如需詳細資訊，請閱讀以下指南： [使用管理資料集有效期 [!UICONTROL 資料衛生] 工作區](../hygiene/ui/dataset-expiration.md).

下表提供「目錄服務」和「資料檢疫」中資料集刪除之間的差異明細：

| 資料集刪除 | 目录服务 | 資料衛生 |
| --- | --- | --- |
| 接受的使用案例 | 刪除Platform中的完整資料集及其相關身分資訊。 | 管理Experience Platform中儲存的資料。 |
| 預估延遲 | Days | Days |
| 受影響的服務 | 透過目錄服務刪除資料集會從Identity Service、即時客戶設定檔和資料湖刪除資料。 | 透過資料檢疫刪除資料集會從身分服務、即時客戶設定檔和資料湖刪除資料。 |
| 刪除模式 | 從由特定資料集建立的Identity Service中刪除連結的身分。 | 根據到期日排程，從由特定資料集建立的Identity Service中刪除連結的身分。 |

{style="table-layout:auto"}

## 刪除後身分圖表的不同狀態

所有身分圖表刪除都會移除兩個或多個身分之間的連結，如刪除請求所指定。 針對資料集刪除請求，會移除指定資料集建立的所有身分連結，而且不一定會將身分從圖形中移除。 對於單一身分刪除請求，會移除指定身分的身分連結，因此會從所有身分圖形中移除身分值本身。 沒有單一連結到其他身分的身分不會儲存在Identity Service中。

以下概述刪除可能對身分圖表狀態產生的影響。

| 身分圖表狀態 | 描述 |
| --- | --- |
| 部分更新 | 成功處理刪除請求後，圖形內至少有兩個身分維持連結，就會發生圖形的部分更新。 刪除後，其餘的身分連結可能會維持彼此連線，或根據已刪除的身分將連結分割成兩個或多個個別的圖表。 |
| 完全移除 | 圖表必須至少有兩個連結的身分才能存在。 因此，如果刪除請求導致移除圖表內的所有現有連結，則圖表將被完全移除。 |
| 无更改 | 如果特定刪除請求包含未與圖表任何成員相關聯的身分或資料集，圖表將不會受到影響。 此外，即使刪除請求確實刪除了資料集或身分資料集組合之間的連結，圖表也不會更新，因為該連結是由未刪除的其他連結所建立。 這表示如果連結存在於兩個不同的資料集中，圖表將不會更新，因為僅會移除其中一個資料集。 |

{style="table-layout:auto"}

## 后续步骤

本檔案說明您可以在Experience Platform上用來刪除身分和資料集的各種機制。 本檔案也概述身分和資料集刪除如何影響身分圖表。 如需Identity Service的詳細資訊，請閱讀 [Identity Service概觀](home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
