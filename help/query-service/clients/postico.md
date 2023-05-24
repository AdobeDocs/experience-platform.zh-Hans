---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；postico；Postico；連線到查詢服務；
solution: Experience Platform
title: 將Postico連線到查詢服務
description: 本檔案包含安裝Adobe Experience Platform查詢服務之備份使用者端Postico的連結。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connect [!DNL Postico] 至查詢服務(Mac)

本檔案說明連線的步驟 [!DNL Postico] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Postico] 並熟悉如何導覽其介面。 更多關於的資訊 [!DNL Postico] 您可在以下網址找到： [正式 [!DNL Postico] 檔案](https://eggerapps.at/postico/docs).
> 
> 此外， [!DNL Postico] 是 **僅限** 可在macOS裝置上使用。

若要連線 [!DNL Postico] 若要查詢服務，請開啟 [!DNL Postico] 並選取 **[!DNL New Favorite]**. 連線設定對話方塊隨即顯示。 從這裡，您可以輸入引數值來與Adobe Experience Platform連線。 輸入下列的連線設定。 操作說明 [使用Postico連線到PostgreSQL伺服器](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 也可從Postico官方網站取得。

| 連線引數 | 描述 |
|---|---|
| **[!DNL Host]:** | PostgreSQL伺服器的主機名稱。 |
| **[!DNL Port]:** | 的連線埠 [!DNL Query Service]. 您必須使用連線埠 **80** 或 **5432** 以連線 [!DNL Query Service]. |
| **[!DNL User]** | 為您的特定連線建立名稱。 將欄位留空將使用您的Mac登入名稱。 |
| **[!DNL Password]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]** 認證。 如果您想要使用不會到期的認證，此值為來自下列專案的串連引數： `technicalAccountID` 和 `credential` 已下載到設定JSON檔案中。 密碼值的格式為：{technicalAccountId}：{credential}。 不會到期的認證的設定JSON檔案是在其初始化期間的一次性下載，Adobe不會保留的副本。 |
| **[!DNL Database]** | 使用您的Experience Platform **[!UICONTROL 資料庫]** 認證值： `prod:all`. |

如需尋找資料庫名稱、主機、連線埠和登入證明資料的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找您的認證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後接 **[!UICONTROL 認證]**.

插入認證後，選取 **[!DNL Connect]** 以連線查詢服務。

連線到Platform後，您將可以看到先前使用Query Service建立的所有關係清單。

## 建立SQL敘述句

若要建立新的SQL查詢，請選取 **[!DNL SQL Query]** 從側邊欄中。 或者，使用鍵盤快速鍵(⇧⌘T)瀏覽至查詢檢視並輸入您要執行的查詢。 完成後，選取 **[!DNL Execute Statement]** 以執行查詢。 此時會出現一個表格，其中包含已完成查詢執行的結果。

如需下列專案的詳細資訊，請參閱正式Postico檔案： [使用查詢檢視](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## 后续步骤

現在您已連線至 [!DNL Query Service]，您可以使用 [!DNL Postico] 以寫入查詢。 如需如何寫入和執行查詢的詳細資訊，請參閱 [running queries指南](../best-practices/writing-queries.md).
