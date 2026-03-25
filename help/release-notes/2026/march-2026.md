---
title: Adobe Experience Platform 发行说明（2026 年 3 月）
description: Adobe Experience Platform 的 2026 年 3 月发行说明。
source-git-commit: 8c55aebcb65327394ffbdf59db1d2a203182ed18
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 36%

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
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 高级数据生命周期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供了一整套数据安全功能，允许您通过程序化删除客户记录和数据集来管理存储的数据。通过使用UI中的数据生命周期工作区或对数据卫生API的调用，您可以有效地管理数据存储。 使用这些功能可确保信息按预期使用、在需要修复不正确的数据时进行更新以及在组织政策认为必要时进行删除。

| 功能 | 描述 |
| --- | --- |
| 多数据集和仅配置文件记录删除（仅限API） | 您可以在`ALL`中提交单个数据集ID、以逗号分隔的数据集ID列表或文本`datasetId`，以删除一个、多个或所有数据集中的身份。 您也可以通过将`targetServices`设置为`["identity","profile","ajo"]`来限制对配置文件相关服务的删除，这样不会更改datalake；此功能只能通过数据卫生API使用。 有关详细信息，请参阅[记录删除工作单指南](../../hygiene/api/workorder.md)。 |

{style="table-layout:auto"}

如需了解更多信息，请阅读[高级数据生命周期管理概述](../../hygiene/home.md)。

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator允许您构建和部署支持AI的代理，这些代理可以自动执行工作流并在多个渠道上与客户进行交互。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [的 [!DNL Microsoft 365 Copilot]Adobe Marketing Agent](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent是您的嵌入式代理，它将Adobe的营销智能直接引入日常工具，如[!DNL Teams]、[!DNL Word]、[!DNL PowerPoint]和其他[!DNL Microsoft 365]应用程序。 您可以使用此代理从Adobe应用程序中获取可信的营销活动见解，同时您还可以在规划营销活动、审查受众、与同事合作回答客户问题以及在不离开[!DNL Microsoft 365]工作流程的情况下做出基于数据的决策。 |

{style="table-layout:auto"}

有关更多信息，请阅读 [Agent Orchestrator 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md)连接 | 新的Adobe Advertising DSP连接提供了与旧连接相同的功能，并且支持其他身份。 使用新的连接器，您还可以将基于Cookie的标识导出到Adobe Advertising DSP。 |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)连接 | 将[!DNL Real-Time CDP]受众作为每日批处理文件发送到FreeWheel，以便您可以在CTV、视频和显示的FreeWheel交易和营销活动中定位他们。 请联系您的Adobe帐户团队以获取访问权限。 |
| [交易台CRM](../../destinations/catalog/advertising/tradedesk-emails.md)和[Pinterest](../../destinations/catalog/advertising/pinterest.md)的外部受众支持 | 您现在可以将受众从分段服务以外的源激活到交易台CRM、Criteo和Pinterest，包括自定义上传受众（从CSV导入）、相似受众、联合受众和在其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中创建的受众。 此更新将在3月底推出。 有关详细信息，请参阅每个目标目录页面上的[支持的受众](../../destinations/catalog/advertising/criteo.md#supported-audiences)部分。 |
| 增加了自定义上传受众的限制 | 您现在可以为每个目标实例激活最多20个自定义上传受众。 以前，此限制为10。 有关详细信息，请参阅[目标护栏](../../destinations/guardrails.md#batch-file-based-activation)。 |
| 外部受众支持[立即导出文件](../../destinations/ui/export-file-now.md)和[临时激活API](../../destinations/api/ad-hoc-activation-api.md) | 现在，在激活到基于文件的批处理目标时，您可以将立即导出文件(UI)和临时激活API与外部受众（例如自定义上传、相似、联合和其他Experience Platform应用程序中的受众）结合使用。 此更新将在3月底推出。 |

{style="table-layout:auto"}

**修复和改进**

| 修复 | 描述 |
| --- | --- |
| [TikTok](../../destinations/catalog/social/tiktok.md)连接器电话号码散列 | 修复了目标卡中的配置错误意味着从电话号码键入的身份没有激活到TikTok的问题。 若要从这项修复中获益，请设置新的激活流程，或从现有流程中删除电话号码映射，保存后再重新添加。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Experience Platform 的数据提供常用的结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供洞察。您可以从客户行为中获得有价值的洞察，通过区段定义客户受众，并使用客户属性实现个性化目的。

| 功能 | 描述 |
| --- | --- |
| XDM实体操作和删除支持 | 可直接从内联表菜单和详细信息页眉菜单访问架构、类、字段组和数据类型的操作。 如果您具有所需的权限，还可以在组织实体未被数据集使用且未为配置文件启用时将其删除。 有关详细信息，请参阅[XDM UI指南](../../xdm/ui/explore.md)。 |

有关详细信息，请参阅 [XDM 概述](../../xdm/home.md)。

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 摄取类型 | 您现在可以查看属性的摄取类型。 这样可让您了解数据的来源，从而创建更好的受众。 有关此功能的详细信息，请阅读[区段生成器指南](/help/segmentation/ui/segment-builder.md)。 |
| 摘要数据 | 您现在可以查看基于帐户和基于人员的受众的属性摘要数据。 有关帐户受众中有关此功能的详细信息，请阅读帐户[受众生成器指南](/help/rtcdp/segmentation/audience-builder.md)。 有关基于人员的受众中有关此功能的详细信息，请阅读[区段生成器指南](/help/segmentation/ui/segment-builder.md)。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../../segmentation/home.md)。

## 源

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| [!DNL Talon.One] | 您现在可以使用新的[!DNL Talon.One] [!DNL Talon.One]批次[和](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md)流式传输[源将Experience Platform连接到](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md)。 使用新源将忠诚度配置文件数据以及交易和忠诚度活动事件摄取到Experience Platform。 |
| 要允许列表的新IP地址 | GBR9的新IP地址：已将英国添加到您必须列入允许列表的地址列表中，以确保成功将批量源连接至Azure上的Experience Platform。 有关详细信息，请查看[IP地址允许列表指南](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)中的列表。 |
| 增强了对变更数据捕获的支持 | 您现在可以将变更数据捕获用于[!DNL Marketo Engage]、[!DNL Microsoft Dynamics]和[!DNL Salesforce CRM]源。 |
| 已改进[[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md)的身份验证指南 | [!DNL Google BigQuery]源的身份验证指南已展开，其中包含以下信息： <ul><li>刷新令牌的必要范围。</li><li>[!DNL Google]标识所需的IAM角色。</li><li>有关使用`largeResultsDataSetId`的其他指南。</li></ul> |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->