---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
source-git-commit: 95c0aa2861952c1468d5ef43aa370d31d2c8a2ef
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 3 月 30 日**

Adobe Experience Platform的新增功能：

- [审核日志](#audit-logs)
- [Real-Time CDP B2B版中的相关帐户](#related-accounts)

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Query Service]](#query-service)
- [源](#sources)
<!-- - [Experience Data Model (XDM)](#xdm) -->

## 审核日志 {#audit-logs}

Experience Platform允许您审核用户活动以获取各种服务和功能。 审核日志提供有关谁执行了操作以及何时执行的信息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 数据集、架构、类、字段组、数据类型、沙盒、目标、区段、合并策略、计算属性、产品配置文件和帐户的审核日志(Adobe) | 这些是审核日志记录的资源。 如果启用了该功能，则会在活动发生时自动收集审核日志。 您无需手动启用日志收集。 |
| 导出审核日志 | 审核日志可下载为 `CSV` 或 `JSON` 文件。 生成的文件将直接保存到您的计算机。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中审核日志的更多信息，请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## Real-Time CDP B2B版中的相关帐户 {#related-accounts}

>[!NOTE]
>
>“相关帐户”功能仅适用于Real-Time CDP B2B Edition的客户。

B2B企业通常将其客户信息存储在多个系统中，每个系统仅包含相同实际业务实体的部分甚至冲突数据。 这给准确了解客户带来了巨大挑战，从而降低其B2B营销和销售工作的效率和有效性。 随着相关帐户的发布， [!DNL Real-time CDP B2B] 现在，会显示与您正在浏览的帐户类似的帐户列表。 您可以在区段定义中包含相关帐户，以扩大您的范围或在区段中应用更广泛的标准。

请在以下文档页面中阅读有关该功能的更多信息：

- [Real-Time CDP B2B版中的相关帐户概述](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帐户配置文件UI指南中的“相关帐户”选项卡](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在区段定义中使用相关帐户](../../rtcdp/segmentation/b2b.md#related-account)

要进一步了解Real-time CDP B2B Edition，请参阅 [概述](../../rtcdp/overview.md).

## 警报 {#alerts}

Experience Platform允许您订阅各种平台活动的基于事件的警报。 您可以通过 [!UICONTROL 警报] 选项卡，可以选择通过UI本身或电子邮件通知接收警报消息。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 两个新的警报规则现在可用于与数据摄取相关的源。 请参阅 [警报规则](../../observability/alerts/rules.md) ，以了解更新的警报类型列表。 |

{style=&quot;table-layout:auto&quot;}

有关平台中警报的更多信息，请参阅 [警报概述](../../observability/alerts/overview.md).

## 仪表板 {#dashboards}

Adobe Experience Platform提供多个 [!DNL dashboards] 通过查看有关贵组织数据的重要信息（在每日快照期间捕获）。

### 用户档案功能板

“配置文件”功能板显示贵组织在“配置文件存储”(Profile Store)中Experience Platform的属性（记录）数据的快照。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 未分段的配置文件小组件 | 小组件提供未附加到任何区段的所有用户档案总数。 生成的数字从上次快照开始就是准确的，它代表了整个组织中激活配置文件的机会。 请参阅 [用户档案标准小组件文档](../../dashboards/guides/profiles.md#standard-widgets) 以了解更多信息。 |
| 未分段的用户档案趋势小组件 | 此小组件为在给定时间段内未附加到任何区段的用户档案数量提供了折线图插图。 可在30天、90天和12个月期间显示趋势。 请参阅 [用户档案标准小组件文档](../../dashboards/guides/profiles.md#standard-widgets) 以了解更多信息。 |
| 按身份小组件划分的未分段用户档案 | 此小组件按其唯一标识符对未分段的用户档案总数进行分类。 数据以条形图形式显示。 请参阅 [用户档案标准小组件文档](../../dashboards/guides/profiles.md#standard-widgets) 以了解更多信息。 |
| 单个身份配置文件小组件 | 此小组件可提供贵组织的配置文件计数，这些配置文件仅具有一种类型的ID类型来创建其身份（电子邮件或ECID）。 请参阅 [用户档案标准小组件文档](../../dashboards/guides/profiles.md#standard-widgets) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

有关“配置文件”功能板的更多信息，请参阅 [配置文件功能板概述](../../dashboards/guides/profiles.md).

### 目标功能板

“目标”功能板显示贵组织在Experience Platform中启用的目标的快照。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 目标计数小组件 | 小组件提供了可在系统中激活和交付受众的可用端点总数。 此数字包括活动和不活动目标。 请参阅 [destinations standard小组件文档](../../dashboards/guides/destinations.md#standard-widgets) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

有关平台中目标功能板的更多信息，请参阅 [目标功能板概述](../../dashboards/guides/destinations.md).

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## 查询服务 {#query-service}

[!DNL Query Service] 允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以连接 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、Data Science Workspace或摄取到实时客户资料。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| `table_exists` | 新功能命令用于确认系统中当前是否存在表。 该命令返回一个布尔值： `true` 如果表 **does** 存在，并且 `false` 如果表格显示 **not** 存在。 请参阅 [SQL语法文档](../../query-service/sql/syntax.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

有关可用功能的更多信息，请参阅 [查询服务概述](../../query-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理整个数据摄取。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 现在有新的源可用于B2B使用 | 现在，您可以在Platform上为B2B用例使用所有可用源。 请参阅 [源目录](../../sources/home.md) 以获取可用源的完整列表。 |
| 全面提供新 [!DNL Oracle Eloqua] 来源 | 您现在可以使用 [!DNL Oracle Eloqua] 源：无缝地从 [!DNL Oracle Eloqua] 实例（帐户、营销活动、联系人）到平台。 请参阅 [创建 [!DNL Oracle Eloqua] 源连接](../../sources/connectors/marketing-automation/oracle-eloqua.md) 以了解更多信息。 |
| 的API增强功能 [!DNL Data Landing Zone] | 的 [!DNL Data Landing Zone] 现在，源支持在使用 [!DNL Flow Service] API。 请参阅 [创建 [!DNL Data Landing Zone] 源连接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

要进一步了解源，请参阅 [源概述](../../sources/home.md).
