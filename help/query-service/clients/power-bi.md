---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Power BI；power bi；連線到查詢服務；
solution: Experience Platform
title: 將Power BI連線至查詢服務
description: 本檔案將逐步說明連線Power BI與Adobe Experience Platform查詢服務的步驟。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# Connect [!DNL Power BI] 至查詢服務

本檔案說明連線的步驟 [!DNL Power BI] 使用Adobe Experience Platform查詢服務的案頭。

## 快速入门

本指南要求您已擁有 [!DNL Power BI] 案頭應用程式，並熟悉如何導覽其介面。 若要下載 [!DNL Power BI] 案頭或如需詳細資訊，請參閱 [正式 [!DNL Power BI] 檔案](https://docs.microsoft.com/zh-cn/power-bi/).

>[!IMPORTANT]
>
> 此 [!DNL Power BI] 案頭應用程式為 **僅限** 可在Windows裝置上使用。

取得連線所需的認證 [!DNL Power BI] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前無權存取查詢工作區，請聯絡您的組織管理員。

安裝後 [!DNL Power BI]，您必須安裝 `Npgsql`，適用於PostgreSQL的.NET驅動程式套件。 有關Npgsql的詳細資訊，請參閱 [Npgsql檔案](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>您必須下載v4.0.10或更低版本，因為較新版本會導致錯誤。

在&quot;[!DNL Npgsql GAC Installation]」在自訂設定畫面上，選取 **[!DNL Will be installed on local hard drive]**.

若要確保Npgsql已正確安裝，請先重新啟動電腦，然後再繼續後續步驟。

## Connect [!DNL Power BI] 至查詢服務 {#connect-power-bi}

若要連線 [!DNL Power BI] 若要查詢服務，請開啟 [!DNL Power BI] 並選取 **[!DNL Get Data]** 在頂端功能表中。 接下來，輸入&quot;[!DNL PostgreSQL]」以縮小資料來源清單。 從顯示的結果中，選取 **[!DNL PostgreSQL database]**，後接 **[!DNL Connect]**.

此 [!DNL PostgreSQL] 資料庫對話方塊隨即顯示，要求伺服器和資料庫的值。 操作說明的額外說明 [從Power Query Desktop連線至PostgreSQL資料庫](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) 可在以下官方網站找到： [!DNL PowerBI] 說明檔案。

這些必要的值會從您的Adobe Experience Platform憑證中取得。 若要尋找您的認證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，然後是 **[!UICONTROL 認證]**. 如需尋找資料庫名稱、主機、連線埠和登入證明資料的詳細資訊，請閱讀 [認證指南](../ui/credentials.md).

![「Experience Platform查詢」工作區中反白了「認證」索引標籤和「過期認證」。](../images/clients/power-bi/query-service-credentials-page.png)

在 **[!DNL Server]** 的欄位 [!DNL PostgreSQL database] 對話方塊中，輸入在查詢服務中找到之主機的值 [!UICONTROL 認證] 區段。 對於生產，請新增連線埠 `:80` 至主機字串的結尾。 例如：`made-up.platform-query.adobe.io:80`。

此 **[!DNL Database]** 欄位可以是「all」或資料集表格名稱。 例如：`prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以提高其可用性，並減少擷取、分析、轉換和報告資料所需的工作量。 請參閱以下說明檔案：[`FLATTEN` 功能](../essential-concepts/flatten-nested-data.md) 以取得連線至資料庫時如何啟用此設定的說明。

### 資料連線模式 {#data-connectivity-mode}

接下來，您可以選取 **[!DNL Data Connectivity mode]**. 在 [!DNL PostgreSQL database] 對話方塊，選取 **[!DNL Import]** 後面接著 **[!DNL OK]** 顯示所有可用表格的清單，或選取 **[!DNL DirectQuery]** 直接查詢資料來源，而不將資料直接匯入或複製到中 [!DNL Power BI].

若要進一步瞭解 **[!DNL Import]** 模式，請閱讀以下章節： [匯入表格](#import). 若要深入瞭解 **[!DNL DirectQuery]** 模式，請閱讀以下章節： [查詢資料集而不匯入資料](#direct-query).

選取 **[!DNL OK]** 確認您的資料庫詳細資料之後。

### 身份验证 {#authentication}

確認資料連線模式後，畫面會顯示提示，詢問您的使用者名稱、密碼和應用程式設定。 在此案例中，使用者名稱是您的組織ID，密碼是您的驗證Token。 兩者皆可在「查詢服務認證」頁面上找到。

填入這些詳細資訊，然後選取 **[!DNL Connect]** 以繼續下一個步驟。

## 匯入表格 {#import}

藉由選取 **[!DNL Import]** [!DNL Data Connectivity mode]，則會匯入完整資料集，讓您使用中選取的表格和欄 [!DNL Power BI] 案頭應用程式原樣。

>[!IMPORTANT]
>
>若要檢視自初始匯入後發生的資料變更，您必須重新整理以下範圍內的資料： [!DNL Power BI] 再次匯入完整資料集。

若要匯入表格，請輸入伺服器和資料庫詳細資訊 [如上所述](#connect-power-bi) 並選取 **[!DNL Import]** [!DNL Data Connectivity mode]，後接 **[!DNL OK]**. 此 [!DNL Navigator] 對話方塊出現，顯示所有可用表格的清單。 選取您要預覽的表格，然後 **[!DNL Load]** 將資料集引進Power BI。 表格現在已匯入 [!DNL Power BI].

[有關連線至PowerBi案頭中資料的一般資訊](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) 應用程式可在官方檔案中找到。

### 使用自訂SQL匯入表格

[!DNL Power BI] 和其他協力廠商工具，例如 [!DNL Tableau] 目前不允許使用者匯入巢狀物件，例如平台中的XDM物件。 若要解決此問題， [!DNL Power BI] 可讓您使用自訂SQL來存取這些巢狀欄位，並建立資料的平面化檢視。 [!DNL Power BI] 然後將先前巢狀資料的這個平面化檢視載入為一般表格。

從 [!DNL PostgreSQL database] 對話方塊，選取 **[!DNL Advanced options]** 若要在中輸入自訂SQL查詢 **[!DNL SQL statement]** 區段。 此自訂查詢應該用於將JSON名稱 — 值配對平面化為表格格式。 官方檔案也提供如何操作的資訊 [使用進階選項中的SQL陳述式連線PowerBI](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

輸入自訂查詢後，選取 **[!DNL OK]** 以繼續連線您的資料庫。 請參閱 [驗證](#authentication) 區段，以取得從此部分工作流程連線資料庫的指引。

驗證完成後，平面化資料的預覽會顯示在 [!DNL Power BI] 案頭儀表板做為表格。 伺服器和資料庫名稱會列在對話方塊的頂端。 選取 **[!DNL Load]** 以完成匯入程式。

視覺效果現在可供編輯和匯出 [!DNL Power BI] 案頭應用程式。

## 查詢資料集而不匯入資料 {#direct-query}

此 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查詢資料來源，而不將資料匯入或複製到中 [!DNL Power BI] 案頭。 使用此連線模式，您可以透過UI以目前資料重新整理所有視覺效果。 不過，產生或重新整理視覺效果所需的時間會因基礎資料來源的效能而異。

更多相關資訊 [使用 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) 以及對其功能的全面討論 [連線選項、使用案例和限制](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) 可在以下官方網站找到： [!DNL PowerBI] 說明檔案。

若要使用此 [!DNL Data Connectivity mode]，選取 **[!DNL DirectQuery]** 切換然後 **[!DNL Advanced options]** 若要在中輸入自訂SQL查詢 **[!DNL SQL statement]** 區段。 確定 **[!DNL Include relationship columns]** 「 」已選取。 完成查詢後，請選取 **[!DNL OK]** 以繼續。

會出現查詢的預覽。 選取 **[!DNL Load]** 以檢視查詢的結果。

## 后续步骤

閱讀本檔案後，您現在應瞭解如何連線至 [!DNL Power BI] 可用的案頭應用程式和各種資料連線模式。 如需如何撰寫和執行查詢的詳細資訊，請參閱 [查詢執行指南](../best-practices/writing-queries.md).
