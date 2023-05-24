---
title: (Beta) Azure Data Lake Storage Gen2連線
description: 瞭解如何連線至Azure Data Lake Storage Gen2以啟用區段和匯出資料集。
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 010818b56154067402a7cd66f489dd2080142e53
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# (Beta) [!DNL Azure Data Lake Storage Gen2] 連線

>[!IMPORTANT]
>
>此目的地目前為測試版，僅供有限數量的客戶使用。 若要請求對的存取權 [!DNL Azure Data Lake Storage Gen2] 連線，請聯絡您的Adobe代表，並提供您的 [!DNL Organization ID].

## 概述 {#overview}

閱讀本頁以瞭解如何建立與您的的即時輸出連線 [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2])資料湖，以定期從Experience Platform匯出資料檔案。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，連同適用的結構描述欄位（例如PPID），如在「 」的「 」選取設定檔屬性「 」畫面中所選。 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](/help/destinations/ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL URL]**：的端點 [!DNL Azure Data Lake Storage Gen2]. 端點模式為： `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL 租使用者]**：包含您應用程式的租使用者資訊。
* **[!UICONTROL 服務主體ID]**：應用程式的使用者端ID。
* **[!UICONTROL 服務主體金鑰]**：應用程式的索引鍵。
* **[!UICONTROL 加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
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

### 计划 {#scheduling}

在 **[!UICONTROL 排程]** 步驟，您可以 [設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 您的 [!DNL Azure Data Lake Storage Gen2] 目的地，您也可以 [設定匯出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在啟動批次目的地UI教學課程中。

## (Beta)匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請參閱 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 驗證資料匯出成功 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Azure Data Lake Storage Gen2] 儲存，並確認匯出的檔案包含預期的設定檔母體。
