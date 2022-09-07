---
title: 归因分析
description: 本文档介绍如何使用查询服务来创建基于首次联系和最近联系的营销归因模型的营销效果衡量技术。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# 归因分析

归因是一个分析概念，可帮助确定有助于促进业务销售或转化的营销策略，如渠道、优惠和消息。 此概念会评估客户历程（客户与公司进行交互以实现目标的过程），从而根据客户接触点（客户任何时候与您的品牌进行交互）进行购买或收购。 通过归因分析，营销人员可以评估将渠道与潜在客户联系起来的投资回报率。

## 快速入门

本文档中的SQL示例是常用于Adobe Analytics数据的查询。 本教程需要对以下组件有一定的了解：

* [用于报表包数据的Adobe Analytics源连接器概述](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Analytics字段映射文档](../../sources/connectors/adobe-applications/mapping/analytics.md) 提供了有关摄取和映射分析数据以与查询服务一起使用的更多信息。
* [Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [Adobe Analytics归因面板指南](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html).

对 `OVER()` 函数 [窗口函数部分](../sql/adobe-defined-functions.md#window-functions). 的 [Adobe营销和商务术语表](https://business.adobe.com/glossary/index.html) 也可能有用。

对于以下每个用例，都提供了参数化SQL查询示例作为模板供您进行自定义。 无论您在何处看到，都提供参数 `{ }` 在SQL示例中，您希望进行评估。

## 目标

归因用例使用Adobe Analytics数据帮助将客户操作与成功结果关联。 这种关联对于了解影响客户体验的因素至关重要。 归因分析数据可用于了解客户接触点在客户历程中的重要性。

本文档中包含的查询示例支持具有不同过期设置的首次联系和最近联系归因的各种用例。 本指南说明了以下主要概念：

* 首次联系和最近联系归因。
* 具有过期超时的首次联系和最近联系归因。
* 具有过期条件的首次联系和最近联系归因。

## 归因查询参数 {#attribution-query-parameters}

下表提供了首次联系和最近联系归因查询中使用的参数及其说明的划分：

| 参数 | 描述 |
|---|---|
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |
| `{EXP_TIMEOUT}` | 查询搜索首次联系事件之前的渠道事件时间窗口（以秒为单位）。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，用于指示渠道在指定条件之前还是之后过期， `{EXP_CONDITION}`，则不会。 这主要针对会话的到期条件启用，以确保未从上一个会话中选择首次联系。 默认情况下，此值设置为 `false`. |

## 查询结果列组件 {#query-result-column-components}

归因查询的结果在 `first_touch` 或 `last_touch` 列。 这些列由以下组件组成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在Azure数据工厂(ADF)中作为标签输入。 |
| `{VALUE}` | 值来自 `{CHANNEL_VALUE}` 即指定 `{EXP_TIMEOUT}` 间隔 |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 最近联系发生的地方 |
| `{FRACTION}` | 最近联系的归因，以小数部分表示。 |

### 首次联系归因 {#first-touch}

首次联系归因将成功结果的100%责任归因于消费者遇到的初始渠道。 此SQL示例用于突出显示导致后续一系列客户操作的交互。

以下查询返回首次联系归因值和目标中渠道的详细信息 [!DNL Experience Event] 数据集。 它还会返回 `struct` 对象，其中包含每行的首次联系值、时间戳和归因。

>[!NOTE]
>
>Experience CloudID(ECID)也称为MCID，可继续用于命名空间。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

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

在下面的结果中，初始跟踪代码 `em:946426` 取自 [!DNL Experience Event] 数据集。 此跟踪代码的归因为100%(`1.0`)，因为这是首次交互。

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

对于 `first_touch` 列，请参阅 [列组件部分](#query-result-column-components).

### 最近联系归因 {#second-touch}

最近联系归因将成功结果的100%责任归因到消费者遇到的最后一个渠道。 此SQL示例用于突出显示一系列客户操作中的最终交互。

查询会返回最近联系归因值和目标中渠道的详细信息 [!DNL Experience Event] 数据集。 它还会返回 `struct` 对象，其中包含每行的最近联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**示例查询**

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

在下面显示的结果中，返回对象中的跟踪代码是每个对象中的最后一次交互 [!DNL Experience Event] 记录。 每个代码的归因为100%(`1.0`)对客户的操作负责，因为它是最后一次交互。

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

对于 `last_touch` 列，请参阅 [列组件部分](#query-result-column-components).

### 具有过期条件的首次联系归因 {#first-touch-attribution-with-expiration-condition}

此查询用于查看哪些交互导致了 [!DNL Experience Event] 由您选择的条件确定的数据集。

查询会返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 数据集，在条件之后或之前过期。 它还会返回 `struct` 对象，其中包含为选定渠道返回的每行的首次联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在以下示例中，记录了购买(`commerce.purchases.value IS NOT NULL`)，并且每天的初始跟踪代码均被归因为100%(`1.0`)对客户操作负责。

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

对于 `first_touch` 列，请参阅 [列组件部分](#query-result-column-components).

### 具有过期超时的首次联系归因 {#first-touch-attribution-with-expiration-timeout}

此查询用于查找在选定时间段内导致客户成功操作的交互。

以下查询返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 数据集。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的首次联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在以下示例中，每个客户操作返回的首次联系是前七天内最早的交互(expTimeout = 86400 * 7)。

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

对于 `first_touch` 列，请参阅 [列组件部分](#query-result-column-components).

### 具有过期条件的最近联系归因 {#last-touch-attribution-with-expiration-condition}

此查询用于查找 [!DNL Experience Event] 由您选择的条件确定的数据集。

以下查询返回目标中单个渠道的最近联系归因值和详细信息 [!DNL Experience Event] 数据集，在条件之后或之前过期。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的最近联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在以下示例中，记录了购买(`commerce.purchases.value IS NOT NULL`)，并且每天的最后一个跟踪代码都被归因为100%(`1.0`)对客户操作负责。

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

**示例结果**

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

对于 `last_touch` 列，请参阅 [列组件部分](#query-result-column-components).

### 具有过期超时的最近联系归因 {#last-touch-attribution-with-expiration-timeout}

此查询用于查找选定时间间隔内的最后一次交互。 查询会返回目标中单个渠道的最近联系归因值和详细信息 [!DNL Experience Event] 数据集。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的最近联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在以下示例中，针对每个客户操作返回的最近联系是随后七天(`expTimeout = 86400 * 7`)。

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

对于 `last_touch` 列，请参阅 [列组件部分](#query-result-column-components).
