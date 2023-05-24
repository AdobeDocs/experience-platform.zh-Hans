---
title: 歸因分析
description: 本檔案說明如何使用查詢服務，根據首次接觸和上次接觸的行銷歸因模型，建立行銷成效測量技術。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# 歸因分析

歸因是一種分析性概念，可協助判斷對業務銷售或轉換有貢獻的行銷策略，例如管道、優惠方案和訊息。 此概念會評估消費者歷程（客戶與公司互動以實現目標的過程），此歷程會根據客戶接觸點（客戶與您的品牌互動的任何時間）導致購買或贏取。 透過歸因分析，行銷人員可評估連結至潛在客戶的管道投資報酬率。

## 快速入门

本檔案中的SQL範例是常與Adobe Analytics資料搭配使用的查詢。 本教學課程需要您實際瞭解下列元件：

* [報告套裝資料的Adobe Analytics來源聯結器總覽](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Analytics欄位對應檔案](../../sources/connectors/adobe-applications/mapping/analytics.md) 提供擷取及對應分析資料以供查詢服務使用的詳細資訊。
* [Attribution IQ概觀](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [Adobe Analytics歸因面板指南](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html).

內引數的說明 `OVER()` 函式位於 [視窗函式區段](../sql/adobe-defined-functions.md#window-functions). 此 [Adobe行銷與商務辭彙表](https://business.adobe.com/glossary/index.html) 可能也有用。

對於以下每個使用案例，都會提供引數化SQL查詢範例作為範本供您自訂。 提供引數到任何您看到的位置 `{ }` 在您想要評估的SQL範例中。

## 目标

歸因使用案例使用Adobe Analytics資料，協助將客戶動作與成功結果建立關聯。 此關聯是瞭解影響客戶體驗的因素的重要部分。 歸因分析資料可用於瞭解客戶在客戶歷程中接觸點的重要性。

本檔案包含的查詢範例支援各種使用案例，適用於具有不同到期日設定的首次接觸和上次接觸歸因。 本指南說明下列重要概念：

* 首次接觸和上次接觸歸因。
* 首次接觸和上次接觸歸因以及到期逾時。
* 具有到期條件的首次接觸和上次接觸歸因。

## 歸因查詢引數 {#attribution-query-parameters}

下表提供用於首次接觸和上次接觸歸因查詢的引數及其說明的劃分：

| 参数 | 描述 |
|---|---|
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標通道的欄或欄位。 |
| `{EXP_TIMEOUT}` | 頻道事件之前的時間視窗（以秒為單位），可供查詢搜尋首次接觸事件。 |
| `{EXP_CONDITION}` | 決定管道到期點的條件。 |
| `{EXP_BEFORE}` | 表示管道在指定條件之前或之後到期的布林值， `{EXP_CONDITION}`，即符合。 這主要是針對工作階段的到期條件啟用，以確保不會從先前的工作階段中選取首次接觸。 預設情況下，此值設定為 `false`. |

## 查詢結果欄元件 {#query-result-column-components}

歸因查詢的結果提供在 `first_touch` 或 `last_touch` 欄。 這些欄由下列元件組成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 此 `{CHANNEL_NAME}`，在Azure Data Factory (ADF)中輸入為標籤。 |
| `{VALUE}` | 值來自 `{CHANNEL_VALUE}` 這是指定範圍內的最後一次接觸 `{EXP_TIMEOUT}` 間隔 |
| `{TIMESTAMP}` | 的時間戳記 [!DNL Experience Event] 上次接觸發生位置 |
| `{FRACTION}` | 上次接觸的歸因，以小數點表示。 |

### 首次接觸歸因 {#first-touch}

首次接觸歸因會100%將成功結果的責任歸於消費者遇到的初始管道。 此SQL範例用於強調導致後續一系列客戶動作的互動。

以下查詢會傳回首次接觸歸因值，以及目標中管道的詳細資料 [!DNL Experience Event] 資料集。 它也會傳回 `struct` 物件，其中包含每列的首次接觸值、時間戳記和歸因。

>[!NOTE]
>
>Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的引數及其說明的完整清單，請參閱 [歸因查詢引數區段](#attribution-query-parameters).

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**结果**

在下列結果中，初始追蹤程式碼 `em:946426` 取自 [!DNL Experience Event] 資料集。 此追蹤程式碼會歸因於100% (`1.0`)，因為這是第一次互動。

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

結果劃分顯示於 `first_touch` 欄，請參閱 [欄元件區段](#query-result-column-components).

### 上次接觸歸因 {#second-touch}

上次接觸歸因會100%將成功結果的責任歸於消費者遇到的最後一個管道。 此SQL範例用於強調一系列客戶動作中的最終互動。

查詢會傳回上次接觸歸因值，以及目標中管道的詳細資料 [!DNL Experience Event] 資料集。 它也會傳回 `struct` 物件，其中包含每列的上次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**结果**

在下方顯示的結果中，傳回物件中的追蹤程式碼是每個物件中的最後一個互動 [!DNL Experience Event] 記錄。 每個程式碼都有100%的歸因(`1.0`)對客戶動作的責任，因為這是最後一次互動。

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

結果劃分顯示於 `last_touch` 欄，請參閱 [欄元件區段](#query-result-column-components).

### 具有到期條件的首次接觸歸因 {#first-touch-attribution-with-expiration-condition}

此查詢是用來檢視哪些互動導致一部分中發生的一系列客戶動作。 [!DNL Experience Event] 資料集由您選擇的條件所決定。

查詢會傳回目標中單一管道的首次接觸歸因值和詳細資料 [!DNL Experience Event] 資料集，在條件之後或之前到期。 它也會傳回 `struct` 物件，具有針對所選管道傳回的每一列的首次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的引數及其說明的完整清單，請參閱 [歸因查詢引數區段](#attribution-query-parameters).

**範例查詢**

在以下範例中，購買會被記錄(`commerce.purchases.value IS NOT NULL`)在結果中顯示的四天（7月15、21、23和29日）的每一天，100%會歸因每天的初始追蹤程式碼(`1.0`)客戶動作的職責。

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**结果**

```console
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

結果劃分顯示於 `first_touch` 欄，請參閱 [欄元件區段](#query-result-column-components).

### 具有到期逾時的首次接觸歸因 {#first-touch-attribution-with-expiration-timeout}

此查詢用於尋找在選定期間內導致成功客戶動作的互動。

以下查詢會傳回目標中單一管道的首次接觸歸因值和詳細資料 [!DNL Experience Event] 指定時段的資料集。 查詢傳回 `struct` 物件，具有針對所選管道傳回的每一列的首次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的引數及其說明的完整清單，請參閱 [歸因查詢引數區段](#attribution-query-parameters).

**範例查詢**

在以下範例中，每個客戶動作傳回的首次接觸是過去七天內最早的互動(expTimeout = 86400 * 7)。

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**结果**

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

結果劃分顯示於 `first_touch` 欄，請參閱 [欄元件區段](#query-result-column-components).

### 具有到期條件的最後一次接觸歸因 {#last-touch-attribution-with-expiration-condition}

此查詢是用來尋找一部分中一連串客戶動作的最後互動。 [!DNL Experience Event] 資料集由您選擇的條件所決定。

以下查詢會傳回目標中單一管道的上次接觸歸因值和詳細資料 [!DNL Experience Event] 資料集，在條件之後或之前到期。 查詢傳回 `struct` 物件，具有針對所選管道傳回之每列的上次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的引數及其說明的完整清單，請參閱 [歸因查詢引數區段](#attribution-query-parameters).

**範例查詢**

在以下範例中，購買會被記錄(`commerce.purchases.value IS NOT NULL`)在結果中顯示的四天（7月15日、21日、23日和29日）的每一天，100%會歸因每天的最後一個追蹤代碼(`1.0`)客戶動作的職責。

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**範例結果**

```console
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

結果劃分顯示於 `last_touch` 欄，請參閱 [欄元件區段](#query-result-column-components).

### 具有到期逾時的最後一次接觸歸因 {#last-touch-attribution-with-expiration-timeout}

此查詢用於尋找所選時間間隔內的上次互動。 查詢會傳回目標中單一管道的上次接觸歸因值和詳細資料 [!DNL Experience Event] 指定時段的資料集。 查詢傳回 `struct` 物件，具有針對所選管道傳回之每列的上次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的引數及其說明的完整清單，請參閱 [歸因查詢引數區段](#attribution-query-parameters).

**範例查詢**

在以下範例中，每個客戶動作傳回的最後一次接觸是未來七天內的最後一次互動(`expTimeout = 86400 * 7`)。

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**结果**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

結果劃分顯示於 `last_touch` 欄，請參閱 [欄元件區段](#query-result-column-components).
