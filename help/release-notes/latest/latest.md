---
title: Adobe Experience Platform 发行说明（2025 年 4 月）
description: Adobe Experience Platform 的 2025 年 4 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6558046e9708267cd0ceda36e7c0bdba6b2f758a
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 98%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发布日期：2025 年 4 月 29 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [Experience League](#experience-league)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [身份标识服务](#identity)
- [查询服务](#query-service)
- [实时客户轮廓](#profile)
- [沙盒](#sandboxes)
- [源](#sources)
- [用例战术手册](#use-case-playbooks)

## Experience League {#experience-league}

Experience League 是一个综合性的学习平台，旨在帮助您提高使用 Adobe 产品的技能。它提供各种资源，包括：课程、文档、社区页面、活动和认证访问权限。

| 功能 | 描述 |
| --- | --- |
| 个性化主页 | 在[Experience League](https://experienceleague.adobe.com/zh-hans/home#)上访问和自定义您的个性化主页。 使用您的 Adobe 凭据登录，然后在顶部菜单上选择 **[!UICONTROL Experience League]**，以开始优化您的学习体验： <ul><li>**书签**：使用[!UICONTROL 书签]功能将您喜爱的资源保存并收集在一个地方。您可以保存各种内容，包括播放列表、文章和教程。</li><li>**定制您的学习**：通过使用最符合您需求的角色、行业、产品和经验水平来更新您的 Experience League 轮廓，从而增强您的学习体验。</li><li>**建议**：查看根据您最近的活动推荐的学习内容。</li><li>**最近查看**：使用[!UICONTROL 最近查看]部分快速导航回最近查看的内容，例如文档和视频。</li><li>**学习资源**：使用[!UICONTROL 所有学习资源]面板导航至教程、文档、社区、活动和认证。</li><li>**最新动态**：查看[!UICONTROL 最新动态]部分，了解 Experience League 上的最新内容。</li><li>**按需观看过往活动**：通过[!UICONTROL 按需观看过往活动]部分，观看之前录制的有关产品聚焦、用例和教程的直播。</li></ul><br> ![Experience League 上的个性化主页。](../2025/assets/april/personalized-home-page.png "Experience League 上的个性化主页。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Adform] 扩展 | [!DNL Adform] 服务器端扩展使品牌能够使用 ECID 轻松地重新定位站外受众。此服务器端扩展不依赖于第三方 cookie 或 cookie 备用 ID。此外，由于这完全是在服务器端完成的，因此不需要额外的像素或其他客户端更改。有关更多信息，请参阅 [Adform 扩展概述](/help/tags/extensions/server/adform/overview.md)。 |
| [!DNL Amazon] 网络事件 API 扩展 | [!DNL Amazon]转化 API 扩展程序使广告商能够直接与 [!DNL Amazon] 分享网站互动，从而提供改进的归因、数据可靠性和营销活动优化。此扩展支持事件转发，允许您发送转化事件（例如购买、购物车添加等），同时确保进行适当的重复数据删除，以实现准确报告。有关更多信息，请参阅 [Amazon 扩展概述](/help/tags/extensions/server/amazon/overview.md)。 |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标** {#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Marketo Engage 人员同步](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe 更新了 [!DNL Marketo Engage Person Sync] 目标，以修复身份标识图中存在多封电子邮件时影响客户的问题。 |
| [(V2) Pega CDH 实时受众连接](/help/destinations/catalog/personalization/pega-v2.md) | 当您在 Pega 帐户中配置了多个 Pega Customer Decision Hub 应用程序时，使用 Adobe Experience Platform 中的 [!DNL (V2) Pega Customer Decision Hub Realtime Audience] 目标将轮廓属性和受众会员资格数据发送到 Pega Customer Decision Hub，以做出下一个最佳行动决策。 |

**新增或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| **每周**&#x200B;和&#x200B;**每月**&#x200B;计划选项，用于导出完整文件 | 现在，当激活到云存储基于文件的目标时，您可以每周或每月为人们和潜在受众安排完整的文件导出。[阅读](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)有关计划选项的更多信息。 |

{style="table-layout:auto"}

**修复、增强功能和其他公告** {#destinations-fixes-and-enhancements}

- **数据集导出结束日期的执行延迟至 2025 年 9 月 1 日**\
  作为 [2024 年 9 月版本](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality)的一部分，Adobe 将&#x200B;*在该版本之前*&#x200B;创建的任何数据集导出数据流的默认结束日期设置为 2025 年 5 月 1 日。Adobe 现将此执行期限延长至 **2025 年 9 月 1 日** ，以便为客户提供更多时间来更新其计划。有关如何编辑数据集导出数据流的结束日期的信息，请参阅[导出数据集教程](../../destinations/ui/export-datasets.md#schedule-dataset-export)的计划部分。

- **改进了 LiveRamp Onboarding 对失败的 SFTP 传输的处理**\
  Adobe 已针对影响通过 SFTP 将文件导出到 [LiveRamp Onboarding](/help/destinations/catalog/advertising/liveramp-onboarding.md) 目标的问题实施了修复。有时，文件传输会由于服务器端的瞬时问题而失败，并且失败的尝试产生的临时文件仍会保留在服务器上。这些无法删除的文件阻止了后续重试操作，因为 Adobe 没有权限覆盖它们。\
  修复后，如果重试操作无法删除临时文件，Adobe 将会生成一个带有附加后缀 `attempt2` 的新文件，以确保重试操作成功完成。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的 XDM 组件**

| 功能 | 描述 |
| --- | --- |
| 字符串字段的最小值为 1 | 默认情况下，新字符串字段的最小长度为 1。非必填字段的空值仍然可以接受。如需了解有关最佳实践的更多信息，请阅读[数据建模最佳实践](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

有关 Experience Platform 中 XDM 的详细信息，请查看 [XDM 系统概述](../../xdm/home.md)。

## 身份标识服务 {#identity}

使用 Adobe Experience Platform 身份标识服务通过跨设备和系统桥接身份标识，全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 现在，开发沙盒中的所有客户都可以访问[!BADGE 有限可用性]{type=Informative} [!DNL Identity Graph Linking Rules]标识图形链接规则。 <ul><li>**激活要求**：该功能将保持非活动状态，直到您配置并保存 [!DNL Identity Settings]。如果没有此配置，系统将会继续正常运行，而行为不会发生任何变化。</li><li>**重要说明**：在此限量发布阶段，边缘分段可能会产生意外的区段会员资格结果。但是，流式处理和批量分段将会按预期运行。</li><li>**后续步骤**：有关如何在生产沙盒中启用此功能的信息，请联系您的 Adobe 帐户团队。</li></ul> |

{style="table-layout:auto"}

有关更多信息，请阅读该[[!DNL Identity Graph Linking Rules] 文档](../../identity-service/identity-graph-linking-rules/overview.md)。

## 查询服务 {#query-service}

使用查询服务，通过标准 SQL 在 Adobe Experience Platform 数据湖中查询数据。无缝组合数据集，并从查询结果中生成新数据集，以增强报告功能、启用数据科学工作流程，或促进向实时客户轮廓引入数据。例如，您可以将客户交易数据与行为数据合并，为有针对性的营销活动识别高价值受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| SQL 受众覆盖 | 通过使用新的 SQL 查询的结果覆盖现有轮廓来刷新受众会员资格。通过在单个操作中移除过时的记录并插入更新的记录，您可以更有效地管理动态受众。有关详细信息，请参阅 [SQL 受众扩展指南](../../query-service/data-distiller-audiences/overview.md#replace-audience)。 |
| 下载并复制查询结果 | [直接从查询编辑器以 CSV、XLSX 或 JSON 文件的格式下载查询结果](../../query-service/ui/overview.md#download-query-results)，或者[将结果作为逗号分隔值 (CSV) 复制到剪贴板](../../query-service/ui/overview.md#copy-results)，以便在 Excel 等电子表格应用程序中快速使用。这些增强功能简化了离线分析、报告和数据验证工作流程。 |
| 全屏查看查询结果 | [在全屏对话框中预览查询结果](../../query-service/ui/overview.md#view-results)，以提高可读性，轻松扫描大型数据集，并选择要复制的行。全屏视图提供了可调整大小的网格布局，帮助您更高效地查看宽表和详细输出。 |
| 模型预测中的增强列选择 | 使用扩展的 `model_predict` 语法选择特定列并应用别名。检索中间预测结果，例如特征向量和概率分数。增强选择功能需要激活相应的功能标记。请参阅[模型生命周期文档](../../query-service/advanced-statistics/models.md#select-specific-output-fields)，了解语法示例和功能标记详细信息。 |
| 使用 CREATE TABLE 和 INSERT INTO 保存模型预测输出 | [使用 CREATE TABLE AS SELECT 将选定的预测输出保存到新表中，或使用 INSERT INTO SELECT 插入到现有表中](../../query-service/advanced-statistics/models.md#predict)。如果启用增强列选择，则特征向量和概率等中间结果也可以与最终预测一起保留。有关使用示例，请参阅 [SQL 语法文档](../../query-service/sql/syntax.md#create-table-as-select)。 |

有关 [!DNL Query Service] 的详细信息，请查看 [[!DNL Query Service] 概述](../../query-service/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

| 功能 | 描述 |
| ------- | ----------- |
| 假名轮廓数据有效期限 | 在轮廓仪表板中管理您的假名轮廓数据过期时间。要详细了解此功能和假名轮廓，请阅读[假名轮廓数据有效期限指南](../../profile/pseudonymous-profiles.md)。 |

{style="table-layout:auto"}

要了解有关实时客户轮廓的更多信息，请阅读[轮廓概述](../../profile/home.md)

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足这一需求，Experience Platform 提供了可将单个 Experience Platform 实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具插件支持扩展 | 现在，在沙盒工具中复制 Journey 对象时，可以将自定义操作复制为依赖对象。此外，您还可以选择现有操作以在目标沙盒中重复使用。它们也可以独立地添加到包中。有关支持的 Adobe Journey Optimizer 对象的完整信息，请阅读 [沙盒工具](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects) 指导。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**新来源**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) 源现已可用。使用此源将 [!DNL Algolia] 用户轮廓亲和度数据导入到 Experience Platform。然后，您可以使用这些数据为网站、电子商务平台和应用程序提供高性能搜索解决方案，从而提高用户参与度、转化率和整体客户体验。有关更多信息，请阅读如何将数据[摄入 [!DNL Algolia User Profiles]  Experience Platform 的指南](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md)。 |
| [!BADGE Beta]{type=Informative} API 对 [!DNL Azure Databricks] 的支持 | [!DNL Azure Databricks] 源当前在 API 中可用。使用 [!DNL Flow Service] API 来连接 [!DNL Databricks] 帐户，并将您的 [!DNL Databricks] 数据带到 Experience Platform。有关更多信息，请阅读有关 [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md) 的文档。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 已更新用于将流媒体数据摄入 Experience Platform 的 XDM 字段。 | 新的 XDM 字段组，`mediaReporting`，现在可以通过 Adobe Analytics 源将流媒体数据摄入 Experience Platform 中。此字段取代 `media.mediaTimed` 字段。</br> <br>在三个月的过渡期内，`media.mediaTimed` 字段的数据摄取将继续进行。但是，在 2025 年 7 月末，`media.mediaTimed` 字段将会被完全弃用，并且不会再显示在 Experience Platform Schema UI 中，而且只能使用 `mediaReporting` 字段发送数据。</br><br>如果在 2025 年 4 月 22 日之前实施了 Analytics 源以将流媒体数据收集到平台的客户，则必须迁移您现有的配置，以便使用新字段组发送数据。此迁移必须在 2025 年 7 月底之前完成。联系您的 Adobe 帐户团队以获取迁移支持。 |
| [!DNL MariaDB] 和 [!DNL PostgreSQL] 的新身份验证类型 | 现在可以使用基本身份验证来验证您在 Experience Platform 上的 [!DNL MariaDB] 和 [!DNL PostgreSQL] 源。有关详细信息，请阅读以下文档： <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| [!DNL Amazon Redshift] 的行级过滤支持 | 您可以使用行级过滤功能来处理 Experience Platform 上的 [!DNL Amazon Redshift] 数据。有关更多信息，请阅读 [API 中关于源的行级数据过滤](../../sources/tutorials/api/filter.md)的指南。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。

## 用例战术手册 {#use-case-playbooks}

用例战术手册最初旨在帮助用户克服使用 Real-Time Customer Data Platform 或 Adobe Journey Optimizer 时遇到的挑战。它们不断发展，现在能够快速启动关键营销用例，并提供灵感和预建资产，以便进行测试并投入生产。

用例战术手册已经从发现工具转变为协作框架。他们现在可以帮助您在不同的组织之间构建、管理和共享您自己的战术手册。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 创作并分享您自己的战术手册 | 新的战术手册创作框架使您能够创建、管理和共享您自己的用例战术手册。这包括支持捕获关键元数据、编辑历程图以及关联相关技术资产。您可以在组织之间共享战术手册，以使营销方法标准化并保持一致性。 |

{style="table-layout:auto"}

要了解如何创作和分享您自己的战术手册，请阅读[创作和分享您自己的战术手册](/help/use-case-playbooks/playbooks/author.md)文档。

若要了解更多信息，请阅读[用例战术手册概述](/help/use-case-playbooks/playbooks/overview.md)，其中概述了战术手册的功能、用途以及端到端演示，包括如何创建实例以及如何将生成的资产导入其他沙盒环境。
