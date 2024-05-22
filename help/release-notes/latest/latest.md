---
title: Adobe Experience Platform 发行说明（2024 年 5 月）
description: Adobe Experience Platform 的 2024 年 5 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 2bdac588114236c6f314217112b9afa805c1f58c
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 17%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年5月21日**

>[!TIP]
>
>此 [Experience PlatformAPI文档](https://developer.adobe.com/experience-platform-apis/) 现在为交互式。 直接从文档页面浏览API端点，以立即获得反馈并加快技术实施。 [了解更多](#interactive-api-documentation) 关于新功能。

对Experience Platform中现有功能的更新：

- [目录服务](#catalog-service)
- [仪表板](#dashboards)
- [数据治理](#governance)
- [查询服务](#query-service)
- [Segmentation Service](#segmentation)
- [源](#sources)

Adobe Experience Platform中的其他更新：

- [文档更新](#documentation-updates)

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然摄取到Experience Platform中的所有数据都作为文件和目录存储在数据湖中，但Catalog包含这些文件和目录的元数据和描述，以用于查找和监控目的。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 批量操作 | 数据集清单现在支持批量操作。 通过批量操作简化数据管理流程，并确保有效管理数据集。 使用批量操作对大量数据集同时执行多个操作以节省时间。  批量操作包括 [移至文件夹](../../catalog/datasets/user-guide.md#move-to-folders)， [编辑标记](../../catalog/datasets/user-guide.md#manage-tags)、和 [删除](../../catalog/datasets/user-guide.md#delete) 数据集。 <br> ![数据集UI工作区中的批量操作。](../2024/assets/may/bulk-actions.png "数据集UI工作区中的批量操作。"){width="100" zoomable="yes"} <br> 有关此功能的详细信息，请参阅 [数据集UI指南](../../catalog/datasets/user-guide.md#bulk-actions). |

{style=“table-layout:auto”}

## 仪表板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可通过这些功能板查看有关贵组织数据的重要见解，如在每日快照期间捕获的数据。

**新增或更新功能**
| 功能 | 描述 | | — | — | | 扩展应用程序报表的可自定义分析 | 无缝 [将SQL分析的输出转换为可理解、业务友好的可视化格式](../../dashboards/data-distiller/customizable-insights/overview.md). 使用自定义SQL查询从各种结构化数据集进行精确的数据操作和创建动态图表。 您可以使用query pro模式执行复杂的SQL分析，然后通过自定义仪表板上的图表与非技术用户共享此分析或将它们导出为CSV文件。 |

{style=“table-layout:auto”}

## 数据治理 {#governance}

Adobe Experience Platform 数据治理是一系列策略和技术，用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策。它在以下方面发挥着关键作用 [!DNL Experience Platform] 在各个级别，包括编目、数据谱系、数据使用标签、数据访问策略和对营销活动数据的访问控制。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| mTLS支持HTTP API目标和Adobe Journey Optimizer自定义操作 | 通过增强的共同传输层安全性(mTLS)协议的安全措施建立客户信任。 此 [Experience PlatformHTTP API目标](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) 和 [Adobe Journey Optimizer自定义操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) 现在向配置的端点发送数据时支持mTLS协议。 您的自定义操作或HTTP API目标中无需额外配置即可激活mTLS；当检测到启用了mTLS的端点时，此过程会自动发生。 您可以 [在此处下载Adobe Journey Optimizer公共证书](../../landing/governance-privacy-security/encryption.md#download-certificates) 和 [此处为目标服务公共证书](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>请参阅 [Experience Platform数据加密文档](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) 有关将数据导出到第三方系统时网络连接协议的更多信息。 |

{style=“table-layout:auto”}

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以从以下位置连接任何数据集： [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 已弃用旧版编辑器 | 旧版编辑器已被弃用，无法再访问。 在其位置，您可以使用 [查询编辑器的增强功能](../../query-service/ui/user-guide.md#query-authoring) 编写、验证和运行查询。 |
| 查询运行延迟 | 通过设置查询运行延迟警报，控制计算时间。 您可以选择在特定时间段后查询状态未更改时接收警报。 只需在Platform UI中设置所需的延迟时间，即可随时了解您的查询进度。 要了解如何在UI中设置此警报，请参阅 [查询计划文档](../../query-service/ui/query-schedules.md#alerts-for-query-status) 或 [内联查询操作指南](../../query-service/ui/monitor-queries.md#query-run-delay). |
| 简化的查询日志清单 | 现在，您可以使用改进的故障排除效率和任务监控 [简化的查询日志UI](../../query-service/ui/query-logs.md#filter-logs)： <ul><li> Platform UI现在默认从日志选项卡中排除所有“系统查询”。 </li><li> 通过取消选中来查看系统查询 **排除系统查询**. </li></ul> <br> ![查询UI工作区中的“日志”选项卡。](../2024/assets/may/query-log.png "查询UI工作区中的“日志”选项卡。"){width="100" zoomable="yes"} <br> 使用简化的查询日志UI获得更集中的视图，帮助您快速识别和分析相关日志。 |
| 数据库选择器 | 使用新的数据库选择器下拉菜单可以 [方便地从Power BI或Tableau访问Customer Journey Analytics数据视图](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). 您现在可以直接从Platform UI中选择所需的数据库，以便更加无缝地集成BI工具。 <br> ![查询UI工作区中的“凭据”选项卡。](../2024/assets/may/database-selector.png "查询UI工作区中的“凭据”选项卡。"){width="100" zoomable="yes"} <br> |

{style=“table-layout:auto”}

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**更新了功能**

| 功能 | 描述 |
| --- | --- |
| 导入外部生成的受众 | 现在，导入外部生成的受众需要“导入受众”权限。 要了解有关权限的更多信息，请阅读 [权限UI指南](../../access-control/home.md#permissions). |

{style=“table-layout:auto”}

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

在Experience Platform中使用源从Adobe应用程序或第三方数据源中摄取数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 的OAuth2客户端凭据身份验证 [!DNL Salesforce] 源 | 您现在可以使用OAuth2客户端凭据来验证您的 [!DNL Salesforce] Experience Platform帐户。 阅读 [!DNL Salesforce] 源 [API指南](../../sources/tutorials/api/create/crm/salesforce.md) 和 [UI指南](../../sources/tutorials/ui/create/crm/salesforce.md) 以了解更多信息。 |
| 支持以下项的示例数据流 [!DNL Marketo Engage] 源 | 此 [!DNL Marketo Engage] 源现在支持示例数据流。 启用示例数据流配置以限制您的摄取率，然后尝试使用Experience Platform功能而无需摄取大量数据。 有关详细信息，请阅读上的指南 [创建数据流 [!DNL Marketo Engage] 在UI中](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| IP地址允许列表更新 | 根据您的位置，必须向允许列表添加一组新的IP地址，才能成功使用流源。 有关新IP地址的完整列表，请阅读 [IP地址允许列表指南](../../sources/ip-address-allow-list.md). |

{style=“table-layout:auto”}

**新文档或更新文档**

| 更新文档 | 描述 |
| --- | --- |
| 的文档更新 [!DNL Google PubSub] | 此 [!DNL Google PubSub] 更新了源文档，提供了完整的先决条件指南。 使用新的先决条件部分了解如何创建服务帐户、在主题或订阅级别授予权限，以及设置配置以优化您的使用 [!DNL Google PubSub] 源。 阅读 [[!DNL Google PubSub] 概述](../../sources/connectors/cloud-storage/google-pubsub.md) 以了解更多信息。 |

{style=“table-layout:auto”}

欲知关于来源的更多信息，请阅读 [源概述](../../sources/home.md).

## 文档更新 {#documentation-updates}

### 交互式Experience PlatformAPI文档 {#interactive-api-documentation}

此 [Experience PlatformAPI文档](https://developer.adobe.com/experience-platform-apis/) 现在为交互式。 现在，所有API引用页面都具有 **试试看** 可用于直接在文档网站页面上测试API调用的功能。 [获取所需的身份验证凭据](/help/landing/api-authentication.md) 并开始使用功能来浏览API端点。

使用此新功能来探索对API端点的请求和响应，以立即获得反馈并加快您的技术实施。 例如，访问 [标识服务API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) 或 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) 端点以探索新的 **试试看** 功能。

![屏幕录制，显示直接从文档网站进行的API调用。](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>请注意，通过在文档页面上使用交互式API功能，您将对端点进行真正的API调用。 在试用生产沙盒时，请牢记这一点。

### 个性化的洞察和参与 {#personalized-insights-engagement}

适用于的新的端到端用例文档页面 [将一次性值发展为生命周期值](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) 现已上线。 阅读此文档，了解如何使用Real-Time CDP和Adobe Journey Optimizer将偶尔访问您的Web资产的用户转化为忠诚客户。
