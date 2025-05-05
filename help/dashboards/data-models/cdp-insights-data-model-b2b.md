---
title: Real-time Customer Data Platform Insights数据模型B2B edition
description: 了解如何将SQL查询与Real-time Customer Data Platform分析数据模型(B2B edition)结合使用，以自定义您自己的营销和KPI用例的Real-Time CDP报表。
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Real-Time CDP Insights数据模型B2B edition

B2B edition的Real-Time CDP分析数据模型公开了支持[帐户配置文件](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview)的分析的数据模型和SQL。 您可以自定义这些SQL查询模板，以为B2B营销和关键绩效指标(KPI)用例创建Real-Time CDP报表。 这些见解随后可用作功能板的自定义构件。

>[!AVAILABILITY]
>
>已购买Real-Time CDP Prime和Ultimate包的客户可以使用此功能。 有关更多信息，请参阅有关可用[Real-Time CDP版本](../../rtcdp/overview.md#rtcdp-editions)的文档，或与您的Adobe代表联系。

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## 先决条件

本指南要求您对自定义功能板有一定的了解。 在继续阅读本指南之前，请阅读有关[如何创建自定义仪表板](../standard-dashboards.md)的文档。

## Real-Time CDP B2B分析报告和用例 {#B2B-insight-reports-and-use-cases}

Real-Time CDP B2B报表为您的帐户配置文件数据以及帐户与机会之间的关系提供见解。 我们开发了以下星型架构模型，用于回答各种常见的营销用例，每个数据模型可以支持多个用例。

>[!IMPORTANT]
>
>用于Real-Time CDP B2B报表的数据对于所选的合并策略以及最近的每日快照而言是准确的。

### 帐户个人资料模型 {#account-profile-model}

帐户配置文件模型由八个数据集组成：

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

下图显示每个数据集中的相关数据字段、其数据类型以及将数据集链接在一起的外键。

![帐户配置文件模型的实体关系图。](../images/data-models/account-profile-model.png)

#### 按行业用例划分的新客户 {#accounts-by-industry}

用于[!UICONTROL 按行业划分的新帐户]分析的逻辑会根据帐户配置文件数及其相对大小返回排名前五的行业。 有关详细信息，请参阅[[!UICONTROL 按行业划分的新帐户]构件文档](../guides/account-profiles.md#accounts-by-industry)。

>[!TIP]
>
>您可以自定义此SQL查询，以返回比前五个行业多或少的数据。

下面的可折叠部分中显示了按行业分析生成新帐户的SQL。

+++SQL查询

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### 新帐户（按类型）用例 {#accounts-by-type}

用于[!UICONTROL 按类型]分析的新帐户的逻辑返回按类型划分的帐户的数值细目。 此洞察力有助于指导业务策略和运营，包括资源分配或营销策略。 有关详细信息，请参阅[[!UICONTROL 按类型新建帐户]构件文档](../guides/account-profiles.md#accounts-by-type)。

在下面的可折叠部分中可以看到按类型分析生成新帐户的SQL。

+++SQL查询

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

### 机会模型 {#opportunity-model}

Opportunity模型包含七个数据集：

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

下图显示了每个数据集中的相关数据字段。

![机会模型的实体关系图。](../images/data-models/opportunity-model.png)
