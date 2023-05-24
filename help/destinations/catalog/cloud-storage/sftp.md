---
keywords: SFTP；sftp
title: sftp連線
description: 建立與您的SFTP伺服器的即時輸出連線，以定期從Adobe Experience Platform匯出限定資料檔案。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: cb0b80f79a849d81216c5500c54b62ac5d85e2f6
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 8%

---

# sftp連線

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>隨著匯出資料集功能的Beta版和改良的檔案匯出功能，您現在可能會看到兩個 [!DNL SFTP] 目的地目錄中的卡片。
>* 如果您已將檔案匯出至 **[!UICONTROL SFTP]** 目的地：請建立新的資料流到新的 **[!UICONTROL SFTP測試版]** 目的地。
>* 如果您尚未建立任何資料流至 **[!UICONTROL SFTP]** 目的地，請使用新的 **[!UICONTROL SFTP測試版]** 要匯出檔案的卡片 **[!UICONTROL SFTP]**.


![並排檢視中的兩個SFTP目的地卡片影像。](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

新功能中的改進 [!DNL SFTP] 目的地卡包括：

* [資料集匯出支援](/help/destinations/ui/export-datasets.md).
* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 可透過以下方式設定匯出檔案中的自訂檔案標頭： [改善對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能夠自訂匯出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 概述 {#overview}

建立與您的SFTP伺服器的即時輸出連線，以定期從Adobe Experience Platform匯出限定資料檔案。

>[!IMPORTANT]
>
> 雖然Experience Platform支援將資料匯出至SFTP伺服器，但建議匯出資料的雲端儲存位置為 [!DNL Amazon S3] 和 [!DNL SFTP].

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![SFTP設定檔匯出型別](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="私有 SSH 密钥"
>abstract="私有 SSH 密钥的格式必须为 Base64 编码的字符串，并且不得受密码保护。"

如果您選取 **[!UICONTROL 基本驗證]** 輸入以連線至您的SFTP位置：

![SFTP目的地基本驗證](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 主機]**：您的SFTP儲存位置位址；
* **[!UICONTROL 使用者名稱]**：登入SFTP儲存位置的使用者名稱；
* **[!UICONTROL 密碼]**：登入SFTP儲存位置的密碼。
* **[!UICONTROL 加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


如果您選取 **[!UICONTROL 使用SSH金鑰的SFTP]** 要連線至您的SFTP位置的驗證型別：

![SFTP目的地SSH金鑰驗證](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 網域]**：填入SFTP帳戶的IP位址或網域名稱
* **[!UICONTROL 連線埠]**：您的SFTP儲存位置使用的連線埠；
* **[!UICONTROL 使用者名稱]**：登入SFTP儲存位置的使用者名稱；
* **[!UICONTROL SSH金鑰]**：用來登入SFTP儲存位置的私人SSH金鑰。 私有 密钥的格式必须为 Base64 编码的字符串，并且不得受密码保护。
* **[!UICONTROL 加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 目的地詳細資料 {#destination-details}

在建立與SFTP位置的驗證連線後，請提供目的地的下列資訊：

![SFTP目的地的可用目的地詳細資料](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 名稱]**：輸入有助於您在Experience Platform使用者介面中識別此目的地的名稱；
* **[!UICONTROL 說明]**：輸入此目的地的說明；
* **[!UICONTROL 資料夾路徑]**：輸入要匯出檔案之SFTP位置中的資料夾路徑。
* **[!UICONTROL 檔案型別]**：選取匯出檔案應使用的格式Experience Platform。 此選項僅適用於 **[!UICONTROL SFTP測試版]** 目的地。 選取 [!UICONTROL CSV] 選項，您也可以 [設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。 此選項僅適用於 **[!UICONTROL SFTP測試版]** 目的地。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## (Beta)匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請參閱 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 匯出的資料 {#exported-data}

對象 [!DNL SFTP] 目的地，平台會建立 `.csv` 檔案的儲存位置。 如需檔案的詳細資訊，請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 區段啟動教學課程中的。

## IP位址允許清單

請參閱 [雲端儲存空間目的地的IP位址允許清單](ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。
