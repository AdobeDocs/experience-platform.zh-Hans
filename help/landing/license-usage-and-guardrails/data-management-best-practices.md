---
title: 数据管理许可证权利最佳实践
description: 了解可用来借助 Adobe Experience Platform 更好地管理您的许可证权利的最佳实践和工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: a14d94a87eb433dd0bb38e5bf3c9c3a04be9a5c6
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 1%

---

# 数据管理许可证权利最佳实践

Adobe Experience Platform是一个开放系统，可将您的数据转换为强大的客户档案以实时更新，并使用AI驱动的见解来帮助您在每个渠道中提供正确的体验。 您可以使用源将不同类型、卷和历史记录的数据引入Experience Platform，然后满足从分段和个性化到分析和机器学习等用例的需求。

Experience Platform提供许可证，用于建立可创建的配置文件数以及可引入的数据量。 由于能够引入任何源、数量或历史数据，因此随着数据量的增长，可能会超出许可权限。

请阅读本指南，以了解可以遵循的最佳实践以及可用来更好地管理Experience Platform许可证权利的工具。

## 功能摘要 {#summary-of-features}

使用本文档中概述的最佳实践和工具更好地管理Experience Platform中的许可证权利使用情况。 本文档在发布附加功能时进行了更新，以帮助向所有Experience Platform客户显示和控制。

下表列出了您目前可以使用的功能，以便更好地管理您的许可证使用授权。

