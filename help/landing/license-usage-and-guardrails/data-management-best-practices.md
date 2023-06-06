---
title: 数据管理许可证权利最佳实践
description: 了解可用来借助 Adobe Experience Platform 更好地管理您的许可证权利的最佳实践和工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 225fee7e2addf5067cb13da11615f6acff62ed72
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 2%

---

# 数据管理许可证权利最佳实践

Adobe Experience Platform是一个开放系统，可将您的数据转换为实时更新的强大客户档案，并使用AI驱动的见解来帮助您在每个渠道中提供正确的体验。 您可以摄取不同类型、卷和历史记录的数据以使用源进行Experience Platform，然后将该数据用于从分段和个性化到分析和机器学习的用例。

Platform提供许可证，用于建立可创建的配置文件数量和可引入的数据量。 由于能够引入任何源、数量或历史数据，因此随着数据量的增长，可能会超出许可授权。

本文档概述了借助 Adobe Experience Platform 更好地管理您的许可证权利需要遵循的最佳实践和可以使用的工具。

## 了解Adobe Experience Platform数据存储

Experience Platform主要由两个数据存储库组成： [!DNL data lake] 和配置文件存储区。

此 **[!DNL data lake]** 主要用途如下：

* 充当将数据载入Experience Platform的暂存区；
* 充当所有Experience Platform数据的长期数据存储；
* 支持数据分析和数据科学等用例。

此 **配置文件存储** 是创建客户配置文件的位置，主要用于以下目的：

* 充当用于支持实时体验的用户档案的数据存储；
* 支持分段、激活和个性化等用例。

>[!NOTE]
>
>您对 [!DNL data lake] 取决于您购买的产品SKU。 有关产品SKU的更多信息，请与您的Adobe代表联系。

## 许可证使用 {#license-usage}

在许可Experience Platform时，您会获得因SKU而异的许可证使用授权：

**[!DNL Addressable Audience]**  — 合同允许在Experience Platform中的客户配置文件总数，包括已知和假名配置文件。

**[!DNL Profile Richness]** -Experience Platform中配置文件数据的平均大小。 您可以提高 [!DNL Profile Richness] 通过购买丰富套餐获得权利。

此 [!DNL Profile Richness] 量度因您购买的许可而异。 有两种计算 [!DNL Profile Richness] 可用：

* Adobe Real-time Customer Data Platform中存储的所有生产数据（即Real-time Customer Profile和Identity Service）在任意时间点的总和，除以 [!DNL Addressable Audience]；
* Platform中存储的所有数据的总和(包括但不限于 [!DNL data lake]、Real-time Customer Profile和Identity Service)以及过去12个月中通过Platform流式传输（而不是存储在）的任何数据，除以 [!DNL Addressable Audience].

这些指标的可用性和每个指标的特定定义因贵组织购买的许可而异。

## 许可证使用情况仪表板

Adobe Experience Platform UI提供了一个功能板，通过该功能板，您可以查看组织的Platform许可证相关数据的快照。 仪表板中的数据与拍摄快照的特定时间点所显示的数据完全相同。 快照既不是近似值，也不是数据示例，并且仪表板没有实时更新。

