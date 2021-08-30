---
keywords: Experience Platform；主页；热门主题；DULE;DULE
solution: Experience Platform
title: 数据使用策略概述
topic-legacy: policies
description: 为了有效支持数据合规性的数据使用标签，必须实施数据使用策略。 数据使用策略是描述您允许或限制对Experience Platform内数据执行的营销操作类型的规则。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# 数据使用策略概述

为了有效支持数据合规性的数据使用标签，必须实施数据使用策略。 数据使用策略是描述允许或限制您对[!DNL Experience Platform]内的数据执行的营销操作类型的规则。

本文档提供了数据使用策略的高级概述，并提供了指向在UI或API中使用策略的更多文档的链接。

## 营销操作 {#marketing-actions}

数据管理框架中的营销操作（也称为营销用例）是[!DNL Experience Platform]数据消费者可以采取的操作，贵组织希望对其限制数据使用。 因此，数据使用策略由以下各项定义：

1. 特定营销操作
2. 限制对其执行操作的数据使用标签

营销操作的示例可能是希望将数据集导出到第三方服务。 如果有策略指出无法导出特定类型的数据(如个人身份信息(PII))，并且您尝试导出包含“I”标签（身份数据）的数据集，您将收到[!DNL Policy Service]的响应，告知您数据使用策略已被违反。

>[!NOTE]
>
>营销操作本身不会限制数据的使用。 必须将它们包含在已启用的数据使用策略中，才能针对策略违规评估这些操作。

当贵组织的服务中发生数据使用情况时，应指示相关的营销操作，以便识别任何违反策略的情况。 然后，您可以使用[策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/)检查集成中是否存在策略违规。

>[!NOTE]
>
>如果您使用[!DNL Real-time Customer Data Platform]，则可以在目标上设置营销用例以自动执行策略。 有关更多信息，请参阅[Real-time CDP](../../rtcdp/privacy/data-governance-overview.md)中的“数据管理”文档。

有关[可用的Adobe定义营销操作](#core-actions)的列表，请参阅本文档的附录。 您还可以使用[!DNL Policy Service] API或[!DNL Experience Platform ]用户界面定义自己的自定义营销操作。 有关使用营销操作和策略的更多信息，请参阅下一节。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理数据使用策略 {#manage}

应用数据使用标签后，数据管理人员可以使用[!DNL Policy Service] API或[!DNL Experience Platform] UI来管理和评估与对包含数据使用标签的数据执行营销操作相关的策略。 您可以创建和更新策略、确定策略的状态，以及使用营销操作来评估特定操作是否违反了数据使用策略。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括由Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，您必须通过API或UI手动启用该策略。

有关在API中使用营销操作和数据使用策略的分步说明，请参阅关于[创建和评估数据使用策略](create.md)的教程。 有关[!DNL Policy Service] API提供的关键操作的详细信息，请参阅[Policy Service开发人员指南](../api/getting-started.md)。

有关如何在[!DNL Platform] UI中使用营销操作和策略的信息，请参阅[数据使用策略用户指南](./user-guide.md)。

## 后续步骤

本文档介绍了[!DNL Data Governance]框架中的数据使用策略。 您现在可以继续阅读本指南中链接的流程文档，以进一步了解如何在API和UI中使用策略。

## 附录

以下部分提供了有关数据使用策略的其他信息。

### Adobe定义的营销操作 {#core-actions}

下表描述了按Adobe提供的现成核心营销操作。

>[!NOTE]
>
>核心营销操作应视为起点，帮助您确定要创建和检查违规的使用策略。 定义及其解释方式取决于贵组织的需求和策略。

| 营销操作 | 描述 |
| --- | --- |
| Analytics | 将数据用于分析目的的操作，例如测量、分析和报告客户对贵组织网站或应用程序的使用情况。 |
| 与直接可识别的数据结合使用 | 将任何个人身份信息(PII)与匿名数据相结合的操作。 来自广告网络、广告服务器和第三方数据提供商的数据合同通常包括禁止使用具有直接可识别数据的此类数据的具体合同。 |
| 跨站点定位 | 一种使用数据进行跨站点广告定位的操作。 来自多个网站的数据组合（包括网站数据和网站外数据的组合或来自多个网站外来源的数据组合）称为跨网站数据。 通常会收集并处理跨站点数据，以便做出有关用户兴趣的推论。 |
| 数据科学 | 将数据用于数据科学工作流的操作。 有些合同明确禁止数据科学使用数据。 有时，这些措辞的措辞禁止将数据用于人工智能(AI)、机器学习(ML)或建模。 |
| 电子邮件定位 | 在电子邮件定位营销活动中使用数据的操作。 |
| 导出到第三方 | 将数据导出到与客户没有直接关系的处理器和实体的操作。 许多数据提供商在合同中都有条款禁止从最初收集的地方导出数据。 例如，社交网络合同通常会限制您从这些合同中收到的数据的传输。 |
| 现场广告 | 一种使用数据进行现场广告的操作，包括在您组织的网站或应用程序上选择和投放广告，或衡量此类广告的投放和效果的操作。 |
| 现场个性化 | 使用数据进行现场内容个性化的操作。 Onsite个性化是指用于推论用户兴趣的任何数据，用于根据这些推论选择提供哪些内容或广告。 |
| 区段匹配 | 使用数据进行Adobe Experience Platform区段匹配的操作，该操作允许两个或多个Platform用户交换区段数据。 通过启用引用此操作的策略，可以限制用于区段匹配的数据。 例如，如果启用了核心策略“限制数据共享”，则具有[C11标签](../labels/reference.md#c11)的任何数据都不能用于区段匹配。 |
| 单个身份个性化 | 一项操作，它要求将单个身份用于个性化目的，而不是拼合来自多个源的身份。 |
