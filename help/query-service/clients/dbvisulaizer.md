---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Db視覺化程式；DbVisualizer；db視覺化程式；連線到查詢服務；
solution: Experience Platform
title: 將DbVisualizer連線到查詢服務
description: 本檔案逐步解說將DbVisualizer連線至Adobe Experience Platform查詢服務的步驟。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Connect [!DNL DbVisualizer] 至 [!DNL Query Service] {#connect-dbvisualizer}

本檔案說明連線 [!DNL DbVisualizer] Adobe Experience Platform資料庫工具 [!DNL Query Service].

## 快速入门

本指南要求您已擁有 [!DNL DbVisualizer] 案頭應用程式，並熟悉如何導覽其介面。 若要下載 [!DNL DbVisualizer] 案頭應用程式或如需詳細資訊，請參閱 [正式 [!DNL DbVisualizer] 檔案](https://www.dbvis.com/download/).

取得連線所需的認證 [!DNL  DbVisualizer] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前無法存取查詢工作區，請聯絡您的組織管理員。

## 建立資料庫連線 {#connect-database}

在本機電腦上安裝案頭應用程式後，請依照官方BDVisualizer指示執行 [建立新的資料庫連線](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

一旦您選取 **[!DNL PostgreSQL]** 從 [!DNL Connections] 清單，一個 [!DNL Object View] 索引標籤以取得新的 [!DNL PostgreSQL] 連線出現。

### 設定連線的驅動程式屬性 {#properties}

從 [!DNL PostgreSQL] 物件檢視標籤，選取 **[!DNL Properties]** 標籤，後面接著 **[!DNL Driver Properties]** 瀏覽側邊欄中的。 更多相關資訊 [驅動程式屬性](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) 請參閱官方檔案。

接下來，輸入下表所述的驅動程式屬性。

>[!IMPORTANT]
>
>若要將DBVisualizer與Adobe Experience Platform連線，您必須啟用使用SSL。 請參閱 [SSL模式檔案](./ssl-modes.md) 瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用連線 `verify-full` SSL模式。

| 属性 | 描述 |
| ------ | ------ |
| `PGHOST` | 的主機名稱 [!DNL PostgreSQL] 伺服器。 此值是您的Experience Platform **[!UICONTROL 主機] 認證**. |
| `ssl` | 定義SSL值 `1` 以啟用使用SSL。 |
| `sslmode` | 這會控制SSL保護的等級。 建議您使用 `require` 將協力廠商使用者端連線至Adobe Experience Platform時的SSL模式。 此 `require` 模式可確保所有通訊都需要加密，並且信任網路可以連線到正確的伺服器。 不需要伺服器SSL憑證驗證。 |
| `user` | 連線至資料庫的使用者名稱是您的組織ID。 其為英數字串，結尾為 `@Adobe.Org`. 此值是您的Experience Platform **[!UICONTROL 使用者名稱] 認證**. |

使用搜尋列來尋找每個屬性，然後為引數值選取對應的儲存格。 儲存格將以藍色反白顯示。 在值欄位中輸入您的Platform認證，然後選取 **[!DNL Apply]** 以新增驅動程式屬性。

>[!NOTE]
>
>新增秒數 `user` 設定檔，選取 `user` 從引數欄中，然後選取藍色+ （加號）圖示，為每個使用者新增認證。 選取 **[!DNL Apply]** 以新增驅動程式屬性。

此 [!DNL Edited] 欄會顯示核取記號，表示引數值已更新。

### 輸入查詢服務認證 {#query-service-credentials}

若要尋找連線BBVisualizer與查詢服務所需的認證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，然後是 **[!UICONTROL 認證]**. 如需尋找您的檔案的詳細資訊， **主機**， **連線埠**， **資料庫**， **使用者名稱**、和 **密碼** 認證，請閱讀 [認證指南](../ui/credentials.md).

![反白顯示認證和到期認證的「Experience Platform查詢」工作區的「認證」頁面。](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 也會提供不會到期的認證，以允許與協力廠商使用者端進行一次性設定。 請參閱以下檔案： [有關如何產生和使用不會到期的認證的完整指示](../ui/credentials.md#non-expiring-credentials). 如果您想要以一次性設定方式連線BDVisualizer，則必須完成此程式。 此 `credential` 和 `technicalAccountId` 取得的值包含DBVisualizer的值 `password` 引數。

## 身份验证 {#authentication}

若要每次建立連線時都需要使用者ID和密碼式驗證，請導覽至 [!DNL Properties] 標籤並選取 **[!DNL Authentication]** 瀏覽側邊欄中的 [!DNL PostgreSQL].

在「連線驗證」面板中，勾選 **[!DNL Require Userid]** 和 **[!DNL Require Password]** 核取方塊，然後選取 **[!DNL Apply]**. 更多相關資訊 [設定驗證選項](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) 請參閱官方檔案。

## 連線至平台

您可以使用即將到期或未到期的認證建立連線。 若要建立連線，請選取 **[!DNL Connection]** 標籤從 [!DNL PostgreSQL] 「物件檢視」標籤，並為下列設定輸入您的Experience Platform認證。 的補充說明 [設定手動連線](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) 可在官方DBVisualizer網站上取得。

>[!NOTE]
>
>除非在引數說明中註明，否則下表中BDVisualizer所需的全部認證對於到期和未到期認證都是相同的。

| 連線引數 | 描述 |
|---|---|
| **[!UICONTROL 名称]** | 為您的連線建立名稱。 建議您提供方便識別連線的人性化名稱。 |
| **[!UICONTROL 資料庫伺服器]** | 這是您的Experience Platform **[!UICONTROL 主機]** 認證。 |
| **[!UICONTROL 資料庫連線埠]** | 的連線埠 [!DNL Query Service]. 您必須使用連線埠 **80** 或 **5432** 以連線 [!DNL Query Service]. |
| **[!UICONTROL 数据库]** | 使用您的Experience Platform **[!UICONTROL 資料庫]** 認證值： `prod:all`. |
| **[!UICONTROL 資料庫使用者ID]** | 這是您的Platform組織Id。 使用您的Experience Platform **[!UICONTROL 使用者名稱]** 認證值。 ID的格式為 `ORG_ID@AdobeOrg`. |
| **[!UICONTROL 資料庫密碼]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]** 認證。 如果您想要使用不會到期的認證，此值為來自下列專案的串連引數： `technicalAccountID` 和 `credential` 已下載到設定JSON檔案中。 密碼值的格式為：{technicalAccountId}：{credential}。 不會到期的認證的設定JSON檔案是在其初始化期間的一次性下載，Adobe不會保留的副本。 |

輸入所有相關認證後，請選取 **[!DNL Connect]**.

此 [!DNL Connect] 對話方塊會在第一次作業階段時顯示。 輸入您的使用者ID和密碼，然後選取 **[!DNL Connect]**. 記錄中會顯示一則訊息，確認連線成功。

## 后续步骤

現在您已連線 [!DNL DbVisualizer] 替換為 [!DNL Query Service]，您可以使用 [!DNL DbVisualizer] 以寫入查詢。 如需如何寫入和執行查詢的詳細資訊，請參閱 [查詢執行指南](../best-practices/writing-queries.md).
