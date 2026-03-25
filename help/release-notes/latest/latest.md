---
title: Adobe Experience Platform 发行说明（2026 年 3 月）
description: Adobe Experience Platform 的 2026 年 3 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6b6a03fb8675ed01dd255f7206b23b05c809f2a6
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 20%

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

**发行日期： 2026年3月24日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [高级数据生命周期管理](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [数据流](#datastreams)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [实时客户轮廓](#real-time-customer-profile)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 高级数据生命周期管理 {#advanced-data-lifecycle-management}

Experience Platform提供了一套数据卫生功能，可帮助您通过以编程方式删除消费者记录和数据集来管理存储的数据。 通过使用UI中的数据生命周期工作区或对数据卫生API的调用，您可以有效地管理数据存储。 使用这些功能可确保信息按预期使用、在需要修复不正确的数据时进行更新以及在组织政策认为必要时进行删除。

| 功能 | 描述 |
| --- | --- |
| 多数据集和仅配置文件记录删除（仅限API） | 您可以在`ALL`中提交单个数据集ID、以逗号分隔的数据集ID列表或文本`datasetId`，以删除一个、多个或所有数据集中的身份。 您也可以通过将`targetServices`设置为`["identity","profile","ajo"]`来限制对配置文件相关服务的删除，这样不会更改datalake；此功能只能通过数据卫生API使用。 有关详细信息，请参阅[记录删除工作单指南](../../hygiene/api/workorder.md)。 |

{style="table-layout:auto"}

如需了解更多信息，请阅读[高级数据生命周期管理概述](../../hygiene/home.md)。

## Agent Orchestrator {#agent-orchestrator}

使用Agent Orchestrator构建和部署AI支持的代理，这些代理可自动化工作流并在多个渠道上与客户进行交互。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [的 [!DNL Microsoft 365 Copilot]Adobe Marketing Agent](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent是您的嵌入式代理，它将Adobe的营销智能直接引入日常工具，如[!DNL Teams]、[!DNL Word]、[!DNL PowerPoint]和其他[!DNL Microsoft 365]应用程序。 您可以使用此代理从Adobe应用程序中获取可信的营销活动见解，同时您还可以在规划营销活动、审查受众、与同事合作回答客户问题以及在不离开[!DNL Microsoft 365]工作流程的情况下做出基于数据的决策。 |

{style="table-layout:auto"}

有关更多信息，请阅读 [Agent Orchestrator 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 数据流 {#datastreams}

数据流表示在实施Adobe Experience Platform Web SDK和Mobile SDK以及Adobe Experience Platform Edge Network服务器API时的服务器端配置。 SDK中的数据流配置命令可处理客户端与之交互的所有服务。

| 功能 | 描述 |
| --- | --- |
| 动态数据流配置一般可用性 | 动态数据流配置现已正式可用。 借助动态数据流配置，您可以为为针对数据流启用的每个服务定义用户可配置的规则集，这些规则集规定哪些Experience Cloud解决方案应接收每种类型的数据。 有关详细信息，请参阅[动态数据流配置指南](../../datastreams/configure-dynamic-datastream.md)。 |

{style="table-layout:auto"}

有关详细信息，请阅读[数据流概述](../../datastreams/overview.md)。

## 目标 {#destinations}

[!DNL Destinations]是与目标平台的预建集成。 使用目标针对跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活您的已知和未知数据。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [Snowflake批次](../../destinations/catalog/warehouses/snowflake-batch.md)区域选择器 | 现在，您可以使用新的可搜索下拉菜单更轻松地找到您的区域，该下拉菜单将搜索和下拉列表组合到一个控件中。 此更新将在3月底推出。 |
| [Snowflake批处理](../../destinations/catalog/warehouses/snowflake-batch.md)目标的新表结构 | 共享到Snowflake帐户中的表现在具有新结构，其中包括单独的受众名称和受众源列。 新的表结构适用于向前设置的所有新目标连接。 对于您设置的任何新连接，将创建两个表结构：新结构以V2为前缀，旧结构保留到2026年6月底，之后将弃用。 有关详细信息，请参阅Snowflake批处理文档的[导出数据](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data)部分。 此更新将在3月底推出。 |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md)连接 | 新的Adobe Advertising DSP连接提供了与旧连接相同的功能，并且支持其他身份。 使用新的连接器，您还可以将基于Cookie的标识导出到Adobe Advertising DSP。 |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)连接 | 将[!DNL Real-Time CDP]受众作为每日批处理文件发送到FreeWheel，以便您可以在CTV、视频和显示的FreeWheel交易和营销活动中定位他们。 请联系您的Adobe帐户团队以获取访问权限。 |
| [交易台CRM](../../destinations/catalog/advertising/tradedesk-emails.md)和[Pinterest](../../destinations/catalog/advertising/pinterest.md)的外部受众支持 | 您现在可以将受众从分段服务以外的源激活到交易台CRM、Criteo和Pinterest，包括自定义上传受众（从CSV导入）、相似受众、联合受众和在其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中创建的受众。 此更新将在3月底推出。 有关详细信息，请参阅每个目标目录页面上的[支持的受众](../../destinations/catalog/advertising/criteo.md#supported-audiences)部分。 |
| 增加了自定义上传受众的限制 | 您现在可以为每个目标实例激活最多20个自定义上传受众。 以前，此限制为10。 有关详细信息，请参阅[目标护栏](../../destinations/guardrails.md#batch-file-based-activation)。 |
| 外部受众支持[立即导出文件](../../destinations/ui/export-file-now.md)和[临时激活API](../../destinations/api/ad-hoc-activation-api.md) | 现在，在激活到基于文件的批处理目标时，您可以将立即导出文件(UI)和临时激活API与外部受众（例如自定义上传、相似、联合和其他Experience Platform应用程序中的受众）结合使用。 此更新将在3月底推出。 |
| 具有OAuth 2和mTLS的[HTTP API](../../destinations/catalog/streaming/http-destination.md)目标 | 当身份验证端点需要双方TLS (mTLS)时，您现在可以创建使用OAuth 2的HTTP API目标并对其进行身份验证；在目标设置期间令牌检索现在支持mTLS。 此更新将在3月底推出。 |

{style="table-layout:auto"}

**修复和改进**

| 修复 | 描述 |
| --- | --- |
| [TikTok](../../destinations/catalog/social/tiktok.md)连接器电话号码散列 | 修复了目标卡中的配置错误意味着从电话号码键入的身份没有激活到TikTok的问题。 若要从这项修复中获益，请设置新的激活流程，或从现有流程中删除电话号码映射，保存后再重新添加。 |
| [Snowflake流](../../destinations/catalog/warehouses/snowflake.md)和[Snowflake批次](../../destinations/catalog/warehouses/snowflake-batch.md)帐户ID验证 | 已向帐户ID步骤中添加了正则表达式验证器。 现在，当您输入ID时，系统会对其进行验证以确保组织ID和帐户ID的格式正确（用点分隔）。 此更新将在3月底推出。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Experience Platform 的数据提供常用的结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供洞察。您可以从客户行为中获得有价值的洞察，通过区段定义客户受众，并使用客户属性实现个性化目的。

| 功能 | 描述 |
| --- | --- |
| XDM实体操作和删除支持 | 可直接从内联表菜单和详细信息页眉菜单访问架构、类、字段组和数据类型的操作。 如果您具有所需的权限，还可以在组织实体未被数据集使用且未为配置文件启用时将其删除。 有关详细信息，请参阅[XDM UI指南](../../xdm/ui/explore.md)。 |

有关详细信息，请参阅 [XDM 概述](../../xdm/home.md)。

## 实时客户轮廓 {#real-time-customer-profile}

Real-time Customer Profile通过组合来自多个渠道的数据（包括在线、离线、CRM和第三方数据）为您提供了每个客户的完整视图。 使用用户档案将您的客户数据整合到一个统一的视图中，并提供每个客户互动的可操作、带时间戳的帐户。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 活动 | 现在，您可以在浏览配置文件时设置事件的回顾时段。 这样，您就可以查看在指定的时间段内与配置文件关联的事件。 有关详细信息，请阅读[配置文件UI指南](../../profile/ui/user-guide.md#events)。 |

{style="table-layout:auto"}

有关详细信息，请参阅 [[!DNL Real-Time Customer Profile]  概述](../../profile/home.md)。

## 运行和操作 {#run-and-operate}

使用运行和操作工具检查、排除和优化Experience Platform实施。 了解计划的批量激活，识别配置问题，并提高系统可靠性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [作业计划](../../run-and-operate/job-schedules.md)一般可用性 | [!DNL Job Schedules]提供了跨数据管道从引入到目标激活的所有已计划批处理作业的统一视图。 检查执行状态，识别计划冲突，并在配置问题影响您的业务运营之前对其进行诊断。 |
| [运行状况检查](../../run-and-operate/health-checks.md)一般可用性 | 较差的架构和身份配置会导致严重的下游问题，包括不正确的配置文件创建、区段鉴别失败以及不准确的激活。 <br>运行状况检查将您的方法从被动故障诊断转变为主动预防性维护。 运行状况检查始终对沙盒中使用的架构和身份进行扫描，并提供可用于探索和故障排除的问题的摘要。 |

{style="table-layout:auto"}

有关详细信息，请阅读[运行和操作概述](../../run-and-operate/overview.md)、[检查作业计划](../../run-and-operate/job-schedules.md)和[平台UI指南](../../landing/ui-guide.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 摄取类型 | 您现在可以查看属性的摄取类型。 这样可让您了解数据的来源，从而创建更好的受众。 有关此功能的详细信息，请阅读[区段生成器指南](../../segmentation/ui/segment-builder.md)。 |
| 摘要数据 | 您现在可以查看基于帐户和基于人员的受众的属性摘要数据。 有关帐户受众中有关此功能的详细信息，请阅读帐户[受众生成器指南](../../rtcdp/segmentation/audience-builder.md)。 有关基于人员的受众中有关此功能的详细信息，请阅读[区段生成器指南](../../segmentation/ui/segment-builder.md)。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。使用这些源连接进行身份验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| 要允许列表的新IP地址 | GBR9的新IP地址：已将英国添加到您必须列入允许列表的地址列表中，以确保成功将批量源连接至Azure上的Experience Platform。 有关详细信息，请查看[IP地址允许列表指南](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)中的列表。 |
| 增强了对变更数据捕获的支持 | 您现在可以将变更数据捕获用于[!DNL Marketo Engage]、[!DNL Microsoft Dynamics]和[!DNL Salesforce CRM]源。 |
| 已改进[[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md)的身份验证指南 | [!DNL Google BigQuery]源的身份验证指南已展开，其中包含以下信息： <ul><li>刷新令牌的必要范围。</li><li>[!DNL Google]标识所需的IAM角色。</li><li>有关使用`largeResultsDataSetId`的其他指南。</li></ul> |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
