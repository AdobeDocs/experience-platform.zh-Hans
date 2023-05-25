---
title: Adobe Experience Platform发行说明2022年3月
description: Adobe Experience Platform 2022年3月版发行说明。
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 3 月 30 日**

Adobe Experience Platform中的新增功能：

- [审核日志](#audit-logs)
- [Real-Time CDP B2B版本中的相关帐户](#related-accounts)

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [数据收集](#data-collection)
- [[!DNL Query Service]](#query-service)
- [源](#sources)

## 审核日志 {#audit-logs}

Experience Platform允许您审核各种服务和功能的用户活动。 审核日志提供有关谁在什么时候做了哪些事情的信息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 数据集、架构、类、字段组、数据类型、沙盒、目标、区段、合并策略、计算属性、产品配置文件和帐户(Adobe)的审核日志 | 这些资源由审核日志记录。 如果启用了此功能，将在活动发生时自动收集审核日志。 您无需手动启用日志收集。 |
| 导出审核日志 | 审核日志可下载为 `CSV` 或 `JSON` 文件。 生成的文件将直接保存到您的计算机。 |

{style="table-layout:auto"}

有关Platform中审核日志的更多信息，请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## Real-Time CDP B2B版本中的相关帐户 {#related-accounts}

>[!NOTE]
>
>“相关帐户”功能仅适用于Real-Time CDP B2B版本的客户。

B2B企业通常将其客户信息存储在多个系统中，每个系统仅包含同一真实世界商业实体的部分甚至冲突数据。 这带来了巨大的挑战，难以准确了解客户的状况，从而降低了其B2B营销和销售工作的效率和有效性。 随着相关帐户的发布， [!DNL Real-Time CDP B2B] 现在显示与正在浏览的帐户类似的帐户列表。 您可以在区段定义中包含相关帐户，以扩大您的覆盖范围或在区段中应用更广泛的标准。

有关该功能的更多信息，请参阅以下文档页面：

- [Real-Time CDP B2B版本中的相关帐户概述](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帐户配置文件UI指南中的“相关帐户”选项卡](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在区段定义中使用相关帐户](../../rtcdp/segmentation/b2b.md#related-accounts)

要了解有关Real-Time CDP B2B版本的更多信息，请参阅 [概述](../../rtcdp/overview.md).

## 警报 {#alerts}

Experience Platform允许您订阅各种Platform活动的基于事件的警报。 您可以通过订阅不同的警报规则 [!UICONTROL 警报] 选项卡，并且可以选择在UI本身中或通过电子邮件通知接收警报消息。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 两个新的警报规则现在可用于与数据摄取相关的源。 请参阅概述，位于 [警报规则](../../observability/alerts/rules.md) 以获取更新的警报类型列表。 |

{style="table-layout:auto"}

有关Platform中警报的更多信息，请参阅 [警报概述](../../observability/alerts/overview.md).

## 仪表板 {#dashboards}

Adobe Experience Platform提供多个 [!DNL dashboards] 通过它可以查看有关您组织的数据的重要信息，如在每日快照期间捕获的数据。

### 配置文件仪表板

配置文件仪表板显示贵组织在Experience Platform的配置文件存储区中拥有的属性（记录）数据的快照。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 未分段的配置文件小组件 | 构件提供未附加到任何区段的所有配置文件总数。 生成的数字截至上次快照时准确，表示在整个组织内激活用户档案的机会。 请参阅 [配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets) 了解更多信息。 |
| 未分段的配置文件趋势构件 | 此小部件为给定时间段内未附加到任何区段的配置文件数量提供了一个折线图说明。可以在30天、90天和12个月期间可视化趋势。 请参阅 [配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets) 了解更多信息。 |
| 按身份小组件分类的未分段配置文件 | 此小部件按其唯一标识符对未分段配置文件的总数进行分类。数据以条形图形式显示。 请参阅 [配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets) 了解更多信息。 |
| 单一身份配置文件小组件 | 此构件提供贵组织仅有一种类型的ID类型的配置文件的计数，用于创建其身份，即电子邮件或ECID。 请参阅 [配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets) 了解更多信息。 |

{style="table-layout:auto"}

有关“用户档案”功能板的详细信息，请参阅 [配置文件功能板概述](../../dashboards/guides/profiles.md).

### 目标仪表板

目标仪表板显示贵组织在Experience Platform中启用的目标快照。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 目标计数构件 | 构件提供可在系统中激活和交付受众的可用端点总数。 此数目包含活动目标数和非活动目标数。请参阅 [目标标准构件文档](../../dashboards/guides/destinations.md#standard-widgets) 了解更多信息。 |

{style="table-layout:auto"}

有关Platform中目标仪表板的更多信息，请参阅 [目标功能板概述](../../dashboards/guides/destinations.md).

## 数据收集 {#data-collection}

Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中丰富和转换数据，并将其分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 全局数据流设置 | 现在，您可以在配置数据流时配置多个新的全局设置：地理位置、第一方ID Cookie和第三方ID同步。 请参阅以下部分： [配置数据流](../../edge/datastreams/overview.md#create) 有关更多信息，请参阅数据流UI指南。 |
| [边缘网络服务器 API](../../server-api/overview.md) | Server API允许客户使用新的经过身份验证的端点与Experience Platform边缘网络进行交互，以支持各种数据收集、个性化、广告和营销用例。 |

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## 查询服务 {#query-service}

[!DNL Query Service] 允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以从以下位置连接任何数据集 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `table_exists` | 新功能命令用于确认系统中当前是否存在表。 该命令返回一个布尔值： `true` 如果表 **是** 存在，并且 `false` 如果表有 **非** 存在。 请参阅 [SQL语法文档](../../query-service/sql/syntax.md) 了解更多信息。 |

{style="table-layout:auto"}

有关可用功能的详细信息，请参阅 [查询服务概述](../../query-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 通过这些源连接，您可以进行身份验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，并管理整个过程中的数据摄取。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 现在有新的源可用于B2B使用 | 您现在可以将Platform上的所有可用源用于B2B用例。 请参阅 [源目录](../../sources/home.md) 以获取可用源的完整列表。 |
| 新产品的正式发布 [!DNL Oracle Eloqua] 源 | 您现在可以使用 [!DNL Oracle Eloqua] 源以无缝地从贵机构的 [!DNL Oracle Eloqua] 实例（帐户、营销活动、联系人）到Platform。 请参阅相关文档 [创建 [!DNL Oracle Eloqua] 源连接](../../sources/connectors/marketing-automation/oracle-eloqua.md) 了解更多信息。 |
| 的API增强功能 [!DNL Data Landing Zone] | 此 [!DNL Data Landing Zone] 源现在支持在使用时自动检测文件属性 [!DNL Flow Service] API。 请参阅相关文档 [创建 [!DNL Data Landing Zone] 源连接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 了解更多信息。 |

{style="table-layout:auto"}

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
