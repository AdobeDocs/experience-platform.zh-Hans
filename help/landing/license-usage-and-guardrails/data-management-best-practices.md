---
keywords: Experience Platform；主页；热门主题；数据管理；许可证授权；许可；最佳实践
title: 数据管理许可证授权最佳实践
description: 本文档概述了要遵循的最佳实践，以及可用于通过Adobe Experience Platform更好地管理许可证授权的工具。
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 02882957fc38058ff092938d631e290725d4bdc2
workflow-type: tm+mt
source-wordcount: '2531'
ht-degree: 0%

---

# 数据管理许可证授权最佳实践

Adobe Experience Platform是一个开放系统，可将数据转换为可实时更新的强大客户配置文件，并且使用AI驱动的分析来帮助您在每个渠道中提供正确的体验。 您可以使用源将不同类型、卷和历史记录的数据导入Experience Platform，然后满足这些数据的需求，从分段和个性化到分析和机器学习等用例。

Platform提供的许可证可确定可创建的用户档案数量和可导入的数据量。 由于能够引入任何数据源、卷或历史，因此随着数据量的增长，可能会超出您的许可授权。

本文档概述了要遵循的最佳实践，以及可用于通过Adobe Experience Platform更好地管理许可证授权的工具。

## 了解Adobe Experience Platform数据存储

Experience Platform主要由两个数据存储库组成：the [!DNL Data Lake] 和用户档案存储区。

的 **[!DNL Data Lake]** 主要用于以下目的：

* 充当将数据载入Experience Platform的暂存区；
* 充当所有Experience Platform数据的长期数据存储；
* 启用数据分析和数据科学等用例。

的 **配置文件存储** 是创建客户用户档案的位置，主要用于以下目的：

* 充当用于支持实时体验的用户档案的数据存储；
* 启用分段、激活和个性化等用例。

>[!NOTE]
>
>您对 [!DNL Data Lake] 取决于您购买的产品SKU。 有关产品SKU的更多信息，请与您的Adobe代表联系。

## 许可证使用情况 {#license-usage}

在Experience Platform许可证时，您会获得许可使用权限，具体取决于SKU:

**[!DNL Addressable Audience]**  — 合同允许Experience Platform的客户用户档案总数，包括已知和假名用户档案。

**[!DNL Profile Richness]** -Experience Platform中用户档案数据的平均大小。 您可以 [!DNL Profile Richness] 购买丰富包的权利。

的 [!DNL Profile Richness] 量度因您购买的许可而异。 有两种计算方法 [!DNL Profile Richness] 可用：

* 在任何时间点存储在Real-time Customer Data Platform中的所有生产数据（即配置文件服务和标识服务）的总和除以 [!DNL Addressable Audience];
* 平台内存储的所有数据的总和(包括但不限于 [!DNL Data Lake]、配置文件服务和Identity服务)以及您在过去12个月内通过（而不是存储在中）Platform流经的任何数据除以 [!DNL Addressable Audience].

这些量度的可用性以及每个量度的具体定义因贵组织购买的许可而异。

## 许可证使用功能板

Adobe Experience Platform UI提供了一个功能板，您可以通过该功能板查看贵组织与许可证相关的Platform数据的快照。 功能板中的数据与拍摄快照时在特定时间点显示的数据完全一样。 快照既不是近似数据，也不是数据样本，而且仪表板不会实时更新。

