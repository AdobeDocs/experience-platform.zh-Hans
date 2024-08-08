---
title: Adobe Experience Platform发行说明2024年7月
description: Adobe Experience Platform 的 2024 年 7 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c38f6845a4819b648abacea2c36a576dac61f38f
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 22%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年7月30日**

Adobe Experience Platform中的新增功能：

- [!BADGE 有限发布版]{type=Informative}[联合受众组合](#federated-audience-composition)

对Experience Platform中现有功能和文档的更新：

- [高级数据生命周期管理](#advanced-data-lifecycle-management)
- [数据收集](#data-collection)
- [数据管理](#data-governance)
- [目标](#destinations)
- [Segmentation Service](#segmentation)
- [源](#sources)
- [统一标记](#unified-tags)

## 联合受众构成 {#federated-audience-composition}

联合受众组合允许企业组合数据以更好地在各种用例之间应用。 使用此新方法，作为Adobe Real-time Customer Data Platform和/或Adobe Journey Optimizer用户，您可以直接从现有数据仓库联合数据集，以在一个系统中创建和扩充Adobe Experience Platform受众和属性。

有关详细信息，请阅读[联合受众组合文档](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/home)。

## 高级数据生命周期管理 {#advanced-data-lifecycle-management}

Experience Platform提供了一套数据卫生功能，允许您通过以编程方式删除消费者记录和数据集来管理存储的数据。 在UI中使用数据生命周期工作区，或通过调用数据卫生API，您可以有效地管理数据存储。 使用这些功能可确保按预期使用信息，在不正确的数据需要修复时更新信息，并在组织策略认为必要时删除信息。

**新文档**

| 新文档 | 描述 |
| --- | --- |
| [!DNL Data Hygiene API]引用 | 使用数据卫生API有效地管理Experience Platform中的数据存储。 利用这些功能，您可以确保信息按预期使用，并在不正确时更新，以及在组织策略认为有必要时删除。<br><br>阅读[数据卫生API参考文档](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/)以了解有关如何使用该API的详细信息。 您可以使用数据卫生API安排数据集过期日期，以编程方式更正或删除存储的客户个人数据，以及检查您的数据卫生配额。 API参考文档包括可用的端点、请求参数和响应格式，以帮助您有效管理存储的客户数据。</br></br> |

有关详细信息，请阅读[高级数据生命周期管理概述](../../hygiene/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Experience PlatformEdge Network，可在其中丰富和转换数据，并将其分发到Adobe或非Adobe目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| Web SDK | 自动跟踪建议交互 | 您现在可以使用Web SDK中的`autoTrackPropositionInteractionsEnabled`属性来确定Web SDK是否应自动收集建议交互。 有关详细信息，请参阅[`autoTrackPropositionInteractionsEnabled`](../../web-sdk/commands/configure/autotrackpropositioninteractionsenabled.md)文档。 |

{style="table-layout:auto"}

**新文档或更新文档**

| 新文档或更新文档 | 描述 |
| --- | --- |
| 记录了Reactor API的新API端点 | 现在可以在[Reactor API参考文档](https://developer.adobe.com/experience-platform-apis/references/reactor/)中找到扩展包使用授权端点。 扩展所有者可以使用这些端点添加、删除和检索扩展包的包授权。 |
| 新的扩展包使用授权端点文档 | 有关扩展包所有者如何授权其他公司使用其私有版本的Reactor API中的包的概述，请参阅[扩展包使用授权端点](/help/tags/api/endpoints/extension-package-usage-authorizations.md)文档。 |
| 新的共享专用扩展指南 | [共享私有扩展](/help/tags/api/guides/extension-packages.md)文档中概述了Reactor API的扩展包授权创建、批准和删除过程。 |

{style="table-layout:auto"}

有关详细信息，请阅读[数据收集概述](../../collection/home.md)。

## 数据管理 {#data-governance}

Adobe Experience Platform 数据治理是一系列策略和技术，用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策。它在 Experience Platform 的各个层面中发挥着关键作用，包括编目、数据谱系、数据使用标记、数据访问策略和营销操作数据访问控制。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| mTLS服务API | [mTLS服务API](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/overview)旨在增强数据交换的安全性。 使用此API可安全检索Adobe为您的组织应用程序颁发的公共证书。 这些证书确保所有通信都经过身份验证和加密，并且可用于从外部验证证书的真实性。 阅读[公共证书终结点指南](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/public-certificate-endpoint)，了解如何安全地检索组织Adobe应用程序的公共证书。 |

{style="table-layout:auto"}

有关详细信息，请阅读[数据管理概述](../../data-governance/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**{#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [(Beta) Merkury Enterprise连接](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md) | 使用[!DNL Merkury Enterprise Connections]目标将受众安全地交付给[!DNL Merkury]。 [!DNL Merkury]为营销人员提供了基于人员的受众的轻松匹配和交付，这些受众可与[!DNL Merkury]的80多个高级可寻址电视/电视、出版商和广告技术连接进行匹配和交付。 [!DNL Merkury]由2.68亿以上的美国成人消费者身份综合图表提供支持。 |
| [(Beta) Merkury企业标识](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md) | 使用[!DNL Merkury Enterprise Identity]目标构建更准确、更全面且有洞察力的消费者个人资料。 通过改进的配置文件数据，营销人员可以更好地提供见解、区段和模型，从而更准确地定位和预测建模。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 受众级别数据流监控 | 以前，监视按受众分组的数据流仅适用于批处理（基于文件）目标。 从此版本开始，受众级别监视也可用于[(Beta) Google Customer Match + DV360流目标](/help/destinations/catalog/advertising/google-customer-match-dv360.md)。 了解有关[受众级别监控](/help/dataflows/ui/monitor-destinations.md#segment-level-view)的更多信息，如果您想加入Beta计划以使用Google Customer Match + DV360目标，请联系您的Adobe代表。 |
| Destination SDK的受众元数据宏中支持扩充属性 | 您现在可以通过专用宏访问[Destination SDK受众元数据模板](../../destinations/destination-sdk/functionality/audience-metadata-management.md)中的扩充属性。 扩充属性仅可用于[自定义上传受众](../../destinations/destination-sdk/functionality/destination-configuration/schema-configuration.md#external-audiences)。 请参阅[批受众激活指南](../../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes)，了解扩充属性选择的工作方式。 有关详细信息，请参阅受众模板[宏列表](../../destinations/destination-sdk/functionality/audience-metadata-management.md#macros)。 |

{style="table-layout:auto"}

有关详细信息，请阅读[目标概述](../../destinations/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新文档**

| 新文档 | 描述 |
| ----------------- | ----------- | 
| [受众门户](../../segmentation/ui/audience-portal.md) | 了解如何使用Audience Portal，通过它，您可以在集中式中心的Adobe Experience Platform中查看、管理和创建受众。 |

{style="table-layout:auto"}

## 源

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

在Experience Platform中使用源从Adobe应用程序或第三方数据源中摄取数据。

**已更新文档**

| 更新文档 | 描述 |
| --- | --- |
| 扩展的[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)身份验证指南 | 阅读[!DNL Snowflake]的扩展身份验证指南，了解如何检索[帐户标识符](../../sources/connectors/databases/snowflake.md#retrieve-your-account-identifier)和[私钥](../../sources/connectors/databases/snowflake.md#retrieve-your-private-key)以进行身份验证。 此外，使用扩展的身份验证指南以了解如何[验证仓库和角色配置](../../sources/connectors/databases/snowflake.md#verify-configurations)的步骤。 |

{style="table-layout:auto"}

有关详细信息，请阅读[源概述](../../sources/home.md)。

## 统一标记

统一标记允许您在Adobe Experience Platform中对业务对象进行分类和管理。 使用统一标记API，您可以创建文件夹和标记以更好地整理Platform对象，如受众或数据集。

**新文档**

| 新文档 | 描述 |
| ----------------- | ----------- |
| [统一标记API指南](../../administrative-tags/api/overview.md) | 请阅读统一标记API指南，了解如何创建文件夹和标记以对您的业务对象进行排序。 |
| [统一标记API引用](https://developer.adobe.com/experience-platform-apis/references/unified-tags/) | 使用统一标记API引用以交互方式尝试使用统一标记端点。 |

{style="table-layout:auto"}

有关详细信息，请阅读[统一标记概述](../../administrative-tags/overview.md)。