| 功能 | 描述 |
| --- | --- |
| [数据集UI — 体验事件数据保留](../../catalog/datasets/user-guide.md#data-retention-policy) | 为数据湖和配置文件存储中的数据配置固定保留期。 在配置的保留期结束时，将删除记录。 |
| [启用/禁用实时客户资料的数据集](../../catalog/datasets/user-guide.md) | 启用或禁用数据集摄取到Real-time Customer Profile的功能。 |
| 配置文件存储区中的[体验事件过期时间](../../profile/event-expirations.md) | 为引入到启用配置文件的数据集中的所有事件应用过期时间。 请联系您的Adobe客户团队或客户关怀团队以启用此功能。 |
| [Adobe Analytics数据准备筛选器](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) | 应用[!DNL Kafka]筛选器以从摄取中排除不必要的数据。 |
| [Adobe Audience Manager源连接器筛选器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 应用Audience Manager源连接筛选器以从摄取中排除不必要的数据。 |
| [事件转发数据筛选器](../../tags/ui/event-forwarding/overview.md) | 应用服务器端[!DNL Kafka]筛选器以从摄取中排除不必要的数据。  有关更多信息，请参阅有关[标记规则](../../tags/ui/managing-resources/rules.md)的文档。 |
| [许可证使用情况仪表板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 根据许可的权利监控贵组织对Experience Platform产品的使用情况。 访问每日使用情况快照、预测趋势和详细的沙盒级别数据，以支持主动许可证管理。 |
| [数据集重叠报表API](../../profile/tutorials/dataset-overlap-report.md) | 输出对可寻址受众贡献最大的数据集。 |
| [身份重叠报表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 输出对可寻址受众贡献最大的身份命名空间。 |
| [假名配置文件数据过期](../../profile/pseudonymous-profiles.md) | 为假名配置文件配置数据过期时间，并自动从配置文件存储中删除数据。 |

{style="table-layout:auto"}

## 了解Experience Platform数据存储

Experience Platform主要由两个数据存储库组成：数据湖和配置文件存储。

数据湖主要具有以下用途：

* 充当将数据载入Experience Platform的暂存区；
* 充当所有Experience Platform数据的长期数据存储；
* 启用数据分析和数据科学等用例。

**配置文件存储**&#x200B;是创建客户配置文件的位置，主要用途如下：

* 充当用于支持实时体验的用户档案的数据存储；
* 支持分段、激活和个性化等用例。

>[!NOTE]
>
>您对[!DNL data lake]的访问权限取决于您购买的产品SKU。 有关产品SKU的更多信息，请联系Adobe代表。

## 许可证使用 {#license-usage}

在许可Experience Platform时，您获得的许可使用权利因SKU而异：

**[!DNL Addressable Audience]**： Experience Platform中按照合同允许的客户配置文件总数，包括已知和假名配置文件。

**[!DNL Total Data Volume]**：在参与工作流中可供实时客户配置文件使用的总数据量。

这些指标的可用性和每个指标的特定定义因贵组织购买的许可而异。

## 许可证用量仪表板

Adobe Experience Platform UI提供了一个功能板，通过该功能板，您可以查看组织的Experience Platform许可证相关数据的快照。 仪表板中的数据与拍摄快照的特定时间点完全相同。 快照既不是近似值，也不是数据示例，并且仪表板没有实时更新。

有关详细信息，请参阅Experience Platform UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data)上的[使用许可证使用情况仪表板指南。

## 数据管理最佳实践

以下各节概述了更好地管理数据可遵循的最佳实践。

### 了解您的数据

在Adobe Experience Platform中，并非所有数据都是相同的。 某些数据可能密集，但值较低，而其他数据可能稀疏，但值较高。 一些数据可能在生成后立即失去价值，而其他数据可能在几个月（甚至几年）内失去价值。

在了解数据的价值时，需要考虑三个维度：

| 维度 | 描述 | 示例 |
| --- | --- | --- |
| 数量 | 表示所摄取的数据的数量和总数。 | Web点击量 — 高流量，中等保真。 值可能会迅速减小。 |
| 时间跨度 | 表示引入的数据继续保持有价值的时间长度。 | 离线购买 — 在数量和保真度方面适度，但可能在较长时间内很有价值。 |
| 保真度 | 表示数据包含信息的丰富程度。 | 客户账户 — 交易量低但保真度高。 在客户的生命周期之外可能很有价值。 |

### 数据管理工具 {#data-management-tools}

在确保您的数据使用量保持在许可证权利限制内时，需要考虑两种主要方案：

### 要将哪些数据引入Experience Platform？

数据可以摄取到Experience Platform的一个或多个系统中，即[!DNL data lake]和/或配置文件存储。 这意味着，在不同的用例中，两个系统中可以存在不同的数据。 例如，您可能希望将历史数据保存在[!DNL data lake]中，但不保存在“配置文件存储”中。 您可以通过启用用于配置文件摄取的数据集来选择要发送到配置文件存储的数据。

>[!NOTE]
>
>您对[!DNL data lake]的访问权限取决于您购买的产品SKU。 有关产品SKU的更多信息，请联系Adobe代表。

### 要保留哪些数据？

您可以同时应用数据摄取过滤器和过期规则，以删除对于用例已过时的数据。 通常，行为数据（如Analytics数据）使用的存储空间远远多于记录数据（如CRM数据）。 例如，与记录数据相比，许多Experience Platform用户有超过90%的用户档案仅由行为数据填充。 因此，管理行为数据对于确保许可证权利范围内的合规性至关重要。

您可以利用许多工具来保持您的许可证使用授权：

* [摄取筛选器](#ingestion-filters)
* [配置文件存储](#profile-service)

### 身份服务和可寻址受众 {#identity-service}

身份图不计入可寻址受众权利总数，因为可寻址受众是指客户配置文件总数。

但是，由于拆分身份，身份图限制可能会影响可寻址受众。 例如，如果从图表中删除了最早的ECID，则ECID将继续作为假名配置文件存在于实时客户配置文件中。 您可以设置[假名配置文件数据有效期](../../profile/pseudonymous-profiles.md)以规避此行为。 若要了解更多信息，请阅读[身份标识服务数据的护栏](../../identity-service/guardrails.md)。

### 摄取筛选器 {#ingestion-filters}

通过摄取过滤器，您可以仅引入用例所需的数据，并过滤掉所有不需要的事件。

| 摄取筛选器 | 描述 |
| --- | --- |
| Adobe Audience Manager源筛选 | 在创建Adobe Audience Manager源连接时，您可以选择将哪些区段和特征引入[!DNL data lake]和实时客户个人资料中，而不是摄取整个Audience Manager数据。 有关详细信息，请参阅[创建Audience Manager源连接](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)指南。 |
| Adobe Analytics数据准备 | 在创建Analytics源连接时，您可以使用[!DNL Data Prep]功能来过滤掉用例不需要的数据。 通过[!DNL Data Prep]，您可以定义哪些属性/列需要发布到配置文件。 您还可以提供条件语句，以告知Experience Platform数据是应发布到配置文件，还是仅发布到[!DNL data lake]。 有关详细信息，请参阅[创建Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md)指南。 |
| 支持为配置文件启用/禁用数据集 | 要将数据摄取到Real-time Customer Profile，您必须启用要在配置文件存储中使用的数据集。 这样做会将添加到您的[!DNL Addressable Audience]和[!DNL Total Data Volume]权利。 一旦客户个人资料用例不再需要某个数据集，您可以禁用该数据集与个人资料的集成，以确保您的数据仍然符合许可证要求。 有关详细信息，请参阅[启用和禁用配置文件](../../catalog/datasets/enable-for-profile.md)的数据集指南。 |
| Web SDK和Mobile SDK数据排除 | Web和移动SDK收集的数据有两种类型：自动收集的数据和开发人员明确收集的数据。 为了更好地管理许可证合规性，您可以通过上下文设置在SDK的配置中禁用自动数据收集。 您的开发人员也可以删除或设置自定义数据。 |
| 服务器端转发数据排除 | 如果您使用服务器端转发将数据发送到Experience Platform，则可以通过以下方法排除发送的数据：在规则操作中删除映射以在所有事件中排除该数据，或者向规则添加条件，以便数据仅针对某些事件触发。 有关详细信息，请参阅有关[事件和条件](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if)的文档。 |
| 在源级别过滤数据 | 在创建连接并将数据摄取到Experience Platform之前，您可以使用逻辑和比较运算符过滤源中的行级数据。 有关详细信息，请阅读有关使用 [!DNL Flow Service] API](../../sources/tutorials/api/filter.md)筛选源的行级数据的指南[。 |

{style="table-layout:auto"}

### 配置文件存储 {#profile-service}

配置文件存储由以下组件组成：

| 配置文件存储组件 | 描述 |
| --- | --- |
| 轮廓片段 | 每个客户配置文件均由多个&#x200B;**配置文件片段**&#x200B;组成，这些片段已合并为该客户的单一视图。 例如，如果某个客户跨多个渠道与您的品牌互动，则贵组织将在多个数据集中显示与该单个客户相关的多个&#x200B;**配置文件片段**。 将这些片段摄取到Experience Platform后，使用身份图将它们拼合在一起，以为该客户创建单个配置文件。 **配置文件片段**&#x200B;包含作为标识符的身份命名空间，其中包含关联的记录数据和/或时间序列数据。 |
| 记录数据（属性） | 个人资料是主题、组织或个人的表示形式，由多个&#x200B;**属性**（也称为&#x200B;**记录数据**）组成。 例如，产品的配置文件可能包括SKU和描述，而人员的配置文件包含名字、姓氏和电子邮件地址等信息。 **记录数据**&#x200B;的卷通常为低/中等，但长期很有价值。 |
| 时间序列数据（行为） | **时间序列数据**&#x200B;提供有关用户行为的信息。 时间序列数据由标准架构类Experience Data Model (XDM) [!DNL ExperienceEvent]表示，它可以描述添加到购物车的项目、点击的链接以及查看的视频等事件。 行为的价值可能会随着时间的推移而降低。 |
| 身份命名空间（身份） | 当客户数据汇集在一起时，会通过使用&#x200B;**身份命名空间**&#x200B;将其合并到单个配置文件中，并且当更多有关用户的信息变得已知时，可以将这些身份拼合在一起。 有关详细信息，请参阅[身份命名空间概述](../../identity-service/features/namespaces.md)。 |

{style="table-layout:auto"}

### 配置文件存储构成报表

有许多报告可帮助您了解配置文件存储区的组成。 这些报告可帮助您针对如何以及在何处设置体验事件过期以更好地优化许可证使用做出明智的决策：

* **数据集重叠报表API**：公开对可寻址受众贡献最大的数据集。 您可以使用此报告来确定要为其设置过期时间的[!DNL ExperienceEvent]数据集。 有关详细信息，请参阅有关[生成数据集重叠报表](../../profile/tutorials/dataset-overlap-report.md)的教程。
* **身份重叠报表API**：公开对可寻址受众贡献最大的身份命名空间。 有关详细信息，请参阅有关[生成身份重叠报表](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report)的教程。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

### 假名配置文件数据过期 {#pseudonymous-profile-expirations}

使用假名配置文件数据过期功能，从配置文件存储中自动删除对您的用例不再有效或有用的数据。 假名配置文件数据过期会删除事件和配置文件记录。 因此，此设置将减少可寻址受众卷。 有关此功能的详细信息，请阅读[假名配置文件数据过期概述](../../profile/pseudonymous-profiles.md)。

### 数据集UI — 体验事件数据集保留 {#data-retention}

配置数据集到期和保留设置，以对Data Lake和配置文件存储中的数据强制执行固定保留期。 保留期结束后，数据将被删除。 Experience Event数据过期仅删除事件而不删除配置文件类数据，这将减少许可证使用量度中的[总数据量](total-data-volume.md)。 有关详细信息，请参阅[设置数据保留策略](../../catalog/datasets/user-guide.md#data-retention-policy)指南。

### 配置文件体验事件过期时间 {#event-expirations}

配置过期时间，以便在行为数据不再可用于用例时，自动将其从启用配置文件的数据集中删除。 有关详细信息，请阅读有关[体验事件过期时间](../../profile/event-expirations.md)的概述。

## 许可证使用合规性最佳实践摘要 {#best-practices}

以下是您可以遵循的一些建议最佳实践列表，以确保更好地遵守您的许可证使用授权：

* 使用[许可证使用情况仪表板](../../dashboards/guides/license-usage.md)跟踪和监控客户使用情况趋势。 这样，您就可以提前了解可能会产生的任何潜在使用过量。
* 通过识别分段和个性化用例所需的事件来配置[引入过滤器](#ingestion-filters)。 这样，您就可以仅发送用例所需的重要事件。
* 确保您只有分段和个性化用例所需的配置文件](#ingestion-filters)的[启用的数据集。
* 为Web数据等高频数据配置[体验事件过期时间](../../catalog/datasets/user-guide.md#data-retention-policy)和[假名配置文件数据过期时间](../../profile/pseudonymous-profiles.md)。
* 为数据湖中的体验事件数据集](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)配置[生存时间(TTL)保留策略，以根据您的许可证权利自动删除过期的记录并优化存储使用情况。
* 定期检查[配置文件构成报告](#profile-store-composition-reports)以了解您的配置文件存储构成。 这使您能够了解对许可证使用量消耗贡献最大的数据源。
