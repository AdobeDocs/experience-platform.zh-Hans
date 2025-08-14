---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: bcf3045fbbf4f9673e954a5ebf95d1225d4cdcd7
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 34%

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

**发行日期：2025年8月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [警报](#alerts)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过 Experience Platform 用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流吞吐量容量警报 | 三个新警报允许用户订阅和配置警报，以主动管理和监控流吞吐量容量的性能。 新警报包括流吞吐量达到80%、90%或超出容量限制时的警报。 有关详细信息，请阅读[容量警报规则](../observability/alerts/rules.md#capacity)指南。 |

有关警报的更多信息，请阅读[[!DNL Observability Insights] 概述](../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations]是预先构建的与目标平台的集成，允许从Experience Platform无缝激活数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

>[!IMPORTANT]
>
>**数据集导出计划扩展**
>
>如果您的组织在2024年11月之前创建了数据集导出数据流，则这些数据流将在&#x200B;**2025年9月1日**&#x200B;停止工作。 如果您需要数据流在2025年9月1日之后继续导出数据，则必须按照[本指南](../destinations/ui/dataset-expiration-update.md)中的步骤为要向其中导出数据集的每个目标扩展其计划。

**新目标**

| 目标 | 描述 |
| --- | --- |
| [!DNL Acxiom Real ID Audience]目标 | 使用[!DNL Acxiom Real ID Audience Connection]目标通过[!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/)技术增强受众并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。 |

**更新的目标**

| 目标 | 描述 |
| --- | --- |
| [!DNL LinkedIn]和[!DNL Pinterest]目标的身份验证到期详细信息 | 帐户过期信息现在直接显示在Experience Platform界面中，因此您可以看到[!DNL LinkedIn]和[!DNL Pinterest]身份验证何时过期并续订，以免对数据流造成任何中断。 |
| 对[!DNL Data Landing Zone]目标的加密支持 | 使用加密保护导出的数据。 现在，您可以附加RSA格式公钥来加密导出的文件，从而为您提供与其他云存储目标相同的敏感信息安全级别。 |
| [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) 内部升级 | 从2025年8月11日开始，您可以在目标目录中并排看到两个&#x200B;**[!DNL Microsoft Bing]**&#x200B;信息卡。 这是由于目标服务内部升级造成的。现有的&#x200B;**[!DNL Microsoft Bing]**&#x200B;目标连接器已重命名为&#x200B;**[!UICONTROL （已弃用） Microsoft Bing]**，现在您可以使用名为&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;的新信息卡。 使用目录中的新&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;连接获取新的激活数据流。 如果您有任何到&#x200B;**[!UICONTROL （已弃用）Microsoft Bing]**&#x200B;目标的活动数据流，它们会自动更新，因此您无需执行任何操作。 <br><br>如果您通过 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 创建数据流，则必须将 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新为以下值：<ul><li>流量规范 ID：`8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>连接规范 ID：`dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 此次升级后，您可能会遇到数据流中向&#x200B;**发送的活动配置文件数**&#x200B;的下降[!DNL Microsoft Bing]。 导致此下降的原因是，针对此目标平台的所有激活引入了&#x200B;**ECID映射要求**。 |
| [!DNL Marketo]目标卡合并 | 使用我们统一的目标卡简化您的[!DNL Marketo]目标设置。 我们已将[!DNL Marketo]个V2和V3信息卡整合到一个简化的选项中，以便更轻松地选择正确的目标并快速入门。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 增强了目标的搜索、筛选和标记功能 | 通过“浏览”和“帐户”选项卡中增强的搜索、筛选和标记功能，改进您的目标管理工作流。 您现在可以按名称搜索特定数据流和帐户，按各种条件（包括目标平台、状态和日期）进行筛选，以及创建自定义标记以组织目标。 列排序还可用于关键字段，如上次数据流运行时，这使识别和管理目标连接更容易。 |

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM是一个开源规范，为引入Experience Platform的数据提供通用结构和定义（架构）。 通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于模型的架构 | 使用基于模型的架构简化数据建模。 现在，您可以通过全面的操作方法示例和指导更轻松地创建架构。 此功能目前可供Campaign Orchestration许可证持有人使用，并将在正式发布时扩展到Data Distiller客户，从而使数据建模更易于访问且更有效。 |

有关详细信息，请阅读[XDM概述](../xdm/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 受众估计 | 受众评估现在会在区段生成器中自动生成。 此值将在您修改受众时更新，并始终反映最新的受众规则。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| UI中的[!BADGE Beta]{type=Informative} Azure专用链接支持 | 通过专用网络连接保护数据安全。 您现在可以创建私有端点并设置绕过公共Internet的数据流，从而增强敏感数据的安全性和网络隔离。 |
| [!DNL Marketo]源文档更新 | 全面了解[!DNL Marketo]数据在进入Experience Platform时如何进行转换。 现在，所有字段映射都包含数据转换的详细解释，因此您可以确切了解`PersonID`如何变为`leadID`，`eventType`如何变为`activityType`。 |
| 支持[!DNL Azure Blob Storage]的服务主体身份验证 | 您现在可以使用服务主体身份验证将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform。 |

有关更多信息，请阅读[来源概述](../sources/home.md)。

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
