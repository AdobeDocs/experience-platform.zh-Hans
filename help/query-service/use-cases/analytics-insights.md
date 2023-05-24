---
title: 網頁和行動互動的Analytics深入分析
description: 本檔案說明如何使用查詢服務，從擷取的Adobe Analytics資料建立可操作分析。
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# 網頁和行動互動的Analytics深入分析

Adobe Experience Platform可讓您使用Experience Data Model (XDM)欄位從Adobe Analytics報表套裝擷取資料，以填入資料集。 已修改此分析資料，以符合 [!DNL XDM ExperienceEvent] 類別。 然後，Query Service可以透過執行SQL查詢來利用此資料，從使用者在數位平台上的行為產生有價值的深入分析。

本檔案提供各種範例SQL查詢，示範從Web和行動Analytics資料建立深入分析時的常見使用案例。

請參閱 [Analytics欄位對應檔案](../../sources/connectors/adobe-applications/mapping/analytics.md) 以取得擷取和對應analytics資料的詳細資訊。

## 快速入门

對於以下每個使用案例，都會提供引數化SQL查詢範例作為範本供您自訂。 提供引數到任何您看到的位置 `{ }` 在您想要評估之資料集、eVar、事件或時間範圍的SQL範例中。

## 目标

下列範例顯示用於分析Adobe Analytics資料的常見使用案例的SQL查詢。

### 產生指定日期每小時的訪客計數

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 識別指定日期檢視次數最多的10個頁面

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### 識別10位最活躍的使用者

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 根據使用者活動，識別10個最理想的城市

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 識別檢視次數最多的10種產品

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 識別最高的10筆訂單收入

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
