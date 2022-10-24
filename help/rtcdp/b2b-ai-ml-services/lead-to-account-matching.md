---
title: 在Real-Time CDP B2B中实现帐户匹配
type: Documentation
description: Experience PlatformCDP B2B中有关导致帐户匹配功能的潜在客户的概述和更多信息。
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---

# 在Real-Time CDP B2B中实现帐户匹配

## 概述 {#overview}

基于帐户的营销是B2B营销的一项越来越重要的策略。 基于帐户的营销为收购特定的高价值客户提供了以下主要优势：

- 明确ROI
- 销售和营销协调
- 个性化方法
- 减少浪费的资源
- 销售周期缩短

基于帐户的营销提供了将已知人员和匿名Web访客关联到销售帐户的功能。 这允许营销团队在客户历程中尽早从目标帐户中接触潜在的潜在客户，以增加其转化机会。 已知人员记录通常包括以下部分或全部信息：

- 人员姓名
- 电子邮件地址
- 联系电话
- 公司名称
- 公司网站
- 职务
- 位置

通过促进帐户匹配，您可以将已知人员用户档案加入帐户用户档案。 然后，您可以在B2B上下文中对数据进行分段和定位，如帐户、机会等。 人员用户档案可以分为以下三类：

- **帐户人员配置文件：** 人员用户档案已通过来自数据源的关系与至少一个帐户用户档案关联。 这意味着至少有一个联系片段。

>[!NOTE]
>
> 运行潜在客户时，帐户人员配置文件不匹配，从而导致帐户匹配作业。

- **已知人员配置文件：** 人员配置文件未与任何帐户配置文件关联，并且以下至少一个人员配置文件属性具有值：

   - 电子邮件地址
   - 公司名称
   - 公司网站

- **匿名人员个人资料：** 人员配置文件未与任何帐户配置文件关联，并且以下任何人员配置文件属性都没有值：

   - 电子邮件地址
   - 公司名称
   - 公司网站

>[!NOTE]
>
> 个人用户档案可能与多个帐户用户档案相关。 但是，导致帐户匹配的潜在客户流程将仅与最佳匹配相匹配。 如果需要更广泛的匹配集，请将潜在客户与相关帐户功能的帐户匹配联系起来。

## 工作原理 {#how-it-works}

每日运行的作业使用确定性因素和可能性因素来匹配已知的潜在客户配置文件，而不会与现有帐户关联。 已知的潜在客户用户档案将具有以下属性之一：

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> b2b.personKey.sourceKey属性必须存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey属性可以位于B2B人员架构的b2b字段组中。

![显示属性的B2B人员架构](/help/rtcdp/accounts/images/b2b-person-schema.png)

在B2B人员架构中，可以将workEmail属性作为顶级字段组找到。

![显示workEmail的B2B人员架构](/help/rtcdp/accounts/images/b2b-person-workemail.png)

仅当匹配分数超过内部置信度阈值时，用户档案才会获得最佳匹配。 结果会保存在现有帐户人员关系XDM的新系统数据集中。

当新人员配置文件快照变为可用时，即会运行“潜在客户匹配”服务，该快照每24小时一次。 有关 [潜在客户配置与帐户匹配](/help/rtcdp/accounts/account-profile-ui-guide.md).

## 如何查看与帐户匹配输出的潜在客户 {#how-to-view}

运行作业后，结果会保存在现有帐户人员关系XDM的新数据集中。

要预览数据集，请选择 **[!UICONTROL 预览数据集]** 在右上方。

![新数据集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

数据集包含匹配的帐户信息以及所选数据集的匹配分数。 的 **[!UICONTROL 关系来源]** 字段指示它是否来自潜在客户到帐户匹配流程。

![预览数据集置信度得分和输出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 监控潜在客户以匹配帐户作业 {#monitoring-jobs}

您可以通过功能板监控导致帐户匹配作业的任何潜在客户的作业状态和关联量度。

有关 [监控潜在客户的作业以匹配帐户](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
