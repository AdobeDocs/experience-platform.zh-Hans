---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；RStudio；rstudio；連線到查詢服務；
solution: Experience Platform
title: 將RStudio連線至查詢服務
description: 本檔案將逐步說明將R Studio與Adobe Experience Platform Query Service連線的步驟。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Connect [!DNL RStudio] 至查詢服務

本檔案將逐步說明連線的步驟 [!DNL RStudio] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] 現已更名為 [!DNL Posit]. [!DNL RStudio] 產品已重新命名為 [!DNL Posit Connect]， [!DNL Posit Workbench]， [!DNL Posit Package] 經理， [!DNL Posit Cloud]、和 [!DNL Posit Academy].
>
> 本指南假設您已擁有 [!DNL RStudio] 並熟悉其使用方式。 更多關於的資訊 [!DNL RStudio] 您可在以下網址找到： [正式 [!DNL RStudio] 檔案](https://rstudio.com/products/rstudio/).
> 
> 此外，若要使用 [!DNL RStudio] 若使用查詢服務，您必須安裝 [!DNL PostgreSQL] JDBC 4.2驅動程式。 您可以從以下網址下載JDBC驅動程式： [[!DNL PostgreSQL] 官方網站](https://jdbc.postgresql.org/download/).

## 建立 [!DNL Query Service] 中的連線 [!DNL RStudio] 介面

安裝後 [!DNL RStudio]，您必須安裝RJDBC套件。 操作說明 [透過命令列連線資料庫](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) 請參閱官方Posit檔案。

如果使用Mac作業系統，您可以選取 **[!UICONTROL 工具]** 從功能表列，後面接著 **[!UICONTROL 安裝套件]** 下拉式選單中的。 或者，選取 **[!DNL Packages]** 索引標籤從RStudio UI選取 **[!DNL Install]**.

隨即出現快顯視窗，顯示 **[!DNL Install Packages]** 畫面。 確定 **[!DNL Repository (CRAN)]** 已為「 」選取「 」 **[!DNL Install from]** 區段。 的值 **[!DNL Packages]** 應為 `RJDBC`. 確定 **[!DNL Install dependencies]** 「 」已選取。 在確認所有值都正確之後，選取 **[!DNL Install]** 以安裝套件。 現在已安裝RJDBC套件，請重新啟動 [!DNL RStudio] 以完成安裝程式。

晚於 [!DNL RStudio] 已重新啟動，您現在可以連線至查詢服務。 選取 **[!DNL RJDBC]** 封裝於 **[!DNL Packages]** 窗格，然後在主控台中輸入下列命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

位置 `{PATH TO THE POSTGRESQL JDBC JAR}` 代表以下專案的路徑： [!DNL PostgreSQL] 安裝在您電腦上的JDBC JAR。

現在，您可以建立與查詢服務的連線。 在主控台中輸入以下命令：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用連線 `verify-full` SSL模式。

如需尋找資料庫名稱、主機、連線埠和登入證明資料的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找您的認證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後接 **[!UICONTROL 認證]**.

主控台輸出中會出現一則訊息，確認連線至查詢服務。

## 寫入查詢

現在您已連線至 [!DNL Query Service]，您可以撰寫查詢來執行及編輯SQL敘述句。 例如，您可以使用 `dbGetQuery(con, sql)` 執行查詢，其中 `sql` 是要執行的SQL查詢。

以下查詢使用的資料集包含 [體驗事件](../../xdm/classes/experienceevent.md) 和會建立網站的頁面檢視長條圖（在指定裝置的熒幕高度時）。

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

成功的回應會傳回查詢的結果：

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

## 后续步骤

如需如何撰寫和執行查詢的詳細資訊，請閱讀以下指南： [正在執行查詢](../best-practices/writing-queries.md).