有关详细信息，请参阅以下指南： [使用Platform UI上的许可证使用情况仪表板](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## 数据管理最佳实践

以下各节概述了更好地管理数据的最佳实践。

### 了解您的数据

并非所有数据在Adobe Experience Platform中都是相同的。 某些数据可能密集，但值较低，而其他数据可能稀疏，但值较高。 一些数据可能会在生成后立即失去价值，而其他数据则可能在几个月（如果不是几年的话）内有价值。

在了解数据的价值时，需要考虑三个维度：

| 维度 | 描述 | 示例 |
| --- | --- | --- |
| 数量 | 表示所摄取数据的数量和总数。 | Web点击量 — 高流量，中等保真。 值可能会迅速减小。 |
| Timespan | 表示摄取的数据继续保持有价值的时间长度。 | 离线购买 — 在数量和保真度方面适度，但可能在较长时期内很有价值。 |
| 保真度 | 表示数据包含信息的丰富程度。 | 客户账户 — 交易量低，但保真度高。 在客户的生命周期之外可能很有价值。 |

### 数据管理工具 {#data-management-tools}

在确保数据使用量保持在许可证授权限制内时，需要考虑两种中心方案：

### 要将哪些数据引入Platform？

数据可以引入Platform中的一个或多个系统，即 [!DNL data lake] 和/或配置文件存储区。 这意味着，在不同的使用案例中，两个系统中可以存在不同的数据。 例如，您可能希望将历史数据保存在 [!DNL data lake]，但不在配置文件存储中。 通过为配置文件摄取启用数据集，可以选择要发送到配置文件存储的数据。

>[!NOTE]
>
>您对 [!DNL data lake] 取决于您购买的产品SKU。 有关产品SKU的更多信息，请与您的Adobe代表联系。

### 要保留哪些数据？

您可以同时应用数据摄取过滤器和过期规则，以删除对用例已过时的数据。 通常，行为数据（如Analytics数据）占用的存储空间远远大于记录数据（如CRM数据）。 例如，与记录数据相比，许多Platform用户最多有90%以上的用户档案仅由行为数据填充。 因此，管理行为数据对于确保许可证权利范围内的合规性至关重要。

您可以利用许多工具来保持许可证使用授权：

* [摄取筛选器](#ingestion-filters)
* [配置文件存储](#profile-service)

### 摄取筛选器 {#ingestion-filters}

通过摄取过滤器，您可以仅引入用例所需的数据，并筛选掉所有不需要的事件。

| 摄取筛选器 | 描述 |
| --- | --- |
| Adobe Audience Manager源筛选 | 创建Adobe Audience Manager源连接时，您可以选取并选择要引入的区段和特征 [!DNL data lake] 和Real-time Customer Profile ，而不是摄取整个Audience Manager数据。 请参阅指南，网址为 [创建Audience Manager源连接](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 了解更多信息。 |
| Adobe Analytics数据准备 | 您可以使用 [!DNL Data Prep] 功能过滤掉用例不需要的数据，创建分析源连接时的功能。 到 [!DNL Data Prep]，您可以定义哪些属性/列需要发布到配置文件。 您还可以提供条件语句，以告知Platform数据是应发布到用户档案，还是应仅发布到 [!DNL data lake]. 请参阅指南，网址为 [创建Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 了解更多信息。 |
| 支持配置文件启用/禁用数据集 | 要将数据摄取到Real-time Customer Profile，您必须启用要在配置文件存储中使用的数据集。 这样，会将添加到您的 [!DNL Addressable Audience] 和 [!DNL Profile Richness] 权利。 一旦客户配置文件用例不再需要某个数据集，您可以禁用该数据集与配置文件的集成，以确保您的数据符合许可证要求。 请参阅指南，网址为 [为配置文件启用和禁用数据集](../../catalog/datasets/enable-for-profile.md) 了解更多信息。 |
| Web SDK和Mobile SDK数据排除 | Web和Mobile SDK收集的数据有两种类型：自动收集的数据和开发人员明确收集的数据。 要更好地管理许可证合规性，您可以通过上下文设置在SDK的配置中禁用自动数据收集。 您的开发人员也可以删除或设置自定义数据。 请参阅指南，网址为 [配置SDK基础](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) 了解更多信息。 |
| 服务器端转发数据排除 | 如果您使用服务器端转发将数据发送到Platform，则可以通过以下方法排除发送的数据：在规则操作中删除映射以在所有事件中排除该数据，或者向规则添加条件，以便数据仅针对某些事件触发。 请参阅相关文档 [事件和条件](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) 了解更多信息。 |
| 在源级别筛选数据 | 在创建连接并将数据摄取到Experience Platform之前，可以使用逻辑运算符和比较运算符从源中筛选行级数据。 有关详细信息，请阅读以下指南： [使用过滤源的行级别数据 [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### 配置文件存储 {#profile-service}

配置文件存储区由以下组件组成：

| 配置文件存储组件 | 描述 |
| --- | --- |
| 配置文件片段 | 每个客户配置文件由多个 **配置文件片段** ，形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织将拥有多个 **配置文件片段** 与出现在多个数据集中的单个客户相关。 将这些片段摄取到Platform中时，会使用身份图将它们拼合在一起，以为该客户创建单个配置文件。 **配置文件片段** 由身份命名空间作为标识符组成，其中包含关联的记录数据和/或时间序列数据。 |
| 记录数据（属性） | 用户档案是主题、组织或个人的表示形式，由多个用户档案组成 **属性** (也称为 **记录数据**)。 例如，产品的配置文件可能包括SKU和描述，而人员的配置文件包含名字、姓氏和电子邮件地址等信息。 **记录数据** 通常容量低/中等，但长期来看很有价值。 |
| 时间序列数据（行为） | **时间序列数据** 提供有关用户行为的信息。 由标准架构类体验数据模型(XDM)表示 [!DNL ExperienceEvent]，时间序列数据可以描述事件，例如添加到购物车的项目、点击的链接和查看的视频。 行为的价值可能会随着时间的推移而减弱。 |
| 身份命名空间（身份） | 当客户数据汇集在一起时，会通过使用将其合并到单个配置文件中 **身份命名空间**，以及在用户了解更多信息时将这些身份绑定在一起的能力。 请参阅 [身份命名空间概述](../../identity-service/namespaces.md) 了解更多信息。 |

{style="table-layout:auto"}

#### 配置文件存储构成报表

有许多报告可帮助您了解配置文件存储区的组成。 这些报告可帮助您针对如何以及在何处设置体验事件过期时间，以便更好地优化许可证使用做出明智的决策：

* **数据集重叠报表API**：公开对可寻址受众贡献最大的数据集。 您可以使用此报告来确定 [!DNL ExperienceEvent] 要为其设置过期时间的数据集。 请参阅上的教程 [生成数据集重叠报告](../../profile/tutorials/dataset-overlap-report.md) 了解更多信息。
* **身份重叠报表API**：公开对可寻址受众贡献最大的身份命名空间。 请参阅上的教程 [生成身份重叠报表](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 了解更多信息。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### 假名配置文件数据过期时间 {#pseudonymous-profile-expirations}

此功能允许您自动从配置文件存储中删除过时的假名配置文件。 有关此功能的详细信息，请阅读 [假名配置文件数据过期概述](../../profile/pseudonymous-profiles.md).

#### 体验事件过期时间 {#event-expirations}

此功能允许您从启用了配置文件的数据集中自动删除对用例不再有用的行为数据。 请参阅概述，位于 [体验事件过期时间](../../profile/event-expirations.md) 以了解此流程在数据集上启用后如何工作的详细信息。

## 许可证使用合规性最佳实践摘要 {#best-practices}

以下是您可以遵循的一些推荐最佳实践列表，以确保更好地遵守您的许可证使用授权：

* 使用 [许可证使用情况仪表板](../../dashboards/guides/license-usage.md) 以跟踪和监控客户使用趋势。 这允许您提前了解可能产生的任何潜在过量。
* 配置 [摄取过滤器](#ingestion-filters) 确定分段和个性化用例所需的事件。 这样，您就可以仅发送用例所需的重要事件。
* 确保您只有 [为配置文件启用数据集](#ingestion-filters) 分段和个性化用例所需的参数。
* 配置 [体验事件过期时间](#event-expirations) 和 [假名配置文件数据过期时间](#pseudonymous-profile-expirations) 高频数据（如Web数据）。
* 定期检查 [用户档案构成报表](#profile-store-composition-reports) 以了解您的个人资料存储合成。 这使您能够了解对许可证使用量消耗贡献最大的数据源。

## 功能摘要和可用性 {#feature-summary}

本文档中概述的最佳实践和工具将帮助您更好地管理Adobe Experience Platform中的许可证权利使用情况。 本文档将随着附加功能的发布而更新，以帮助向所有Experience Platform客户提供可见性和控制力。

下表列出了您目前可以使用的功能，以便更好地管理您的许可证使用授权。

| 功能 | 描述 |
| --- | --- |
| [为配置文件启用/禁用数据集](../../catalog/datasets/user-guide.md) | 启用或禁用数据集摄取到Real-Time Customer Profile。 |
| [体验事件过期时间](../../profile/event-expirations.md) | 为摄取到启用配置文件的数据集中的所有事件应用过期时间。 请联系您的Adobe客户团队或客户关怀团队以启用此功能。 |
| [Adobe Analytics数据准备过滤器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 应用 [!DNL Kafka] 用于从摄取中排除不必要数据的过滤器 |
| [Adobe Audience Manager源连接器过滤器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 应用Audience Manager源连接筛选器以从摄取中排除不必要的数据 |
| [Alloy SDK数据过滤器](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | 应用Alloy筛选器以从摄取中排除不必要的数据 |
| [事件转发数据过滤器](../../tags/ui/event-forwarding/overview.md) | 应用服务器端 [!DNL Kafka] 用于从摄取中排除不必要的数据的过滤器。  请参阅相关文档 [标记规则](../../tags/ui/managing-resources/rules.md) 以获取其他信息。 |
| [许可证使用情况功能板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 查看贵组织的许可证相关数据的快照以供Experience Platform |
| [数据集重叠报表API](../../profile/tutorials/dataset-overlap-report.md) | 输出对可寻址受众贡献最大的数据集 |
| [身份重叠报表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 输出对可寻址受众贡献最大的身份命名空间 |

{style="table-layout:auto"}
