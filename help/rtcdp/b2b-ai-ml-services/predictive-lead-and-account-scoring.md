---
title: Real-Time CDP B2B中的预测性商机和客户评分
type: Documentation
description: 有关Experience Platform CDP B2B中的预测商机和客户评分功能的概述和更多信息。
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions" newtab=true
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 3%

---

# Real-Time CDP B2B中的预测性商机和客户评分

B2B营销人员在营销funnel的顶部面临多个挑战。 为了变得有效，B2B营销人员需要一种自动化方法来鉴别大量人员，以便他们能够专注于高价值目标。 资格鉴定应与最终销售结果保持一致，而不仅仅是营销转化。

客户，是购买B2B产品和服务的最终实体。 为了有效地营销和销售，B2B营销人员不仅要了解个人的购买情况，还要了解账户的购买可能性。

特别是基于帐户的营销，可将帐户策略化为营销目标。 客户购买倾向分数可以极大地帮助B2B营销人员确定客户之间的优先级，以最大限度地提高投资回报。

预测商机和客户评分服务通过从机会阶段转化事件中学习并预测，并将人员活动聚合到客户级别以产生客户得分，从而解决上述挑战。 这些得分可随时用作人员配置文件和帐户配置文件上的自定义字段，并可轻松作为细分标准包含在内，以优化受众。 此外，汇总和单位级别均提供主要影响因素，以帮助B2B营销人员更好地了解哪些元素驱动了分数。

## 了解预测性商机和客户评分 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo]数据源当前是必需的，因为它是唯一可以在人员配置文件级别提供转化事件的数据源。

预测商机和帐户评分使用基于树的（随机森林/梯度提升）机器学习方法来构建预测商机评分模型。

管理员能够配置多个用户档案评分目标（也称为模型），每个已配置的转化事件配置一个模型，从而允许为每个已配置的目标生成单独的分数。

预测商机和帐户评分支持以下转化目标类型和字段：

| 目标类型 | 字段 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>示例： `opportunityEvent.dataValueChanges.attributeName`等于`Stage`，`opportunityEvent.dataValueChanges.newValue`等于`Contract`</ul> |

该算法考虑了以下属性和输入数据：

* 人员配置文件

| XDM字段 | 必需/可选 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 必需 |
| `workAddress.country` | 可选 |
| `extSourceSystemAudit.createdDate` | 必需 |
| `extendedWorkDetails.jobTitle` | 可选 |

>[!NOTE]
> 
>算法仅检查Person`sourceAccountKey.sourceKey`字段组中的:personComponents字段。

* 帐户轮廓

| XDM字段 | 必需/可选 |
| --- | --- |
| `accountKey.sourceKey` | 必需 |
| `extSourceSystemAudit.createdDate` | 必需 |
| `accountOrganization.industry` | 可选 |
| `accountOrganization.numberOfEmployees` | 可选 |
| `accountOrganization.annualRevenue.amount` | 可选 |

* 体验事件

| XDM字段 | 必需/可选 |
| --- | --- |
| `_id` | 必需 |
| `personKey.sourceKey` | 必需 |
| `timestamp` | 必需 |
| `eventType` | 必需 |

支持多种机型，并设置了以下硬限制：

* 每个生产沙盒有权使用五个模型。
* 每个开发沙盒都有权使用一种模型。

数据质量要求如下：

* 理想情况下，对于培训目的，可以使用两年的最新数据。
* 所需的最小数据长度为6个月加上预测窗口。
* 对于每个预测目标，至少需要10个符合条件的转化事件。

评分作业每天运行，其结果将作为配置文件属性和帐户属性进行保存，然后可用于区段定义和个性化。 现成的Analytics Insights也可在帐户概述功能板上找到。

请参阅文档以了解有关如何[管理预测商机和帐户评分](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)服务的更多信息。

## 查看预测商机和客户评分结果 {#how-to-view}

作业运行后，将结果保存在名为`LeadsAI.Scores` - ***得分名称***&#x200B;的每个模型的新系统数据集中。 每个得分字段组都可以位于`{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`。

| 属性 | 描述 |
| --- | --- |
| 得分 | 用户档案在定义的时间范围内实现预测目标的相对可能性。 该值不应被视为概率百分比，而应被视为用户档案相对于群体总数的可能性。 此得分从0到100不等。 |
| 百分位数 | 此值提供有关用户档案相对于其他类似评分的用户档案的性能信息。 百分位数的范围是1到100。 |
| 模型类型 | 所选模型类型指示这是人员分数还是帐户分数。 |
| 得分日期 | 评分发生的日期。 |
| 影响因素 | 个人资料可能发生转化的预测原因。 因子由以下属性组成：<ul><li>代码：对个人资料的预测得分产生积极影响的个人资料或行为属性。</li><li>值：配置文件或行为属性的值。</li><li>重要性：指示用户档案或行为属性对预测得分（低、中、高）的权重。</li></ul> |

### 查看客户个人资料分数

要查看人员配置文件的预测得分，请选择左侧面板中客户部分下的&#x200B;**[!UICONTROL Profiles]**，然后输入身份命名空间和身份值。 完成后，选择&#x200B;**[!UICONTROL View]**。

接下来，从列表中选择配置文件。

![客户个人资料](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

**[!UICONTROL Detail]**&#x200B;页面现在包含预测得分。 单击预测得分旁边的图表图标。

![客户个人资料预测得分](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

弹出对话框显示分数、总体分数分布、此分数的主要影响因素以及分数目标定义。

![客户个人资料预测得分详细信息](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 监控预测性商机和客户评分作业 {#monitoring-jobs}

您可以通过仪表板监控基本指标和每日作业运行状态。 这些指标包括：

* 评分的人员/帐户配置文件总数
* 下一个评分作业（日期）
* 下一个培训作业（日期）

有关详细信息，请参阅有关[监控预测商机和帐户评分的作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)的文档。
