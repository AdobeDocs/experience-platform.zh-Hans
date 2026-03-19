---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

---

# Adobe Experience Platform预发行说明

>[!IMPORTANT]
>
>本文档旨在作为当月发行说明的&#x200B;**预览**。 版本项目可能会发生更改，并且可能会在最终版本中添加或删除。

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/latest)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期： 2026年3月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [高级数据生命周期管理](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [目标](#destinations)
- [查询服务](#query-service)
- [实时客户轮廓](#profile)
- [运行和操作](#run-and-operate)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 高级数据生命周期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供了一整套数据安全功能，允许您通过程序化删除客户记录和数据集来管理存储的数据。使用 UI 中的数据生命周期工作区或通过调用 Data Hygiene API，您可以有效地管理数据存储。使用这些功能可确保信息按预期使用、在需要修复不正确的数据时进行更新以及在组织政策认为必要时进行删除。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 多数据集和仅配置文件记录删除（仅限API） | 您可以在`ALL`中提交单个数据集ID、以逗号分隔的数据集ID列表或文本`datasetId`，以删除一个、多个或所有数据集中的身份。 您还可以通过将`targetServices`设置为`["identity","profile","ajo"]`来限制对配置文件服务的删除，这样会保留datalake不变。 有关详细信息，请参阅[记录删除工作单指南](../hygiene/api/workorder.md)。 |

{style="table-layout:auto"}

如需了解更多信息，请阅读[高级数据生命周期管理概述](../hygiene/home.md)。

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator允许您构建和部署支持AI的代理，这些代理可以自动执行工作流并在多个渠道上与客户进行交互。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent | [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent是您的嵌入式代理，它将Adobe的营销智能直接引入日常工具，如[!DNL Teams]、[!DNL Word]、[!DNL PowerPoint]和其他[!DNL Microsoft 365]应用程序。 在规划Adobe营销活动、审查受众或与同事协作、回答客户问题以及在不离开[!DNL Microsoft 365]工作流程的情况下做出基于数据的决策时，您可以使用此代理从Campaign应用程序中获取可信的营销活动见解。 |

{style="table-layout:auto"}

有关详细信息，请参阅[Agent Orchestrator文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [Snowflake批次](../destinations/catalog/warehouses/snowflake-batch.md)区域选择器 | 现在，您可以使用新的可搜索下拉菜单更轻松地找到您的区域，该下拉菜单将搜索和下拉列表组合到一个控件中。 |
| 将受众元数据导出到[Snowflake批处理](../destinations/catalog/warehouses/snowflake-batch.md)目标 | 现在，导出到此目标的文件包含受众元数据。 新的表结构适用于向前设置的所有新目标连接。 旧表结构将再保留三个月，然后将被弃用。 |
| [!DNL Adobe Advertising Cloud DSP]连接 | 新的Adobe Advertising DSP连接提供了与旧连接相同的功能，并且支持其他身份。 |
| [Trade Desk CRM](../destinations/catalog/advertising/tradedesk-emails.md)、[Criteo](../destinations/catalog/advertising/criteo.md)和[Pinterest](../destinations/catalog/advertising/pinterest.md)的外部受众支持 | 现在，您可以将Segmentation Service区段之外的受众激活到交易台CRM、标准和Pinterest，包括自定义上传受众（从CSV导入）、相似受众、联合受众和在其他Experience Platform应用程序（如Adobe Journey Optimizer）中创建的受众。 有关详细信息，请参阅每个目标目录页面上的[支持的受众](../destinations/catalog/advertising/criteo.md#supported-audiences)部分。 |
| 增加了自定义上传受众限制 | 您现在可以为每个目标实例激活最多20个自定义上传受众。 以前，此限制为10。 |
| 外部受众支持[立即导出文件](../destinations/ui/export-file-now.md)和[临时激活API](../destinations/api/ad-hoc-activation-api.md) | 现在，在激活到基于文件的批处理目标时，您可以将立即导出文件(UI)和临时激活API与外部受众（例如自定义上传、相似、联合和其他Experience Platform应用程序中的受众）结合使用。 |
| 具有OAuth 2和mTLS的HTTP API目标 | 当身份验证端点需要双方TLS (mTLS)时，您现在可以创建使用OAuth 2的HTTP API目标并对其进行身份验证；在目标设置期间令牌检索现在支持mTLS。 |
| ZoomInfo帐户目标 | 您现在可以从Real-Time Customer Data Platform (B2B)将帐户受众发送到ZoomInfo。 |

{style="table-layout:auto"}

**修复和改进**

| 修复 | 描述 |
| --- | --- |
| [Snowflake流](../destinations/catalog/warehouses/snowflake.md)帐户ID验证 | 已向帐户ID步骤中添加了正则表达式验证器。 现在，当您输入ID时，系统会对其进行验证以确保组织ID和帐户ID的格式正确（用点分隔）。 |
| [TikTok](../destinations/catalog/social/tiktok.md)连接器电话号码散列 | 修复了目标卡中的配置错误意味着从电话号码键入的身份没有激活到TikTok的问题。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 配置文件事件时间选择器 | 现在，您可以在配置文件事件选项卡上设置时间窗口，以查看和分析该范围内的事件。 您可以将时间窗口设置为最多30天。 默认情况下，它显示过去48小时内的事件。 |

{style="table-layout:auto"}

更多信息请阅读[实时客户轮廓概述](../profile/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以加入来自 [!DNL Data Lake] 的任何任何数据集，并将查询结果捕获为新数据集，以用于报告、Data Science Workspace，或将数据摄取到实时客户轮廓。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据Distiller加速器 | 现在，您可以从“加速器”选项卡中选择加速器，输入所需的参数，运行或计划生成的SQL而不自己编写它；将任何加速器克隆到自定义模板中以进行编辑。 |

{style="table-layout:auto"}

有关详细信息，请阅读[查询服务概述](../query-service/home.md)。

## 运行和操作 {#run-and-operate}

使用运行和操作工具检查、排除和优化Experience Platform实施。 了解计划的批量激活，识别配置问题，并提高系统可靠性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [作业计划](../run-and-operate/job-schedules.md)一般可用性 | [!DNL Job Schedules]提供了跨数据管道从引入到目标激活的所有已计划批处理作业的统一视图。 检查执行状态，识别计划冲突，并在配置问题影响您的业务运营之前对其进行诊断。 |
| 运行状况检查一般可用性 | 较差的架构和身份配置会导致严重的下游问题，包括不正确的配置文件创建、区段鉴别失败以及不准确的激活。 <br>运行状况检查将您的方法从被动故障诊断转变为主动预防性维护。 运行状况检查始终对沙盒中使用的架构和身份进行扫描，并提供可用于探索和故障排除的问题的摘要。 |

{style="table-layout:auto"}

有关详细信息，请阅读[运行和操作概述](../run-and-operate/overview.md)、[检查作业计划](../run-and-operate/job-schedules.md)和[平台UI指南](../landing/ui-guide.md)。

## Segmentation Service {#segmentation}

Experience Platform允许您根据客户数据创建受众区段，并允许对这些受众进行完整的生命周期管理。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 受众生成器中的摄取源 | 现在，您可以在Audience Builder中查看每个属性是否来自批次、流或边缘源，以避免构建无效或低效的流受众。 |
| 在帐户受众生成器中仅显示包含数据的字段 | 现在，您可以进行筛选，在创建帐户受众时仅显示包含数据的属性。 |

{style="table-layout:auto"}

有关详细信息，请阅读[受众概述](../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| 增强了对变更数据捕获的支持 | 您现在可以将变更数据捕获用于[!DNL Marketo Engage]、[!DNL Microsoft Dynamics]和[!DNL Salesforce CRM]源。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../sources/home.md)。

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->