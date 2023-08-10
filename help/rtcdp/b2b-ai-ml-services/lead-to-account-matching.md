---
title: Real-Time CDP B2B中的商机帐户匹配
type: Documentation
description: 有关Experience PlatformCDP B2B中的商机帐户匹配功能的概述和更多信息。
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 2%

---

# Real-Time CDP B2B中的商机帐户匹配

## 概述 {#overview}

基于帐户的营销是B2B营销中越来越重要的策略。 基于帐户的营销为获取特定的高价值客户提供了以下主要优势：

- 清除ROI
- 销售和营销协调
- 个性化方法
- 减少浪费的资源
- 缩短销售周期

基于帐户的营销可将已知人员和匿名Web访客关联到销售帐户。 这允许营销团队在客户历程的早期，与目标客户的潜在潜在客户接洽，以提高其转化几率。 已知人员记录通常包括以下部分或全部信息：

- 人员姓名
- 电子邮件地址
- 联系电话
- 公司名称
- 公司网站
- 职务
- 位置

通过商机帐户匹配，可将已知人员配置文件联接到帐户配置文件。 然后，您可以在B2B上下文（如帐户、机会等）中对数据进行分段和定位。 人员配置文件可以分为以下三个类别：

- **帐户人员配置文件：** 人员配置文件已通过来自数据源的关系与至少一个帐户配置文件关联。 这意味着至少有一个联系人片段。

>[!NOTE]
>
> 运行潜在客户与帐户匹配作业时，帐户人员配置文件不匹配。

- **已知人员配置文件：** 人员配置文件未与任何帐户配置文件关联，并且以下至少一个人员配置文件属性具有值：

   - 电子邮件地址
   - 公司名称
   - 公司网站

- **匿名人员个人资料：** 人员配置文件未关联到任何帐户配置文件，并且以下任何人员配置文件属性都没有值：

   - 电子邮件地址
   - 公司名称
   - 公司网站

>[!NOTE]
>
> 一个人员配置文件可能与多个帐户配置文件相关。 但是，商机与帐户的匹配过程将仅与最佳匹配匹配。 如果需要更广泛的匹配集，请将商机关联到与相关帐户功能匹配的帐户。

## 工作原理 {#how-it-works}

每天运行的作业同时使用确定性和概率因素来匹配已知的潜在客户配置文件，而无需现有的帐户关联。 已知的潜在客户配置文件将具有以下任一可用属性：

- b2b.companyName
- b2b.companyWebsite
- 工作电子邮件

>[!NOTE]
>
> b2b.personKey.sourceKey属性必须存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey属性可以位于B2B person架构的b2b字段组中。

![显示属性的B2B人员模式](/help/rtcdp/accounts/images/b2b-person-schema.png)

workEmail属性可作为B2B人员架构中的顶级字段组找到。

![显示工作电子邮件的B2B人员模式](/help/rtcdp/accounts/images/b2b-person-workemail.png)

仅当匹配分数超过内部置信度阈值时，才会最佳匹配用户档案。 结果保存在现有帐户人员关系XDM的新系统数据集中。

当有新的人员配置文件快照可用（每24小时一次）时，会运行商机帐户匹配服务。 请参阅文档以了解有关 [商机帐户匹配的配置](/help/rtcdp/accounts/account-profile-ui-guide.md).

## 如何查看潜在客户与帐户的匹配输出 {#how-to-view}

作业运行后，结果将保存在现有帐户人员关系XDM的新数据集中。

要预览数据集，请选择 **[!UICONTROL 预览数据集]** 在右上角。

![新数据集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

数据集包含匹配的帐户信息以及所选数据集的匹配分数。 此 **[!UICONTROL 关系源]** 字段指示它是否来自商机帐户匹配流程。

![预览数据集置信度分数和输出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 监控潜在客户到帐户匹配作业 {#monitoring-jobs}

您可以通过仪表板监控任何潜在客户到帐户匹配作业的作业状态和相关量度。

请参阅文档以了解有关 [监控销售线索与帐户匹配的作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
