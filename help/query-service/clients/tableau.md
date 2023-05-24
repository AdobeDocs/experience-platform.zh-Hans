---
keywords: Experience Platform；首頁；熱門主題；tableau；Tableau；查詢服務；查詢服務；連線到查詢服務；
solution: Experience Platform
title: 将 Tableau 连接到查询服务
description: 本檔案將逐步說明連線Tableau與Adobe Experience Platform查詢服務的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connect [!DNL Tableau] 至查詢服務

本檔案提供連線的相關資訊 [!DNL Tableau] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Tableau] 並熟悉如何導覽其介面。 更多關於的資訊 [!DNL Tableau] 您可在以下網址找到： [正式 [!DNL Tableau] 檔案](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

操作說明 [使用Tableau連線到PostgreSQL伺服器](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 可從官方Tableau網站取得。 連線設定的對話方塊出現後，請在引數欄位中輸入您的Platform憑證以連線Adobe Experience Platform。 以下列出必要的連線引數清單。

| 連線引數 | 描述 |
|---|---|
| **[!DNL Server]** | SFTP儲存位置的位址。 使用Experience Platform的值 **[!UICONTROL 主機]** 認證。 |
| **[!DNL Port]:** | 的連線埠 [!DNL Query Service]. 您必須使用連線埠 **80** 或 **5432** 以連線 [!DNL Query Service]. |
| **[!DNL Database]** | 您要存取的資料庫。 使用Experience Platform的值 **[!UICONTROL 資料庫]** 認證： `prod:all`. |
| **[!DNL Authentication]:** | 您選擇的證明使用者身分的方法。 建議您選取 [!DNL Username and Password] 從下拉式選單的可用選項中選取。 |
| **[!DNL Username]** | 這是您的平台組織ID。 使用Experience Platform的值 **[!UICONTROL 使用者名稱]** 認證。 ID的格式為 `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]** 認證。 如果您想要使用不會到期的認證，此值為來自下列專案的串連引數： `technicalAccountID` 和 `credential` 已下載到設定JSON檔案中。 密碼值的格式為：{technicalAccountId}：{credential}。 不會到期的認證的設定JSON檔案是在其初始化期間的一次性下載，Adobe不會保留的副本。 |

如需尋找您的使用者名稱、密碼和登入憑證的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找您的認證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後接 **[!UICONTROL 認證]**.

確定您已核取 **[!UICONTROL 需要SSL]** 方塊。 請參閱 [SSL模式檔案](./ssl-modes.md) 瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援。

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以提高其可用性，並減少擷取、分析、轉換和報告資料所需的工作量。 請參閱以下說明檔案：[`FLATTEN` 功能](../essential-concepts/flatten-nested-data.md) 以取得連線至資料庫時如何啟用此設定的說明。

填寫完您的所有認證後，請確認您的設定以繼續。 您現在已連線Adobe Experience Platform。

## 后续步骤

現在您已連線至 [!DNL Query Service]，您可以使用 [!DNL Tableau] 以寫入查詢。 如需如何撰寫和執行查詢的詳細資訊，請閱讀以下指南： [正在執行查詢](../best-practices/writing-queries.md).
