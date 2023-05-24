---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查閱者；查閱者；連線到查詢服務；
solution: Experience Platform
title: 將查閱者連線至查詢服務
description: 本檔案將逐步說明將Looker與Adobe Experience Platform查詢服務連線的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] 至查詢服務

本檔案說明連線的步驟 [!DNL Looker] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Looker] 並熟悉如何導覽其介面。 更多關於的資訊 [!DNL Looker] 您可在以下網址找到： [正式 [!DNL Looker] 檔案](https://docs.looker.com/).

## 建立新的資料庫連線 {#create-connection}

登入之後 [!DNL Looker]，選取 **[!DNL Admin]**，後接 **[!DNL Connections]**. 此 [!DNL Connections] 頁面隨即開啟。 於 [!DNL Connections] 頁面，選取 **[!DNL Add Connection]**.

從這裡，輸入下列連線設定的詳細資料。 請參閱以下專案的官方Looker檔案： [建立新資料庫連線的指示和可用屬性的說明](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]：** 連線的名稱。
- **[!DNL Dialect]：** SQL資料庫使用的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]：** 的主機端點及其連線埠 [!DNL Query Service].
- **[!DNL Database]：** 將使用的資料庫。
- **[!DNL Username and Password]：** 將使用的登入認證。 使用者名稱將以下列形式提供 `ORG_ID@AdobeOrg`.
- **SSL**：啟用SSL以確保網路上的安全連線。

若要尋找連線Looker與查詢服務所需的認證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，然後是 **[!UICONTROL 認證]**. 如需尋找您的檔案的詳細資訊， **主機**， **連線埠**， **資料庫**， **使用者名稱**、和 **密碼** 認證，請閱讀 [認證指南](../ui/credentials.md).

![反白顯示認證和到期認證的「Experience Platform查詢」工作區的「認證」頁面。](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 也會提供不會到期的認證，以允許與協力廠商使用者端進行一次性設定。 請參閱以下檔案： [有關如何產生和使用不會到期的認證的完整指示](../ui/credentials.md#non-expiring-credentials). 如果您想要以一次性設定方式連線Looker，則必須完成此程式。 此 `credential` 和 `technicalAccountId` 取得的值包含Looker的值 `password` 引數。

若要瞭解Adobe Experience Platform對協力廠商連線的SSL支援，請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md). 本檔案提供如何使用進行連線的指示 `verify-full` SSL模式。

輸入連線詳細資料後，請選取 **[!DNL Test These Settings]** 以確保您的憑證正常運作。 更多相關資訊 [測試您的連線設定](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) Looker官方檔案中提供。 成功連線後，畫面上會顯示一則訊息，指示您可以連線。 連線成功後，請選取 **[!DNL Add Connection]** 以建立連線。

## 后续步骤

現在您已連線至 [!DNL Query Service]，您可以使用 [!DNL Looker] 以寫入查詢。 如需如何寫入和執行查詢的詳細資訊，請參閱 [running queries指南](../best-practices/writing-queries.md).
