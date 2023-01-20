---
keywords: Experience Platform；查询服务；查询服务；嵌套数据结构；嵌套数据；
title: 在查询服务中使用嵌套数据结构
description: 本文档提供了使用CTAS和INSERT INTO语句处理和转换嵌套数据字段的工作示例。
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# 在查询服务中使用嵌套数据结构

Adobe Experience Platform查询服务支持使用嵌套数据字段。 企业数据结构的复杂性使得转换或处理此类数据变得复杂。 本文档提供了有关如何创建、处理或转换具有复杂数据类型（包括嵌套数据结构）的数据集的示例。

查询服务提供 [!DNL PostgreSQL] 用于对由Experience Platform管理的所有数据集运行SQL查询的接口。 平台支持在表列（如struct、数组、映射）中使用基元或复杂数据类型，以及深度嵌套的结构、数组和映射。 数据集还可以包含嵌套结构，其中列数据类型可能与嵌套结构数组一样复杂，或者映射图，其中键值对的值可以是具有多个嵌套级别的结构。

## 快速入门

本教程需要使用第三方PSQL客户端或查询编辑器工具在Experience Platform用户界面(UI)中写入、验证和运行查询。 有关如何通过UI运行查询的完整详细信息，请参阅 [查询编辑器UI指南](../ui/user-guide.md). 有关第三方桌面客户端可以连接到查询服务的详细列表，请参阅 [客户端连接概述](../clients/overview.md).

您还应该对 `INSERT INTO` 和 `CTAS` 语法。 有关其使用的特定信息，请参阅 [`INSERT INTO`](../sql/syntax.md#insert-into) 和 [`CTAS`](../sql/syntax.md#create-table-as-select) 部分 [SQL语法参考文档](../sql/syntax.md).

## 创建数据集

查询服务提供“创建选定表”(`CTAS`)功能，用于根据 `SELECT` 语句，或者与本例一样，通过引用Adobe Experience Platform中的现有XDM架构来实现。 下面显示了 `Final_subscription` 创建。

![final_subscription架构的图表。](../images/best-practices/final-subscription-schema.png)

以下示例演示了用于创建 `final_subscription_test2` 数据集。 `final_subscription_test2` 是使用 `Final_subscription` 架构。 使用 `SELECT` 子句来填充某些行。

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

在初始数据集中 `final_subscription_test2`，则struct数据类型将用于包含 `subscription` 字段和 `userid` 每个用户都具有的唯一值。 的 `subscription` 字段描述用户的产品订阅。 可以有多个订阅，但一个表格只能包含每行一个订阅的信息。

## 使用INSERT INTO更新嵌套数据字段

在 `final_subscription_test2` 数据集已创建， `INSERT INTO` 语句用于将附加数据附加到表。 复制数据时，源和目标中的数据类型必须匹配。 或者，源数据类型必须为 `CAST` 到目标数据类型。 然后，使用以下SQL将增量数据添加到目标数据集中。

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

## 处理嵌套数据集中的数据

要从数据集中查找用户的活动订阅列表，您必须编写一个查询，将数组的元素分为多行和多列。 要实现此目的，您必须首先了解数据模型的形状，因为订阅信息会保存在数据集内嵌套的数组中。

PSQL `\d` 命令用于逐级导航到所需的订阅数据。 下表说明了 `final_subscription_test2` 数据集。 复杂数据类型可以一目了然地识别，因为它们不是典型的类型值，如文本、布尔值、时间戳等。

| 栏目 | 类型 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

下一列的字段使用 `\d final_subscription_test2__lumaservices3` 命令。

| 栏目 | 类型 |
|---------|-------|
| `userid` | 文本 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 是结构元素数组。 其字段使用 `\d _lumaservices3_subscription_e[]` 命令。

| 栏目 | 类型 |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | 文本 |
| `offer_id` | 文本 |
| `subscription_id` | 文本 |

要查询订阅的嵌套字段，您必须首先将 `subscription` 将数组分成多行，并使用分解函数返回结果。 以下SQL示例根据 `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

此简化的示例解决方案仅允许一个活动用户订阅。 实际上，单个用户可能有许多活动订阅。 以下示例修改了上一个查询，以允许同时进行多个活动订阅。

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

尽管此SQL示例的复杂性越来越高， `collect_list` 对于活动订阅，不保证输出与源的顺序相同。 要为用户创建活动订阅列表，必须使用GROUP BY或Shwiffling来聚合列表结果。

## 后续步骤

通过阅读本文档，您现在可以了解如何在Adobe Experience Platform查询服务中处理或转换使用复杂数据类型的数据集。 请参阅 [查询执行指南](../best-practices/writing-queries.md) 有关在数据湖中的数据集上运行SQL查询的详细信息。
