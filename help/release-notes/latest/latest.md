---
title: Adobe Experience Platform 发行说明（2026 年 1 月）
description: Adobe Experience Platform 的 2026 年 1 月发行说明。
source-git-commit: d6c720ad162d25f24f982df896d3d47bdd9f9aad
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 21%

---


# Adobe Experience Platform 发行说明

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/pre-release-notes)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期： 2026年1月27日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [Agent Orchestrator](#agent-orchestrator)
- [目标](#destinations)
- [实时客户轮廓](#real-time-customer-profile)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator允许您构建和部署支持AI的代理，这些代理可以自动执行工作流并在多个渠道上与客户进行交互。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 面向Adobe Experience Platform代理使用的试用版 | **选择客户现在可以免费试用访问Adobe Experience Platform代理**。 您可以通过由Adobe Experience Platform Agent Orchestrator提供支持的AI Assistant界面，使用该试用版来探索代理并与代理交互。 该试用版提供了在客户现有Experience Cloud产品和环境的环境中运行的AI代理的实践体验，使团队能够在承诺完全购买之前评估价值。 Adobe Experience Platform代理受用户输入和监督的指导，并遵守现有的产品级访问控制，确保用户只能执行操作或查看他们在基础Experience Cloud应用程序中获得授权的数据。 有关如何开始使用的信息，请阅读[Experience Platform代理使用情况绑定的试用概述](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial)。 |

{style="table-layout:auto"}

有关详细信息，请参阅[Agent Orchestrator文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [Kevel目标](/help/destinations/catalog/advertising/kevel.md)连接器现已可用 | Adobe Experience Platform的[!DNL Kevel]流目标允许客户将Adobe受众直接激活到[!DNL Kevel]的UserDB和区段管理API中，以支持在广告决策时进行实时定位。 [[!DNL Kevel]](https://www.kevel.com/)提供支持人工智能的技术和专家指导，帮助创新的商业领袖在零售媒体中启动、扩展和取得成功。 [!DNL Kevel]的Retail Media Cloud功能支持针对网站内和网站外广告采用可归因的可自定义广告格式。 |
| [索引Exchange目标](/help/destinations/catalog/advertising/index-exchange.md)连接器现已可用 | 使用此目标连接器将受众区段直接从Adobe Experience Platform导出到[!DNL Index Exchange]的程序化广告平台。 [!DNL Index]是一个全球广告供应方平台，可帮助媒体所有者最大限度地实现其内容在每个屏幕上的价值。 凭借超过20年的行业领先地位，[!DNL Index]将世界上最大的品牌与高级体验制作者联系起来，以提供高质量的消费者体验。 |
| 对Braze连接的区域端点支持 | [支持的所有](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)区域特定的端点[!DNL Braze]现在都可在目标配置流期间进行选择。 询问您的[!DNL Braze]代表您应使用哪个端点实例。 |
| 对[Liveramp入门](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling)的每周和每月计划支持 | 您现在可以为Liveramp载入目标配置每周和每月导出计划。 <br>此版本正在逐步推出，将于1月30日前完成。 |
| 增强了[交易台](../../destinations/catalog/advertising/tradedesk.md)和[Microsoft Bing](../../destinations/catalog/advertising/bing.md)目标的激活体验 | Trade Desk和Microsoft Bing目标现在包含预定义的强制映射，以便优化激活体验。  <br>此版本正在逐步推出，将于1月30日前完成。 ![显示交易台](../2026/assets/january/mandatory-mappings-ttd.png)的预定义映射的图像{width="150" align="center" zoomable="yes"} <br> ![图像显示Microsoft Bing的预定义映射](../2026/assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| 对[Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目标的AES256加密支持 | 您现在可以为Amazon S3导出配置AES256加密。 提供了两个选项： <ul><li>**[!UICONTROL Default]**：将使用存储段上设置的默认加密算法对静态数据进行加密。</li><li>**[!UICONTROL SSE-S3/AES256]**： Experience Platform在导出中添加了`s3:x-amz-server-side-encryption": "AES256`标头，当数据登录到S3时，将使用AES256算法静态加密数据。 **此选项优先于S3存储桶**&#x200B;上配置的任何默认加密算法。</li></ul> 此版本正在逐步推出，将于1月30日完成。 |
| [交易台 — CRM](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing)连接的电话号码激活支持 | 除了电子邮件地址之外，Trade Desk - CRM目标现在还支持电话号码激活。 您可以对交易台帐户激活E.164格式的未哈希处理电话号码和哈希处理电话号码（SHA256_E.164格式），以便根据CRM数据确定受众目标和进行抑制。 在激活之前，电话号码必须标准化为E.164格式。 |
| [Snowflake批次](../../destinations/catalog/warehouses/snowflake-batch.md)目标更新 | Snowflake批处理目标现在在目标配置期间包括区域选择功能。 您现在可以选择为实例配置的特定Snowflake区域，确保最佳数据传输并符合区域要求。 此外，已删除默认合并策略限制，允许您导出映射到任何合并策略的受众。 <br> [!DNL Snowflake]批次目标当前仅适用于Experience Platform VA7区域中配置的Real-Time CDP客户。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 更新了[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)目标的护栏限制 | 可以映射到单个Adobe Target目标的受众的最大数量已从50增至250。 这使Adobe Target与其他目标的标准受众限制保持一致，从而提供了更大的受众激活工作流灵活性。 您现在可以向Adobe Target目标激活更多受众，而无需创建多个数据流。 |
| [编辑目标](/help/destinations/ui/edit-destination.md)和[编辑营销操作](/help/destinations/ui/edit-activation.md#edit-marketing-actions)一般可用性 | 编辑目标和营销操作的选项现在可供所有用户使用。 |
| 切换映射[步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中的字段显示名称 | 将架构字段映射到目标时，您现在可以在显示完整XDM字段名称和仅显示显示名称之间进行切换。<br> ![显示显示名称切换的屏幕录制。](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 实时客户轮廓 {#real-time-customer-profile}

实时客户配置文件允许您通过组合来自多个渠道的数据（包括在线、离线、CRM和第三方数据）来查看每个客户的整体视图。 用户档案允许您将客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [流式处理容量](/help/landing/license-usage-and-guardrails/capacity.md)实施 | Experience Platform现在为Real-time Customer Profile和Identity Service强制执行流式处理吞吐量功能。 当客户超过其合同规定的流容量时，数据将以“先进先出”的方式排队和处理。 这可以确保可预测的系统性能，并防止容量违规影响数据摄取质量。 重要说明： <ul><li>当超出容量时，流更新插入将不在数据湖上可用</li><li>此强制不适用于具有Adobe Journey Optimizer许可证的客户</li><li>一旦容量可用，将按顺序处理排队的数据。</li></ul> 有关详细信息，请阅读[容量概述](/help/landing/license-usage-and-guardrails/capacity.md)。 |
| 实体查找已弃用 | 现在，所有Real-Time CDP Prime客户都不再使用体验事件的实体查找API。 此弃用内容有助于使Real-Time CDP与许可功能保持一致。 计划使用此功能的Real-Time CDP Ultimate客户可以联系Adobe客户关怀团队以重新启用此功能。  有关详细信息，请阅读[实体API指南](/help/profile/api/entities.md)。 |
| 监测配置文件摄取作业状态 | 您现在可以监测批量配置文件摄取数据流运行的作业级进度百分比。 此功能可实时查看批量摄取作业的当前进度，包括指示摄取是否准备好进行客户细分和Adobe Journey Optimizer查找的关键检查点。 对于可能需要几个小时才能处理的大型摄取，此进度透明度可帮助您了解作业是正常进行还是遇到问题，从而减少数据处理过程中的不确定性。 有关详细信息，请阅读[监视器配置文件指南](/help/dataflows/ui/monitor-profiles.md)。 |
| 配置文件查看器增强功能(GA) | 现在正式提供了配置文件查看器的以下增强功能。 <ul><li>**组合视图**：将属性、事件和洞察组合到同一个视图中。</li><li>**AI 生成的洞察**：轮廓详细信息页面现在显示 AI 生成的洞察，让您了解从轮廓生成的详细信息。这些洞察可能包括倾向性得分和趋势分析等信息。</li><li>**样式更新**：轮廓详细信息页面更新了外观。</li><li>**浏览**：您现在可以通过一个具有搜索和自定义功能的基于信息卡的交互式轮播组件来浏览轮廓。</li></ul> 有关详细信息，请阅读[配置文件查看器指南](/help/profile/ui/user-guide.md)。 |

{style="table-layout:auto"}

有关详细信息，请参阅 [[!DNL Real-Time Customer Profile]  概述](../../profile/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 外部受众数据过期刷新 | 外部受众（例如CSV上传）现在支持对数据过期设置进行强制刷新功能。 此功能允许用户手动刷新外部受众的数据过期时间，从而更好地控制受众生命周期管理。 这对于需要在初始数据过期后保留数据或需要在不重新上传数据的情况下重新激活的受众尤其有用。 有关此功能的详细信息，请阅读[受众门户概述](../../segmentation/ui/audience-portal.md#audience-summary)。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2源 | 新的[!DNL Oracle Eloqua]源连接器现已可用，它取代了[已弃用的连接器](/help/sources/connectors/marketing-automation/oracle-eloqua.md)。 此更新的连接器增强了从[!DNL Oracle Eloqua]将数据摄取到Experience Platform中的功能和可靠性。 使用现有连接器的客户应迁移到新实施，因为现有连接将无法再正常运行。 新连接器支持连接到[!DNL Oracle Eloqua]并摄取营销自动化数据所需的所有设置和配置步骤。 |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2源 | 新的[!DNL Salesforce Marketing Cloud]源连接器现已可用，它取代了[已弃用的连接器](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md)。 此更新的连接器提高了性能，并为将数据从[!DNL Salesforce Marketing Cloud]摄取到Experience Platform提供了其他功能。 使用现有连接器的客户应过渡到新实施。 新连接器包含用于连接到[!DNL Salesforce Marketing Cloud]和摄取营销自动化数据的全面设置说明。 |

有关更多信息，请阅读[来源概述](../../sources/home.md)。

