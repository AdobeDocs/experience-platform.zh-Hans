---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；寫入查詢；寫入查詢；
solution: Experience Platform
title: 查詢服務中查詢執行的一般指引
type: Tutorial
description: 本檔案概述在Adobe Experience Platform查詢服務中寫入查詢時需要瞭解的重要細節。
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: adf8da46d09c60b86df16493043efeacbdd24fe2
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 3%

---

# 中查詢執行的一般指引 [!DNL Query Service]

本檔案詳細說明在Adobe Experience Platform中撰寫查詢時需要瞭解的重要細節 [!DNL Query Service].

如需中使用的SQL語法的詳細資訊， [!DNL Query Service]，請閱讀 [SQL語法檔案](../sql/syntax.md).

## 查詢執行模型

Adobe Experience Platform [!DNL Query Service] 有兩種查詢執行模式：互動式和非互動式。 互動式執行用於商業智慧工具中的查詢開發和報表產生，而非互動式則用於大型作業和作業查詢作為資料處理工作流程的一部分。

### 互動式查詢執行

透過提交查詢，能以互動方式執行查詢。 [!DNL Query Service] UI或 [透過連線的使用者端](../clients/overview.md). 執行時 [!DNL Query Service] 透過連線的使用者端，使用中的工作階段會在使用者端和之間執行 [!DNL Query Service] 直到提交的查詢傳回或逾時。

互動式查詢執行有下列限制：

| 参数 | 限制 |
| --------- | ---------- |
| 查詢逾時 | 10 分钟 |
| 傳回的最大列數 | 50,000 |
| 最大並行查詢數 | 5 |

>[!NOTE]
>
>若要覆寫最大列數限制，請包含 `LIMIT 0` （在您的查詢中）。 10分鐘的查詢逾時仍然適用。

依預設，互動式查詢的結果會傳回至使用者端，並會 **not** 持續存在。 為了將結果作為資料集儲存在中 [!DNL Experience Platform]，查詢必須使用 `CREATE TABLE AS SELECT` 語法。

### 非互動式查詢執行

透過提交的查詢 [!DNL Query Service] API是以非互動方式執行。 非互動式執行意味著 [!DNL Query Service] 會接收API呼叫，並依接收順序執行查詢。 非互動式查詢一律會在中產生新資料集 [!DNL Experience Platform] 以接收結果，或將新列插入現有資料集中。

## 存取物件中的特定欄位

若要存取查詢中物件內的欄位，您可以使用點標籤法(`.`)或方括弧標籤法(`[]`)。 下列SQL陳述式使用點標籤法來遍歷 `endUserIds` 物件向下延伸至 `mcid` 物件。

>[!NOTE]
>
>Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

下列SQL陳述式使用方括弧記號來遍歷 `endUserIds` 物件向下延伸至 `mcid` 物件。

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

>[!NOTE]
>
>由於每個記號型別會傳回相同的結果，因此您選擇使用的結果取決於您的偏好。

上述兩個查詢範例都傳回平面化的物件，而不是單一值：

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

傳回的 `endUserIds._experience.mcid` 物件包含下列引數的對應值：

- `id`
- `namespace`
- `primary`

當欄僅宣告為向下至物件時，會將整個物件傳回為字串。 若只要檢視ID，請使用：

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 引號

單引號、雙引號及後引號在Query Service查詢中的使用方式不同。

### 單引號

單引號(`'`)來建立文字字串。 例如，它可用於 `SELECT` 陳述式傳回結果中的靜態文字值，以及 `WHERE` 子句來評估資料行內容。

下列查詢會宣告靜態文字值(`'datasetA'`)代表欄：

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

下列查詢使用單引號字串(`'homepage'`)的WHERE子句中傳回特定頁面的事件。

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### 雙引號

雙引號(`"`)來宣告含空格的識別碼。

當一欄的識別碼中包含空格時，下列查詢會使用雙引號來傳回指定欄的值：

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>雙引號 **無法** 與點標籤法欄位存取權搭配使用。

### 後引號

後引號 `` ` `` 用於逸出保留的欄名稱 **僅限** 使用點標籤法語法時。 例如，從 `order` 是SQL中的保留字，您必須使用反引號來存取欄位 `commerce.order`：

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

後引號也可用來存取以數字開頭的欄位。 例如，若要存取欄位 `30_day_value`，您需要使用後引號標籤法。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

後引號為 **not** 如果您使用方括弧標籤法則需要。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 檢視表格資訊

連線到Query Service後，您可以使用 `\d` 或 `SHOW TABLES` 命令。

### 標準表格檢視

此 `\d` 命令顯示標準 [!DNL PostgreSQL] 檢視以列出表格。 此命令的輸出範例如下所示：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 詳細的表格檢視

`SHOW TABLES` command是自訂命令，可提供有關表格的詳細資訊。 此命令的輸出範例如下所示：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 結構描述資訊

若要檢視表格中綱要的詳細資訊，您可以使用 `\d {TABLE_NAME}` 命令，其中 `{TABLE_NAME}` 是要檢視其綱要資訊的表格名稱。

以下範例顯示 `luma_midvalues` 表格，可透過以下方式檢視： `\d luma_midvalues`：

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

此外，您可以將欄的名稱附加至表格名稱，以取得特定欄的詳細資訊。 這會以格式撰寫 `\d {TABLE_NAME}_{COLUMN}`.

以下範例顯示的其他資訊 `web` 欄，並使用下列命令叫用和： `\d luma_midvalues_web`：

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 加入資料集

您可以將多個資料集聯結在一起，以將其他資料集的資料包含在查詢中。

以下範例將連線以下兩個資料集(`your_analytics_table` 和 `custom_operating_system_lookup`)並建立 `SELECT` 前50名作業系統（依頁面檢視次數）的陳述式。

**查询**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**结果**

| 作業系統 | 頁面檢視 |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| 行動iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003 和 XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## 重复数据删除

查詢服務支援重複資料刪除，或從資料中移除重複資料列。 如需重複資料刪除的詳細資訊，請閱讀 [查詢服務重複資料刪除指南](../essential-concepts/deduplication.md).

## 查詢服務中的時區計算

查詢服務會使用UTC時間戳記格式，標準化Adobe Experience Platform中的持續資料。 如需有關如何將時區要求轉換為UTC時間戳記的詳細資訊，請參閱 [有關如何將時區變更為UTC時間戳記及從UTC時間戳記變更的常見問題集區段](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## 后续步骤

閱讀本檔案後，您已經瞭解使用撰寫查詢時的一些重要考量 [!DNL Query Service]. 如需有關如何使用SQL語法來撰寫您自己的查詢的詳細資訊，請參閱 [SQL語法檔案](../sql/syntax.md).

如需可在Query Service中使用的更多查詢範例，請閱讀以下使用案例檔案：

- [Analytics深入分析](../use-cases/analytics-insights.md)
- [建立事件的趨勢報表](../use-cases/trended-report-of-events.md)
- [檢視訪客的統計報表](../use-cases/roll-up-report-of-a-visitor.md)
- [列出使用者的頁面檢視](../use-cases/list-visitor-sessions.md)
- [依訪客的頁面檢視次數列出訪客](../use-cases/visitors-by-number-of-page-views.md)
