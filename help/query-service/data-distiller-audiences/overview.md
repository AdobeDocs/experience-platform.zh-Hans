---
title: 使用SQL构建受众
description: 了解如何在Adobe Experience Platform的Data Distiller中使用SQL受众扩展来使用SQL命令创建、管理和发布受众。 本指南涵盖受众生命周期的所有方面，包括创建、更新和删除用户档案，以及使用数据驱动的受众定义来定位基于文件的目标。
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: c66a7cf779c1b6e55ace86916985087dfaa3363b
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 1%

---

# 使用SQL构建受众

使用SQL受众扩展通过数据湖中的数据构建受众，包括任何现有的维度实体（例如客户属性或产品信息）。

使用此SQL扩展可提高创建受众的能力，因为在定义受众区段时，您不需要在配置文件中使用原始数据。 使用此方法创建的受众会自动在受众工作区中注册，您可以进一步将这些受众定位到基于文件的目标。

![显示SQL受众扩展工作流程的信息图。 这些阶段包括：使用SQL命令通过查询服务构建受众，在平台UI中管理受众，以及在基于文件的目标中激活受众。](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

本文档介绍如何在Adobe Experience Platform的数据Distiller中使用SQL受众扩展来使用SQL命令创建、管理和发布受众。

## Data Distiller中的受众创建生命周期 {#audience-creation-lifecycle}

按照以下步骤创建、管理和激活受众。 创建的受众可无缝地集成到“受众流”中，因此您可以从基本受众构建区段，并定位基于文件的目标（例如，CSV上传或云存储位置）以进行客户外联。 “受众流”是指创建、管理和激活受众的完整过程，从而确保跨目标的无缝集成。

作为“受众流”的一部分，使用以下SQL命令在Adobe Experience Platform中[创建](#create-audience)、[修改](#add-profiles-to-audience)和[删除](#delete-audience)受众。

### 创建受众 {#create-audience}

使用`CREATE AUDIENCE AS SELECT`命令定义新受众。 创建的受众将保存在数据集中，并在Data Distiller下的[!UICONTROL 受众]工作区中注册。

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**参数**

使用以下参数定义SQL受众创建查询：

| 参数 | 描述 |
|--------------------|------------------------------------------------------------------|
| `schema` | 可选。 为查询创建的数据集定义XDM架构。 |
| `table_name` | 表和受众的名称。 |
| `primary_identity` | 指定受众的主标识列。 |
| `identity_namespace` | 标识的命名空间。 您可以使用现有命名空间或创建新命名空间。 要查看可用的命名空间，请使用`SHOW NAMESPACES`命令。 要创建新命名空间，请使用`CREATE NAMESPACE`。 例如： `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`。 |
| `select_query` | 定义受众的SELECT语句。 可在[SELECT查询](../sql/syntax.md#select-queries)部分找到SELECT查询的语法。 |

{style="table-layout:auto"}

>[!NOTE]
>
>要为复杂的数据结构提供更大的灵活性，您可以在定义受众时嵌套扩充属性。 扩充属性（如`orders`、`total_revenue`、`recency`、`frequency`和`monetization`）可用于根据需要筛选受众。

**示例：**

以下示例演示了如何构建SQL受众创建查询：

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

在此示例中，`userId`列被标识为标识列，并且分配了适当的命名空间(`lumaCrmId`)。 其余列（`orders`、`total_revenue`、`recency`、`frequency`和`monetization`）是丰富属性，为受众提供额外的上下文。

**限制：**

使用SQL创建受众时，请注意以下限制：

- 主标识列&#x200B;**必须**&#x200B;处于数据集的最高级别，且不能嵌套在其他属性或类别中。
- 使用SQL命令创建的外部受众具有30天的保留期。 30天后，这些受众将自动删除，这是规划受众管理策略时考虑的重要事项。

### 将用户档案添加到现有受众 {#add-profiles-to-audience}

使用`INSERT INTO`命令将配置文件（或整个受众）添加到现有受众。

```sql
INSERT INTO table_name
SELECT select_query
```

**参数**

下表说明了`INSERT INTO`命令所需的参数：

| 参数 | 描述 |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | 作为create audience命令的一部分创建的表的名称。 |
| `select_query` | SELECT语句。 SELECT查询的语法可以在SELECT查询部分找到。 |

{style="table-layout:auto"}

**示例：**

以下示例演示了如何使用`INSERT INTO`命令将配置文件添加到现有受众：

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### RFM模型受众示例 {#rfm-model-audience-example}

以下示例演示了如何使用“回访间隔”、“频度”和“盈利(RFM)”模型创建受众。 此示例根据回访间隔、频度和盈利得分划分客户，以确定关键群体，例如忠诚客户、新客户和高价值客户。

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

以下查询为RFM受众创建架构。 该语句设置字段以保存客户信息，如`userId`、`days_since_last_purchase`、`orders`、`total_revenue`等。

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

创建受众后，使用客户数据填充该受众，并根据其RFM得分划分用户档案。 以下SQL语句使用`NTILE(4)`函数根据客户的RFM（回访间隔、频度、盈利）得分将客户分到四分位数中。 这些分数将客户分为六个区段，例如“核心”、“忠诚度”和“鲸鱼”。 然后将分段客户数据插入到受众`adls_rfm_profile`表中。”

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
```

### 删除受众（删除受众） {#delete-audience}

使用`DROP AUDIENCE`命令删除现有受众。 如果受众不存在，则除非指定`IF EXISTS`，否则会发生异常。

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**参数**

该表包含`DROP AUDIENCE`命令所需的参数：

| 参数 | 描述 |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | 可选。 如果指定，则在未找到表的情况下，不会引发异常。 |
| `db_name` | 指定用于限定受众数据集的数据组。 |
| `table_name` | 作为create audience命令的一部分创建的表的名称。 |

{style="table-layout:auto"}

**示例：**

以下示例演示了如何使用DROP AUDIENCE命令删除受众：

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### 自动受众注册和可用性 {#registration-and-availability}

使用SQL扩展创建的受众会自动注册到Audience工作区的Data Distiller [!UICONTROL Origin]中。 注册后，这些受众即可在基于文件的目标中进行定位，从而增强分段和定位策略。 此过程不需要额外配置，可简化受众管理。 有关如何在Platform UI中查看、管理和创建受众的详细信息，请参阅[受众门户概述](../../segmentation/ui/audience-portal.md)。

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![Adobe Experience Platform中的Audience工作区，显示Distiller自动发布并可供使用的数据。](../images/data-distiller/sql-audiences/audiences.png)

## 将受众激活到目标 {#activate-audiences}

通过将受众定位到任何基于文件的目标（如[!DNL Amazon S3]、[!DNL SFTP]或[!DNL Azure Blob]）来激活受众。 可以根据需要对丰富的受众属性进行进一步细化和筛选。

![Adobe Experience Platform目标类型的流程图，显示公用和专用/自定义目标，包括批处理选项和流选项。](../images/data-distiller/sql-audiences/destination-types.png)

## 功能说明 {#faqs}

本节介绍有关在Data Distiller中使用SQL创建和管理外部受众的常见问题解答。

**问题**：

- 是否仅支持为平面数据集创建受众？

+++回答

目前，在定义受众时，受众创建仅限于平面（根级别）属性。

+++

- 创建受众会生成单个数据集还是多个数据集，或者是否因配置而异？

+++回答

受众和数据集之间存在一对一的映射。

+++

- 在受众创建期间创建的数据集是否标记为用户档案？

+++回答

不会，在创建受众期间创建的数据集不会标记为配置文件。

+++

- 是否在数据湖中创建数据集？

+++回答

是，会在数据湖中创建与受众关联的数据集。 此数据集中的属性在受众编辑器和目标流中可以作为扩充属性使用。

+++

- 受众中的属性是否仅限于基于文件的企业批处理目标？ （是或否）

+++回答

不会。受众中扩充的属性可在企业批处理目标和基于文件的目标中使用。 如果您遇到错误，如“以下区段ID具有此目标不允许的命名空间： e917f626-a038-42f7-944c-xyxyx”，请在Data Distiller中创建一个新区段，并将其用于任何可用的目标。

+++

- 我是否可以创建一个使用数据Distiller受众的受众？

+++回答

能，您可以创建使用数据Distiller受众的受众。

+++

- 这些受众是否会显示在Adobe Journey Optimizer中？ 如果没有，那么在规则生成器中创建一个包含此受众所有成员的新受众时，会发生什么情况？

+++回答

Adobe Journey Optimizer中还提供了数据Distiller受众。 您可以在Adobe Journey Optimizer中使用Data Distiller受众，并根据扩充属性筛选结果。

+++

- Data Distiller受众是外部受众，是否每30天删除一次？

+++回答

是，由于数据Distiller受众是外部受众，因此每30天会删除一次这些受众。

+++

## 后续步骤

在阅读本文档后，您已了解如何在Data Distiller中使用SQL受众扩展，以使用SQL命令有效创建、管理和发布受众。 您现在可以根据独特的业务需求自定义受众定义，并在各种目标中激活这些定义，从而优化营销策略和数据驱动型决策。

接下来，您可以阅读以下文档，以进一步开发和优化您的Platform受众管理策略：

- **浏览受众评估**：了解Adobe Experience Platform中的[受众评估方法](../../segmentation/home.md#evaluate-segments)：用于实时更新的流式分段、用于计划或按需处理的批量分段以及用于在Edge Network上即时评估的边缘分段。
- **与目标集成**：阅读有关如何使用Platform目标UI [按需将文件导出到批处理目标](../../destinations/ui/export-file-now.md)的指南。
- **审核受众性能**：分析您的SQL定义的受众在不同渠道中的执行情况。 使用数据洞察来调整和改进受众定义和定位策略。 请阅读有关[受众分析](../../dashboards/insights/audiences.md)的文档，了解如何在Adobe Real-Time CDP中访问和调整SQL查询以获取受众分析。 然后，您可以通过自定义受众仪表板创建自己的见解并将原始数据转换为可操作的信息，从而有效地可视化并使用这些见解做出更好的决策。

