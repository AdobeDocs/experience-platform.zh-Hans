---
title: Adobe Experience Platform 发行说明（2022 年 3 月）
description: Adobe Experience Platform 的 2022 年 3 月发行说明。
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 16%

---

# Adobe Experience Platform 发行说明

**发行日期： 2022年3月30日**

Adobe Experience Platform 的新功能：

- [审核日志](#audit-logs)
- [Real-Time CDP B2B edition中的相关帐户](#related-accounts)

Adobe Experience Platform 中现有功能的更新：

- [警报](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [数据收集](#data-collection)
- [[!DNL Query Service]](#query-service)
- [源](#sources)

## 审核日志 {#audit-logs}

Experience Platform允许您审核各种服务和功能的用户活动。 审核日志提供有关谁做什么以及何时做什么的信息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 数据集、架构、类、字段组、数据类型、沙盒、目标、区段、合并策略、计算属性、产品配置文件和帐户的审核日志(Adobe) | 这些资源由审核日志记录。 如果启用该功能，将在活动发生时自动收集审核日志。 您无需手动启用日志收集。 |
| 导出审核日志 | 审核日志可以下载为`CSV`或`JSON`文件。 生成的文件将直接保存到您的计算机。 |

{style="table-layout:auto"}

有关Experience Platform中审核日志的更多信息，请参阅[审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md)。

## Real-Time CDP B2B edition中的相关帐户 {#related-accounts}

>[!NOTE]
>
>“相关帐户”功能仅适用于Real-Time CDP B2B edition的客户。

B2B企业通常将其客户信息存储在多个系统中，每个系统仅包含同一真实世界商业实体的部分甚至冲突数据。 这就带来了巨大的挑战，难以准确了解客户的状况，从而降低了其B2B营销和销售工作的效率和有效性。 随着相关帐户的发布，[!DNL Real-Time CDP B2B]现在将向您显示与正在浏览的帐户类似的帐户列表。 您可以在区段定义中包含相关帐户，以扩大您的覆盖范围或在区段中应用更广泛的标准。

请在以下文档页面中阅读有关该功能的更多信息：

- [Real-Time CDP B2B edition中的相关帐户概述](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帐户配置文件UI指南中的“相关帐户”选项卡](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在区段定义中使用相关帐户](../../rtcdp/segmentation/b2b.md#related-accounts)

要进一步了解Real-Time CDP B2B edition，请参阅[概述](../../rtcdp/overview.md)。

## 警报 {#alerts}

通过Experience Platform，您可以为各种Experience Platform活动订阅基于事件的警报。 您可以通过Experience Platform用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，还可以选择在UI中或通过电子邮件通知接收警报消息。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 两个新的警报规则现在可用于与数据摄取相关的源。 有关更新的警报类型列表，请参阅[警报规则](../../observability/alerts/rules.md)的概述。 |

{style="table-layout:auto"}

有关Experience Platform中警报的更多信息，请参阅[警报概述](../../observability/alerts/overview.md)。

## 仪表板 {#dashboards}

Adobe Experience Platform提供了多个[!DNL dashboards]，您可以通过它们查看有关您组织的数据的重要信息，如在每日快照期间捕获的数据。

### 配置文件仪表板

配置文件仪表板显示贵组织在Experience Platform中的配置文件存储区中拥有的属性（记录）数据的快照。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 未分段的配置文件小组件 | 构件提供未附加到任何区段的所有用户档案的总数。 生成的数字与上一个快照时是准确的，表示在您的组织内激活配置文件的机会。 有关详细信息，请参阅[配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets)。 |
| 未分段配置文件趋势构件 | 此小组件为给定时间段内未附加到任何区段的轮廓数量提供了一个折线图说明。可以在30天、90天和12个月的时段内可视化趋势。 有关详细信息，请参阅[配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets)。 |
| 未分段的配置文件（按身份构件） | 此构件按唯一标识符对未分段配置文件总数进行分类。 数据以条形图显示。 有关详细信息，请参阅[配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets)。 |
| 单一身份配置文件小组件 | 此构件提供贵组织仅有一种类型的ID类型用于创建其身份的配置文件的计数，即电子邮件或ECID。 有关详细信息，请参阅[配置文件标准构件文档](../../dashboards/guides/profiles.md#standard-widgets)。 |

{style="table-layout:auto"}

有关配置文件功能板的更多信息，请参阅[配置文件功能板概述](../../dashboards/guides/profiles.md)。

### 目标仪表板

目标仪表板显示贵组织在 Experience Platform 中启用的目标快照。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 目标计数构件 | 构件提供可在系统中激活和交付受众的可用端点总数。 此数字包括活动目标和不活动目标。 有关详细信息，请参阅[目标标准构件文档](../../dashboards/guides/destinations.md#standard-widgets)。 |

{style="table-layout:auto"}

有关Experience Platform中目标功能板的详细信息，请参阅[目标功能板概述](../../dashboards/guides/destinations.md)。

## 数据收集 {#data-collection}

Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中丰富和转换数据，并将其分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 全局数据流设置 | 现在，您可以在配置数据流时配置多个新的全局设置：地理位置、第一方ID Cookie和第三方ID同步。 有关详细信息，请参阅数据流UI指南中有关[配置数据流](../../datastreams/overview.md#create)的部分。 |
| [Edge Network服务器API](../../server-api/overview.md) | 服务器API允许客户使用新的经过身份验证的端点与Experience Platform Edge Network交互，以支持各种数据收集、个性化、广告和营销用例。 |

有关Experience Platform中数据收集的更多信息，请参阅[数据收集概述](../../collection/home.md)。

## 查询服务 {#query-service}

[!DNL Query Service]允许您使用标准SQL在Adobe Experience Platform [!DNL Data Lake]中查询数据。 您可以加入来自 [!DNL Data Lake] 的任何任何数据集，并将查询结果捕获为新数据集，以用于报告、Data Science Workspace，或将数据摄取到实时客户轮廓。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `table_exists` | 新功能命令用于确认系统中当前是否存在表。 如果表&#x200B;**确实存在**，则命令返回布尔值： `true`；如果表确实存在&#x200B;**确实不存在**，则返回`false`。 有关详细信息，请参阅[SQL语法文档](../../query-service/sql/syntax.md)。 |

{style="table-layout:auto"}

有关可用功能的详细信息，请参阅[查询服务概述](../../query-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。通过这些源连接，您可以进行身份验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，并管理整个过程中的数据摄取。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 现在提供了可用于B2B使用的新源 | 您现在可以将Experience Platform上的所有可用源用于B2B用例。 有关可用源的完整列表，请参阅[源目录](../../sources/home.md)。 |
| 新[!DNL Oracle Eloqua]源的正式发布 | 您现在可以使用[!DNL Oracle Eloqua]源从[!DNL Oracle Eloqua]实例（帐户、营销活动、联系人）中无缝地将数据摄取到Experience Platform。 有关详细信息，请参阅有关[创建 [!DNL Oracle Eloqua] 源连接](../../sources/connectors/marketing-automation/oracle-eloqua.md)的文档。 |
| [!DNL Data Landing Zone]的API增强 | 使用[!DNL Flow Service] API时，[!DNL Data Landing Zone]源现在支持自动检测文件属性。 有关详细信息，请参阅有关[创建 [!DNL Data Landing Zone] 源连接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md)的文档。 |

{style="table-layout:auto"}

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
