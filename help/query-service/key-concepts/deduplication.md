---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；重复数据删除；重复数据删除；
solution: Experience Platform
title: 查询服务中的重复数据删除
type: Tutorial
description: 本文档概述了子选择和完整示例查询示例，用于为三个常见用例（体验事件、购买和量度）去重。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# [!DNL Query Service]中的重复数据删除

Adobe Experience Platform [!DNL Query Service]支持重复数据删除。 当需要从计算中删除整个行或忽略特定字段集（因为行中只有部分数据是重复信息）时，可以执行重复数据删除。

去重通常涉及在窗口内对一个ID（或一对ID）在有序时间内使用`ROW_NUMBER()`函数，这返回一个新字段，表示检测到重复项的次数。 时间通常使用[!DNL Experience Data Model] (XDM) `timestamp`字段表示。

当`ROW_NUMBER()`的值为`1`时，它引用原始实例。 通常，这是您希望使用的实例。 此操作通常在子选择内完成，其中重复数据删除在更高级别的`SELECT`中完成，如执行聚合计数。

重复数据删除用例可以是全局的，也可以限制为`identityMap`中的单个用户或最终用户ID。

本文档概述了如何针对三个常见用例执行重复数据删除：体验事件、购买和量度。

每个示例都包括范围、窗口键、重复数据删除方法的大纲以及完整SQL查询。

## 体验事件 {#experience-events}

如果出现重复的体验事件，您可能希望忽略整行。

>[!CAUTION]
>
>[!DNL Experience Platform]中的许多数据集(包括Adobe Analytics Data Connector生成的数据集)已应用体验事件级重复数据删除。 因此，重新应用此级别的重复数据删除是不必要的，并且会减慢查询速度。
>
>了解数据集的来源以及是否已应用体验事件级别的重复数据删除非常重要。 对于流式传输的任何数据集(例如来自Adobe Target的数据集)，您&#x200B;**将**&#x200B;需要应用体验事件级重复数据删除，因为这些数据源具有“至少一次”语义。

**范围：**&#x200B;全局

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

## 购买次数 {#purchases}

如果存在重复购买，则您可能希望保留[!DNL Experience Event]行中的大部分内容，但忽略与购买关联的字段（如`commerce.orders`量度）。 购买包含用于购买ID的特殊字段，即`commerce.order.purchaseID`。

建议在访客范围中使用`purchaseID`，因为它是用于XDM中购买ID的标准语义字段。 建议使用访客范围来删除重复的购买数据，因为查询速度比使用全局范围更快，并且在多个访客ID之间不可能存在重复的购买ID。

**范围：**&#x200B;访客

**窗口键：** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

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
>在某些情况下，原始Analytics数据具有跨访客ID的重复购买ID，您&#x200B;**可能**&#x200B;需要对所有访客运行购买ID重复计数。 当购买ID不存在时，此方法要求您包含条件，该条件将使用事件ID来尽可能快地保留查询。

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

如果您有一个量度正在使用可选的唯一ID，并且显示该ID的重复项，则您可能需要忽略该量度值并保留体验事件的其余部分。

在XDM中，几乎所有量度都使用`Measure`数据类型，该数据类型包含可用于重复数据删除的可选`id`字段。

**范围：**&#x200B;访客

**窗口键：** identityMap[$NAMESPACE].ID和度量值对象的ID

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

本文档提供了重复数据删除的示例，并概述了如何在查询服务中执行重复数据删除。 有关使用查询服务编写查询时的更多最佳实践，请阅读[编写查询指南](../best-practices/writing-queries.md)。
