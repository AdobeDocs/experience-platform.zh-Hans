---
keywords: Experience Platform；查询服务；查询服务；嵌套数据结构；嵌套数据；
title: 在查询服务中使用嵌套数据结构
description: 本文档提供了一个使用CTAS和INSERT INTO语句处理和转换嵌套数据字段的工作示例。
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# 在查询服务中使用嵌套数据结构

Adobe Experience Platform查询服务支持使用嵌套数据字段。 企业数据结构的复杂性会使这些数据的转换和处理变得复杂。 本文档提供了如何使用复杂数据类型（包括嵌套数据结构）创建、处理或转换数据集的示例。

查询服务提供了一个[!DNL PostgreSQL]接口，用于对Experience Platform管理的所有数据集运行SQL查询。 Experience Platform支持在表列（如struct、arrays、map和深度嵌套的struct、arrays和map）中使用原始或复杂数据类型。 数据集还可以包含嵌套结构，其中列数据类型可以像嵌套结构的数组一样复杂，或者包含映射映射，其中键值对的值可以是具有多个嵌套级别的结构。

## 快速入门

本教程需要使用第三方PSQL客户端或查询编辑器工具在Experience Platform用户界面(UI)中编写、验证和运行查询。 有关如何通过UI运行查询的完整详细信息，请参阅[查询编辑器UI指南](../ui/user-guide.md)。 有关第三方桌面客户端可以连接到查询服务的详细列表，请参阅[客户端连接概述](../clients/overview.md)。

您还应很好地了解`INSERT INTO`和`CTAS`语法。 可以在[SQL语法参考文档](../sql/syntax.md)的[`INSERT INTO`](../sql/syntax.md#insert-into)和[`CTAS`](../sql/syntax.md#create-table-as-select)部分中找到有关其使用的特定信息。

## 创建数据集

查询服务提供了以选择方式创建表(`CTAS`)功能，以根据`SELECT`语句的输出创建表，或者在此情况下通过使用对Adobe Experience Platform中现有XDM架构的引用创建表。 下面显示的是为此示例创建的`Final_subscription`的XDM架构。

![final_subscription架构的图表。](../images/best-practices/final-subscription-schema.png)

以下示例演示了用于创建`final_subscription_test2`数据集的SQL。 `final_subscription_test2`是使用`Final_subscription`架构创建的。 使用`SELECT`子句从源中提取数据以填充某些行。

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

在初始数据集`final_subscription_test2`中，结构数据类型用于包含`subscription`字段和每个用户唯一的`userid`。 `subscription`字段描述了用户的产品订阅。 可以有多个预订，但表格只能包含每行一个预订的信息。

## 使用INSERT INTO更新嵌套数据字段

创建`final_subscription_test2`数据集后，`INSERT INTO`语句用于将其他数据附加到表。 在复制数据时，源和目标中的数据类型必须匹配。 或者，源数据类型必须为目标数据类型`CAST`。 然后，使用以下SQL将增量数据添加到目标数据集中。

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

## 处理来自嵌套数据集的数据

要从数据集中查找用户的活动订阅列表，必须编写一个查询，将数组的元素分隔成多个行和列。 为此，您必须首先了解数据模型的形状，因为订阅信息将保存在嵌套在数据集中的数组中。

PSQL `\d`命令用于逐级导航到所需的订阅数据。 这些表说明了`final_subscription_test2`数据集的结构。 复杂数据类型不是典型的类型值（如文本、布尔值、时间戳等），因此一眼就能识别。

| 列 | 类型 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

使用`\d final_subscription_test2__lumaservices3`命令显示下一列的字段。

| 列 | 类型 |
|---------|-------|
| `userid` | 文本 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription`是一个结构元素数组。 其字段使用`\d _lumaservices3_subscription_e[]`命令显示。

| 列 | 类型 |
|---------|-------|
| `last_eventtime` | 时间戳 |
| `last_status` | 文本 |
| `offer_id` | 文本 |
| `subscription_id` | 文本 |

要查询预订的嵌套字段，必须首先将`subscription`数组的元素分隔成多行，然后使用explode函数返回结果。 以下SQL示例根据`userid`返回用户的活动订阅。

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

此简化的示例解决方案仅允许一个活动用户订阅。 实际上，单个用户可能存在许多活动订阅。 下面的示例将上一个查询修改为允许多个同时活动的订阅。

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

尽管此SQL示例的复杂性不断增加，但活动订阅的`collect_list`无法保证输出与源保持相同的顺序。 要为用户创建活动订阅列表，必须使用GROUP BY或随机化来聚合列表的结果。

## 后续步骤

通过阅读本文档，您现在了解如何在Adobe Experience Platform查询服务中处理或转换使用复杂数据类型的数据集。 有关在数据湖中的数据集上运行SQL查询的详细信息，请参阅[查询执行指南](../best-practices/writing-queries.md)。