有关详细信息，请参阅 [使用Platform UI中的许可证使用功能板](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## 数据管理最佳实践

以下各节概述了为更好地管理数据而应遵循的最佳实践。

### 了解数据

并非所有数据在Adobe Experience Platform中都是相同的。 某些数据可能是密集的，但值较低，而其他数据可能是稀疏的，但值较高。 一些数据一旦产生就可能失去价值，而另一些数据可能会在几个月内有价值，甚至数年。

要了解数据的值，需要考虑三个维度：

| 维度 | 描述 | 示例 |
| --- | --- | --- |
| 数量 | 表示摄取的数据量和总量。 | Web点击量 — 量高且保真度适中。 价值可能会迅速下降。 |
| 时间跨度 | 表示摄取的数据持续保持有价值的时长。 | 离线购买 — 量和保真度适中，但在较长时间内可能很有价值。 |
| 富达 | 表示数据与信息的丰富程度。 | 客户帐户 — 数量低，但保真度高。 在客户的整个生命周期内都会很有价值。 |

### 数据管理工具 {#data-management-tools}

在确保数据使用情况保持在许可证授权限制范围内时，需要考虑以下两种主要方案：

### 要将哪些数据引入Platform?

数据可以摄取到Platform中的一个或多个系统，即 [!DNL Data Lake] 和/或配置文件存储区。 这意味着针对不同的用例，两个系统中都可以存在不同的数据。 例如，您可能希望在 [!DNL Data Lake]，但在配置文件存储区中不会。 您可以通过启用数据集进行用户档案摄取来选择要发送到用户档案存储的数据。

>[!NOTE]
>
>您对 [!DNL Data Lake] 取决于您购买的产品SKU。 有关产品SKU的更多信息，请与您的Adobe代表联系。

### 要保留哪些数据？

您可以应用数据摄取过滤器和到期规则（也称为存留期“TTL”），以删除对于您的用例已过时的数据。 通常，行为数据（如Analytics数据）消耗的存储比记录数据（如CRM数据）消耗的存储要多得多。 例如，与记录数据相比，许多Platform用户仅使用行为数据填充的用户档案多达90%。 因此，管理行为数据对于确保许可证授权内的合规性至关重要。

您可以利用许多工具来保留在许可证使用授权范围内：

* [摄取过滤器](#ingestion-filters)
* [配置文件服务TTL](#profile-service)

### 摄取过滤器 {#ingestion-filters}

摄取过滤器允许您仅导入用例所需的数据，并过滤出所有不需要的事件。

| 摄取过滤器 | 描述 |
| --- | --- |
| Adobe Audience Manager源过滤 | 在创建Adobe Audience Manager源连接时，您可以选择要引入的区段和特征 [!DNL Data Lake] 和用户档案服务，而不是摄取整个Audience Manager数据。 请参阅 [创建Audience Manager源连接](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 以了解更多信息。 |
| Adobe Analytics数据准备 | 您可以使用 [!DNL Data Prep] 功能来过滤掉用例中不需要的数据。 到达 [!DNL Data Prep]，则可以定义需要将哪些属性/列发布到配置文件。 您还可以提供条件语句，以告知Platform数据是应发布到用户档案，还是仅发布到 [!DNL Data Lake]. 请参阅 [创建Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以了解更多信息。 |
| 支持启用/禁用配置文件数据集 | 要将数据摄取到配置文件服务，您必须启用数据集才能在配置文件存储中使用。 这样做会增加 [!DNL Addressable Audience] 和 [!DNL Profile Richness] 权利。 在客户配置文件用例不再需要某个数据集后，您可以禁用该数据集与配置文件的集成，以确保您的数据符合许可证要求。 请参阅 [启用和禁用配置文件的数据集](../../catalog/datasets/enable-for-profile.md) 以了解更多信息。 |
| Web SDK和Mobile SDK数据排除 | Web SDK和Mobile SDK收集的数据有两种类型：自动收集的数据以及开发人员明确收集的数据。 为了更好地管理许可证合规性，您可以通过上下文设置在SDK配置中禁用自动数据收集。 您的开发人员也可以删除或不设置自定义数据。 请参阅 [配置SDK基础知识](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) 以了解更多信息。 |
| 服务器端转发数据排除 | 如果您使用服务器端转发将数据发送到平台，则可以通过以下两种方式排除发送的数据：删除规则操作中的映射以在所有事件中排除该数据，或向规则添加条件，以便数据仅针对特定事件触发。 请参阅 [事件和条件](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

### 配置文件服务 {#profile-service}

配置文件服务TTL（存留期）功能允许您对配置文件存储中的数据应用TTL。 这样，系统就可以自动删除随着时间的推移而价值已经缩水的数据。

配置文件存储由以下组件组成：

| 配置文件存储组件 | 描述 |
| --- | --- |
| 配置文件片段 | 每个客户用户档案由多个 **配置文件片段** 以形成该客户的单一视图。 例如，如果客户在多个渠道中与您的品牌进行交互，则您的组织将具有多个 **配置文件片段** 与出现在多个数据集中的单个客户相关。 将这些片段摄取到平台后，将使用身份图拼合在一起，以便为该客户创建单个配置文件。 **配置文件片段** 由标识命名空间作为标识符，以及关联的记录数据和/或时序数据。 |
| 记录数据（属性） | 用户档案是由许多主体、组织或个人组成的主体、组织或个人的代表 **属性** (也称为 **记录数据**)。 例如，产品的配置文件可能包含SKU和描述，而人员的配置文件包含名字、姓氏和电子邮件地址等信息。 **记录数据** 通常在卷中处于低/中，但对于较长的时段很有价值。 |
| 时间系列数据（行为） | **时间序列数据** 提供有关用户行为的信息。 由标准架构类体验数据模型(XDM)表示 [!DNL ExperienceEvent]、时间系列数据可描述事件，例如添加到购物车的项目、被点击的链接和查看的视频。 行为的价值可能会随着时间的推移而下降。 |
| 身份命名空间（身份） | 当客户数据汇总在一起时，会通过使用 **身份命名空间**，以及在用户的更多信息公开后将这些身份拼合在一起的功能。 请参阅 [身份命名空间概述](../../identity-service/namespaces.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

#### 配置文件存储组合报表

有许多报表可帮助您了解用户档案存储的构成。 这些报表可帮助您就如何以及在何处设置配置文件TTL做出明智决策，以更好地优化许可证使用：

* **数据集重叠报表API**:显示对可寻址受众贡献最大的数据集。 您可以使用此报表确定 [!DNL ExperienceEvent] 数据集来设置TTL。 请参阅 [生成数据集重叠报表](../../profile/tutorials/dataset-overlap-report.md) 以了解更多信息。
* **身份重叠报表API**:显示对可寻址受众贡献最大的身份命名空间。 请参阅 [生成身份重叠报表](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) 以了解更多信息。
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous TTL for different time thresholds. You can use this report to identify which pseudonymous TTL threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### [!DNL ExperienceEvent] 数据集TTL {#dataset-ttl}

您可以将TTL应用于启用了配置文件的数据集，以从配置文件存储区中删除对用例不再有价值的行为数据。 将TTL应用于启用了配置文件的数据集后，Platform会通过两步流程自动删除不再需要的数据：

* 所有新数据在获取时将应用TTL过期值；
* 所有现有数据都将在一次性回填系统作业中应用TTL过期值。

您可以预期每个事件的TTL值都来自事件时间戳。 运行系统作业时，所有早于TTL过期值的事件都会立即丢弃。 所有其他事件在接近事件时间戳中指定的TTL过期值时都会被丢弃。

请参阅以下示例，以帮助您了解 [!DNL ExperienceEvent] 数据集TTL。

如果在5月15日应用TTL值30天，则：

* 所有新事件的TTL在输入时将为30天；
* 时间戳早于4月15日的所有现有事件都会被系统作业立即删除。;
* 在4月15日之后具有时间戳的事件将到期其事件时间戳+ TTL天。 因此，一个具有4月18日时间戳的事件将在5月15日后的三天内停止运行。

>[!IMPORTANT]
>
>应用TTL后，任何早于所选TTL天数的数据都将为 **永久性** 已删除，无法还原。

在应用TTL之前，必须确保在TTL边界内保留任何区段的回顾窗口。 否则，在应用TTL后，区段结果可能会不正确。 例如，如果对Adobe Analytics数据应用TTL 30天，对存储内事务数据应用TTL 365天，则以下区段将创建错误结果：

* 最近60天内查看过产品页面，然后进行店内购买；
* 添加到购物车，然后在过去60天内没有购买。

相反，以下内容仍会产生正确的结果：

* 查看了产品页面之前的14天内查看过的产品页面，之后又进行了店内购买；
* 最近30天内在线查看了特定帮助页面；
* 最近120天内离线购买了产品；
* 添加到购物车，然后在过去14天内购买。

>[!TIP]
>
>为方便起见，您可以为所有数据集保留相同的TTL，这样您就无需在分段逻辑中担心TTL对数据集的影响。

有关将TTL应用到用户档案数据的更多信息，请参阅 [配置文件服务TTL](../../profile/apply-ttl.md).

## 许可证使用合规性最佳实践摘要 {#best-practices}

以下是一些推荐的最佳实践列表，您可以按照这些最佳实践来确保更好地遵守您的许可证使用权利：

* 使用 [许可证使用仪表板](../../dashboards/guides/license-usage.md) 以跟踪和监控客户使用趋势。 这样，您就可以提前处理可能发生的任何潜在超量情况。
* 配置 [摄取过滤器](#ingestion-filters) 通过确定分段和个性化用例所需的事件来实现。 这样，您就只能发送用例所需的重要事件。
* 确保您仅 [为配置文件启用数据集](#ingestion-filters) 分段和个性化用例所需的区段。
* 配置 [[!DNL ExperienceEvent] 数据集TTL](#dataset-ttl) 用于高频数据，如web数据。
* 定期检查 [用户档案构成报表](#profile-store-composition-reports) 以了解用户档案库的构成。 这样，您就可以了解对许可证使用情况贡献最大的数据源。

## 功能摘要和可用性 {#feature-summary}

本文档中概述的最佳实践和工具将帮助您更好地管理Adobe Experience Platform中的许可证权利使用情况。 随着其他功能的发布，本文档将进行更新，以帮助向所有Experience Platform客户提供可见性和控制。

下表概述了您当前可使用的功能列表，以便更好地管理许可证使用权限。

| 功能 | 描述 |
| --- | --- |
| [启用/禁用配置文件的数据集](../../catalog/datasets/user-guide.md) | 在配置文件服务中启用或禁用数据集摄取 |
| [!DNL ExperienceEvent] 数据集TTL | 对配置文件存储中的行为数据集应用TTL到期。 请联系您的Adobe支持代表。 |
| [Adobe Analytics数据准备过滤器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | 应用 [!DNL Kafka] 从摄取中排除不必要数据的过滤器 |
| [Adobe Audience Manager源连接器过滤器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | 应用Audience Manager源连接过滤器，从摄取中排除不必要的数据 |
| [Alloy SDK数据过滤器](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | 应用Alloy过滤器以从摄取中排除不必要的数据 |
| [事件转发数据过滤器](../../tags/ui/event-forwarding/overview.md) | 应用服务器端 [!DNL Kafka] 过滤器从摄取中排除不必要的数据。  请参阅 [标记规则](../../tags/ui/managing-resources/rules.md) 以了解其他信息。 |
| [许可证使用功能板UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | 查看贵组织与许可证相关的数据的快照以进行Experience Platform |
| [数据集重叠报表API](../../profile/tutorials/dataset-overlap-report.md) | 输出对可寻址受众贡献最大的数据集 |
| [身份重叠报表API](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | 输出对可寻址受众贡献最大的身份命名空间 |

{style=&quot;table-layout:auto&quot;}
