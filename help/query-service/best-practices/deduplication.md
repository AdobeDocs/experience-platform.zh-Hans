---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；重复数据删除；
solution: Experience Platform
title: 查询服务中的重复数据删除
type: Tutorial
description: 本文档概述了用于删除重复的三个常见用例（体验事件、购买和量度）的子选择和完整示例查询示例。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 中的重复数据删除 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支持重复数据删除。 当需要从计算中删除整行或忽略一组特定字段时，可以执行重复数据删除，因为该行中只有一部分数据是重复信息。

重复数据删除通常包括使用 `ROW_NUMBER()` 函数，以获取ID（或一对ID）在订购时间内的值，这会返回一个新字段，表示检测到重复项的次数。 时间通常使用 [!DNL Experience Data Model] (XDM) `timestamp` 字段。

当 `ROW_NUMBER()` is `1`，它是指原始实例。 通常，这是您希望使用的实例。 这通常在子选择中完成，在子选择中，重复数据删除在较高级别中完成 `SELECT` 例如执行聚合计数。

重复数据删除用例可以是全局用例，也可以限制为 `identityMap`.

本文档概述了如何针对三个常见用例执行重复数据删除：体验事件、购买和量度。

每个示例都包括范围、窗口键、重复数据删除方法的大纲以及完整的SQL查询。

## 体验事件 {#experience-events}

如果体验事件重复，您可能希望忽略整行。

>[!CAUTION]
>
>中的许多数据集 [!DNL Experience Platform]，包括Adobe Analytics Data Connector生成的重复数据删除，已应用体验级别的重复数据删除。 因此，不必重新应用此级别的重复数据删除，这会减慢查询速度。
>
>了解数据集的来源，并了解体验事件级别的重复数据删除是否已应用，这一点非常重要。 对于流式处理的任何数据集(例如，来自Adobe Target的数据集)，您 **will** 需要应用体验事件级别的重复数据删除，因为这些数据源具有“至少一次”语义。

**范围：** 全球

**窗口键：** `id`

### 重复数据删除示例

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### 完整示例

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

如果您购买了重复的产品，则可能希望保留 [!DNL Experience Event] 行，但忽略与购买关联的字段(例如 `commerce.orders` 量度)。 购买包含购买ID的特殊字段，即 `commerce.order.purchaseID`.

建议使用 `purchaseID` 在访客范围内，因为它是XDM内用于购买ID的标准语义字段。 建议使用访客范围来删除重复的购买数据，因为查询比使用全局范围更快，并且购买ID不太可能在多个访客ID中重复。

**范围：** 访客

**窗口键：** identityMap[$命名空间].id &amp; commerce.order.purchaseID

### 重复数据删除示例

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
>在某些情况下，原始Analytics数据具有跨访客ID的重复购买ID时，您 **5月** 需要在所有访客中运行购买ID重复计数。 当购买ID不存在时，此方法要求您包含一个条件，以改为使用事件ID来尽可能快地保持查询。

### 完整示例

以下示例在购买ID不存在的情况下使用条件子句来使用事件ID。

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

如果您的量度使用的是可选唯一ID，并且显示了该ID的副本，则您可能需要忽略该量度值并保留体验事件的其余部分。

在XDM中，几乎所有量度都使用 `Measure` 包含可选数据类型 `id` 字段中指定的值。

**范围：** 访客

**窗口键：** identityMap[$命名空间]测量对象的.id和id

### 重复数据删除示例

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

### 完整示例

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

本文档概述了如何在查询服务中执行重复数据删除，以及重复数据删除示例。 有关使用查询服务编写查询时的更多最佳实践，请阅读 [编写查询指南](./writing-queries.md).
