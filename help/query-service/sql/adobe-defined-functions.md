---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；adobe定義的函式；sql；
solution: Experience Platform
title: 查詢服務中的Adobe定義SQL函式
description: 本檔案提供Adobe Experience Platform查詢服務中可用的Adobe定義函式的資訊。
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 3%

---

# 查詢服務中的Adobe定義SQL函式

Adobe定義的函式（在此稱為ADF）是Adobe Experience Platform查詢服務中預先建立的函式，可協助您執行以下常見的業務相關工作 [!DNL Experience Event] 資料。 這些包括下列函式 [工作階段化](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) 和 [歸因](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) 如同Adobe Analytics中的那些。

本檔案提供Adobe定義函式的資訊，這些函式可在 [!DNL Query Service].

>[!NOTE]
>
>Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。

## 視窗函式 {#window-functions}

大多數的商業邏輯要求收集客戶的接觸點並在時間之前訂購它們。 此支援由以下人員提供 [!DNL Spark] SQL的視窗函式形式。 視窗函式是標準SQL的一部分，並且受到許多其他SQL引擎的支援。

視窗函式會更新彙總，並為已訂購子集中的每個資料列傳回單一料號。 最基本的彙總函式是 `SUM()`. `SUM()` 會取得您的列，並提供一個總計。 如果您改為套用 `SUM()` 對於視窗，將其轉換為視窗函式，您會收到每列的累計總和。

大部分 [!DNL Spark] SQL輔助程式是視窗函式，會更新視窗中每一資料列，並加入該資料列的狀態。

**查詢語法**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 根據欄或可用欄位的一組子列。 | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 用來排序子集或列的欄或可用欄位。 | `ORDER BY timestamp` |
| `{FRAME}` | 分割區中資料列的子群組。 | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 工作階段化

當您使用時 [!DNL Experience Event] 源自網站、行動應用程式、互動式語音回應系統或任何其他客戶互動頻道的資料，如果事件可依相關活動期間分組，則會有所幫助。 通常，您有特定意圖可推動您的活動，例如研究產品、支付帳單、檢查帳戶餘額、填寫應用程式等。

此分組或資料工作階段化有助於建立事件關聯，以發掘更多有關客戶體驗的內容。

