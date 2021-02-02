---
keywords: Experience Platform；主题；热门主题；查询服务；查询服务；数据外部重复数据删除;外部重复数据删除;
solution: Experience Platform
title: 数据外部重复数据删除
topic: queries
type: Tutorial
description: 此文档概述了用于消除重复的三个常见用例(体验事件、购买和指标)的子选择和完整的查询示例。
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# [!DNL Query Service]中的数据外部重复数据删除

Adobe Experience Platform[!DNL Query Service]支持数据外部重复数据删除。 当需要从计算中删除整个行或忽略特定字段集时，可以执行外部重复数据删除，因为行中只有一部分数据是重复信息。

外部重复数据删除通常涉及在按顺序的时间跨窗口使用`ROW_NUMBER()`函数来查找ID（或一对ID），这会返回一个表示检测到重复的次数的新字段。 该时间通常使用[!DNL Experience Data Model](XDM)`timestamp`字段表示。

当`ROW_NUMBER()`的值为`1`时，它引用原始实例。 通常，这是您希望使用的实例。 这通常在子选择中完成，外部重复数据删除在更高级别`SELECT`中完成，如执行聚合计数。

外部重复数据删除用例可以是全局的，也可以限制为`identityMap`中的单个用户ID或最终用户ID。

本文档概述了如何对三个常见用例执行外部重复数据删除:体验事件、购买和指标。

每个示例都包括范围、窗口键、外部重复数据删除方法的大纲以及完整的SQL查询。

## 体验事件{#experience-events}

对于重复体验事件，您可能希望忽略整行。

>[!CAUTION]
>
>[!DNL Experience Platform]中的许多数据集(包括由Adobe Analytics数据连接器生成的数据集)已应用体验事件级外部重复数据删除。 因此，重新应用此外部重复数据删除级别是不必要的，并会降低查询速度。
>
>了解数据集的来源并了解体验事件级别的外部重复数据删除是否已应用，这一点非常重要。 对于流化的任何数据集(例如，来自Adobe Target的数据集)，您&#x200B;**将**&#x200B;需要应用体验事件级外部重复数据删除，因为这些数据源具有“至少一次”语义。

**范围：全** 局

**窗口键：** `id`

### 外部重复数据删除示例

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

如果您有重复购买，您可能希望保留大多数体验事件行，但忽略与购买相关的字段（如`commerce.orders`度量）。 购买包含购买ID的特殊字段，该字段为`commerce.order.purchaseID`。

**范围：** 访客

**窗口** 键[:identityMap]$命名空间.id &amp; commerce.order.purchaseID

### 外部重复数据删除示例

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

### 完整示例

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

如果您有使用可选唯一ID的度量，并且显示该ID的重复，您可能希望忽略该度量值并保留体验事件的其余部分。

在XDM中，几乎所有度量都使用`Measure`数据类型，该数据类型包含一个可选的`id`字段，您可以使用该字段进行外部重复数据删除。

**范围：** 访客

**Window键：** identityMap[$命名空间].id和Measure对象的id

### 外部重复数据删除示例

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

本文档概述了如何在查询服务中执行数据外部重复数据删除，以及数据外部重复数据删除示例。 有关使用查询服务编写查询的更多最佳实践，请阅读[编写查询指南](./writing-queries.md)。