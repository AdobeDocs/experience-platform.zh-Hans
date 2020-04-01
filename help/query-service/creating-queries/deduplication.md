---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据外部重复数据删除
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 查询服务中的数据外部重复数据删除

当可能需要从计算中删除整个行或忽略特定的字段集时，Adobe Experience Platform查询服务支持数据外部重复数据删除，因为行中只有一部分数据是重复。 外部重复数据删除的常见模式包括在按顺序时间(使用体验数据模型(XDM)字段)跨窗口使用ID或ID对的函数来返回表示检测到重复的次数的新字段。 `ROW_NUMBER()``timestamp` 当此值为时， `1`即表示原始实例，在大多数情况下，即您希望使用的实例，忽略其他每个实例。 这通常在子选择中完成，外部重复数据删除在更高级别中完成，如执 `SELECT` 行聚合计数。

## 用例

某些外部重复数据删除用例在日期范围内是全局的，有些用例在日期范围内限制为单个访客或最终用户ID `identityMap`。

此文档概述了用于消除重复三个常见用例的子选择和完整的查询示例：
- [ExperienceEvents](#experienceevents)
- [购买](#purchases)
- [量度](#metrics)

### ExperienceEvents {#experienceevents}

对于重复ExperienceEvents，您可能希望忽略整行。

>[!CAUTION] Experience Platform中的许多数据集（包括Adobe Analytics Data Connector生成的数据集）已应用ExperienceEvent级外部重复数据删除。 因此，重新应用此外部重复数据删除级别是不必要的，并会降低您的查询。 了解数据集的来源并了解ExperienceEvent级别的外部重复数据删除是否已应用，这一点很重要。 对于流化的任何数据集(例如，来自Adobe目标的数据集)，您需要应用ExperienceEvent级外部重复数据删除，因为这些数据源具有“至少一次”语义。

**范围：** Global

**窗口键：** id

#### 子选择

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### 完整示例

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

### 购买 {#purchases}

如果您有重复购买，您可能希望保留大部分ExperienceEvent行，但忽略与购买关联的字段(如度 `commerce.orders` 量)。 对于购买，有一个用于购买ID的特殊字段。 此字段为 `commerce.order.purchaseID`。

**范围：** 访客

**窗口键：** identityMap[$命名空间].id &amp; commerce.order.purchaseID

#### 子选择

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

#### 完整示例

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

### 量度 {#metrics}

如果您有一个使用可选唯一ID的度量，并显示该ID的重复，您可能希望忽略该度量值并保留ExperienceEvent的其余部分。 在XDM中，几乎所有指标都使用 `Measure` 数据类型，该数据类型包含可用 `id` 于外部重复数据删除的可选字段。

**范围：** 访客

**窗口键：** identityMap[$命名空间].id和度量对象的id

#### 子选择

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

#### 完整示例

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
