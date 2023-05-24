---
title: （字母） [!DNL LiveRamp SFTP] 連線
description: 瞭解如何使用LiveRamp聯結器將對象從Adobe Real-time Customer Data Platform載入LiveRamp Connect。
hidefromtoc: true
hide: true
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: d7625018b7b36d8e9516f7884fc00b726d391103
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 3%

---

# （字母） [!DNL LiveRamp - SFTP] 連線 {#liveramp-destination}

使用LiveRamp連線將對象從Adobe Real-time Customer Data Platform上線到 [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>此目的地連線目前處於Alpha階段，僅供有限數量的客戶選擇。 功能和檔案可能會有所變更。</p>
&gt;<p>此目的地連線的最終版本可能需要客戶移轉。</p>


## 用例 {#use-cases}

為了協助您更清楚瞭解應該如何及何時使用 [!DNL LiveRamp SFTP] 目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

身為行銷人員，我想要將受眾從Adobe Experience Platform傳送至內建身分識別 [!DNL LiveRamp Connect] 以便我可以在以下位置鎖定使用者： [!DNL CTV] 平台，使用 [!DNL Ramp ID] 識別碼。

## 先决条件 {#prerequisites}

此 [!DNL LiveRamp - SFTP] 連線匯出檔案，使用 [LiveRamp的SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) 儲存。

從Experience Platform將資料傳送至之前 [!DNL LiveRamp SFTP]，您需要您的 [!DNL LiveRamp] 認證。 請聯絡您的 [!DNL LiveRamp] 代表取得您的認證（若尚未取得）。

## 支援的身分 {#supported-identities}

LiveRamp SFTP支援身分啟用，例如PII型識別碼、已知識別碼和自訂ID，如官方檔案所述 [LiveRamp檔案](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

在 [對應步驟](#map) 在啟動工作流程中，您必須將目標對應定義為自訂屬性。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，而這些成員具有「 」中使用的識別碼（名稱、電話號碼或其他）。 [!DNL LiveRamp SFTP] 目的地。 |
| 匯出頻率 | **[!UICONTROL 每日批次]** | 由於設定檔會根據區段評估在Experience Platform中更新，因此設定檔（身分）會每天更新一次，以提供給目的地平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

**使用密碼的SFTP驗證** {#sftp-password}

![顯示如何使用含有密碼的SFTP驗證目的地身份的範例熒幕擷圖](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL 使用者名稱]**：您的使用者名稱 [!DNL LiveRamp SFTP] 儲存位置。
* **[!UICONTROL 密碼]**：您的密碼 [!DNL LiveRamp SFTP] 儲存位置。
* **[!UICONTROL pgp/GPG加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。 如果您提供加密金鑰，也必須提供 **[!UICONTROL 加密子金鑰ID]** 在 [目的地詳細資料](#destination-details) 區段。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/advertising/liveramp/pgp-key.png)

**具有SSH金鑰驗證的SFTP** {#sftp-ssh}

![顯示如何使用SSH金鑰驗證目的地的範例熒幕擷圖](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL 使用者名稱]**：您的使用者名稱 [!DNL LiveRamp SFTP] 儲存位置。
* **[!UICONTROL SSH金鑰]**：私人 [!DNL SSH] 用來登入您的 [!DNL LiveRamp SFTP] 儲存位置。 私密金鑰必須格式化為 [!DNL Base64]-encoded string ，且不得受密碼保護。

   * 若要連線您的 [!DNL SSH] 索引鍵 [!DNL LiveRamp SFTP] 伺服器，您必須透過提交票證 [!DNL LiveRamp]的技術支援入口網站，並提供您的公開金鑰。 如需詳細資訊，請參閱 [LiveRamp檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL pgp/GPG加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 如果您提供加密金鑰，也必須提供 **[!UICONTROL 加密子金鑰ID]** 在 [目的地詳細資料](#destination-details) 區段。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/advertising/liveramp/pgp-key.png)

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="加密子密钥 ID"
>abstract="用于加密（基于 LiveRamp 公共加密密钥）的子密钥 ID。如果您在身份验证步骤中提供了加密密钥，则此字段是必需的。"
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="了解如何获取子密钥 ID"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

![顯示如何填寫目的地詳細資訊的Platform UI熒幕擷圖](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 資料夾路徑]**：的路徑 [!DNL LiveRamp] `uploads` 將託管匯出檔案的子資料夾。 此 `uploads` 字首會自動新增至資料夾路徑。
   * 例如，如果要將檔案匯出至 `uploads/my_export_folder`，輸入 `my_export_folder` 在 **[!UICONTROL 資料夾路徑]** 欄位。
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。 可用選項包括 **[!UICONTROL GZIP]** 或 **[!UICONTROL 無]**.
* **[!UICONTROL 加密子金鑰ID]**：用於加密的子金鑰，根據 [!DNL LiveRamp] 公開加密金鑰。 如果您在「 」中提供加密金鑰，則必須填寫此欄位 [驗證](#authenticate) 步驟。 請參閱 [!DNL LiveRamp] [加密檔案](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) 以瞭解如何取得子索引鍵ID。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請閱讀以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [啟用對象資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 计划 {#scheduling}

在 [!UICONTROL 排程] 步驟，使用下列設定為每個區段建立匯出排程。

>[!IMPORTANT]
>
>所有啟用至此目的地的區段都必須設定為完全相同的排程，如下所示。

* **[!UICONTROL 檔案匯出選項]**： [!UICONTROL 匯出完整檔案]. [增量檔案匯出](../../ui/activate-batch-profile-destinations.md#export-incremental-files) 目前不支援 [!DNL LiveRamp] 目的地。
* **[!UICONTROL 頻率]**： [!UICONTROL 每日]
* 將匯出時間設為 **[!UICONTROL 區段評估後]**. 已排程的區段匯出和 [隨選檔案匯出](../../ui/export-file-now.md) 目前不支援 [!DNL LiveRamp] 目的地。
* **[!UICONTROL 日期]**：視需要選取匯出開始和結束時間。

![顯示區段排程步驟的平台UI熒幕擷圖。](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

匯出的檔案名稱目前無法由使用者設定。 所有匯出至 [!DNL LiveRamp SFTP] 目的地會根據下列範本自動命名：

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![顯示匯出檔案名稱範本的平台UI熒幕擷圖。](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

例如，為名為的組織匯出的檔案名稱 [!DNL Luma] 可能會看起來類似這樣：

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟，您可以選取要為設定檔匯出的屬性和身分。

>[!IMPORTANT]
>
>此目的地支援為每個啟用流程啟用一個來源身分名稱空間。 如果您需要匯出多個身分名稱空間，例如 `Email` 和 `Phone`，您必須 [建立個別的啟動流程](../../ui/activate-batch-profile-destinations.md) 每個身分識別。

在 **[!UICONTROL 對應]** 步驟， **[!UICONTROL 目標欄位]** mapping會定義匯出的CSV檔案中欄標題的名稱。 您可以為提供自訂名稱，將匯出檔案中的CSV欄標題變更為任何您想要的易記名稱。 **[!UICONTROL 目標欄位]**.

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 您會在畫面上看到新的對應列。

   ![顯示「對應」畫面的Experience PlatformUI畫面。](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. 在 **[!UICONTROL 選取來源欄位]** 視窗，選擇 **[!UICONTROL 選取屬性]** 類別並選取您要對應的XDM屬性，或選擇 **[!UICONTROL 選取身分名稱空間]** 類別並選取身分以對應至您的目的地。

   ![顯示來源「對應」畫面的Experience PlatformUI畫面。](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. 在 **[!UICONTROL 選取目標欄位]** 視窗中，輸入您要將選取的來源欄位對應到的屬性名稱。 此處定義的屬性名稱將在匯出的CSV檔案中反映為欄標題。

   ![顯示目標「對應」畫面的Experience PlatformUI畫面。](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   您也可以直接在「 」中輸入屬性名稱 **[!UICONTROL 目標欄位]**.

   ![顯示目標「對應」畫面的Experience PlatformUI畫面。](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

新增所有需要的對應後，選取 **[!UICONTROL 下一個]** 並完成啟動工作流程。

## 匯出的資料/驗證資料匯出 {#exported-data}

您的資料會匯出至 [!DNL LiveRamp SFTP] 您設定的儲存位置，如CSV檔案。

將檔案匯出至 [!DNL LiveRamp SFTP] 目的地，Platform會為每個目的地產生一個CSV檔案 [合併原則ID](../../../profile/merge-policies/overview.md).

例如，我們考慮以下區段：

* 區段A （合併原則1）
* 區段B （合併原則2）
* 區段C （合併原則1）
* 區段D （合併原則1）

Platform會將兩個CSV檔案匯出至 [!DNL LiveRamp SFTP]：

* 一個包含區段A、C和D的CSV檔案；
* 一個包含區段B的CSV檔案。

匯出的CSV檔案包含設定檔，該設定檔具有所選屬性和對應的區段狀態，位於單獨的欄上，並以屬性名稱和區段ID作為欄標題。

匯出檔案中包含的設定檔可符合下列其中一個區段資格狀態：

* `Active`：設定檔目前符合區段的資格。
* `Expired`：設定檔不再符合區段的資格，但過去已符合資格。
* `""`（空字串）：此設定檔從未符合該區段的資格。


例如，匯出的CSV檔案中有一個 `email` 屬性和3個區段看起來可能像這樣：

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

因為Platform會為每個CSV檔案產生一個 [合併原則ID](../../../profile/merge-policies/overview.md)，也會為每個合併原則ID產生個別的資料流執行。

這表示 **[!UICONTROL 身分已啟用]** 和 **[!UICONTROL 已接收的設定檔]** 中的量度 [資料流執行](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 會針對使用相同合併原則的每個區段群組彙總頁面，而非針對每個區段顯示。

由於針對使用相同合併原則的一組區段產生資料流執行，區段名稱不會顯示在 [監視儀表板](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![顯示身分啟用量度的Experience PlatformUI熒幕。](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## 將匯出的資料上傳至LiveRamp {#upload-to-liveramp}

在您的資料成功匯出至 [!DNL LiveRamp - SFTP] 儲存，您必須將資料上傳至 [!DNL LiveRamp] 平台。

如需如何上傳檔案的詳細資訊，請參閱 [!DNL LiveRamp - SFTP] 儲存至 [!DNL LiveRamp] 對象，請參閱下列檔案： [上傳第一個檔案至對象時的注意事項](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請閱讀 [資料控管概觀](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

如需如何設定LiveRamp SFTP儲存空間的詳細資訊，請參閱 [正式檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
