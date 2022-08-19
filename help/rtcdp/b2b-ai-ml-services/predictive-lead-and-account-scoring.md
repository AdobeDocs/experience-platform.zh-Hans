---
title: Real-time CDP B2B中的预测潜在客户和客户评分
type: Documentation
description: 有关Experience PlatformCDP B2B中的预测潜在客户和帐户评分功能的概述和更多信息。
source-git-commit: 5ac8e099a6de563371f9a53a8b4816e6cf4d1953
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Real-time CDP B2B中的预测潜在客户和客户评分

B2B营销人员在营销漏斗的顶部面临多项挑战。 为了提高效率，B2B营销人员需要一种自动的方式来鉴定大量人员的资格，以便他们能够专注于高价值目标。 资格鉴定应与最终销售结果保持一致，而不仅仅是营销转化。

Accounts是购买B2B产品和服务的最终实体。 为了有效地进行营销和销售，B2B营销人员不仅需要了解个人购买的可能性，还需要了解客户购买的可能性。

尤其是基于帐户的营销，将帐户作为营销目标进行战略化。 帐户购买倾向评分可极大地帮助B2B营销人员在帐户中排定优先级，以最大化其投资回报。

预测性潜在客户和帐户评分服务通过学习机会阶段转化事件并预测机会阶段转化事件并将人员活动汇总到帐户级别以生成帐户评分来解决上述挑战。 这些得分可作为个人用户档案和帐户用户档案上的自定义字段使用，并且可以轻松作为区段标准包含在内以优化受众。 在汇总和单位级别，还提供了一些最具影响力的因素，以帮助B2B营销人员更好地了解哪些因素推动了分数。

## 了解预测潜在客户和帐户评分 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] 数据源当前是必需的，因为它是唯一可在人员配置文件级别提供转化事件的数据源。

预测潜在客户和帐户评分使用基于树的（随机林/梯度提升）机器学习方法来构建预测潜在客户评分模型。

管理员能够为每个已配置的转化事件配置多个用户档案评分目标（也称为模型），从而为每个已配置的目标生成单独的得分。

预测潜在客户和帐户评分支持以下转化目标类型和字段：

| 目标类型 | 字段 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>示例： `opportunityEvent.dataValueChanges.attributeName` 等于 `Stage` 和 `opportunityEvent.dataValueChanges.newValue` 等于 `Contract`</ul> |

算法考虑了以下属性和输入数据：

* 人员配置文件

| XDM字段 | 必填/可选 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 必需 |
| `workAddress.country` | 可选 |
| `extSourceSystemAudit.createdDate` | 必需 |
| `extendedWorkDetails.jobTitle` | 可选 |

>[!NOTE]
> 
>算法仅检查 `sourceAccountKey.sourceKey` 字段。

* 帐户配置文件

| XDM字段 | 必填/可选 |
| --- | --- |
| `accountKey.sourceKey` | 必需 |
| `extSourceSystemAudit.createdDate` | 必需 |
| `accountOrganization.industry` | 可选 |
| `accountOrganization.numberOfEmployees` | 可选 |
| `accountOrganization.annualRevenue.amount` | 可选 |

* 体验事件

| XDM字段 | 必填/可选 |
| --- | --- |
| `_id` | 必需 |
| `personKey.sourceKey` | 必需 |
| `timestamp` | 必需 |
| `eventType` | 必需 |

支持多个模型，并设置以下硬限制：

* 每个生产沙盒有权使用五种模型。
* 每个开发沙盒都有权使用一个模型。

数据质量要求如下：

* 理想情况下，为培训目的，需要使用两年的最新数据。
* 所需数据的最小长度为六个月加上预测窗口。
* 对于每个预测目标，至少需要10个符合条件的转化事件。

评分作业每天运行，结果另存为用户档案属性和帐户属性，然后可在区段定义和个性化中使用这些属性和属性。 帐户概述功能板中还提供了现成的分析分析。

有关如何 [管理预测潜在客户和帐户评分](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) 服务。

## 查看预测潜在客户和帐户评分结果 {#how-to-view}

运行作业后，结果将保存在名称下每个模型的新系统数据集中 `LeadsAI.Scores` - ***分数名称***. 每个得分字段组可位于 `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| 属性 | 描述 |
| --- | --- |
| 得分 | 配置文件在定义的时间范围内实现预测目标的相对可能性。 此值不应视为概率百分比，而应视为用户档案与整体群体的比较可能性。 此分数的范围为0到100。 |
| 百分位数 | 此值提供有关用户档案相对于其他类似评分用户档案的性能的信息。 百分位数介于1到100之间。 |
| 模型类型 | 选定的模型类型指示这是人员还是帐户分数。 |
| 得分日期 | 打分的日期。 |
| 影响因素 | 预测了用户档案可能转换的原因。 因素包括以下属性：<ul><li>代码：积极影响用户档案预测分数的用户档案或行为属性。</li><li>值：配置文件或行为属性的值。</li><li>重要性：指示用户档案或行为属性对预测得分（低、中、高）的权重。</li></ul> |

### 查看客户配置文件分数

要查看人员用户档案的预测得分，请选择 **[!UICONTROL 用户档案]** 在左侧面板的客户部分下，然后输入身份命名空间和身份值。 完成后，选择 **[!UICONTROL 查看]**.

接下来，从列表中选择用户档案。

![客户用户档案](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

的 **[!UICONTROL 详细信息]** 页面现在包含预测得分。 单击预测得分旁边的图表图标。

![客户用户档案预测得分](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

弹出对话框显示得分、整体得分分布、此得分的最大影响因素以及得分目标定义。

![客户用户档案预测得分详细信息](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 监控预测潜在客户和帐户评分作业 {#monitoring-jobs}

您可以通过功能板监控基本量度和每日作业运行状态。 这些量度包括：

* 得分的人员/帐户用户档案总数
* 下一个得分作业（日期）
* 下一份培训工作（日期）

有关更多信息，请参阅 [监控预测潜在客户和帐户评分的作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
