---
title: 帐户配置文件分析
description: 发现支持您的帐户配置文件分析的SQL，并使用这些查询生成自定义分析，从而进一步探索您的客户及其消费者体验。
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 帐户配置文件分析

[帐户配置文件](../../rtcdp/accounts/account-profile-overview.md)用于合并来自各种来源（包括多个营销渠道和组织系统）的帐户信息。 此统一视图允许全面了解客户帐户，从而增强B2B营销活动。 通过分析数据模型得出的洞察信息使Adobe Real-time Customer Data Platform B2B数据更易于访问、理解并具有更大的决策影响力。

通过访问提供见解的SQL，您可以更好地了解您的B2B数据并生成您自己的高度自定义的可重用见解，以进一步探索您的客户帐户信息。 通过使用现有的Real-Time CDP数据模型SQL作为灵感，根据独特的业务需求创建查询，将原始数据转换为新的可操作洞察。

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

以下分析均可用作[帐户配置文件仪表板](../guides/account-profiles.md)或[自定义仪表板](../user-defined-dashboards.md)的一部分。 有关如何自定义仪表板或[在构件库和[用户定义的仪表板](../user-defined-dashboards.md#create-widget)中创建和编辑新构件](../customize/custom-widgets.md)的说明，请参阅[自定义概述](../customize/overview.md)。

## 已添加帐户轮廓 {#account-profiles-added}

通过此洞察回答的问题：

- 在给定时间段内添加了多少帐户配置文件？

+++选择以显示生成此分析的SQL

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## 按行业划分的新客户 {#accounts-by-industry}

通过此洞察回答的问题：

- 帐户配置文件所属的前五个行业是什么？

+++选择以显示生成此分析的SQL

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## 按类型的新帐户 {#accounts-by-type}

通过此洞察回答的问题：

- 按帐户类型划分的帐户数是多少？

+++选择以显示生成此分析的SQL

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

## 新增机会 {#opportunities-added}

通过此洞察回答的问题：

- 在给定时间段内添加了多少个机会？

+++选择以显示生成此分析的SQL

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## 按人员角色显示的新机会 {#opportunities-by-person-role}

通过此洞察回答的问题：

- 机会中各种角色的相对规模和数量是多少？

+++选择以显示生成此分析的SQL

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## 按收入显示的新机会 {#opportunities-by-revenue}

通过此洞察回答的问题：

- 按收入排名的前20个机会是什么（以美元计）？

+++选择以显示生成此分析的SQL

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## 按状态和阶段显示的新机会 {#opportunities-by-status-and-stage}

通过此洞察回答的问题：

- 存在哪些潜在机会？这些机会位于销售或营销漏斗的哪个阶段？
- 存在哪些已结束的销售机会？它们在销售或营销漏斗的哪个阶段完成？

+++选择以显示生成此分析的SQL

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## 赢得新机会 {#opportunities-won}

通过此洞察回答的问题：

- 已成功关闭或最终完成的机会数量是多少？

+++选择以显示生成此分析的SQL

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## 赢得的机会（折线图） {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

通过此洞察回答的问题：

- 在给定时间段内成功关闭或完成（赢得）多少机会？

+++选择以显示生成此分析的SQL

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## 后续步骤

通过阅读本文档，您现在了解了生成帐户个人资料仪表板分析的SQL以及此分析可解决哪些常见问题。 您现在可以对SQL进行编辑和迭代，以生成您自己的见解。

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

您还可以阅读并了解为[配置文件](./profiles.md)、[受众](./audiences.md)和[目标](./destinations.md)仪表板生成分析的SQL。
