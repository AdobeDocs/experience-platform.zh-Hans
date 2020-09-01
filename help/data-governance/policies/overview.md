---
keywords: Experience Platform;home;popular topics;dule;DULE
solution: Experience Platform
title: 数据使用策略概述
topic: policies
description: 为了使数据使用标签能够有效支持数据合规性，必须实施数据使用策略。 数据使用策略是描述您允许或限制对Experience Platform内数据执行的营销操作种类的规则。
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---


# 数据使用策略概述

为了使数据使用标签能够有效支持数据合规性，必须实施数据使用策略。 数据使用策略是描述允许或限制您对中的数据执行的营销操作种类的规则 [!DNL Experience Platform]。

此文档提供了数据使用策略的高级概述，并提供了在UI或API中使用策略的进一步文档的链接。

## 营销操作 {#marketing-actions}

**数据治理**&#x200B;框架中的营销 **操作(也称为营销使用案例**)是数据消费者可以采取的操作，您的组织 [!DNL Experience Platform] 希望为此限制数据使用。 因此，数据使用策略由以下各项定义：

1. 特定营销活动
2. 限制不执行操作的数据使用标签

营销行动的一个例子可能是希望将数据集导出到第三方服务。 如果有策略表明无法导出特定类型的数据(如个人身份信息(PII))，并且您尝试导出包含“I”标签（身份数据）的数据集，您将收到来自通知您已违反数据使用 [!DNL Policy Service] 策略的响应。

>[!NOTE]
>
>营销活动本身并不限制数据使用。 必须将它们包含在启用的数据使用策略中，才能评估这些操作是否违反了策略。

当组织的服务中发生数据使用情况时，应指示相关的营销操作，以便识别任何违反策略的行为。 然后，您可以使用 [策略服务](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) API检查集成中是否存在策略违规。

>[!NOTE]
>
>如果您使用的 [!DNL Real-time Customer Data Platform]是，您可以在目标上设置营销使用案例，以自动执行策略。 有关详细信 [息，请参见实时CDP中的文档](../../rtcdp/privacy/data-governance-overview.md) “数据治理”。

请参阅本文档的附录，了解一列表可 [用的Adobe定义营销操作](#core-actions)。 您还可以使用API或用户界面定义您自己 [!DNL Policy Service] 的自定义营 [!DNL Experience Platform ]销操作。 下一节提供了有关使用营销操作和策略的更多信息。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理数据使用策略 {#manage}

应用数据使用标签后，数据管理人员可以使 [!DNL Policy Service] 用API或 [!DNL Experience Platform] UI来管理和评估与对包含数据使用标签的数据执行营销操作相关的策略。 您可以创建和更新策略、确定策略状态以及使用营销操作来评估特定操作是否违反了数据使用策略。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须通过API或UI手动启用该策略。

有关在API中使用营销操作和数据使用策略的分步说明，请参阅有关创建和评估数 [据使用策略的教程](create.md)。 有关API提供的关键操作的详细信 [!DNL Policy Service] 息，请参阅“策略 [服务开发人员指南”](../api/getting-started.md)。

有关如何在UI中使用营销操作和策略的 [!DNL Platform] 信息，请参阅 [数据使用策略用户指南](./user-guide.md)。

## 后续步骤

本文档介绍了框架中的数据使用策 [!DNL Data Governance] 略。 您现在可以继续阅读本指南中链接的流程文档，进一步了解如何在API和UI中使用策略。

## 附录

以下部分提供了有关数据使用策略的其他信息。

### Adobe定义的营销活动 {#core-actions}

下表描述了按Adobe提供的现成核心营销活动。

>[!NOTE]
>
>应将核心营销活动视为起点，以帮助您确定要创建和检查违规的使用策略。 定义及其解释方式取决于贵组织的需求和策略。

| 营销活动 | 描述 |
| --- | --- |
| Analytics | 将数据用于分析目的的操作，如衡量、分析和报告客户对您组织的站点或应用程序的使用情况。 |
| 与PII结合 | 将任何个人识别信息(PII)与匿名数据相结合的操作。 从广告网络、广告服务器和第三方数据提供商获取的数据合同通常包括特定合同禁止使用具有直接可识别数据的数据。 |
| 跨站点定位 | 使用数据进行跨站点广告定位的操作。 来自多个站点的数据的组合，包括现场数据和非现场数据的组合或来自多个非现场源的数据的组合，称为跨站点数据。 跨站点数据通常会被收集和处理，以推断用户的兴趣。 |
| 数据科学 | 将数据用于数据科学工作流的操作。 有些合同明确禁止数据科学的使用。 有时，这些术语的用词是禁止将数据用于人工智能(AI)、机器学习(ML)或建模。 |
| 电子邮件定位 | 在电子邮件定位活动中使用数据的操作。 |
| 导出到第三方 | 将数据导出到与客户没有直接关系的处理器和实体的操作。 许多数据提供商在合同中都有条款禁止从最初收集数据的地方出口数据。 例如，社交网络合同通常会限制您从它们收到的数据的传输。 |
| 现场广告 | 使用数据进行现场广告的操作，包括在您组织的网站或应用程序上选择和投放广告，或衡量此类广告的投放和效果。 |
| 现场个性化 | 使用数据进行现场内容个性化的操作。 现场个性化是用于推论用户兴趣的任何数据，用于根据这些推论选择提供哪些内容或广告。 |
| 单一身份个性化 | 需要将单个身份用于个性化目的而不是拼接多个来源的身份的操作。 |
