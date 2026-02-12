---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: eceafa1852fc7c17660263d6ef7878a3e7bd0841
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 32%

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

**发行日期： 2026年2月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [Agent Orchestrator](#agent-orchestrator)
- [警报](#alerts)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [查询服务](#query-service)
- [源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator允许您构建和部署支持AI的代理，这些代理可以自动执行工作流并在多个渠道上与客户进行交互。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据载入代理 | 使用数据载入代理配置源连接、验证数据质量、应用语义扩充、查看和验证架构以及运行数据摄取。 对B2C和B2B流执行分步工作流，审查预期输出，并对常见问题进行故障诊断。 |
| 数据Distiller代理 | 使用Data Distiller代理从自然语言创建SQL作业，优化SQL性能，从SQL错误中恢复，调度和管理SQL作业以及监视作业状态。 查看护栏、所需权限和疑难解答指南以开始操作。 |
| 数据收集代理 | 使用数据收集代理获取复杂数据收集配置的上下文指南，并通过对话式见解探索数据收集对象中的谱系、依赖项和关系。 |

{style="table-layout:auto"}

有关详细信息，请参阅[Agent Orchestrator文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过Experience Platform用户界面的[!UICONTROL Alerts]选项卡订阅各种警报规则，并且可以选择在UI中或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 面向客户的警报[!DNL Slack]集成 | 您现在可以向[!DNL Slack]提供面向客户的警报。 按照分步教程设置[!DNL Slack]集成并直接在[!DNL Slack]工作区中接收警报通知。 |

{style="table-layout:auto"}

有关详细信息，请参阅 [[!DNL Observability Insights]  概述](../observability/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform数据收集提供了一系列技术，可让您收集客户端客户体验数据并将这些数据发送到Adobe Experience Platform Edge Network和其他目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Platform Tags扩展管理 | 使用新的扩展管理功能，可上传、打包和发布您组织的扩展，将其分发到开发、专用和公共分发环境。 在顶级公司视图中查找共享私有扩展以及您拥有的扩展。 此功能支持Web、Edge和移动扩展。 |

{style="table-layout:auto"}

有关详细信息，请阅读[数据收集文档](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!DNL Snowflake]批次一般可用 | [!DNL Snowflake]批次目标已移至一般可用性。 现在，您可以在导出数据中连同现有列（例如时间戳、映射属性和受众成员资格）一起查看合并策略ID列。 |
| 对[Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目标的AES256加密支持 | 您现在可以为Amazon S3导出配置AES256加密。 从两个选项中进行选择： <ul><li>**[!UICONTROL Default]**： Experience Platform使用存储段上设置的默认加密算法对静态数据进行加密。</li><li>**[!UICONTROL SSE-S3/AES256]**：Experience Platform将`s3:x-amz-server-side-encryption": "AES256`标头添加到导出中，并在数据登录到S3时使用AES256算法加密静态数据。 **此选项优先于您在S3存储桶上配置的任何默认加密算法**。</li></ul> |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Experience Platform 的数据提供常用的结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供洞察。您可以从客户行为中获得有价值的洞察，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 架构库存组织和搜索 | 架构浏览页面现在包括增强的搜索和筛选、内联操作以及用户定义的标记和文件夹支持。 这些更新可让您更轻松地跨沙盒查找、组织和管理架构，同时减少手动导航和维护工作量。 |
| 限制编辑包含数据集的架构 | 现在，在架构存在数据集后，会限制导致重大更改的编辑操作。 关联数据集后，您将无法再重命名或删除字段、更改字段数据类型或格式、修改身份描述符、管理相关字段以删除现有字段或更改分配的类；仍支持添加更改和字段弃用。 |

有关详细信息，请参阅 [[!DNL XDM]  概述](../xdm/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以加入来自 [!DNL Data Lake] 的任何任何数据集，并将查询结果捕获为新数据集，以用于报告、Data Science Workspace，或将数据摄取到实时客户轮廓。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据Distiller年度计算重置日期调整（限量发布） | 现在，数据Distiller年度计算小时数会根据购买或续订许可证的时间，在数据Distiller合同的周年日重置。 这会使“许可证使用情况”报告与您的合同条款保持一致，并且可能会导致一次性调整当前使用值。 |
| 数据Distiller会话管理（限量发布） | 作为授权管理员，您可以通过UI查看和管理组织和沙盒中的活动查询服务和数据Distiller会话。 使用会话管理来标识空闲会话并终止它们以释放容量。 内置的保护措施可防止您终止包含活动查询的会话。 该功能会记录所有逐出操作以进行审核，并通知受影响的用户。 您需要&#x200B;**管理查询会话**&#x200B;权限才能访问此功能。 |

{style="table-layout:auto"}

有关详细信息，请阅读[查询服务概述](../query-service/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| [!DNL Databricks]源连接器中的Unity Catalog支持 | [!DNL Databricks]源连接器现在支持Unity目录。 阅读更新的[[!DNL Databricks]](../sources/connectors/databases/databricks.md)文档，了解如何在配置源连接时使用Unity Catalog。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../sources/home.md)。
