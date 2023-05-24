---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；adobe campaign；行銷活動
title: Adobe Campaign連線
description: Adobe Campaign是一套解決方案，可協助您跨所有線上和離線管道個人化並傳遞行銷活動。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Adobe Campaign連線

## 概述 {#overview}

Adobe Campaign是一套解決方案，可協助您跨所有線上和離線管道個人化並傳遞行銷活動。 另請參閱 [開始使用Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 以取得詳細資訊。

若要將區段資料傳送至Adobe Campaign，您必須先 [連線目的地](#connect-destination) 在Adobe Experience Platform中，然後 [設定資料匯入](#import-data-into-campaign) 從您的儲存位置移至Adobe Campaign。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

請參閱 [雲端儲存空間目的地的IP位址允許清單](../cloud-storage/ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或連絡您的產品管理員以取得必要許可權

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

Adobe Campaign支援下列連線型別：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 使用密碼的SFTP]**
* **[!UICONTROL 使用SSH金鑰的SFTP]**
* **[!UICONTROL Azure Blob]**

將資料傳送至Adobe Campaign的偏好方法為透過 [!DNL Amazon S3] 或 [!DNL Azure Blob].

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* 對象 **[!UICONTROL Amazon S3]** 連線，您必須提供 [!UICONTROL 存取金鑰ID] 和 [!UICONTROL 秘密存取金鑰].
* 對象 **[!UICONTROL 使用密碼的SFTP]** 連線，您必須提供 [!UICONTROL 網域]， [!UICONTROL 連線埠]， [!UICONTROL 使用者名稱]、和 [!UICONTROL 密碼].
* 對象 **[!UICONTROL 使用SSH金鑰的SFTP]** 連線，您必須提供 [!UICONTROL 網域]， [!UICONTROL 連線埠]， [!UICONTROL 使用者名稱]、和 [!UICONTROL SSH金鑰].
* 對象 **[!UICONTROL Azure Blob]** 連線時，您必須提供連線字串。
* 或者，您可以附加RSA格式的公開金鑰，將PGP/GPG的加密新增至匯出的檔案，位於 **[!UICONTROL 金鑰]** 區段。 您的公開金鑰必須寫成 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**：為您的目的地選擇相關名稱。
* **[!UICONTROL 說明]**：輸入目的地的說明。
* **[!UICONTROL 貯體名稱]**： *S3連線*. 輸入S3儲存貯體的地點，其中 [!DNL Platform] 會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 資料夾路徑]**：提供儲存位置的路徑，其中 [!DNL Platform] 會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 容器]**： *用於Blob連線*. 包含資料夾路徑所在Blob的容器。
* **[!UICONTROL 檔案格式]**：選取 **CSV** 以將CSV檔案匯出至您的儲存位置。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。


另請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 目的地屬性 {#destination-attributes}

啟用區段至此目的地時，Adobe建議您從 [聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱 [在電子郵件行銷目的地啟用對象時的最佳實務](overview.md#best-practices).

## 匯出的資料 {#exported-data}

對象 [!DNL Adobe Campaign] 目的地， [!DNL Platform] 建立 `.csv` 檔案的儲存位置。 如需檔案的詳細資訊，請參閱 [驗證區段啟用](../../ui/activate-batch-profile-destinations.md#verify) 區段啟動教學課程中的。

## 設定將資料匯入Adobe Campaign中 {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 請記住 [!DNL SFTP] 在執行此整合時，根據Adobe Campaign合約中的儲存空間限制、資料庫儲存空間限制和作用中設定檔限制。
>* 您需要使用排程、匯入及對應匯出的Adobe Campaign區段 [!DNL Campaign] 工作流程。 請參閱 [設定循環匯入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) 在Adobe Campaign Classic檔案和 [關於資料管理活動](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) 在Adobe Campaign Standard檔案中。
>* 將資料傳送至Adobe Campaign的偏好方法為透過 [!DNL Amazon S3] 或 [!DNL Azure Blob].


連線之後 [!DNL Platform] 至您的 [!DNL Amazon S3] 或 [!DNL Azure Blob] 存放區時，您必須將資料從存放區位置匯入至Adobe Campaign。 若要瞭解如何完成此作業，請參閱下列Adobe Campaign檔案頁面：
* [開始使用匯入和匯出資料](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hans) 和 [資料載入（檔案）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) (位於Adobe Campaign Classic檔案中)。
* [開始使用流程和資料管理](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 和 [載入檔案](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) (位於Adobe Campaign Standard檔案中)。
