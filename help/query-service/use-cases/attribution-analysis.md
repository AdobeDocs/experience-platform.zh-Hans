---
title: 归因分析
description: 本文档介绍如何使用查询服务基于首次联系和最近联系的营销归因模型创建营销效果衡量技术。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# 归因分析

归因是一种分析概念，可帮助确定对业务销售或转化有贡献的营销策略，例如渠道、优惠和消息。 此概念可评估客户历程（客户与公司互动以实现目标的过程），从而根据客户接触点（客户与您的品牌互动的任何时间）进行购买或收购。 通过归因分析，营销人员可以评估将其与潜在客户关联的渠道的投资回报。

## 快速入门

本文档中的SQL示例是通常与Adobe Analytics数据一起使用的查询。 本教程需要深入了解以下组件：

* [用于报表包数据的Adobe Analytics源连接器概述](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Analytics字段映射文档](../../sources/connectors/adobe-applications/mapping/analytics.md) 提供了有关摄取和映射分析数据以供查询服务使用的更多信息。
* [Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [Adobe Analytics归因面板指南](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html).

中的参数说明 `OVER()` 函数位于 [窗口函数部分](../sql/adobe-defined-functions.md#window-functions). 此 [Adobe营销和商业术语表](https://business.adobe.com/glossary/index.html) 也可能有用。

对于以下每个用例，都会提供一个参数化SQL查询示例作为模板供您自定义。 提供您看到的任何位置的参数 `{ }` 您希望进行评估的SQL示例中的。

## 目标

归因用例使用Adobe Analytics数据帮助将客户操作与成功结果相关联。 这种关联是了解影响客户体验的因素的关键部分。 归因分析数据可用于了解客户接触点在客户历程中的重要性。

本文档中包含的查询示例支持具有不同到期设置的首次联系和最近联系归因的各种用例。 本指南说明了以下关键概念：

* 首次联系和最近联系归因。
* 首次联系和最近联系归因及过期超时。
* 具有到期条件的首次联系和最近联系归因。

## 归因查询参数 {#attribution-query-parameters}

下表提供了在首次联系和最近联系归因查询中使用的参数及其说明的明细：

| 参数 | 描述 |
|---|---|
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |
| `{EXP_TIMEOUT}` | 渠道事件之前的时间窗口（以秒为单位），表示查询将搜索首次接触事件。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，指示渠道在指定的条件之前还是之后过期， `{EXP_CONDITION}`，满足。 这主要针对会话的到期条件启用，以确保不会从上一个会话中选择首次联系。 默认情况下，此值设置为 `false`. |

## 查询结果列组件 {#query-result-column-components}

归因查询的结果在 `first_touch` 或 `last_touch` 列。 这些列由以下组件组成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 此 `{CHANNEL_NAME}`，在Azure数据工厂(ADF)中输入为标签。 |
| `{VALUE}` | 值来自 `{CHANNEL_VALUE}` 即指定范围内的最后接触 `{EXP_TIMEOUT}` 间隔 |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 上次接触发生的地方 |
| `{FRACTION}` | 最后接触的归因，以小数表示。 |

### 首次接触归因 {#first-touch}

首次接触归因将100%的成功结果责任归于消费者遇到的初始渠道。 此SQL示例用于突出显示导致后续一系列客户操作的交互。

以下查询返回首次接触归因值和目标中渠道的详细信息 [!DNL Experience Event] 数据集。 它还返回 `struct` 所选渠道的对象，具有每行的首次接触值、时间戳和归因。

>[!NOTE]
>
>Experience CloudID (ECID)也称为MCID，它将继续用在命名空间中。

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

在下面的结果中，初始跟踪代码 `em:946426` 取自 [!DNL Experience Event] 数据集。 此跟踪代码归因于100% (`1.0`)，因为这是首次交互。

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

要查看“ ”中显示的结果细分， `first_touch` 列中，请参见 [列组件部分](#query-result-column-components).

### 最后接触归因 {#second-touch}

最后接触归因将100%的成功结果责任归因到消费者遇到的最后一个渠道。 此SQL示例用于突出显示一系列客户操作中的最终交互。

查询返回最近联系归因值和目标中渠道的详细信息 [!DNL Experience Event] 数据集。 它还返回 `struct` 所选渠道的对象，具有每行的最近联系值、时间戳和归因。

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

在下方显示的结果中，返回对象中的跟踪代码是每个对象中的最后一个交互 [!DNL Experience Event] 记录。 每个代码都归因于100% (`1.0`)负责客户的操作，因为这是最后一次交互。

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

要查看“ ”中显示的结果细分， `last_touch` 列中，请参见 [列组件部分](#query-result-column-components).

### 具有到期条件的首次接触归因 {#first-touch-attribution-with-expiration-condition}

此查询用于查看哪些交互导致一部分客户采取了一系列行动 [!DNL Experience Event] 数据集由您选择的条件决定。

查询返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 数据集，在条件之后或之前过期。 它还返回 `struct` 对象具有针对所选渠道返回的每一行的首次接触值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在下面显示的示例中，记录了购买(`commerce.purchases.value IS NOT NULL`)在结果中显示的4天（7月15日、21日、23日和29日）中的每一天，每天的初始跟踪代码均被归因100%(`1.0`)负责客户操作。

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

要查看“ ”中显示的结果细分， `first_touch` 列中，请参见 [列组件部分](#query-result-column-components).

### 具有过期超时的首次联系归因 {#first-touch-attribution-with-expiration-timeout}

此查询用于查找在选定时间段内导致成功客户操作的交互。

以下查询返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 指定时间段的数据集。 查询返回 `struct` 对象具有针对所选渠道返回的每一行的首次接触值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在以下示例中，为每个客户操作返回的首次联系是前七天中最早的交互(expTimeout = 86400 * 7)。

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

要查看“ ”中显示的结果细分， `first_touch` 列中，请参见 [列组件部分](#query-result-column-components).

### 带到期条件的最后一次接触归因 {#last-touch-attribution-with-expiration-condition}

此查询用于查找部分客户活动中一系列客户操作的最后一个交互。 [!DNL Experience Event] 数据集由您选择的条件决定。

以下查询返回目标中单个渠道的上次接触归因值和详细信息 [!DNL Experience Event] 数据集，在条件之后或之前过期。 查询返回 `struct` 对象，其中包含为所选渠道返回的每一行的最近联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在下面显示的示例中，记录了购买(`commerce.purchases.value IS NOT NULL`)在结果中显示的四天（7月15日、21日、23日和29日）的每一天，每天的最后一个跟踪代码都获得100%的归因(`1.0`)负责客户操作。

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

要查看“ ”中显示的结果细分， `last_touch` 列中，请参见 [列组件部分](#query-result-column-components).

### 带有过期超时的最后联系归因 {#last-touch-attribution-with-expiration-timeout}

此查询用于查找选定时间间隔内的最后一次交互。 查询返回目标中单个渠道的上次接触归因值和详细信息 [!DNL Experience Event] 指定时间段的数据集。 查询返回 `struct` 对象，其中包含为所选渠道返回的每一行的最近联系值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅 [归因查询参数节](#attribution-query-parameters).

**示例查询**

在以下示例中，为每个客户操作返回的最后一次联系是随后七天内的最终交互(`expTimeout = 86400 * 7`)。

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

要查看“ ”中显示的结果细分， `last_touch` 列中，请参见 [列组件部分](#query-result-column-components).
