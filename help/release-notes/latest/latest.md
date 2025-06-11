---
title: Adobe Experience Platform 发行说明（2025 年 5 月）
description: Adobe Experience Platform 的 2025 年 5 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ab9302a40547349c8d0390baafd8591ed6859e1
workflow-type: ht
source-wordcount: '1530'
ht-degree: 100%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/latest)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发布日期：2025 年 5 月 20 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [AI 助手](#ai-assistant)
- [目录服务](#catalog-service)
- [数据准备](#data-prep)
- [目标](#destinations)
- [身份标识服务](#identity)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## AI 助手 {#ai-assistant}

Adobe Experience Platform 中的 AI 助手是一种对话体验，您可以使用它来加速 Adobe 应用程序中的工作流程。您可以使用 AI 助手更好地了解产品知识、解决问题或搜索信息并找到运营洞察。AI 助手支持 Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 产品支持代理全面上线 | 您现在可以在 AI 助手中使用产品支持代理，无需离开工作流程，即可顺畅排查问题。您组织中的支持管理员现在可以使用产品支持代理创建客户支持工单，其中包含您与 AI 助手互动中的上下文信息和会话详情。<br><br>产品支持代理的访问权限将持续至 2025 年 11 月 30 日。若需在此日期之后继续使用产品支持代理，您必须联系您的 Adobe 客户代表以获取相关授权。有关更多信息，请阅读[产品支持代理文档](../../ai-assistant/new-features/customer-support.md)。 |

有关更多信息，请阅读 [AI 助手概述](../../ai-assistant/landing.md)。

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录保存这些文件和目录的元数据和描述以供查找和监控目的。

| 功能 | 描述 |
| --- | --- |
| 通过数据集级别的保留规则优化数据存储效率 | 通过按设定时间范围自动删除过时数据的保留策略，高效管理数据存储。 <ul><li>**数据集保留**：定义数据集规则，以移除数据湖和轮廓存储中的过时数据。</li><li>**存储洞察**：通过内联量度监控使用情况，确保符合许可授权要求。</li><li>**可见性增强**：通过优化的监控功能，全程追踪数据集从摄取到删除的活动流程。</li><li>**简化管理**：在统一视图中便捷访问保留设置、监控状态、审核日志及洞察信息。</li></ul> 阅读[数据集保留规则](../../catalog/datasets/user-guide.md#data-retention-policy)指南，了解更多信息。 |

{style="table-layout:auto"}

有关详细信息，请参阅[目录服务概述](../../catalog/home.md)。

## 数据准备 {#data-prep}

使用数据准备从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 支持 Adobe Analytics 的导入与导出映射配置 | 您现在可在使用 Adobe Analytics 源连接器时，针对 Adobe Analytics 报告包数据启用导入与导出映射功能。<br><br>将映射配置导出为 CSV 文件，并可在本地通过电子表格对其进行配置。然后，您可以使用 UI 中的映射界面将更新后的映射导入 Experience Platform。您可以使用此功能配置大量映射，而无需在 UI 中手动生成映射。此外，在创建新数据流时，您可以将映射的副本直接上传到 Experience Platform，以加快工作流程。<br><br>如需了解更多信息，请阅读[将 Adobe Analytics 连接至 Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md)指南。</br> |

{style="table-layout:auto"}

有关更多信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [Facebook 自定义受众](../../destinations/catalog/social/facebook.md)升级以及对地址相关标识符提供支持 | 从 2025 年 5 月 23 日开始直至整个 2025 年 6 月，您在目标目录中可能会短暂看到两个 **[!DNL Facebook Custom Audience]** 目标卡片，持续时间最长可达数小时。出现该情况是由于目标服务的内部升级，以及为支持新字段以提升在 Facebook 相关平台上与轮廓的定位与匹配效果。有关新增地址相关字段的详细信息，请参阅[支持的身份标识](#supported-identities)部分。<br><br>如果您看到标有&#x200B;**[!UICONTROL （新）Facebook自定义受众]**&#x200B;的卡片，请使用该卡片创建新的激活数据流。您现有的数据流将自动更新，无需执行任何操作。在此期间，您对现有数据流所做的任何更改将在升级后保留。升级完成后，**[!UICONTROL （新）Facebook自定义受众]**&#x200B;目标卡将重命名为 **[!DNL Facebook Custom Audience]**。<br><br>如果您使用 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 创建数据流，则必须将 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新为以下值： <ul><li>流量规范 ID：`bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>连接规范 ID：`c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| 对 [Google 目标客户匹配功能 + Display &amp; Video 360](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities) 目标的移动广告 ID 支持 | 您现在可以基于移动广告 ID（例如 [!DNL GAID] 和 [!DNL IDFA]）将受众激活到 [Google 目标客户匹配功能 + Display &amp; Video 360 ](../../destinations/catalog/advertising/google-customer-match-dv360.md#supported-identities)目标。 |
| 为 [Google 目标客户匹配功能](../../destinations/catalog/advertising/google-customer-match.md)提供额外的标识符支持 | Google 目标客户匹配功能目标现已支持地址相关字段的映射，有助于在 Google 平台中提升匹配率。<br><br>为确保 Google 能成功匹配地址，您必须映射全部四个地址字段（`address_info_first_name`、`address_info_last_name`、`address_info_country_code` 和 `address_info_postal_code`），且导出的轮廓中这些字段均不得缺失数据。<br> 如任一字段未映射或包含缺失数据，Google 将无法完成地址匹配。 |
| [Facebook](../../destinations/catalog/social/facebook.md) 连接现支持“帐户过期”栏 | 您现在可在[浏览](../../destinations/ui/destinations-workspace.md#browse)和[帐户](../../destinations/ui/destinations-workspace.md#accounts)选项卡中查看 Facebook 帐户令牌的过期日期。 |
| 导出通过 API 创建的数据集 | 您现在可以导出通过 API 创建的数据集。此前仅支持导出通过 UI 创建的数据集的限制现已解除。阅读[导出数据集](../../destinations/ui/export-datasets.md)以了解更多信息。 |

{style="table-layout:auto"}

如需了解更多信息，请阅读[目标概述](../../destinations/home.md)。

## 身份标识服务 {#identity}

使用 Adobe Experience Platform 身份标识服务通过跨设备和系统桥接身份标识，全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] 现已正式发布。[!DNL Identity Graph Linking Rules] 可防止“图形折叠”，确保在 Experience Platform 与各类应用中生成清晰且精准的客户轮廓，用于个性化营销。主要功能包括：<ul><li>[图形模拟工具](../../identity-service/identity-graph-linking-rules/graph-simulation.md)：探索算法机制并测试身份标识设置配置效果。</li><li> [身份设置](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md)：配置唯一命名空间并设定优先级。</li><li>[身份仪表板](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)：监控图形表现并验证身份标识设置。</li></ul> **注意事项**：在您手动配置身份标识设置之前，您的数据不会发生任何变更。 |

{style="table-layout:auto"}

有关详细信息，请参阅[身份标识服务概述](../../identity-service/home.md)。

## 查询服务 {#query-service}

使用查询服务，通过标准 SQL 在 Adobe Experience Platform 数据湖中查询数据。无缝组合数据集，并从查询结果中生成新数据集，以增强报告功能、启用数据科学工作流程，或促进向实时客户轮廓引入数据。例如，您可以将客户交易数据与行为数据合并，为有针对性的营销活动识别高价值受众。

**新增功能或更新后的功能**

| 功能 | 描述 |
|--------|-------------|
| 从 JWT 向 OAuth 凭据迁移 | 为避免服务中断，所有永久有效的 JWT 凭据必须在 2025 年 6 月 30 日前迁移至 OAuth 服务器到服务器模式。此项变更将提升安全性并增强平台一致性。详见[从 JWT 迁移至 OAuth 服务器到服务器凭据指南](../../query-service/ui/migrate-jwt-to-oauth.md)，以了解更多信息。 |
| 旧版结果表（限量开放） | 依赖拖拽选择工作流程的用户可申请访问旧版结果表，该表支持浏览器原生的选择与复制操作。粘贴的输出为制表符分隔格式，确保在 Excel 中的列保持对齐、易于阅读，有助于简化表格审核与质检流程。详见[查询编辑器用户界面指南](../../query-service/ui/user-guide.md#legacy-results-table)，以获取更多信息。 |

有关 [!DNL Query Service] 的详细信息，请查看 [[!DNL Query Service] 概述](../../query-service/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足这一需求，Experience Platform 提供了可将单个 Experience Platform 实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具插件支持扩展 | 现已可通过沙盒工具迁移营销活动，并支持同时迁移附属依赖对象，其中包括渠道配置、统一决策、试验设置/变量等内容。有关支持迁移的营销活动对象的完整列表，以及所有受支持的 Adobe Journey Optimizer 对象，请参阅[沙盒工具](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects)指南。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流媒体细分标准更新 | 自 2025 年 5 月版本起，受众符合流式分段条件的判定标准已更新。有关这些变化的更多信息，请参阅[流式分段资格标准更新](../../segmentation/eligibility-criteria-update.md)。 |

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持 [!DNL MySQL] 的基本身份验证功能 | 您现在可以使用基本身份验证，将您的 [!DNL MySQL] 数据库连接至 Experience Platform。有关更多信息，请阅读[[!DNL MySQL] 数据源概述](../../sources/connectors/databases/mysql.md)。 |

{style="table-layout:auto"}

有关更多信息，请阅读[数据源概述](../../sources/home.md)。