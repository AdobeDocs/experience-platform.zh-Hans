---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Aqua Data Studio；Aqua Data Studio；連線到查詢服務；
solution: Experience Platform
title: 將Aqua Data Studio連線至查詢服務
description: 本檔案將逐步說明將Aqua Data Studio與Adobe Experience Platform Query Service連線的步驟。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] 至查詢服務

本檔案說明連線的步驟 [!DNL Aqua Data Studio] 使用Adobe Experience Platform [!DNL Query Service].

## 快速入门

本指南要求您已擁有下列專案的存取權： [!DNL Aqua Data Studio] 並熟悉如何導覽其介面。 更多關於的資訊 [!DNL Aqua Data Studio] 您可在以下網址找到： [正式 [!DNL Aqua Data Studio] 檔案](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>有 [!DNL Windows] 和 [!DNL macOS] 版本 [!DNL Aqua Data Studio]. 本指南中的熒幕擷取畫面是使用 [!DNL macOS] 案頭應用程式。 不同版本之間的UI可能會有細微差異。

取得連線所需的認證 [!DNL Aqua Data Studio] 若要Experience Platform，您必須擁有 [!UICONTROL 查詢] Platform UI中的工作區。 如果您目前沒有「 」的存取權，請聯絡您的組織管理員 [!UICONTROL 查詢] 工作區。

## 註冊伺服器 {#register-server}

安裝後 [!DNL Aqua Data Studio]，您必須先註冊伺服器。 如需操作方法的說明，請參閱官方Aqua Data Studio檔案 [啟動 [!DNL Register Server] 對話方塊](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) 和 [註冊伺服器](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

一旦 **[!DNL Register Server]** PostgresSQL伺服器會出現對話方塊，提供下列伺服器設定的詳細資訊。

- **[!DNL Name]**：連線的名稱。 建議您提供易記名稱以辨識連線。
- **[!DNL Login Name]**：登入名稱是您的Platform組織ID。 其形式為 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**：這是在「 」上找到的英數字串 [!DNL Query Service] 認證儀表板。
- **[!DNL Host and Port]**：的主機端點及其連線埠 [!DNL Query Service]. 您必須使用連線埠80來連線 [!DNL Query Service].
- **[!DNL Database]：** 將使用的資料庫。 使用平台UI認證的值 `dbname`： `prod:all`.

### [!DNL Query Service] 認證

若要尋找您的認證，請登入 [!DNL Platform] UI並選取 **[!UICONTROL 查詢]** 從左側導覽，然後是 **[!UICONTROL 認證]**. 如需尋找您的登入證明資料、主機、連線埠和資料庫名稱的完整指示，請閱讀 [認證指南](../ui/credentials.md).

[!DNL Query Service] 也會提供不會到期的認證，以允許與協力廠商使用者端進行一次性設定。 請參閱以下檔案： [有關如何產生和使用不會到期的認證的完整指示](../ui/credentials.md#non-expiring-credentials).

### 設定SSL模式

接下來，您必須將SSL模式值設定為 `?sslmode=require`. 這是從以下位置完成的： [!DNL Driver] 的標籤 [!DNL Edit Server Properties] 對話方塊。 如需操作方法的說明，請參閱官方Aqua Data Studio檔案 [編輯驅動程式屬性](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) 和 [設定SSL [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). 使用搜尋列尋找 `sslmode` 屬性。

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用連線 `verify-full` SSL模式。

輸入連線詳細資料後，從相同索引標籤中選取 **[!DNL Test Connection]** 以確保您的憑證正常運作。 如果連線測試成功，請選取 **[!DNL Save]** 註冊您的伺服器。 確認對話方塊隨即出現，確認連線，連線圖示隨即顯示在圖示板上。 您現在可以連線到伺服器並檢視其綱要物件。

## 后续步骤

現在您已連線至 [!DNL Query Service]，您可以使用 **[!DNL Query Analyzer]** 範圍 [!DNL Aqua Data Studio] 執行及編輯SQL敘述句。 如需如何寫入和執行查詢的詳細資訊，請參閱 [running queries指南](../best-practices/writing-queries.md).
