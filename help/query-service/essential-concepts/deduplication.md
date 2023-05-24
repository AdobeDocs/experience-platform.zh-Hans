---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；重複資料刪除；重複資料刪除；
solution: Experience Platform
title: 查詢服務中的重複資料刪除
type: Tutorial
description: 本檔案概述子選取和完整範例查詢範例，用於去除三個常見使用案例（體驗事件、購買和量度）的重複資料。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 中的重複資料刪除 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支援重複資料刪除。 當需要從計算中移除整個列或忽略特定欄位集（因為列中只有部分資料是重複資訊）時，可以執行重複資料刪除。

去重複化通常涉及使用 `ROW_NUMBER()` 在視窗中隨著有序的時間對ID （或一對ID）執行函式，這會傳回代表偵測到重複專案次數的新欄位。 時間通常以表示 [!DNL Experience Data Model] (XDM) `timestamp` 欄位。

當 `ROW_NUMBER()` 是 `1`，即指原始例項。 一般而言，這是您想要使用的例項。 這通常會在子選取的範圍內完成，而重複資料刪除會在較高層級完成 `SELECT` 例如執行彙總計數。

重複資料刪除使用案例可以是全域的，或限製為單一使用者或一般使用者ID，在 `identityMap`.

本檔案概述如何針對三個常見使用案例執行重複資料刪除：體驗事件、購買和量度。

每個範例都包含範圍、視窗索引鍵、重複資料刪除方法的大綱，以及完整SQL查詢。

## 體驗事件 {#experience-events}

如果出現重複的體驗事件，您可能會想要忽略整列。

>[!CAUTION]
>
>中有許多資料集 [!DNL Experience Platform]包括Adobe Analytics Data Connector產生的專案，已套用Experience-Event層級的重複資料刪除。 因此，重新套用此層級的重複資料刪除並無必要，而且會減慢查詢速度。
>
>請務必瞭解資料集的來源，並知道是否已套用體驗事件層級的重複資料刪除。 對於任何串流的資料集(例如來自Adobe Target的資料集)，您可以 **將** 需要套用體驗事件層級的重複資料刪除，因為這些資料來源具有「至少一次」語意。

**範圍：** 全域

**視窗索引鍵：** `id`

### 重複資料刪除範例

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### 完整範例

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## 购买 {#purchases}

如果您有重複購買專案，您可能會想要保留大部分的 [!DNL Experience Event] 列，但忽略與購買相關聯的欄位(例如 `commerce.orders` 量度)。 購買包含購買ID的特殊欄位，即 `commerce.order.purchaseID`.

建議使用 `purchaseID` ，因為這是XDM中購買ID的標準語意欄位。 建議使用訪客範圍來移除重複的購買資料，因為查詢的速度比使用全域範圍來得快，而且購買ID不太可能跨多個訪客ID重複。

**範圍：** 訪客

**視窗索引鍵：** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### 重複資料刪除範例

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

>[!NOTE]
>
>在某些情況下，原始Analytics資料在各個訪客ID間會有重複的購買ID，因此 **五月** 需要對所有訪客執行購買ID重複計數。 當購買ID不存在時，此方法需要您納入條件，而使用事件ID來儘可能快地保留查詢。

### 完整範例

以下範例使用condition子句，在購買ID不存在的情況下使用事件ID。

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## 量度 {#metrics}

如果您的量度使用選用的唯一ID，且系統出現該ID的重複專案，您可能會想要忽略該量度值，並保留體驗事件的其餘部分。

在XDM中，幾乎所有量度都使用 `Measure` 包含選用的資料型別 `id` 可用於重複資料刪除的欄位。

**範圍：** 訪客

**視窗索引鍵：** identityMap[$NAMESPACE]Measure物件的.id和id

### 重複資料刪除範例

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### 完整範例

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## 后续步骤

本檔案提供重複資料刪除的範例，並概述如何在查詢服務中執行重複資料刪除。 如需使用查詢服務撰寫查詢時的最佳實務，請參閱 [撰寫查詢指南](../best-practices/writing-queries.md).
