---
keywords: Experience Platform；查询服务；查询服务；嵌套数据结构；嵌套数据；
title: 在查询服务中使用嵌套数据结构
description: 本文档提供了一个使用CTAS和INSERT INTO语句处理和转换嵌套数据字段的工作示例。
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# 在查询服务中使用嵌套数据结构

Adobe Experience Platform查询服务支持使用嵌套数据字段。 企业数据结构的复杂性会使这些数据的转换或处理变得复杂。 本文档提供了有关如何创建、处理或转换具有复杂数据类型（包括嵌套数据结构）的数据集的示例。

查询服务提供 [!DNL PostgreSQL] 界面，用于对由Experience Platform管理的所有数据集运行SQL查询。 Platform支持在表列（如struct 、 arrays 、 maps和深度嵌套的struct 、 arrays和maps ）中使用原始或复杂数据类型。 数据集还可以包含嵌套结构，其中列数据类型可以像嵌套结构数组一样复杂，或者包含映射映射，其中键值对的值可以是具有多个嵌套级别的结构。

## 快速入门

本教程需要使用第三方PSQL客户端或查询编辑器工具在Experience Platform用户界面(UI)中编写、验证和运行查询。 有关如何通过UI运行查询的完整详细信息请参见 [查询编辑器UI指南](../ui/user-guide.md). 有关第三方桌面客户端可以连接到查询服务的详细列表，请参阅 [客户端连接概述](../clients/overview.md).

您还应很好地了解 `INSERT INTO` 和 `CTAS` 语法。 欲知关于其用途的特定信息，请参阅 [`INSERT INTO`](../sql/syntax.md#insert-into) 和 [`CTAS`](../sql/syntax.md#create-table-as-select) 的部分 [SQL语法参考文档](../sql/syntax.md).

## 创建数据集

查询服务提供Create Table作为选择(`CTAS`)功能，用于根据 `SELECT` 语句，或者像在本例中一样，使用对Adobe Experience Platform中现有XDM架构的引用。 下面显示的是的XDM架构 `Final_subscription` 已针对此示例创建。

![final_subscription模式的图表。](../images/best-practices/final-subscription-schema.png)

以下示例演示了用于创建 `final_subscription_test2` 数据集。 `final_subscription_test2` 创建时使用 `Final_subscription` 架构。 使用从源中提取数据 `SELECT` 子句以填充某些行。

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

在初始数据集中 `final_subscription_test2`，struct数据类型用于同时包含 `subscription` 字段和 `userid` 对于每个用户都是唯一的。 此 `subscription` 字段描述用户的产品订阅。 可以有多个订阅，但一个表只能包含每行一个订阅的信息。

## 使用INSERT INTO更新嵌套数据字段

在 `final_subscription_test2` 已创建数据集， `INSERT INTO` 语句用于将其他数据附加到表。 在复制数据时，源和目标中的数据类型必须匹配。 或者，源数据类型必须是 `CAST` 到目标数据类型。 然后，使用以下SQL将增量数据添加到目标数据集中。

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

要从数据集中查找用户的活动订阅列表，必须编写一个查询，将数组的元素分为多个行和列。 要实现此目的，您必须首先了解数据模型的形状，因为订阅信息将保存在嵌套在数据集中的数组内。

PSQL `\d` 命令用于逐级导航到所需的订阅数据。 这些表说明了 `final_subscription_test2` 数据集。 复杂数据类型不是典型的类型值（如文本、布尔值、时间戳等），因此一眼就能识别。

| 栏目 | 类型 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

下一列的字段使用 `\d final_subscription_test2__lumaservices3` 命令。

| 栏目 | 类型 |
|---------|-------|
| `userid` | 文本 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 是一个结构元素数组。 其字段使用 `\d _lumaservices3_subscription_e[]` 命令。

| 栏目 | 类型 |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | 文本 |
| `offer_id` | 文本 |
| `subscription_id` | 文本 |

要查询订阅的嵌套字段，必须首先分隔 `subscription` 数组，并使用explode函数返回结果。 以下SQL示例返回用户的活动订阅，该订阅基于 `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

此简化的示例解决方案仅允许一个活动用户订阅。 实际上，单个用户可以有多个活动订阅。 下面的示例修改了之前的查询，以允许同时使用多个活动订阅。

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

尽管此SQL示例的复杂性不断增加， `collect_list` 对于活动订阅，并不保证输出与源的顺序相同。 要为用户创建活动订阅列表，必须使用GROUP BY或随机排列来聚合列表的结果。

## 后续步骤

通过阅读本文档，您现在了解如何在Adobe Experience Platform查询服务中处理或转换使用复杂数据类型的数据集。 请查看 [查询执行指南](../best-practices/writing-queries.md) 有关对Data Lake中的数据集运行SQL查询的详细信息。
