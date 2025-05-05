---
title: 归因分析
description: 本文档介绍如何使用查询服务基于首次联系和最近联系营销归因模型创建营销效果衡量技术。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# 归因分析

归因是一种分析概念，可帮助确定对业务销售或转化有贡献的营销策略，例如渠道、优惠和消息。 此概念可评估客户历程（客户与公司互动以实现目标的过程），从而根据客户接触点（随时消费者与您的品牌互动）完成购买或收购。 通过归因分析，营销人员可以评估将其与潜在客户关联的渠道的投资回报。

## 快速入门

本文档中的SQL示例是通常用于Adobe Analytics数据的查询。 本教程需要您实际了解以下组件：

* [报告包数据概述的Adobe Analytics源连接器](../../sources/connectors/adobe-applications/mapping/analytics.md)。
* [Analytics字段映射文档](../../sources/connectors/adobe-applications/mapping/analytics.md)提供了有关摄取和映射Analytics数据以便与查询服务一起使用的更多信息。
* [Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=zh-Hans)
* [Adobe Analytics归因面板指南](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=zh-Hans)。

可以在[窗口函数部分](../sql/adobe-defined-functions.md#window-functions)中找到`OVER()`函数中参数的说明。 [Adobe营销和Commerce术语词汇表](https://business.adobe.com/glossary/index.html)可能也很有用。

对于以下每个用例，都会提供一个参数化SQL查询示例作为模板供您自定义。 在SQL示例中任何您想要评估的`{ }`处提供参数。

## 目标

归因用例使用Adobe Analytics数据帮助将客户操作与成功结果相关联。 这种关联是了解影响客户体验的因素的关键部分。 归因分析数据可用于了解客户接触点在客户历程中的重要性。

本文档中包含的查询示例支持具有不同到期设置的首次联系和最近联系归因的各种用例。 本指南说明了以下主要概念：

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
| `{EXP_TIMEOUT}` | 渠道事件之前的时间窗口（以秒为单位），查询将搜索首次接触事件。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，指示渠道是在满足指定的条件`{EXP_CONDITION}`之前还是之后过期。 这主要针对会话的到期条件启用，以确保不会从上一个会话中选择首次联系。 默认情况下，此值设置为`false`。 |

## 查询结果列组件 {#query-result-column-components}

归因查询的结果在`first_touch`或`last_touch`列中给出。 这些列由以下组件组成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 在Azure数据工厂(ADF)中作为标签输入的`{CHANNEL_NAME}`。 |
| `{VALUE}` | `{CHANNEL_VALUE}`的值，即指定`{EXP_TIMEOUT}`间隔内的最后一次接触 |
| `{TIMESTAMP}` | 发生最近联系的[!DNL Experience Event]的时间戳 |
| `{FRACTION}` | 最后接触的归因，以小数表示。 |

### 首个联系归因 {#first-touch}

首次接触归因将成功结果的责任100%归因于消费者遇到的初始渠道。 此SQL示例用于突出显示导致后续一系列客户操作的交互。

以下查询返回目标[!DNL Experience Event]数据集中的首次接触归因值和渠道详细信息。 对于选定的渠道，它还返回`struct`对象，其中具有每一行的首次接触值、时间戳和归因。

>[!NOTE]
>
>Experience CloudID (ECID)也称为MCID，它将继续用在命名空间中。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅[归因查询参数部分](#attribution-query-parameters)。

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

在下面的结果中，初始跟踪代码`em:946426`是从[!DNL Experience Event]数据集中获取的。 由于此跟踪代码是第一次交互，因此它具有100% (`1.0`)的客户操作责任。

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

有关`first_touch`列中显示的结果的细分，请参阅[列组件部分](#query-result-column-components)。

### 最后接触归因 {#second-touch}

最后接触归因将成功结果的责任100%归因于消费者遇到的最后一个渠道。 此SQL示例用于突出显示一系列客户操作中的最终交互。

查询返回目标[!DNL Experience Event]数据集中的最近联系归因值和渠道详细信息。 对于所选渠道，它还返回`struct`对象，其中包含每行的最近联系值、时间戳和归因。

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

在下面显示的结果中，返回对象中的跟踪代码是每个[!DNL Experience Event]记录中的最后一个交互。 由于每个代码是最后一次交互，因此其对于客户操作具有100% (`1.0`)的责任。

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

有关`last_touch`列中显示的结果的细分，请参阅[列组件部分](#query-result-column-components)。

### 具有到期条件的首次接触归因 {#first-touch-attribution-with-expiration-condition}

此查询用于查看在[!DNL Experience Event]数据集的一部分中哪个交互导致了一系列客户操作，该部分由您选择的条件确定。

查询返回目标[!DNL Experience Event]数据集中单个渠道的首次接触归因值和详细信息，这些值与条件后或条件前过期。 对于针对所选渠道返回的每一行，它还返回一个具有首个联系值、时间戳和归因的`struct`对象。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅[归因查询参数部分](#attribution-query-parameters)。

**示例查询**

在以下示例中，在结果（7月15日、7月21日、7月23日和29日）中显示的四天中的每一天都记录一次购买(`commerce.purchases.value IS NOT NULL`)，并且每天的初始跟踪代码都归因于100% (`1.0`)的客户操作责任。

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

有关`first_touch`列中显示的结果的细分，请参阅[列组件部分](#query-result-column-components)。

### 首次接触归因及过期超时 {#first-touch-attribution-with-expiration-timeout}

此查询用于查找在选定时间段内导致客户操作成功的交互。

以下查询返回目标[!DNL Experience Event]数据集中的单个渠道在指定时间段内的首次接触归因值和详细信息。 查询会返回一个`struct`对象，该对象具有针对所选渠道返回的每一行的首次接触值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅[归因查询参数部分](#attribution-query-parameters)。

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

有关`first_touch`列中显示的结果的细分，请参阅[列组件部分](#query-result-column-components)。

### 带到期条件的最后一次接触归因 {#last-touch-attribution-with-expiration-condition}

此查询用于查找在[!DNL Experience Event]数据集的一部分内的一系列客户操作中的最后一个交互，该部分由您选择的条件确定。

以下查询返回目标[!DNL Experience Event]数据集中单个渠道的上次接触归因值和详细信息，这些值与条件后或条件前过期。 查询会返回一个`struct`对象，其中包含为所选渠道返回的每一行的最后一次接触值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅[归因查询参数部分](#attribution-query-parameters)。

**示例查询**

在以下示例中，在结果（7月15日、7月21日、7月23日和29日）中显示的四天中的每一天都记录一次购买(`commerce.purchases.value IS NOT NULL`)，并且每天的最后一次跟踪代码都归因于100% (`1.0`)客户操作的责任。

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

有关`last_touch`列中显示的结果的细分，请参阅[列组件部分](#query-result-column-components)。

### 最后接触归因及到期超时 {#last-touch-attribution-with-expiration-timeout}

此查询用于查找选定时间间隔内的最后一次交互。 查询返回目标[!DNL Experience Event]数据集中的单个渠道在指定时间段内的最近联系归因值和详细信息。 查询会返回一个`struct`对象，其中包含为所选渠道返回的每一行的最后一次接触值、时间戳和归因。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有关可能需要的参数及其说明的完整列表，请参阅[归因查询参数部分](#attribution-query-parameters)。

**示例查询**

在下面显示的示例中，为每个客户操作返回的最后一次联系是接下来的七天内(`expTimeout = 86400 * 7`)的最后一次交互。

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

有关`last_touch`列中显示的结果的细分，请参阅[列组件部分](#query-result-column-components)。
