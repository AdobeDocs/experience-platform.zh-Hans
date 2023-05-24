---
title: (Beta) Google雲端儲存空間連線
description: 瞭解如何連線至Google Cloud Storage並啟用區段或匯出資料集。
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# (Beta) [!DNL Google Cloud Storage] 連線

>[!IMPORTANT]
>
>此目的地目前為測試版，僅供有限數量的客戶使用。 若要請求對的存取權 [!DNL Google Cloud Storage] 連線，請聯絡您的Adobe代表，並提供您的 [!DNL Organization ID].

## 概述 {#overview}

建立與的即時輸出連線 [!DNL Google Cloud Storage] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的貯體。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，連同適用的結構描述欄位，如在「 」的「 」選取設定檔屬性「 」畫面中所選。 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線的必要條件設定 [!DNL Google Cloud Storage] 帳戶 {#prerequisites}

為了將平台連線到 [!DNL Google Cloud Storage]，您必須先為以下專案啟用互通性： [!DNL Google Cloud Storage] 帳戶。 若要存取互通性設定，請開啟 [!DNL Google Cloud Platform] 並選取 **[!UICONTROL 設定]** 從 **[!UICONTROL 雲端儲存空間]** 選項。

![Google Cloud Platform控制面板，醒目提示「雲端儲存空間」和「設定」。](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

此 **[!UICONTROL 設定]** 頁面便會顯示。 從這裡，您可以檢視關於您的網站資訊， [!DNL Google] 專案ID和您的詳細資訊 [!DNL Google Cloud Storage] 帳戶。 若要存取互通性設定，請選取 **[!UICONTROL 互通性]** 從頂端標題。

![Google Cloud Platform儀表板中醒目提示的「互通性」索引標籤。](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

此 **[!UICONTROL 互通性]** 頁面包含驗證、存取金鑰以及與您的服務帳戶相關聯的預設專案的資訊。 若要為您的服務帳戶產生新的存取金鑰ID和秘密存取金鑰，請選取 **[!UICONTROL 建立服務帳戶的金鑰]**.

![Google Cloud Platform控制面板中醒目提示的「建立服務帳戶控制項」索引鍵。](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新產生的存取金鑰ID和秘密存取金鑰來連線 [!DNL Google Cloud Storage] 至平台的帳戶。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](/help/destinations/ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 存取金鑰ID]**：由61個字元組成的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 至平台的帳戶。 如需如何取得此值的詳細資訊，請閱讀 [必備條件](#prerequisites) 區段。
* **[!UICONTROL 秘密存取金鑰]**：用於驗證您的URL的40字元base64編碼字串， [!DNL Google Cloud Storage] 至平台的帳戶。 如需如何取得此值的詳細資訊，請閱讀 [必備條件](#prerequisites) 區段。
* **[!UICONTROL 加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

如需這些值的詳細資訊，請閱讀 [Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 來源概觀](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 貯體名稱]**：輸入 [!DNL Google Cloud Storage] 要由此目的地使用的貯體。
* **[!UICONTROL 資料夾路徑]**：輸入存放匯出檔案的目標資料夾路徑。
* **[!UICONTROL 檔案型別]**：選取匯出檔案應使用的格式Experience Platform。 選取 [!UICONTROL CSV] 選項，您也可以 [設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 计划

在 **[!UICONTROL 排程]** 步驟，您可以 [設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 您的 [!DNL Google Cloud Storage] 目的地，您也可以 [設定匯出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在啟動批次目的地UI教學課程中。

## (Beta)匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請參閱 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 驗證資料匯出成功 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Google Cloud Storage] 貯體，並確保匯出的檔案包含預期的設定檔母體。
