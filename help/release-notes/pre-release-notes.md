---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
hide: true
hidefromtoc: true
source-git-commit: c716bac1db556fe7a47462e38ee64d7b46bbefcc
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 44%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/pre-release-notes)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期： 2025年6月18日**

Adobe Experience Platform中的新增功能及对现有功能的更新：

- [访问控制](#access-control)
- [高级数据生命周期管理](#advanced-data-lifecycle-management)
- [仪表板](#dashboards)
- [数据治理](#data-governance)
- [目标](#destinations)
- [联合受众构成](#fac)
- [Privacy Service](#privacy-service)
- [沙盒](#sandboxes)
- [源](#sources)

## 访问控制 {#access-control}

Experience Platform利用[Adobe Admin Console](https://adminconsole.adobe.com)产品配置文件将用户与权限和沙盒关联起来。 权限可控制对各种Experience Platform功能的访问，包括数据建模、配置文件管理和沙盒管理。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 导出功能板数据权限 | 功能板中的&#x200B;**[!UICONTROL 下载CSV]**&#x200B;和&#x200B;**[!UICONTROL 以电子邮件形式发送]**&#x200B;选项现在需要&#x200B;**[!UICONTROL 导出功能板数据]**&#x200B;权限。 此权限可确保仅授权用户可以导出列表化的insight数据，从而支持更严格的治理和数据访问控制策略。 |

有关详细信息，请参阅[访问控制概述](../access-control/home.md)。

## 高级数据生命周期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供了一整套数据安全功能，允许您通过程序化删除客户记录和数据集来管理存储的数据。使用 UI 中的数据生命周期工作区或通过调用 Data Hygiene API，您可以有效地管理数据存储。使用这些功能可确保信息按预期使用、在需要修复不正确的数据时进行更新以及在组织政策认为必要时进行删除。

**新文档**

| 新文档 | 描述 |
| --- | --- |
| 记录删除一般可用性 | 您现在可以使用UI或API根据身份字段删除单个记录。 此功能允许从单个数据集或所有数据集进行删除，从而帮助减少存储、强制执行治理并改进数据卫生。 容量限制和授权要求适用。 |

如需了解更多信息，请阅读[高级数据生命周期管理概述](../hygiene/home.md)。

## 仪表板 {#dashboards}

Experience Platform 提供了多个仪表板，您可以通过这些仪表板查看在每日快照中摄取的有关您组织数据的重要洞察。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 以电子邮件导出方式发送选项 | 现在，通过从&#x200B;**[!UICONTROL 查看更多]**&#x200B;菜单中选择&#x200B;**[!UICONTROL 以电子邮件形式发送]**，您最多可以从Query Pro模式功能板导出10,000条记录。 此选项会将下载链接安全地发送到与Adobe相关的电子邮件，以便进行较大的导出。 |

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../dashboards/home.md)。

## 数据治理 {#data-governance}

Adobe Experience Platform 数据治理是一系列策略和技术，用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策。它在 Experience Platform 的 [!DNL Experience Platform] 各个层面中发挥着关键作用，包括编目、数据谱系、数据使用标记、数据访问策略和营销操作数据访问控制。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 列入允许列表 Azure CMK警报和IP配置 | 现在，您可以在Azure密钥库中允许列表Adobe的静态IP地址，以确保在启用网络限制时继续访问。 这有助于防止因密钥访问受限而导致Platform服务中断。 |
| CMK配置警报和解决方案 | 现在，当Adobe服务无法访问您的Azure密钥保管库(例如，由于删除了IP Experience Platform条目或禁用的密钥)时，列入允许列表会触发警报。 新指南可帮助您了解每个警报并采取纠正措施。 |

有关更多信息，请参阅[数据治理概述](../data-governance/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**

| 目标 | 描述 |
| --- | --- |
| 阿尔及利亚用户区段 | “阿尔及利亚用户区段”目标使营销专业人士能够在主页和搜索站点之间提供一致的个性化。 从多个数据源构建丰富的受众，并在各种渠道间共享这些受众，以改进定位策略和营销活动个性化。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| LinkedIn帐户到期信息 | LinkedIn目标的帐户过期信息现在可直接在[!UICONTROL 浏览]和[!UICONTROL 帐户]视图中获取。 以前，此信息仅在文档中可用。 此增强功能可更好地显示LinkedIn身份验证状态和凭据管理。 |
| Google客户匹配+ DV360正式发布和增强功能 | Google客户匹配+ DV360目标现在可供所有Experience Platform用户使用。 该文档现在包含有关Adobe与Google广告帐户之间关联的详细指南。 |
| 数据登录区(DLZ)目标加密支持 | 为数据登陆区目标添加了加密支持。 您现在可以附加RSA格式公钥以向导出的文件添加加密。 |
| 面向企业目标的受众级别监控 | 受众级别监视现在可用于以下企业目标： [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)、[[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md)、[[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)。 |

{style="table-layout:auto"}

如需了解更多信息，请阅读[目标概述](../destinations/home.md)。

## 联合受众构成 {#fac}

联合受众构成允许企业构成数据，以便在各种用例中更好地应用。通过这种新方法，作为 Adobe Real-Time Customer Data Platform 和/或 Adobe Journey Optimizer 用户，您可以直接从现有数据仓库联合数据集，以便在一个系统中创建和丰富 Adobe Experience Platform 受众和属性。

| 新功能 | 描述 |
| ----------- | ----------- |
| HIPAA 准备就绪 | 联合受众组合现在符合HIPAA要求。 有关联合受众组合隐私和安全措施的更多信息，请阅读联合受众组合概述中的[隐私和安全性](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/privacy-security)。 有关一般Experience Platform产品的HIPAA合规性的更多信息，请阅读[HIPAA和Adobe产品和服务概述](https://www.adobe.com/trust/compliance/hipaa-ready.html)。 |

如需了解更多信息，请阅读[联合受众构成文档](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/home)。

## [!DNL Privacy Service] {#privacy}

多项法律和组织规定赋予用户相应的权利，允许他们根据要求从数据存储中访问或删除其个人数据的权利。Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和用户界面，帮助您管理客户数据请求。借助 [!DNL Privacy Service]，您可以提交从 Adobe Experience Cloud 应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 对田纳西州和明尼苏达州隐私法的支持 | Privacy Service现在支持《田纳西州信息保护法案》(`tipa_tn_usa`)和《明尼苏达州消费者数据隐私法案》(`mcdpa_mn_usa`)。 您可以按照这些新的州级法规处理访问和删除请求。 有关详细信息，请参阅[法规概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/privacy/regulations/overview)。 |

有关该服务的更多信息，请参阅 [Privacy Service 概述](../privacy-service/home.md) 。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 对象配置更新迁移 | 现在，您可以在初始复制后跨沙盒迁移迭代对象配置更新。 此增强功能支持开发工作流，在这些工作流中，需要更新配置并在多个环境中传播配置，而无需重新创建整个沙盒设置。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../sandboxes/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持[!DNL Azure Synapse Analytics]的新身份验证类型 | 除了现有的连接字符串身份验证之外，[!DNL Azure Synapse Analytics]现在还将支持服务主体身份验证。 |

**重要身份验证更新**

| 更新 | 描述 |
| --- | --- |
| [!DNL Salesforce]基本身份验证已弃用 | Salesforce CRM和Salesforce Service Cloud的基本身份验证将于2026年1月被弃用。 客户必须迁移到OAuth 2.0身份验证以保持连接。 此更改会影响源连接器，并确保提高安全性并符合Salesforce的身份验证标准。 |

{style="table-layout:auto"}

有关更多信息，请阅读[数据源概述](../sources/home.md)。
