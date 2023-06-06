---
title: 基于十分位数的派生属性用例
description: 本指南演示了使用查询服务创建基于十分位数的派生属性以与配置文件数据一起使用所需的步骤。
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# 基于十分位数的派生属性用例

派生属性有助于分析来自Data Lake的数据（可用于其他下游Platform服务或发布到您的Real-time Customer Profile数据中）的复杂用例。

此示例用例演示了如何创建基于十分位数的派生属性，以便与实时客户档案数据一起使用。 本指南以航空公司忠诚度方案为例，告知您如何创建数据集，该数据集使用分类十分位数根据排名属性划分和创建受众。

说明了以下主要概念：

* 用于十分位数分段的架构创建。
* 绝对十进制的创建。
* 创建复杂的派生属性。
* 计算回顾期间的十分位数。
* 一个示例查询，用于演示聚合、排名和添加唯一标识，以允许基于这些十分位数存储桶生成受众。

## 快速入门

本指南要求您实际了解 [查询服务中的查询执行](../best-practices/writing-queries.md) 以及Adobe Experience Platform的以下组件：

* [Real-time Customer Profile概述](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [模式组合基础](../../xdm/schema/composition.md)：对Experience Data Model (XDM)架构以及构建架构的构建块、原则和最佳实践的简介。
* [如何为Real-time Customer Profile启用架构](../../profile/tutorials/add-profile-data.md)：本教程概述了将数据添加到Real-Time Customer Profile所需的步骤。
* [如何定义自定义数据类型](../../xdm/api/data-types.md)：数据类型用作类或架构字段组中的引用类型字段，并允许一致地使用可以包含在架构中任何位置的多字段结构。

## 目标

本文档中给出的示例使用十分位数构建派生属性，用于排名来自航空公司忠诚度架构的数据。 通过派生属性，可根据所选类别的前“n”%确定受众，从而最大限度地提高数据的效用。

## 构建基于十分位数的派生属性

要根据特定维度和相应的量度定义十分位数排名，必须设计架构以允许十分位数分段。

本指南使用航空公司忠诚度数据集来演示如何使用查询服务根据各个回顾期间的飞行英里数构建十分位。

## 使用查询服务创建十分位

使用查询服务，您可以创建包含类别十分位数的数据集，然后可以对其进行分段以根据属性排名创建受众。 只要定义了类别并且量度可用，就可以应用以下示例中显示的概念来创建其他十进制存储段数据集。

示例航空公司忠诚度数据使用 [XDM ExperienceEvents类](../../xdm/classes/experienceevent.md). 每个活动都是业务交易的记录，包括里程数（记入或借记）以及“传单”、“常用”、“银牌”或“金牌”的会员忠诚度状态。 主标识字段为 `membershipNumber`.

### 示例数据集

此示例的初始航空公司忠诚度数据集为“航空公司忠诚度数据”，并具有以下架构。 请注意，架构的主要标识为 `_profilefoundationreportingstg.membershipNumber`.

![航空公司忠诚度数据架构的示意图。](../images/use-cases/airline-loyalty-data.png)

**示例数据**

下表显示了 `_profilefoundationreportingstg` 用于此示例的对象。 它提供了使用十进制存储桶创建复杂派生属性的上下文。

>[!NOTE]
>
>为简单起见，租户ID `_profilefoundationreportingstg` 在列标题中命名空间的开头处省略，并且文档中的后续提及都省略。

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | 新成员 | 5000 | 传单 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | 银级 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | 银级 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | 银级 |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | 新信用卡 | 10000 | 传单 |

{style="table-layout:auto"}

## 生成十进制数据集

在上面所示的航空公司忠诚度数据中， `.mileage` 值包含成员每次飞行的英里数。 此数据用于在生命周期回顾和各种回顾期间为飞行英里数创建十分位。 为此，将创建一个数据集，该数据集在每个回顾期间的映射数据类型中包含十分位，并为下分配的每个回顾期间包含适当的十分位 `membershipNumber`.

创建“航空公司忠诚度十分位数架构”以使用查询服务创建十分位数数据集。

![“航空公司忠诚度十分位数模式”的图表。](../images/use-cases/airline-loyalty-decile-schema.png)

### 为Real-time Customer Profile启用架构

被引入Experience Platform以供Real-time Customer Profile使用的数据必须符合 [为配置文件启用的体验数据模型(XDM)架构](../../xdm/ui/resources/schemas.md). 要为配置文件启用架构，它必须实施XDM Individual Profile或XDM ExperienceEvent类。

[使用架构注册表API启用架构以在Real-Time Customer Profile中使用](../../xdm/tutorials/create-schema-api.md) 或 [架构编辑器用户界面](../../xdm/tutorials/create-schema-ui.md).  有关如何为配置文件启用架构的详细说明，请参阅其各自的文档。

接下来，创建一个数据类型以重复用于所有十进制相关的字段组。 创建十分位数字段组是每个沙盒的一次性步骤。 它也可用于所有与十分位数相关的架构。

### 创建身份命名空间并将其标记为主要标识符 {#identity-namespace}

为与十分位数一起使用而创建的任何架构都必须分配有主标识。 您可以 [在Adobe Experience Platform架构UI中定义标识字段](../../xdm/ui/fields/identity.md#define-an-identity-field)，或通过 [架构注册表API](../../xdm/api/descriptors.md#create).

查询服务还允许您直接通过SQL为临时架构数据集字段设置标识或主标识。 请参阅相关文档 [在临时架构标识中设置辅助标识和主标识](../data-governance/ad-hoc-schema-identities.md) 了解更多信息。

### 创建查询以计算回顾期间的十分位 {#create-a-query}

以下示例演示了用于计算回溯时段内十分位数的SQL查询。

可以使用UI中的查询编辑器或通过 [查询服务API](../api/query-templates.md#create-a-query-template).

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

### 查询审核

下面将更详细地检查示例查询的各个部分。

#### 回顾时段

十分位数数据类型包含1、3、6、9、12和生命周期回溯的存储桶。 查询使用回顾周期1、3和6个月，因此每个部分将包含一些“重复”查询，以便为每个回顾周期创建临时表。

>[!NOTE]
>
>如果源数据没有可用于确定回顾期间的列，则所有十分位数类排名都将根据 `decileMonthAll`.

#### 聚合

在创建十分位数存储桶之前，使用公用表表达式(CTE)将里程聚合在一起。 这会提供特定回顾期间的总英里数。 CTE是暂时存在的，只能在较大的查询范围内使用。

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

该块在模板中重复两次(`summed_miles_3` 和 `summed_miles_6`)，更改了日期计算以便生成其他回顾期间的数据。

请务必注意查询的身份、维度和量度列(`membershipNumber`， `loyaltyStatus` 和 `totalMiles` （分别）。

#### 排名

十分位数允许您执行分类分段。 要创建排名编号，请 `NTILE` 函数与参数 `10` 在按以下对象分组的窗口中： `loyaltyStatus` 字段。 这会导致排名从1到10。 设置 `ORDER BY` 子句 `WINDOW` 到 `DESC` 以确保排名值为 `1` 提供给 **greatest** 维度中的量度。

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

对于多个回顾期间，您需要使用 `MAP_FROM_ARRAYS` 和 `COLLECT_LIST` 函数。 在示例代码片段中， `MAP_FROM_ARRAYS` 使用一对键创建映射(`loyaltyStatus`)和值(`decileBucket`)数组。 `COLLECT_LIST` 返回一个数组，该数组包含指定列中的所有值。

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
>如果仅在生命周期内需要十分位数排名，则不需要聚合映射。

#### 唯一标识

唯一标识列表(`membershipNumber`)才能创建所有成员资格的唯一列表。

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>如果仅在生命周期期内需要十分位数排名，则可以忽略此步骤并聚合以下各项 `membershipNumber` 可以在最后一步完成。

#### 拼合所有临时数据

最后一步是将所有临时数据拼合到一个表单中，该表单与字段组中的十进制的结构相同。

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

如果只有生命周期数据可用，则您的查询将显示如下：

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

由于使用了十位数，因此查询结果中可确保排名数和百分位数之间的相关性。 每个排名相当于排名10%，因此根据前30%确定受众只需针对排名1、2和3。

### 运行查询模板

运行查询以填充十分位数数据集。 您还可以将查询另存为模板，并安排其以节奏运行。 当另存为模板时，还可以更新查询以使用引用了 `table_exists` 命令。 有关如何使用 `table_exists`命令位于 [SQL语法指南](../sql/syntax.md#table-exists).

## 后续步骤

以上提供的示例用例重点说明了使十进制属性在实时客户档案中可用的步骤。 这允许分段服务通过用户界面或RESTful API基于这些十分位数存储桶生成受众。 请参阅 [分段服务概述](../../segmentation/home.md) 有关如何创建、评估和访问区段的信息。
