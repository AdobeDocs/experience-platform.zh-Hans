---
keywords: Experience Platform；主页；热门主题；DULE;DULE
solution: Experience Platform
title: 数据使用策略概述
topic-legacy: policies
description: 数据使用策略是描述您允许或限制对Adobe Experience Platform中的数据执行的营销操作类型的规则。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# 数据使用策略概述 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="限制数据使用"
>abstract="数据使用策略类型会评估应用于数据管理标签的特定营销操作，以限制营销活动的数据使用。"

为了有效支持数据合规性的数据使用标签，必须实施数据使用策略。 数据使用策略是描述您允许或限制对内数据执行的营销操作类型的规则 [!DNL Experience Platform].

可用的策略有两种类型：

* **[!UICONTROL 数据管理政策]**:根据正在执行的营销操作以及相关数据携带的数据使用标签限制数据激活。
* **[!UICONTROL 同意策略]**:筛选可激活的用户档案 [目标](../../destinations/home.md) 基于客户的同意或偏好

>[!NOTE]
>
>不要将数据使用策略与 [访问控制策略](../../access-control/abac/end-to-end-guide.md#policy)，用于确定贵组织中的某些Platform用户是否可以访问某些数据字段，并通过 [!UICONTROL 权限] 选项卡。

本文档提供了数据使用策略的高级概述，并提供了指向在UI或API中使用策略的更多文档的链接。

## 营销操作 {#marketing-actions}

在数据管理框架中，营销操作（也称为营销用例）是 [!DNL Experience Platform] 数据消费者可以采用，贵组织希望限制其数据使用。 因此，数据使用策略由以下各项定义：

1. 特定营销操作
2. 限制执行该操作的条件

营销操作的示例可能是希望将数据集导出到第三方服务。 如果有策略指出无法导出特定类型的数据(如个人身份信息(PII))，并且您尝试导出包含“I”标签（身份数据）的数据集，则会收到 [!DNL Policy Service] 告诉您数据使用策略已被违反。

>[!NOTE]
>
>营销操作本身不会限制数据的使用。 必须将它们包含在已启用的数据使用策略中，才能针对策略违规评估这些操作。

当贵组织的服务中发生数据使用情况时，应指示相关的营销操作，以便识别任何违反策略的情况。 然后，您可以使用 [策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 来检查集成中是否存在违反策略的情况。

>[!NOTE]
>
>您可以对目标设置营销用例以自动执行策略。 请参阅 [目标文档](../../destinations/home.md) 有关特定目标配置选项的详细信息。

有关 [可用的Adobe定义的营销操作](#core-actions). 您还可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] 用户界面。 有关使用营销操作和策略的更多信息，请参阅下一节。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理数据使用策略 {#manage}

应用数据使用标签后，数据管理人员可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] UI，用于管理和评估与对包含数据使用情况标签的数据执行营销操作相关的策略。 您可以创建和更新策略、确定策略的状态，以及使用营销操作来评估特定操作是否违反了数据使用策略。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括由Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，您必须通过API或UI手动启用该策略。

有关在API中使用营销操作和数据使用策略的分步说明，请参阅 [创建和评估数据使用策略](create.md). 有关详细信息，请参阅 [!DNL Policy Service] API，请参阅 [策略服务开发人员指南](../api/getting-started.md).

有关如何在 [!DNL Platform] UI，请参阅 [数据使用策略用户指南](./user-guide.md).

## 后续步骤

本文档介绍了数据管理框架中的数据使用策略。 您现在可以继续阅读本指南中链接的流程文档，以进一步了解如何在API和UI中使用策略。

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
| 数据科学 | 将数据用于数据科学工作流的操作。 一些合同明确禁止数据科学使用数据。 有时，这些措辞的措辞禁止将数据用于人工智能(AI)、机器学习(ML)或建模。 |
| 电子邮件定位 | 在电子邮件定位营销活动中使用数据的操作。 |
| 导出到第三方 | 将数据导出到与客户没有直接关系的处理器和实体的操作。 许多数据提供商在合同中都有条款禁止从最初收集的地方导出数据。 例如，社交网络合同通常会限制您从这些合同中收到的数据的传输。 |
| 现场广告 | 一种使用数据进行现场广告的操作，包括在您组织的网站或应用程序上选择和投放广告，或衡量此类广告的投放和效果的操作。 |
| 现场个性化 | 使用数据进行现场内容个性化的操作。 Onsite个性化是指用于推论用户兴趣的任何数据，用于根据这些推论选择提供哪些内容或广告。 |
| 区段匹配 | 使用数据进行Adobe Experience Platform区段匹配的操作，该操作允许两个或多个Platform用户交换区段数据。 通过启用引用此操作的策略，可以限制用于区段匹配的数据。 例如，如果启用了核心策略“限制数据共享”，则任何具有 [C11标签](../labels/reference.md#c11) 无法用于区段匹配。 |
| 单个身份个性化 | 一项操作，它要求将单个身份用于个性化目的，而不是拼合来自多个源的身份。 |
