---
title: 探索性数据分析
description: 了解如何使用Data Distiller浏览和分析Python笔记本中的数据。
source-git-commit: 60c5a624bfbe88329ab3e12962f129f03966ce77
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 15%

---

# 探索性数据分析

本文档提供了一些使用Data Distiller探索和分析来自的数据(例如 [!DNL Python] 笔记本。

## 开始使用

在继续本指南之前，请确保已在中创建了到Data Distiller的连接， [!DNL Python] 笔记本。 有关如何执行操作的说明，请参阅文档 [连接 [!DNL Python] notebook to Data Distiller](./establish-connection.md).

## 获取基本统计信息 {#basic-statistics}

使用以下代码检索数据集中的行数和不同的用户档案。

```python
table_name = 'ecommerce_events'

basic_statistics_query = f"""
SELECT
    COUNT(_id) as "totalRows",
    COUNT(DISTINCT _id) as "distinctUsers"
FROM {table_name}"""

df = qs_cursor.query(basic_statistics_query, output="dataframe")
df
```

**示例输出**

|     | totalRows | 非重复用户 |
| --- | ----------- | -------------- |
| 0 | 1276563 | 1276563 |

## 创建大型数据集的采样版本 {#create-dataset-sample}

如果要查询的数据集非常大，或者如果不需要探索查询的准确结果，请使用 [取样功能](../../essential-concepts/dataset-samples.md) 可用于Data Distiller查询。 此过程分为两步：

- 首先， **分析** 用于创建具有指定采样率的采样版本的数据集
- 接下来，查询数据集的采样版本。 根据应用于采样数据集的函数，您可能希望将输出扩展到整个数据集的数字

### 创建5%的示例 {#create-sample}

以下示例分析数据集并创建一个5%示例：

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### 查看示例 {#view-sample}

您可以使用 `sample_meta` 函数以查看从给定数据集创建的任何示例。 下面的代码片段演示了如何使用 `sample_meta` 函数。

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**示例输出**：

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | sampling_rate | filter_condition_on_source_dataset | sample_num_rows | 已创建 |
|---|---|---|---|---|---|---|---|---|
| 0 | cmle_synthetic_data_experience_event_dataset_c... | 650f7a09ed6c3e28d34d7fc2 | 64fb4d7a7d748828d304a2f4 | 一致 | 0.5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### 查询您的示例 {#query-sample-data}

您可以通过引用返回元数据中的示例表名称来直接查询示例。 然后，可以将结果乘以采样率以获得估计值。

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# Divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**示例输出**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## 电子邮件漏斗分析 {#email-funnel-analysis}

漏斗分析是一种了解实现目标结果所需的步骤以及完成每个步骤的用户数量的方法。 以下示例对导致用户订阅新闻稿的步骤进行了简单的漏斗分析。 订阅结果由以下事件类型表示 `web.formFilledOut`.

首先，运行查询以获取每一步的用户数。

```python
simple_funnel_analysis_query = f'''SELECT eventType, COUNT(DISTINCT _id) as "distinctUsers",COUNT(_id) as "distinctEvents" FROM {table_name} GROUP BY eventType ORDER BY distinctUsers DESC'''

funnel_df = qs_cursor.query(simple_funnel_analysis_query, output="dataframe")
funnel_df
```

**示例输出**

|   | 事件类型 | 非重复用户 | distinctEvents |
|---|---|---|---|
| 0 | directMarketing.emailSent | 598840 | 598840 |
| 1 | directMarketing.emailOpened | 239028 | 239028 |
| 2 | web.webpagedetails.pageViews | 120118 | 120118 |
| 3 | advertising.impressions | 119669 | 119669 |
| 4 | directMarketing.emailClicked | 51581 | 51581 |
| 5 | commerce.productViews | 37915 | 37915 |
| 6 | decisioning.propositionDisplay | 37650 | 37650 |
| 7 | web.webinteraction.linkClicks | 37581 | 37581 |
| 8 | web.formFilledOut | 17860 | 17860 |
| 9 | advertising.clicks | 7610 | 7610 |
| 10 | decisioning.propositionInteract | 2964 | 2964 |
| 11 | decisioning.propositionDismiss | 2889 | 2889 |
| 12 | commerce.purchases | 2858 | 2858 |

{style="table-layout:auto"}

### 绘制查询结果 {#plot-results}

接下来，使用 [!DNL Python] `plotly` 库：

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**示例输出**

![eventType电子邮件漏斗的信息图。](../../images/data-distiller/email-funnel.png)

## 事件关联 {#event-correlations}

另一种常见分析是计算事件类型与目标转化事件类型之间的关联。 在此示例中，订阅事件由表示 `web.formFilledOut`. 此示例使用 [!DNL Spark] 可在Data Distiller查询中使用的函数以实现以下步骤：

1. 按配置文件计算每种事件类型的事件数。
2. 跨配置文件汇总每个事件类型的计数，并通过计算每个事件类型的关联 `web,formFilledOut`.
3. 将计数和关联的数据流转换为每个特征的皮尔森相关系数（事件类型计数）与目标事件的表。
4. 以图表的形式显示结果。

此 [!DNL Spark] 函数会聚合数据以返回一个小型结果表，这样您就可以在整个数据集中执行此类查询。

```python
large_correlation_query=f'''
SELECT SUM(webFormsFilled) as webFormsFilled_totalUsers,
       SUM(advertisingClicks) as advertisingClicks_totalUsers,
       SUM(productViews) as productViews_totalUsers,
       SUM(productPurchases) as productPurchases_totalUsers,
       SUM(propositionDismisses) as propositionDismisses_totaUsers,
       SUM(propositionDisplays) as propositionDisplays_totaUsers,
       SUM(propositionInteracts) as propositionInteracts_totalUsers,
       SUM(emailClicks) as emailClicks_totalUsers,
       SUM(emailOpens) as emailOpens_totalUsers,
       SUM(webLinkClicks) as webLinksClicks_totalUsers,
       SUM(webPageViews) as webPageViews_totalusers,
       corr(webFormsFilled, emailOpens) as webForms_EmailOpens,
       corr(webFormsFilled, advertisingClicks) as webForms_advertisingClicks,
       corr(webFormsFilled, productViews) as webForms_productViews,
       corr(webFormsFilled, productPurchases) as webForms_productPurchases,
       corr(webFormsFilled, propositionDismisses) as webForms_propositionDismisses,
       corr(webFormsFilled, propositionInteracts) as webForms_propositionInteracts,
       corr(webFormsFilled, emailClicks) as webForms_emailClicks,
       corr(webFormsFilled, emailOpens) as webForms_emailOpens,
       corr(webFormsFilled, emailSends) as webForms_emailSends,
       corr(webFormsFilled, webLinkClicks) as webForms_webLinkClicks,
       corr(webFormsFilled, webPageViews) as webForms_webPageViews
FROM(
    SELECT _{tenant_id}.cmle_id as userID,
            SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) as webFormsFilled,
            SUM(CASE WHEN eventType='advertising.clicks' THEN 1 ELSE 0 END) as advertisingClicks,
            SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) as productViews,
            SUM(CASE WHEN eventType='commerce.productPurchases' THEN 1 ELSE 0 END) as productPurchases,
            SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) as propositionDismisses,
            SUM(CASE WHEN eventType='decisioning.propositionDisplay' THEN 1 ELSE 0 END) as propositionDisplays,
            SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) as propositionInteracts,
            SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) as emailClicks,
            SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) as emailOpens,
            SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) as emailSends,
            SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) as webLinkClicks,
            SUM(CASE WHEN eventType='web.webinteraction.pageViews' THEN 1 ELSE 0 END) as webPageViews
    FROM {table_name}
    GROUP BY userId
)
'''
large_correlation_df = qs_cursor.query(large_correlation_query, output="dataframe")
large_correlation_df
```

**示例输出**：

|   | webFormsFilled_totalUsers | advertisingClicks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDismisses_totaUsers | propositionDisplays_totaUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | ... | webForms_advertisingClicks | webForms_productViews | webForms_productPurchases | webForms_propositionDismisses | webForms_propositionInteracts | webForms_emailClicks | webForms_emailOpens | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | … | 0.026805 | 0.2779 | None | 0.06014 | 0.143656 | 0.305657 | 0.218874 | 0.192836 | 0.259353 | None |

{style="table-layout:auto"}

### 将行转换为事件类型关联 {#event-type-correlation}

接下来，将上面查询输出中的单行数据转换为一个表，该表显示每种事件类型与目标订阅事件的关联：

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**示例输出**：

|    | 变量 | 值 | 特征 | 皮尔逊关联 |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0.218874 | EmailOpens | 0.218874 |
| 1 | `webForms_advertisingClicks` | 0.026805 | 广告点击量 | 0.026805 |
| 2 | `webForms_productViews` | 0.277900 | 产品视图 | 0.277900 |
| 3 | `webForms_productPurchases` | 0.000000 | 产品购买 | 0.000000 |
| 4 | `webForms_propositionDismisses` | 0.060140 | propositionDismises | 0.060140 |
| 5 | `webForms_propositionInteracts` | 0.143656 | propositionInteracts | 0.143656 |
| 6 | `webForms_emailClicks` | 0.305657 | 电子邮件点击次数 | 0.305657 |
| 7 | `webForms_emailOpens` | 0.218874 | emailOpens | 0.218874 |
| 8 | `webForms_emailSends` | 0.192836 | emailSends | 0.192836 |
| 9 | `webForms_webLinkClicks` | 0.259353 | webLinkClicks | 0.259353 |
| 10 | `webForms_webPageViews` | 0.000000 | webPageViews | 0.000000 |


最后，您可以可视化与 `matplotlib` Python库：

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![事件结果的皮尔逊事件关联的条形图](../../images/data-distiller/pearson-correlations.png)

## 后续步骤

通过阅读本文档，您已了解如何使用Data Distiller来探索和分析来自的数据 [!DNL Python] 笔记本。 在机器学习环境中创建从Experience Platform到馈送自定义模型的功能管道的下一步是 [机器学习的工程师功能](./feature-engineering.md).
