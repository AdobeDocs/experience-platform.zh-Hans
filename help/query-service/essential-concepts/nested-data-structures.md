---
keywords: Experience Platform；查詢服務；查詢服務；巢狀資料結構；巢狀資料；
title: 在查詢服務中使用巢狀資料結構
description: 本檔案提供使用CTAS和INSERT INTO陳述式處理和轉換巢狀資料欄位的工作範例。
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# 在查詢服務中使用巢狀資料結構

Adobe Experience Platform查詢服務支援使用巢狀資料欄位。 企業資料結構的複雜性可能會使轉換或處理這些資料變得複雜。 本檔案提供範例，說明如何建立、處理或轉換具有複雜資料型別（包括巢狀資料結構）的資料集。

查詢服務提供 [!DNL PostgreSQL] 介面，可對Experience Platform管理的所有資料集執行SQL查詢。 Platform支援在表格欄中使用基本或複雜的資料型別，例如結構、陣列、對映和深度巢狀結構、陣列和對映。 資料集也可以包含巢狀結構，其中的欄資料型別可以像巢狀結構陣列一樣複雜，或是對應地圖，其中索引鍵/值組的值可以是具有多個巢狀層級的結構。

## 快速入门

本教學課程需要使用協力廠商PSQL使用者端或查詢編輯器工具，在Experience Platform使用者介面(UI)中撰寫、驗證和執行查詢。 有關如何透過UI執行查詢的完整詳細資訊，請參閱 [查詢編輯器UI指南](../ui/user-guide.md). 如需第三方案頭使用者端可連線至查詢服務的詳細清單，請參閱 [使用者端連線概觀](../clients/overview.md).

您也應該充分瞭解 `INSERT INTO` 和 `CTAS` 語法。 關於其使用的特定資訊可在以下網址找到： [`INSERT INTO`](../sql/syntax.md#insert-into) 和 [`CTAS`](../sql/syntax.md#create-table-as-select) 的區段 [SQL語法參考檔案](../sql/syntax.md).

## 建立資料集

查詢服務提供以選取方式建立表格(`CTAS`)功能，可根據 `SELECT` 陳述式，或在此案例中一樣，透過對Adobe Experience Platform中現有XDM結構的參考來進行。 以下顯示的是的XDM結構描述 `Final_subscription` 已針對此範例建立。

![final_subscription綱要的圖表。](../images/best-practices/final-subscription-schema.png)

下列範例示範用來建立 `final_subscription_test2` 資料集。 `final_subscription_test2` 是使用 `Final_subscription` 結構描述。 系統會使用「 」從來源擷取資料 `SELECT` 子句以填入某些資料列。

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

在初始資料集中 `final_subscription_test2`，結構資料型別會用來包含這兩個 `subscription` 欄位和 `userid` 每個使用者所獨有的。 此 `subscription` 欄位說明使用者的產品訂閱。 可能有多個訂閱，但表格只能包含每列一個訂閱的資訊。

## 使用INSERT INTO來更新巢狀資料欄位

晚於 `final_subscription_test2` 已建立資料集， `INSERT INTO` 陳述式用於將其他資料附加至表格。 複製資料時，來源和目標中的資料型別必須相符。 或者，來源資料型別必須是 `CAST` 至目標資料型別。 然後使用以下SQL將增量資料新增到目標資料集中。

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## 處理巢狀資料集中的資料

若要從資料集中找出使用者的作用中訂閱清單，您必須編寫查詢，將陣列元素分隔成多個列和欄。 若要這麼做，您必須先瞭解資料模型的形狀，因為訂閱資訊會儲存在巢狀於資料集中的陣列中。

PSQL `\d` 命令可用來逐層導覽至所需的訂閱資料。 這些表格說明 `final_subscription_test2` 資料集。 複雜的資料型別不是典型的型別值（例如文字、布林值、時間戳記等），因此一眼就能辨識。

| 栏目 | 类型 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

下一欄的欄位會使用 `\d final_subscription_test2__lumaservices3` 命令。

| 栏目 | 类型 |
|---------|-------|
| `userid` | 文本 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 是結構元素的陣列。 其欄位會使用 `\d _lumaservices3_subscription_e[]` 命令。

| 栏目 | 类型 |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | 文本 |
| `offer_id` | 文本 |
| `subscription_id` | 文本 |

若要查詢訂閱的巢狀欄位，您必須先分隔 `subscription` 陣列化成多列，並使用explode函式傳回結果。 下列SQL範例會根據下列條件傳回使用者的使用中訂閱 `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

此簡化的範例解決方案僅允許一位使用中的使用者訂閱。 實際上，單一使用者可以有許多作用中的訂閱。 下列範例將先前的查詢修改為允許多個同時作用中訂閱。

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

儘管此SQL範例的複雜性不斷增加， `collect_list` 對於使用中訂閱，無法保證輸出的順序會與來源相同。 若要為使用者建立作用中訂閱清單，您必須使用GROUP BY或隨機排列來彙總清單的結果。

## 后续步骤

閱讀本檔案後，您現在瞭解如何在Adobe Experience Platform查詢服務中處理或轉換使用複雜資料型別的資料集。 請參閱 [查詢執行指南](../best-practices/writing-queries.md) 以取得在Data Lake內對資料集執行SQL查詢的詳細資訊。
