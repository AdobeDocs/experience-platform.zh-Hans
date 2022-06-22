---
title: 派生属性
description: 派生属性允许您在常规轮次上计算属性，并（可选）将这些派生属性作为配置文件属性发布到实时客户配置文件中。 本文档概述了如何使用查询服务创建派生属性，以便与用户档案数据一起使用。
hide: true
hidefromtoc: true
source-git-commit: fc2d2e7dadb95460f5d735ba33e5f106880a0198
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---

# 派生属性

派生属性允许您在常规轮次上计算属性，并（可选）将这些派生属性作为配置文件属性发布到实时客户配置文件中。

对于分析用户档案数据的各种用例，派生属性（如使用十次数据创建的属性）是必需的。 使用十进制数据，您可以根据区段的百分位数或给定属性的排名，从区段创建受众。 例如，潜在用例可能包括：

* 根据按频道的收视量确定最低10%的订阅者。 这将允许营销人员定位特定受众并销售新订阅者包。
* 根据旅行里程总数确定在前10%的传单中具有“传单”状态的受众。 此受众可用于有选择地定位新信用卡选件的销售。

## 快速入门

此概述需要对 [平台API调用](../landing/api-guide.md) 及Adobe Experience Platform的以下组成部分：

* [实时客户资料概述](../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [架构组合的基础知识](../xdm/schema/composition.md):介绍体验数据模型(XDM)架构以及构建架构的构建块、原则和最佳实践。
* [如何为实时客户用户档案启用架构](../profile/tutorials/add-profile-data.md):本教程概述了向实时客户用户档案添加数据所需的步骤。

## 对派生属性的SQL支持

要根据特定维度（类别）和相应量度（收入、点数、观看持续时间等）定义十文件的排名，必须设计架构以允许进行十文件分段。 此架构可用作较大的配置文件架构的一部分。

### 为配置文件架构创建标识命名空间 {#identity-namespace}

身份命名空间是 [ Identity Service](../identity-service/home.md) 的组件，充当与身份相关的上下文指示器。完全限定的标识包括ID值和命名空间。 在配置文件片段之间匹配和合并记录数据时，标识值和命名空间必须匹配。

创建的与身份相关的数据集可以作为数据组分组在一起，并有助于维护数据生命周期。 自定义命名空间可使用 [Identity Service API](../identity-service/api/create-custom-namespace.md) 或通过UI。 请参阅 [管理自定义命名空间文档](../identity-service/namespaces.md#manage-namespaces) 以了解如何通过UI执行此操作。

主标识描述符可以分配给架构UI中的字段，也可以使用架构注册表API创建。 有关如何 [在Adobe Experience Platform UI中定义标识字段](../xdm/ui/fields/identity.md#define-an-identity-field)，或通过 [架构注册表API](../xdm/api/descriptors.md#create).

查询服务还允许您直接通过SQL为临时架构数据集字段设置标识或主标识。 请参阅 [在临时架构标识中设置辅助标识和主标识](./data-governance/ad-hoc-schema-identities.md) 以了解更多信息。

## 创建派生属性

本文档中提供的示例查询重点介绍用于对大型数据集进行分类和对数据从最高值到最低值（或反之）进行排名的文件，并根据时间段进行过滤。

### 德基莱 {#deciles}

10是一种将一组排名数据拆分为10个相等部分的方法。 当数据被划分为十个文件时，会为数据集中的每一行分配一个十个级别。 这允许数据按降序或升序顺序排序。

10级按从低到高的顺序排列数据，并按1到10的比例进行，其中每个连续数都对应于增加10个百分点。

十个分类存储段表示排名组的数量，用于为数据集中的维度（类别）分配排名。 该存储段可以是一个数字或表达式，其计算结果为每个分区的正整数值。 存储段不得具有空值。

四分位数用于将分布除以四，百分位数除以100。

### 为数据存储段创建架构 {#create-schema}

为十个存储段创建的架构有三个组成部分：数据类型、数据类型的字段组（每个源数据集）和主标识字段。

>[!NOTE]
>
>必须先创建标识命名空间，然后才能创建架构。 请参阅 [标识命名空间](#identity-namespace) 部分以了解更多详细信息。

Adobe提供了多个标准（“核心”）XDM类，包括XDM个人配置文件和XDM ExperienceEvent。 除了这些核心类之外，您还可以创建自己的自定义类，以描述贵组织的更具体用例。 请参阅有关如何 [在UI中创建和编辑架构](../xdm/ui/resources/schemas.md#create) 或使用 [架构注册API中的架构端点](../xdm/api/schemas.md#create) 以了解更多详细信息。

被摄取到Experience Platform以供实时客户资料使用的数据必须符合为资料启用的体验数据模型(XDM)架构。 要为配置文件启用架构，必须实施XDM个人配置文件或XDM ExperienceEvent类。

您可以 [使用架构注册API启用可在实时客户资料中使用的架构](../xdm/tutorials/create-schema-api.md) 或 [架构编辑器用户界面](../xdm/tutorials/create-schema-ui.md).  有关如何为用户档案启用架构的详细说明，请参阅其各自的文档。

### 创建数据类型 {#create-data-type}

数据类型用作类或架构字段组中的引用类型字段，并允许一致地使用可在架构中任何位置包含的多字段结构。 数据类型的创建是每个沙盒的一次性步骤，因为它可以重复用于所有与文件相关的字段组。

有关如何 [定义自定义数据类型](../xdm/api/data-types.md) 使用 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### 创建文件字段组 {#create-field-group}

字段组的创建是每个沙盒的一次性步骤。 它还可以重复用于所有与文件相关的架构。

有关如何 [通过UI创建字段组](../xdm/ui/resources/field-groups.md#create)

## 使用查询服务创建文件

查询服务提供了一种创建包含类别文件的数据集的理想方法。 然后，可以将它与Segmentation Service结合使用，以根据属性排名创建受众。

只要定义了类别（维度）并且量度可用，以下示例中显示的概念便可用于创建其他十年级存储段数据集。 这些示例基于航空公司忠诚度计划的数据。 航空公司忠诚度数据利用体验事件类，其中每个事件是 **里程**、贷记或借记以及会员资格 **忠诚度状态** “传单”、“常客”、“银色”或“金色”。 主标识字段为 `membershipNumber`.

### 创建查询模板 {#create-a-query-template}

可以使用UI中的查询编辑器创建模板，或通过 [查询服务API](./api/query-templates.md#create-a-query-template).

将更详细地检查下面显示的查询模板的各个部分。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### 回顾时段

十年数据类型包含用于1、3、6、9、12和生命周期回顾的存储段。 查询使用的回顾时间段为1、3和6个月，因此每个部分都将包含一些“重复”查询，以便为每个回顾时间段创建临时表。

>[!NOTE]
>
>如果源数据没有可用于确定回顾周期的列，则所有十级类排名都将在 `decileMonthAll`.

#### 聚合

使用通用表表达式(CTE)在创建十年级存储段之前，先将里程汇总在一起。 这会提供特定回顾时段的总里程数。 CTE暂时存在，并且仅在较大查询的范围内可用。

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

块在模板中重复两次(`summed_miles_3` 和 `summed_miles_6`)，以便为其他回顾时段生成数据。

请注意查询的标识、维度和量度列(`membershipNumber`, `loyaltyStatus` 和 `totalMiles` )。

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

### 运行查询模板

查询可以是 [通过UI执行](./ui/user-guide.md#executing-queries) 或 [查询服务API](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

由于使用了十位数，因此查询结果中保证了排名数与百分位数之间的关联。 每个等级等于10%，因此根据前30%的受众来识别受众，只需将1、2和3等级设为目标。

## 后续步骤

Segmentation Service提供了用户界面和RESTful API，允许您根据这些数据存储段生成受众。 请参阅 [Segmentation Service概述](../segmentation/home.md) 有关如何创建、评估和访问区段的信息。

有关如何在区段生成器（分段服务的UI实施）中创建和使用区段的详细信息，请参阅 [区段生成器指南](../segmentation/ui/overview.md).

有关使用API构建区段定义的信息，请参阅 [使用API创建受众区段](../segmentation/tutorials/create-a-segment.md).
