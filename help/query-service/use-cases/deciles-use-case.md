---
title: 基于数据集的派生属性用例
description: 本指南演示了使用查询服务创建基于文件的派生属性以用于用户档案数据所需的步骤。
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# 基于数据的派生属性用例

派生属性有助于分析数据湖中的数据的复杂用例，这些数据湖可用于其他下游平台服务或发布到您的实时客户资料数据中。

此示例用例演示了如何创建基于数据的派生属性，以用于实时客户资料数据。 以航空公司忠诚度方案为例，本指南会告知您如何创建使用类别数据进行分段的数据集，以及如何根据排名属性创建受众。

下列主要概念如下所示：

* 为分段分段创建架构。
* 类别数据创建。
* 创建复杂的派生属性。
* 在回顾期内计算十文件。
* 一个示例查询，用于演示聚合、排名和添加唯一标识，以便允许根据这些十个分时段生成受众。

## 快速入门

本指南需要对 [查询服务中的查询执行](../best-practices/writing-queries.md) 及Adobe Experience Platform的以下组成部分：

* [实时客户资料概述](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [架构组合的基础知识](../../xdm/schema/composition.md):介绍体验数据模型(XDM)架构以及构建架构的构建块、原则和最佳实践。
* [如何为实时客户用户档案启用架构](../../profile/tutorials/add-profile-data.md):本教程概述了向实时客户用户档案添加数据所需的步骤。
* [如何定义自定义数据类型](../../xdm/api/data-types.md):数据类型用作类或架构字段组中的引用类型字段，并允许一致地使用可在架构中任何位置包含的多字段结构。

## 目标

本文档中提供的示例使用数据集构建派生属性，以从航空公司忠诚度架构对数据进行排名。 利用派生属性，可根据所选类别的前“n”%来识别受众，从而最大化数据的效用。

## 构建基于数据集的派生属性

要根据特定维度和相应量度定义文件排名，必须设计一种架构以允许分数据分段。

本指南使用航空公司忠诚度数据集来演示如何使用查询服务根据不同回顾期间飞行的里程来构建数据。

## 使用查询服务创建文件

使用查询服务，您可以创建包含类别文件的数据集，然后对类别文件进行分段，以根据属性排名创建受众。 只要定义了类别并且量度可用，以下示例中显示的概念便可用于创建其他十年级存储段数据集。

航空公司忠诚度数据示例使用 [XDM ExperienceEvents类](../../xdm/classes/experienceevent.md). 每个事件都是一项里程业务交易记录，包括记入或借记的里程数，以及“传单”、“常客”、“银”或“金”的会员忠诚度状态。 主标识字段为 `membershipNumber`.

### 示例数据集

此示例的初始航空公司忠诚度数据集为“航空公司忠诚度数据”，且具有以下架构。 请注意，架构的主标识是 `_profilefoundationreportingstg.membershipNumber`.

![航空公司忠诚度数据架构的图表。](../images/use-cases/airline-loyalty-data.png)

**示例数据**

下表显示 `_profilefoundationreportingstg` 对象。 它为使用数据存储段创建复杂派生属性提供了上下文。

>[!NOTE]
>
>为简便起见，租户ID `_profilefoundationreportingstg` 在列标题中的命名空间开头以及整个文档中的后续提及中已忽略。

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | 新会员 | 5000 | 飞片 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | 肯尼迪机场 | 7500 | 银色 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | 肯尼迪机场 | 7500 | 银色 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | 银色 |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | 新信用卡 | 10000 | 飞片 |

{style=&quot;table-layout:auto&quot;}

## 生成数据集

在上面显示的航空公司忠诚度数据中， `.mileage` 值包含成员每次乘坐飞机时飞行的英里数。 此数据用于为在生命周期回顾和各种回顾期内飞行的英里数创建十位数。 为此，会创建一个数据集，其中包含每个回顾期的映射数据类型中的文件，以及在 `membershipNumber`.

创建“航空忠诚度分级架构”，以使用查询服务创建分级数据集。

![“航空公司忠诚度决策架构”的图表。](../images/use-cases/airline-loyalty-decile-schema.png)

### 启用实时客户用户档案的架构

被摄取到Experience Platform以供实时客户资料使用的数据必须符合 [为用户档案启用的体验数据模型(XDM)架构](../../xdm/ui/resources/schemas.md). 要为配置文件启用架构，必须实施XDM个人配置文件或XDM ExperienceEvent类。

[使用架构注册API启用您的架构，以便在实时客户资料中使用](../../xdm/tutorials/create-schema-api.md) 或 [架构编辑器用户界面](../../xdm/tutorials/create-schema-ui.md).  有关如何为用户档案启用架构的详细说明，请参阅其各自的文档。

接下来，创建一个数据类型，以便重新用于所有与文件相关的字段组。 创建decile字段组是每个沙盒的一个步骤。 它还可以重复用于所有与文件相关的架构。

### 创建标识命名空间并将其标记为主标识符 {#identity-namespace}

创建的任何用于文件的架构都必须分配了主标识。 您可以 [在Adobe Experience Platform模式UI中定义标识字段](../../xdm/ui/fields/identity.md#define-an-identity-field)，或通过 [架构注册表API](../../xdm/api/descriptors.md#create).

查询服务还允许您直接通过SQL为临时架构数据集字段设置标识或主标识。 请参阅 [在临时架构标识中设置辅助标识和主标识](../data-governance/ad-hoc-schema-identities.md) 以了解更多信息。

### 创建查询以计算回顾期内的文件 {#create-a-query}

以下示例演示了在回顾期间计算十进制文件的SQL查询。

可以使用UI中的查询编辑器创建模板，或通过 [查询服务API](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### 查询审阅

下面将详细检查示例查询的各个部分。

#### 回顾期

十年数据类型包含用于1、3、6、9、12和生命周期回顾的存储段。 查询使用的回顾期为1、3和6个月，因此每个部分都将包含一些“重复”查询，以便为每个回顾期创建临时表。

>[!NOTE]
>
>如果源数据没有可用于确定回顾周期的列，则所有十级类排名都将在 `decileMonthAll`.

#### 聚合

使用通用表表达式(CTE)在创建十年级存储段之前，先将里程汇总在一起。 这会提供特定回顾期的总英里数。 CTE暂时存在，并且仅在较大查询的范围内可用。

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

块在模板中重复两次(`summed_miles_3` 和 `summed_miles_6`)，以便为其他回顾期生成数据。

请务必记下查询(`membershipNumber`, `loyaltyStatus` 和 `totalMiles` )。

#### 排名

数据集允许您执行类别分段。 要创建排名数字，请 `NTILE` 函数与的参数一起使用 `10` 按 `loyaltyStatus` 字段。 这将产生从1到10的排名。 设置 `ORDER BY` 条款 `WINDOW` to `DESC` 以确保 `1` 是给 **最大** 量度。

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### 映射聚合

对于多个回顾期，您需要使用 `MAP_FROM_ARRAYS` 和 `COLLECT_LIST` 函数。 在示例代码片段中， `MAP_FROM_ARRAYS` 创建一对键的映射(`loyaltyStatus`)和值(`decileBucket`)数组。 `COLLECT_LIST` 返回一个数组，其中包含指定列中的所有值。

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>如果仅在生命周期期间需要十年级别，则不需要映射聚合。

#### 唯一标识

唯一标识的列表(`membershipNumber`)才能创建所有成员关系的唯一列表。

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>如果仅在生命周期期间需要进行分级排名，则可以忽略此步骤并聚合 `membershipNumber` 可以在最后步骤中完成。

#### 拼合所有临时数据

最后一步是将所有临时数据拼合到一个与字段组中文件结构相同的表单中。

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

如果仅存留期数据可用，则查询将如下所示：

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

由于使用了十位数，因此查询结果中保证了排名数与百分位数之间的关联。 每个等级等于10%，因此根据前30%的受众来识别受众，只需将1、2和3等级设为目标。

### 运行查询模板

运行查询以填充十个数据集。 您还可以将查询另存为模板，并安排查询在某个频率下运行。 另存为模板时，还可以更新查询，以使用引用 `table_exists` 命令。 有关如何使用 `table_exists`命令 [SQL语法指南](../sql/syntax.md#table-exists).

## 后续步骤

上面提供的示例用例重点介绍了如何在实时客户资料中提供文档属性的步骤。 这允许Segmentation Service通过用户界面或RESTful API，能够根据这些数据存储段生成受众。 请参阅 [Segmentation Service概述](../../segmentation/home.md) 有关如何创建、评估和访问区段的信息。