如需Adobe Analytics中工作階段化的詳細資訊，請參閱以下檔案： [內容感知作業](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**查詢語法**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{EXPIRATION_IN_SECONDS}` | 事件之間符合目前工作階段結束和新工作階段開始所需的秒數。 |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**结果**

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

對於給定的範例查詢，結果會提供在 `session` 欄。 此 `session` 欄由下列元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 目前記錄與先前記錄之間的時間差異（以秒為單位）。 |
| `{NUM}` | 「 」中定義之索引鍵的唯一工作階段編號，從1開始 `PARTITION BY` 視窗函式的。 |
| `{IS_NEW}` | 用於識別記錄是否為工作階段第一個的布林值。 |
| `{DEPTH}` | 工作階段中目前記錄的深度。 |

### SESS_START_IF

此查詢會根據目前時間戳記和指定的運算式，傳回目前列的工作階段狀態，並以目前列開始新的工作階段。

**查詢語法**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{TEST_EXPRESSION}` | 您要用來檢查資料欄位的運算式。 例如：`application.launches > 0`。 |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**结果**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

對於給定的範例查詢，結果會提供在 `session` 欄。 此 `session` 欄由下列元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 目前記錄與先前記錄之間的時間差異（以秒為單位）。 |
| `{NUM}` | 「 」中定義之索引鍵的唯一工作階段編號，從1開始 `PARTITION BY` 視窗函式的。 |
| `{IS_NEW}` | 用於識別記錄是否為工作階段第一個的布林值。 |
| `{DEPTH}` | 工作階段中目前記錄的深度。 |

### SESS_END_IF

此查詢會根據目前時間戳記和指定的運算式，傳回目前列的工作階段狀態，結束目前的工作階段，並在下一列開始新的工作階段。

**查詢語法**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{TEST_EXPRESSION}` | 您要用來檢查資料欄位的運算式。 例如：`application.launches > 0`。 |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**结果**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

對於給定的範例查詢，結果會提供在 `session` 欄。 此 `session` 欄由下列元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 目前記錄與先前記錄之間的時間差異（以秒為單位）。 |
| `{NUM}` | 「 」中定義之索引鍵的唯一工作階段編號，從1開始 `PARTITION BY` 視窗函式的。 |
| `{IS_NEW}` | 用於識別記錄是否為工作階段第一個的布林值。 |
| `{DEPTH}` | 工作階段中目前記錄的深度。 |


## 路径分析

路徑分析可用來瞭解客戶的參與深度、確認體驗的預期步驟是否如預期運作，以及識別影響客戶的潛在痛點。

下列ADF支援從先前和後續的關係建立路徑檢視。 您可以建立先前的頁面和後續頁面，或逐步執行多個事件以建立路徑。

### 上一頁

決定視窗內距離特定欄位已定義步數的先前值。 請注意，在範例中， `WINDOW` 函式設定了以下框架： `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 設定ADF檢視目前列和所有後續列。

**查詢語法**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{KEY}` | 事件中的欄或欄位。 |
| `{SHIFT}` | （選用）遠離目前事件的事件數。 預設值為1。 |
| `{IGNORE_NULLS}` | （選用）表示是否為空值的布林值 `{KEY}` 值應被忽略。 預設值為 `false`. |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**结果**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

對於給定的範例查詢，結果會提供在 `previous_page` 欄。 內的值 `previous_page` 欄是根據 `{KEY}` 用於ADF。

### 下一页

在視窗內決定某個特定欄位的下一個值，以及離開該欄位的定義步數。 請注意，在範例中， `WINDOW` 函式設定了以下框架： `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 設定ADF檢視目前列和所有後續列。

**查詢語法**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{KEY}` | 事件中的欄或欄位。 |
| `{SHIFT}` | （選用）遠離目前事件的事件數。 預設值為1。 |
| `{IGNORE_NULLS}` | （選用）表示是否為空值的布林值 `{KEY}` 值應被忽略。 預設值為 `false`. |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**结果**

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

對於給定的範例查詢，結果會提供在 `previous_page` 欄。 內的值 `previous_page` 欄是根據 `{KEY}` 用於ADF。

## 時間間隔

「時間間隔」可讓您在事件發生之前或之後，探索特定時段內的潛在客戶行為。

### 上一個相符專案之間的時間

此查詢會傳回一個數字，代表自出現上一個相符事件以來的時間單位。 如果找不到相符的事件，則會傳回null。

**查詢語法**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件填入的資料集中找到時間戳記欄位。 |
| `{EVENT_DEFINITION}` | 限定上一個事件的運算式。 |
| `{TIME_UNIT}` | 輸出單位。 可能的值包括天、小時、分鐘和秒。 根據預設，該值為秒。 |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**结果**

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

對於給定的範例查詢，結果會提供在 `average_minutes_since_registration` 欄。 內的值 `average_minutes_since_registration` 欄是指目前和先前事件之間的時間差異。 時間單位之前定義於 `{TIME_UNIT}`.

### 下一個相符專案之間的時間

此查詢傳回負數，代表下一個相符事件之後的時間單位。 如果找不到相符的事件，則會傳回null。

**查詢語法**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件填入的資料集中找到時間戳記欄位。 |
| `{EVENT_DEFINITION}` | 限定下一個事件的運算式。 |
| `{TIME_UNIT}` | （選用）輸出單位。 可能的值包括天、小時、分鐘和秒。 根據預設，該值為秒。 |

內引數的說明 `OVER()` 函式位於 [視窗函式區段](#window-functions).

**範例查詢**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**结果**

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

對於給定的範例查詢，結果會提供在 `average_minutes_until_order_confirmation` 欄。 內的值 `average_minutes_until_order_confirmation` 欄是目前事件與下一個事件之間的時間差異。 時間單位之前定義於 `{TIME_UNIT}`.

## 后续步骤

使用此處所述的函式，您可以撰寫查詢來存取您自己的查詢 [!DNL Experience Event] 資料集使用 [!DNL Query Service]. 如需有關在中編寫查詢的詳細資訊 [!DNL Query Service]，請參閱以下說明檔案： [建立查詢](../best-practices/writing-queries.md).

## 其他资源

以下影片說明如何在Adobe Experience Platform介面和PSQL使用者端中執行查詢。 此外，影片也使用涉及XDM物件中個別屬性的範例、使用Adobe定義的函式，以及使用CREATE TABLE AS SELECT (CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
