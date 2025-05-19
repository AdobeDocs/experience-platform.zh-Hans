---
keywords: Experience Platform；主页；热门主题；dule；DULE
solution: Experience Platform
title: 数据使用策略概述
description: 数据使用策略是描述允许或限制您对Adobe Experience Platform中的数据执行的营销操作类型的规则。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 17%

---

# 数据使用策略概述 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="限制数据使用"
>abstract="数据使用策略类型将评估应用于数据治理标签的具体营销行为，以便限制用于营销操作的数据使用。"

为了使数据使用标签有效地支持数据合规性，必须实施数据使用策略。 数据使用策略是描述允许或限制您对[!DNL Experience Platform]内的数据执行的营销操作类型的规则。

有两种可用的策略：

* **[!UICONTROL 数据治理策略]**：根据正在执行的营销操作和相关数据携带的数据使用标签限制数据激活。
* **[!UICONTROL 同意策略]**：根据客户的同意或偏好筛选可激活到[目标](../../destinations/home.md)的用户档案

>[!NOTE]
>
>数据使用策略不应与[访问控制策略](../../access-control/abac/end-to-end-guide.md#policy)混淆，后者用于确定组织中的某些Experience Platform用户是否可以访问某些数据字段，并通过[!UICONTROL 权限]选项卡进行配置。

本文档提供了数据使用策略的高级概述，并提供了指向有关在UI或API中使用策略的其他文档的链接。

## 营销操作 {#marketing-actions}

数据管理框架上下文中的营销操作（也称为营销用例）是[!DNL Experience Platform]数据使用者可以采取的操作，贵组织希望限制对这些操作的数据使用。 因此，数据使用策略由以下内容定义：

1. 特定的营销活动
2. 限制执行该操作的条件

营销操作的示例可能是希望将数据集导出到第三方服务。 如果有策略规定无法导出特定类型的数据(如个人身份信息(PII))，并且您尝试导出包含“I”标签（身份数据）的数据集，您将收到[!DNL Policy Service]的响应，告知您违反了数据使用策略。

>[!NOTE]
>
>营销操作本身不会限制数据使用。 它们必须包含在启用的数据使用策略中，才能针对策略违规评估这些操作。

当贵组织的服务中使用数据时，应指示相关的营销操作，以便识别任何策略违规。 然后，您可以使用[策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/)检查集成中是否存在策略违规。

>[!NOTE]
>
>您可以在目标上设置营销用例以自动实施策略。 有关特定目标的配置选项的详细信息，请参阅[目标文档](../../destinations/home.md)。

请参阅本文档的附录，以获取[可用的Adobe定义的营销操作](#core-actions)的列表。 您还可以使用[!DNL Policy Service] API或[!DNL Experience Platform]用户界面定义您自己的自定义营销操作。 下一节将提供有关使用营销操作和策略的更多信息。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Experience Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理数据使用策略 {#manage}

应用数据使用标签后，数据管理员可以使用[!DNL Policy Service] API或[!DNL Experience Platform] UI来管理和评估与对包含数据使用标签的数据执行的营销操作相关的策略。 您可以创建和更新策略，确定策略的状态，然后使用营销操作来评估特定操作是否违反了数据使用策略。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括Adobe提供的核心策略)都处于禁用状态。 为了考虑实施单个策略，您必须通过API或UI手动启用该策略。

有关在API中使用营销操作和数据使用策略的分步说明，请参阅有关[创建和评估数据使用策略](create.md)的教程。 有关[!DNL Policy Service] API提供的密钥操作的详细信息，请参阅[策略服务开发人员指南](../api/getting-started.md)。

有关如何在[!DNL Experience Platform]用户界面中使用营销操作和策略的信息，请参阅[数据使用策略用户指南](./user-guide.md)。

## 后续步骤

本文档介绍了数据管理框架中的数据使用策略。 您现在可以继续阅读本指南中链接的流程文档，详细了解如何在API和UI中使用策略。

## 附录

以下部分提供了有关数据使用策略的其他信息。

### Adobe定义的营销操作 {#core-actions}

下表描述了Adobe提供的现成可用的核心营销操作。

>[!NOTE]
>
>应将核心营销操作视为一个起点，帮助您确定要创建并检查违规的使用策略。 定义和解释方式取决于贵组织的需求和策略。

| 营销操作 | 描述 |
| --- | --- |
| Analytics | 一个将数据用于分析目的的操作，例如衡量、分析和报告客户对您组织的网站或应用程序的使用情况。 |
| 与直接可识别的数据相结合 | 一个将任何个人身份信息 (PII) 与匿名数据结合使用的操作。来自广告网络、广告服务器和第三方数据提供商的数据的合同通常包括具体的合同禁令，禁止将此类数据与可直接识别的数据一起使用。 |
| 跨站点定位 | 一个将数据用于跨站点广告定位的操作。来自多个站点的数据的组合（包括现场数据和场外数据的组合或来自多个场外来源的数据的组合）称为跨站点数据。 通常，收集和处理跨站点数据以推断用户的兴趣。 |
| 数据科学 | 一个将数据用于数据科学工作流的操作。一些合同包含明确禁令，禁止将数据用于数据科学。有时，这些措辞禁止将数据用于人工智能 (AI)、机器学习 (ML) 或建模。 |
| 数据导出 | 一个将数据导出到Adobe产品和服务之外的任何位置或目标的操作。 例如，将数据下载到本地计算机、从屏幕复制数据、计划将数据提交到Adobe之外的位置、Customer Journey Analytics计划项目、下载报表、报表API等。 |
| 电子邮件定位 | 一个在电子邮件定位活动中使用数据的操作。 |
| 导出到第三方 | 一个将数据导出到与客户没有直接关系的处理器和实体的操作。许多数据提供商在合同中都设立了条款，禁止从最初收集数据的地方导出数据。例如，社交网络合同通常会限制您从他们那里收到的数据传输。 |
| 现场Advertising | 一个将数据用于现场广告的操作，包括在您组织的网站或应用程序上选择和投放广告，或衡量此类广告的投放和有效性。 |
| 现场Personalization | 一个使用数据进行现场内容个性化的操作。 现场个性化是用于推断用户兴趣的任何数据，并用于根据这些推断选择提供哪些内容或广告。 |
| 区段匹配 | 一个将数据用于Adobe Experience Platform区段匹配的操作，它允许两个或更多Experience Platform用户交换受众数据。 通过启用引用此操作的策略，您可以限制用于区段匹配的数据。 例如，如果启用了核心策略“限制数据共享”，则任何带有[C11标签](../labels/reference.md#c11)的数据都不能用于区段匹配。 |
| 单一身份Personalization | 一个操作，它要求将单一身份标识用于个性化目的，而不是将来自多个来源的身份标识拼接起来。 |
