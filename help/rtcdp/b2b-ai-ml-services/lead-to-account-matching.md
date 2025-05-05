---
title: Real-Time CDP B2B中的商机帐户匹配
type: Documentation
description: 有关Experience PlatformCDP B2B中的商机帐户匹配功能的概述和更多信息。
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Real-Time CDP B2B中的商机帐户匹配

## 概述 {#overview}

基于帐户的营销是B2B营销中越来越重要的策略。 基于帐户的营销为获取特定的高价值客户提供了以下主要优势：

- 清除ROI
- 销售和营销协调
- 个性化方法
- 减少浪费的资源
- 缩短销售周期

基于帐户的营销提供将已知客户关联到销售帐户的功能。 这允许营销团队在客户历程的早期，与目标客户的潜在潜在客户接洽，以提高其转化几率。 已知人员记录通常包括以下部分或全部信息：

- 人员姓名
- 电子邮件地址
- 联系电话
- 公司名称
- 公司网站
- 职务名称
- 位置

## 工作原理 {#how-it-works}

每天运行的作业同时使用确定性和概率因素来匹配已知的潜在客户配置文件，而无需现有的帐户关联。 已知的潜在客户配置文件将具有以下任一可用属性：

- b2b.companyName
- b2b.companyWebsite
- 工作电子邮件

>[!NOTE]
>
> b2b.personKey.sourceKey属性必须存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey属性可以位于B2B person架构的b2b字段组中。

![B2B人员架构显示属性](/help/rtcdp/accounts/images/b2b-person-schema.png)

workEmail属性可作为B2B人员架构中的顶级字段组找到。

![B2B人员架构显示workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

仅当匹配分数超过内部置信度阈值时，才会最佳匹配用户档案。 结果保存在现有帐户人员关系XDM的新系统数据集中。

当有新的人员配置文件快照可用（每24小时一次）时，会运行商机帐户匹配服务。 有关商机与帐户匹配[&#128279;](/help/rtcdp/accounts/account-profile-ui-guide.md)的配置的更多信息，请参阅文档。

## 如何查看潜在客户与帐户的匹配输出 {#how-to-view}

作业运行后，结果将保存在现有帐户人员关系XDM的新数据集中。

要预览数据集，请选择右上角的&#x200B;**[!UICONTROL 预览数据集]**。

![新数据集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

数据集包含匹配的帐户信息以及所选数据集的匹配分数。 **[!UICONTROL Relationship Source]**&#x200B;字段指示它是否来自潜在客户与帐户的匹配流程。

![预览数据集置信度分数和输出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 监控潜在客户到帐户匹配作业 {#monitoring-jobs}

您可以通过仪表板监控任何潜在客户到帐户匹配作业的作业状态和相关量度。

有关商机与帐户匹配[&#128279;](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)的监视作业的详细信息，请参阅文档。
