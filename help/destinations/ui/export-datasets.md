---
title: （測試版）將資料集匯出至雲端儲存空間目標
type: Tutorial
description: 瞭解如何將資料集從Adobe Experience Platform匯出至您偏好的雲端儲存位置。
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: d0de642eb6118e6597925c12c76917ffa98c3a5a
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 5%

---

# （測試版）將資料集匯出至雲端儲存空間目標

>[!IMPORTANT]
>
>* 匯出資料集的功能目前為測試版，並非所有使用者都可使用。 文档和功能可能会发生变化。
>* 此Beta版功能支援匯出第一代資料，如Real-time Customer Data Platform所定義 [產品說明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* 已購買Real-Time CDP Prime和Ultimate套件的客戶可使用此功能。 如需詳細資訊，請聯絡您的Adobe代表。


本文會說明匯出所需的工作流程 [資料集](/help/catalog/datasets/overview.md) 從Adobe Experience Platform到您偏好的雲端儲存位置，例如 [!DNL Amazon S3]、 SFTP位置或 [!DNL Google Cloud Storage] 使用Experience PlatformUI。

您也可以使用Experience Platform API來匯出資料集。 閱讀 [匯出資料集API教學課程](/help/destinations/api/export-datasets.md) 以取得詳細資訊。

## 支援的目的地 {#supported-destinations}

目前，您可以將資料集匯出至熒幕擷取畫面中反白顯示及以下列出的雲端儲存空間目的地。

![支援資料集匯出的目的地](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 何時啟用區段或匯出資料集 {#when-to-activate-segments-or-activate-datasets}

Experience Platform目錄中的某些檔案型目的地同時支援區段啟用和資料集匯出。

* 當您想要將資料結構化為依對象興趣或資格分組的設定檔時，請考慮啟用區段。
* 或者，當您想要匯出未依對象興趣或資格進行分組或建構的原始資料集時，請考慮匯出資料集。 您可以將此資料用於報告、資料科學工作流程、滿足合規性要求以及許多其他使用案例。

本檔案包含匯出資料集所需的所有資訊。 如果您想要對雲端儲存空間或電子郵件行銷目的地啟用區段，請閱讀 [啟用對象資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md).

## 先决条件 {#prerequisites}

若要將資料集匯出至雲端儲存體目的地，您必須已成功 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地並設定您要使用的目的地。

### 所需权限 {#permissions}

若要匯出資料集，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**、和 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

為確保您擁有匯出資料集的必要許可權，且目的地支援匯出資料集，請瀏覽目的地目錄。 如果目的地有 **[!UICONTROL 啟動]** 或 **[!UICONTROL 匯出資料集]** 控制項，則表示您擁有適當的許可權。

## 選取您的目的地 {#select-destination}

依照指示選取可匯出資料集的目的地：

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![反白顯示目錄控制項的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 選取 **[!UICONTROL 啟動]** 或 **[!UICONTROL 匯出資料集]** 對應至要將資料集匯出至之目的地的卡片上。

   ![反白顯示「啟動」控制項的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 選取 **[!UICONTROL 資料型別資料集]** 並選取您要匯出資料集的目的地連線，然後選取 **[!UICONTROL 下一個]**.

>[!TIP]
> 
>如果要設定匯出資料集的新目的地，請選取「 」 **[!UICONTROL 設定新目的地]** 以觸發 [連線到目的地](/help/destinations/ui/connect-destination.md) 工作流程。

![強調顯示具有資料集控制項的目的地啟用工作流程。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 此 **[!UICONTROL 選取資料集]** 檢視隨即顯示。 繼續下一節至 [選取您的資料集](#select-datasets) 以匯出。

## 選取您的資料集 {#select-datasets}

使用資料集名稱左側的核取方塊，選取您要匯出至目的地的資料集，然後選取 **[!UICONTROL 下一個]**.

![資料集匯出工作流程顯示「選取資料集」步驟，您可在此選取要匯出的資料集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 排程資料集匯出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="数据集的文件导出选项"
>abstract="选择&#x200B;**导出增量文件**&#x200B;以仅导出自上次导出后添加到数据集的数据。<br>第一个增量文件导出包括数据集中的所有数据，充当回填。后续增量文件仅包含自第一次导出后添加到数据集的数据。"

在 **[!UICONTROL 排程]** 步驟，您可以設定資料集匯出的開始日期和匯出節奏。

此 **[!UICONTROL 匯出增量檔案]** 選項會自動選取。 這會觸發匯出，其中第一個檔案是資料集的完整快照，後續檔案是自上次匯出以來資料集的增量新增。

>[!IMPORTANT]
>
>第一個匯出的增量檔案包含資料集中的所有現有資料，可作為回填。

![顯示排程步驟的資料集匯出工作流程。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用 **[!UICONTROL 頻率]** 選取器以選取匯出頻率：

   * **[!UICONTROL 每日]**：排程增量檔案每天於您指定的時間匯出一次。
   * **[!UICONTROL 每小時]**：排程每3、6、8或12小時匯出一次增量檔案。

2. 使用 **[!UICONTROL 時間]** 選擇器以選擇一天中的時間，在 [!DNL UTC] 格式，應何時進行匯出。

3. 使用 **[!UICONTROL 日期]** 選擇器來選擇應進行匯出的間隔。 請注意，在此功能的測試版中，無法設定匯出的結束日期。 如需詳細資訊，請檢視 [已知限制](#known-limitations) 區段。

4. 選取 **[!UICONTROL 下一個]** 以儲存排程並前往 **[!UICONTROL 檢閱]** 步驟。

>[!NOTE]
> 
>對於資料集匯出，檔案名稱具有無法修改的預設集預設格式。 請參閱區段 [驗證資料集匯出成功](#verify) 以取得詳細資訊和匯出檔案的範例。

## 请查看 {#review}

於 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選取範圍並開始將資料集匯出至目的地。

![顯示稽核步驟的資料集匯出工作流程。](/help/destinations/assets/ui/export-datasets/review.png)

## 驗證資料集匯出成功 {#verify}

匯出資料集時，Experience Platform會建立 `.json` 或 `.parquet` 檔案的儲存位置。 預期會根據您提供的匯出排程，將新檔案儲存在您的儲存位置。

Experience Platform會在您指定的儲存位置中建立資料夾結構，存放匯出的資料集檔案。 每次匯出時都會建立一個新資料夾，其模式如下：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

預設檔案名稱是隨機產生的，並確保匯出的檔案名稱是唯一的。

### 範例資料集檔案 {#sample-files}

這些檔案出現在您的儲存位置即表示匯出成功。 若要瞭解匯出檔案的結構，您可以下載範例 [.parquet檔案](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 或 [.json檔案](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## 從目的地移除資料集 {#remove-dataset}

若要從現有資料流中移除資料集，請遵循下列步驟：

1. 登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 並選取 **[!UICONTROL 目的地]** 左側導覽列中的。 選取 **[!UICONTROL 瀏覽]** 以檢視您現有的目的地資料流。

   ![目的地瀏覽檢視，其中顯示目的地連線，其餘則模糊化。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >選取篩選圖示 ![篩選圖示](../assets/ui/edit-activation/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

1. 從 **[!UICONTROL 啟用資料]** 欄，選取資料集控制項以檢視對應至此匯出資料流的所有資料集。

   ![可用的資料集導覽選項會在「啟動資料」欄中反白顯示。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 此 **[!UICONTROL 啟用資料]** 目的地頁面隨即顯示。 選取 **[!UICONTROL 移除資料集]** 右側欄中觸發「移除資料集」確認對話方塊。

   ![移除資料集對話方塊在右側欄中顯示「移除資料集」控制項。](../assets/ui/export-datasets/remove-dataset-control.png)

1. 在確認對話方塊中，選取 **[!UICONTROL 移除]** 立即將資料集從匯出至目的地時移除。

   ![對話方塊顯示確認從資料流移除資料集選項。](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 已知限制 {#known-limitations}

針對資料集匯出的Beta版，請牢記以下限制：

* 目前只有單一許可權(**[!UICONTROL 管理和啟用資料集目的地]**)，包括資料集目的地的管理和啟用許可權。 這些控制項在未來將分割為更精細的許可權。 檢閱 [必要許可權](#permissions) 區段，以取得匯出資料集所需的完整許可權清單。
* 目前，您只能匯出增量檔案，而且無法為資料集匯出選取結束日期。
* 匯出的檔案名稱目前無法自訂。
* UI目前不會阻止您刪除匯出至目的地的資料集。 請勿刪除任何正匯出至目的地的資料集。 [移除資料集](#remove-dataset) 從目的地資料流中刪除之前。
* 資料集匯出的監控量度目前與設定檔匯出的數字混雜在一起，因此無法反映真正的匯出數字。
