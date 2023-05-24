---
title: 目的地啟用工作流程中的身分處理
description: 瞭解在啟用工作流程中如何根據目的地型別處理身分匯出
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---

# 目的地啟用工作流程中的身分處理

此頁面說明身分識別如何匯出至不同目的地型別的特殊性，並教導您如何根據目的地找到哪些身分識別可供匯出。

>[!TIP]
>
> 如需身分、身分名稱空間和身分相關辭彙定義的詳細資訊，請閱讀 [identity service概述](/help/identity-service/home.md).

中的每個目的地 [目錄](/help/destinations/catalog/overview.md) 稍有不同，因此沒有適用於所有目的地的設定。 不過，有一些模式可指導目的地的設定及其身分需求，如下節所述。

## 以檔案為基礎的目的地 {#file-based}

對象 [檔案型目的地](/help/destinations/destination-types.md#file-based) (例如 [!DNL Amazon S3]、 SFTP、大多數電子郵件行銷目的地，例如 [!DNL Adobe Campaign]， [!DNL Oracle Eloqua]， [!DNL Salesforce Marketing Cloud])，這些目的地中的身分設定大多是開放的，這表示您不需要在 [選取屬性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) 批次啟用工作流程的步驟。

如果您選擇將身分新增至檔案匯出，請注意，只有來自的單一身分 [身分名稱空間](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) 可以在匯出中選取。 當您選取要匯出的身分時，會自動選取它作為 [強制屬性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) 和 [重複資料刪除索引鍵](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![選取為必要屬性和重複資料刪除索引鍵的身分。](/help/destinations/assets/how-destinations-work/selected-identity.png)

作為因應措施，如果這些身分已作為屬性引入Experience Platform，您可以向匯出新增更多身分。 請參閱以下範例，其中除了身分名稱空間之外，還選取要匯出的XDM屬性電子郵件地址 `Phone_E.164`.

![選取要匯出的電子郵件地址屬性範例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 從身分對應匯出身分與將身分匯出為XDM屬性 — 差異 {#identity-map-or-attribute}

根據您是從身分對應選取匯出身分識別，還是從已當作屬性擷取到Experience Platform的身分識別，匯出的記錄數量可能不同。 [合併原則](/help/profile/merge-policies/overview.md) 當您從身分對應選取身分時，也會在匯出的記錄數量上扮演重要角色。

例如，假設從兩個不同的資料集，您有下列設定檔片段將合併到單一客戶設定檔中：

**設定檔片段一**

| 身分對應 | 名字 | 姓氏 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件1，忠誠度ID1 | John | 完成 | 電子郵件1 |


**設定檔片段二**

| 身分對應 | 名字 | 姓氏 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件2，忠誠度ID1 | John | 完成 | 電子郵件2 |

合併的設定檔如下所示：

| 身分對應 | 名字 | 姓氏 | 電子郵件屬性 |
|---------|----------|---------|--------|
| 電子郵件1、電子郵件2、忠誠度ID1 | John | 完成 | 電子郵件2 |

匯出行為會因您選取的而異 `IdentityMap: Email` 或 `xdm: personalEmail.address` 以匯出。

如果客戶啟用 `IdentityMap: Email`，匯出的檔案中將有兩個記錄，一個用於email1，另一個用於email2。

但是，如果客戶啟用 `xdm: personalEmail.address`，只有email2會出現在記錄中，因為email attribute欄位僅包含email2。 這些情況可以解決不同的使用案例，您可能會想要啟用至客戶檔案中的所有電子郵件地址，或僅啟用至客戶檔案中最新的電子郵件地址。

結果是，您匯出的記錄數量取決於您選擇的合併原則，以及您在匯出中是否選取了身分或屬性。

## API型串流目的地 {#streaming-destinations}

[API型串流目的地](/help/destinations/destination-types.md#streaming-destination) 建置方式 [Destination SDK](/help/destinations/destination-sdk/overview.md) (例如 [!DNL Facebook]， [!DNL Google Customer Match]， [!DNL Pinterest]， [!DNL Braze]、和其他)僅支援特定ID以供匯出。 如需可匯出至每個目的地的特定身分詳細資訊，請閱讀 *支援的身分* 區段(例如，請參閱 [支援的身分割槽段](/help/destinations/catalog/advertising/pinterest.md) 在 [!DNL Pinterest] 目的地頁面)。

但請注意，您有彈性使用下列來源的資料： [私人圖表](/help/profile/merge-policies/overview.md#id-stitching) 或從屬性當做身分識別。 這表示您可以將XDM屬性對應至目的地所需的身分欄位。 請參閱以下範例，瞭解 [!DNL Pinterest] 目的地，其中XDM屬性 `personalEmail.address` 已對應至必要的 [!DNL Pinterest] 身分 `pinterest_audience`.

>[!TIP]
>
>當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 讓Experience Platform在啟動時自動雜湊資料的選項。 深入瞭解 **[!UICONTROL 套用轉換]** 中的選項 [串流目的地啟用教學課程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![對應至Pinterest目的地之身分欄位的電子郵件地址屬性範例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依賴第三方Cookie整合的廣告目的地 {#third-party-cookie-destinations}

依賴第三方Cookie的廣告目的地(例如： [!DNL Google Ads]， [!DNL Google Ad Manager]， [!DNL Google DV360]， [!DNL Bing]， [!DNL The Trade Desk])不會要求客戶在啟用工作流程中選取ID。 對於這些目的地，在設定啟用工作流程時，Experience Platform會自動查詢由以下專案建構的身分比對表： [[!UICONTROL Experience CloudID服務]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en) 和會匯出設定檔可用且目的地支援的所有身分。

這些目的地需要透過以下任一方式進行ID同步： [!UICONTROL Experience CloudID服務] 或透過 [!UICONTROL Experience PlatformWeb SDK].

如果您使用 [!UICONTROL Experience PlatformWeb SDK] 和舊版 [!UICONTROL Experience CloudID服務] 未在頁面上實作，則您需要確保相關網站的資料流已啟用，以允許同步協力廠商ID，如 [設定資料流檔案](/help/edge/datastreams/configure.md#create).

如上方連結的檔案所述，在設定資料串流時，您需要確保 **[!UICONTROL 協力廠商ID同步]** 滑桿已啟用。 大部分客戶都會離開 `container_id` 欄位空白（預設為0）。 如果您的舊版Audience Manager實作使用特定容器ID，您才需要變更此值（但請注意，這將為極少數客戶）。

>[!NOTE]
>
>Audience Manager支援這些廣告目的地的絕大部分(這些目的地型別在Audience Manager中稱為以裝置為基礎的目的地)。 參閱 [Audience Manager中所有支援的以裝置為基礎的目的地清單](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en))。 Experience Platform中僅列出少數幾項。 如需在Experience Platform和Audience Manager之間共用資料的資訊，請閱讀以下章節： [Experience Platform啟用不同Audience Manager之間的資料共用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). 目前沒有支援更多第三方Cookie目的地的計畫。

## 企業目的地 {#enterprise-destinations}

[企業目的地](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis]， [!DNL Azure Event Hubs]、HTTP API)的資料匯出不需要特定ID，因為這些是專為企業整合使用案例所設計。 不過，您可以視需要將身分匯出為XDM屬性，或從身分對應中匯出。 檢視 [匯出至HTTP目的地的資料範例](/help/destinations/catalog/streaming/http-destination.md#exported-data)，其中包含 `personalEmail.address` XDM屬性和身分 `ECID` 和 `email_lc_sha256` （雜湊電子郵件地址）。

## 個人化目的地 {#personalization-destinations}

[個人化（或邊緣）目的地](/help/destinations/destination-types.md#edge-personalization-destinations) (例如：Adobe Target、 [!DNL Custom Personalization])不需要在啟動工作流程中選擇任何身分，因為整合是設定檔查詢。 使用者端([!DNL Target]， [!DNL Web SDK]，或其他)查詢 [[!UICONTROL Edge]](/help/collection/home.md#edge) 和會提取站上個人化所需的設定檔資訊。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在瞭解如何找出個別目的地支援或需要的身分識別。 您現在也知道身分選取如何適用於每個目的地型別。

接下來，您可以閱讀有關哪些 [匯出設定](/help/destinations/how-destinations-work/destinations-configurations.md) 目的地適用的是各種目的地型別通用的，開發人員可以在個別目的地層級進行設定，使用者還可以在啟動工作流程中編輯哪些設定。

您也可以在「 」中籤出所有可用的目的地 [目錄](/help/destinations/catalog/overview.md).
