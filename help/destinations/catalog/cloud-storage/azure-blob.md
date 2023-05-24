---
keywords: Azure Blob；Blob目的地；s3；Azure Blob目的地
title: Azure Blob連線
description: 建立與您的Azure Blob儲存體的即時輸出連線，以定期從Adobe Experience Platform匯出CSV資料檔案。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 4%

---

# [!DNL Azure Blob] 連線

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>隨著匯出資料集功能的Beta版和改良的檔案匯出功能，您現在可能會看到兩個 [!DNL Azure Blob] 目的地目錄中的卡片。
>* 如果您已將檔案匯出至 **[!UICONTROL Azure Blob]** 目的地：請建立新的資料流到新的 **[!UICONTROL Azure Blob測試版]** 目的地。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Azure Blob]** 目的地，請使用新的 **[!UICONTROL Azure Blob測試版]** 要匯出檔案的卡片 **[!UICONTROL Azure Blob]**.


![並排檢視中的兩個Azure Blob目的地卡片。](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

新功能中的改進 [!DNL Azure Blob] 目的地卡包括：

* [資料集匯出支援](/help/destinations/ui/export-datasets.md).
* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 可透過以下方式設定匯出檔案中的自訂檔案標頭： [改善對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能夠自訂匯出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 概述 {#overview}

[!DNL Azure Blob] (以下稱 [!DNL Blob])是Microsoft的雲端物件儲存解決方案。 本教學課程提供建立 [!DNL Blob] 目的地使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Blob] 目的地，您可以略過本檔案的其餘部分，並前往上的教學課程 [啟用區段至您的目的地](../../ui/activate-batch-profile-destinations.md).

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 支持的文件格式 {#file-formats}

[!DNL Experience Platform] 支援匯出至下列檔案格式 [!DNL Azure Blob]：

* 逗號分隔值(CSV)：目前僅支援使用逗號分隔值的匯出資料檔案。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 連線字串]**：需要連線字串才能存取Blob儲存空間中的資料。 此 [!DNL Blob] 連線字串模式開頭為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 如需有關設定的詳細資訊 [!DNL Blob] 連線字串，請參閱 [設定Azure儲存體帳戶的連線字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) (位於Microsoft檔案中)。
* **[!UICONTROL 加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 資料夾路徑]**：輸入存放匯出檔案的目標資料夾路徑。
* **[!UICONTROL 容器]**：輸入 [!DNL Azure Blob Storage] 此目的地要使用的容器。
* **[!UICONTROL 檔案型別]**：選取匯出檔案應使用的格式Experience Platform。 此選項僅適用於 **[!UICONTROL Azure Blob測試版]** 目的地。 選取 [!UICONTROL CSV] 選項，您也可以 [設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。 此選項僅適用於 **[!UICONTROL Azure Blob測試版]** 目的地。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## (Beta)匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請參閱 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 匯出的資料 {#exported-data}

對象 [!DNL Azure Blob Storage] 目的地， [!DNL Platform] 建立 `.csv` 檔案的儲存位置。 如需檔案的詳細資訊，請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 區段啟動教學課程中的。