---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；重复数据删除；重复数据删除；
solution: Experience Platform
title: 查询服务中的重复数据删除
type: Tutorial
description: 本文档概述了子选择和完整示例查询示例，用于为三个常见用例（体验事件、购买和量度）进行重复数据删除。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 中的重复数据删除 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支持重复数据删除。 当需要从计算中删除整个行或由于行中只有部分数据是重复信息而忽略特定字段集时，可以执行重复数据删除。

重复数据删除通常涉及使用 `ROW_NUMBER()` 在有序时间内跨窗口查找ID（或一对ID）的函数，这会返回一个新字段，表示检测到重复项的次数。 时间通常使用表示 [!DNL Experience Data Model] (XDM) `timestamp` 字段。

当 `ROW_NUMBER()` 是 `1`，它是指原始实例。 通常，这是您希望使用的实例。 这通常在子选择内完成，其中重复数据删除在更高级别完成 `SELECT` 如执行聚合计数。

重复数据删除用例可以是全局的，也可以限制为中的单个用户或最终用户ID。 `identityMap`.

本文档概述了如何针对三个常见用例执行重复数据删除：体验事件、购买和量度。

每个示例都包括范围、窗口键、重复数据删除方法大纲以及完整SQL查询。

## 体验事件 {#experience-events}

如果出现重复的体验事件，您可能希望忽略整行。

>[!CAUTION]
>
>中的许多数据集 [!DNL Experience Platform]包括由Adobe Analytics Data Connector生成的重复数据删除，已应用体验事件级重复数据删除。 因此，无需重新应用此级别的重复数据删除，这将减慢查询速度。
>
>了解数据集的来源并了解是否已应用体验事件级别的重复数据删除非常重要。 对于流式传输的任何数据集(例如，来自Adobe Target的数据集)，您可以 **将** 需要应用体验事件级别的重复数据删除，因为这些数据源具有“至少一次”语义。

**范围：** 全局

**窗口键：** `id`

### 去重示例

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

如果您重复购买，则可能希望保留大部分 [!DNL Experience Event] 行，但忽略与购买关联的字段(例如 `commerce.orders` 量度)。 购买包含用于购买ID的特殊字段，即 `commerce.order.purchaseID`.

建议使用 `purchaseID` ，因为这是XDM中用于购买ID的标准语义字段。 建议使用访客范围删除重复的购买数据，因为查询速度比使用全局范围更快，并且购买ID不太可能在多个访客ID之间重复。

**范围：** 访客

**窗口键：** identitymap[$NAMESPACE].id和commerce.order.purchaseID

### 去重示例

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
>在某些情况下，如果原始Analytics数据跨访客ID具有重复的购买ID，则您可以 **五月** 需要对所有访客运行购买ID重复计数。 当购买ID不存在时，此方法要求您包含条件，该条件将使用事件ID来尽可能快地保留查询。

### 完整示例

以下示例使用condition子句在购买ID不存在的情况下使用事件ID。

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

如果您有一个使用可选唯一ID的量度，并且显示该ID的重复项，则您可能需要忽略该量度值并保留体验事件的其余部分。

在XDM中，几乎所有量度都使用 `Measure` 包含可选数据类型的 `id` 可用于删除重复项的字段。

**范围：** 访客

**窗口键：** identitymap[$NAMESPACE]度量值对象的.id和id

### 去重示例

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

本文档提供了重复数据删除的示例，并概述了如何在查询服务中执行重复数据删除。 有关使用查询服务编写查询时的更多最佳实践，请阅读 [编写查询指南](../best-practices/writing-queries.md).
