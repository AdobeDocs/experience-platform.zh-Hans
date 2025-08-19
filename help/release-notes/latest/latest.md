---
title: Adobe Experience Platform 发行说明（2025 年 8 月）
description: Adobe Experience Platform 的 2025 年 8 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: af669d58ac4031354e477954a8a733cf0bd7a64b
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 38%

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

**发行日期： 2025年8月19日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [警报](#alerts)
- [目录服务](#catalog-service)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [实时客户轮廓](#profile)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过 Experience Platform 用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 流吞吐量容量警报 | 三个新警报允许用户订阅和配置警报，以主动管理和监控流吞吐量容量的性能。 新警报包括流吞吐量达到80%、90%或超出容量限制时的警报。 有关详细信息，请阅读[容量警报规则](../../observability/alerts/rules.md#capacity)指南。 |

有关警报的更多信息，请阅读[[!DNL Observability Insights] 概述](../../observability/home.md)。

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录保存这些文件和目录的元数据和描述以供查找和监控目的。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Real-time Customer Profile的数据保留 | 您只能&#x200B;**每30天**&#x200B;更新一次实时客户配置文件的数据保留期。 |

有关目录服务的详细信息，请阅读[目录服务概述](../../catalog/home.md)。

## 目标 {#destinations}

[!DNL Destinations]是预先构建的与目标平台的集成，允许从Experience Platform无缝激活数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

>[!IMPORTANT]
>
>**数据集导出计划扩展**
>
>如果您的组织在2024年11月之前创建了数据集导出数据流，则这些数据流将在&#x200B;**2025年9月1日**&#x200B;停止工作。 如果您需要数据流在2025年9月1日之后继续导出数据，则必须按照[本指南](../../destinations/ui/dataset-expiration-update.md)中的步骤为要向其中导出数据集的每个目标扩展其计划。

>[!IMPORTANT]
>
>基于API的目标需要&#x200B;**IP允许列表更新**
>
>列入允许列表 列入允许列表由于升级到流式目标导出引擎，对基于API的目标使用[IP地址](../../destinations/catalog/streaming/ip-address-allow-list.md)的组织必须在2025年9月15日之前将以下IP地址添加到其&#x200B;**中**：
>
>**必需的IP地址：**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**此更改适用于以下目标类型：**
>
>- [流式受众导出目标](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH实时受众](/help/destinations/catalog/personalization/pega-v2.md)，与[Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)和[Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)的基于API的集成)
>- 通过[Destination SDK](../../destinations/destination-sdk/getting-started.md)构建的公共或专用目标
>
>**所需操作：**&#x200B;如果您已与Adobe合作，将任何IP地址允许列表列入允许列表到基于API的流目标，则需要将上述IP地址添加到您的中，以确保数据流不会中断到基于API的目标。

**新目标**

| 目标 | 描述 |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md)目标 | 使用[!DNL Acxiom Real ID Audience Connection]目标通过[!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/)技术增强受众并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。 |

**更新的目标**

| 目标 | 描述 |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) 内部升级 | 从2025年8月11日开始，您可以在目标目录中并排看到两个&#x200B;**[!DNL Microsoft Bing]**&#x200B;信息卡。 这是由于目标服务内部升级造成的。现有的&#x200B;**[!DNL Microsoft Bing]**&#x200B;目标连接器已重命名为&#x200B;**[!UICONTROL （已弃用） Microsoft Bing]**，现在您可以使用名为&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;的新信息卡。 使用目录中的新&#x200B;**[!UICONTROL Microsoft Bing]**&#x200B;连接获取新的激活数据流。 如果您有任何到&#x200B;**[!UICONTROL （已弃用）Microsoft Bing]**&#x200B;目标的活动数据流，它们会自动更新，因此您无需执行任何操作。 <br><br>如果您通过 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 创建数据流，则必须将 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新为以下值：<ul><li>流量规范 ID：`8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>连接规范 ID：`dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> 此次升级后，您可能会遇到数据流中向&#x200B;**发送的活动配置文件数**&#x200B;的下降[!DNL Microsoft Bing]。 导致此下降的原因是，针对此目标平台的所有激活引入了&#x200B;**ECID映射要求**。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 增强了目标的搜索、筛选和标记功能 | 通过跨[浏览](../../destinations/ui/destinations-workspace.md#browse)和[帐户](../../destinations/ui/destinations-workspace.md#accounts)选项卡的增强搜索、筛选和标记功能，改进您的目标管理工作流。 您现在可以按名称搜索特定数据流和帐户，按各种条件（包括目标平台、状态和日期）进行筛选，以及创建自定义标记以组织目标。 列排序还可用于关键字段，如上次数据流运行时，这使识别和管理目标连接更容易。 |

## Experience Data Model (XDM) {#xdm}

XDM是一个开源规范，为引入Experience Platform的数据提供通用结构和定义（架构）。 通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于模型的架构 | 使用基于模型的架构简化数据建模。 现在，您可以通过全面的操作方法示例和指导更轻松地创建架构。 此功能目前可供Campaign Orchestration许可证持有人使用，并将在正式发布时扩展到Data Distiller客户，从而使数据建模更易于访问且更有效。 |

有关详细信息，请阅读[XDM概述](../../xdm/home.md)。

## 实时客户轮廓 {#profile}

Real-time Customer Profile通过将所有渠道的数据整合到单个配置文件中，为每个客户提供统一、可操作的视图。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 实体API中的增强查找功能 | 实体API现在支持以下内容： <ul><li>人员（个人资料）</li><li>体验事件</li><li>帐户</li><li>机会</li></ul> 此更新简化了API的使用，并帮助确保最佳性能和可靠性。 如果您以前对其他实体类型（包括联接表和自定义多实体类型）使用查找，现在可以借此良机查看API使用情况并利用改进的体验。 有关详细信息，请参阅[Real-Time CDB B2B edition架构升级指南](../../rtcdp/b2b-architecture-upgrade.md)。 |

有关Real-time Customer Profile的详细信息，请阅读[配置文件概述](../../profile/home.md)。

## 沙盒 {#sandboxes}

Experience Platform 旨在全球范围内扩充数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 导入工作流中的依赖关系对象重复数据删除 | 沙盒工具现在将始终在检测到具有相同名称的对象时重复使用现有对象，以避免对象激增。 此更改适用于以下对象： <ul><li>架构</li><li>字段组</li><li>受众</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> 详情请参阅[沙盒工具支持对象指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |
| 跨组织包共享提供整个沙盒支持 | 沙盒工具现在支持跨组织包共享中的&#x200B;**整个沙盒**&#x200B;类型。 您现在可以跨组织共享整个沙盒和多对象包。 详情请参阅 [沙盒工具支持对象指南](../../sandboxes/ui/sharing-packages-across-orgs.md)。 |

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 受众估计 | 受众评估现在会在区段生成器中自动生成。 此值将在您修改受众时更新，并始终反映最新的受众规则。 此外，估计值现在将显示为&#x200B;**范围**，该范围基于采样数据的置信区间。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 用户界面中对[!BADGE 的]{type=Informative}Beta[!DNL Azure Private Links]支持 | 您现在可以将[!DNL Azure Private Links]用于UI中的选定源组。 使用此功能可创建您的源可以连接的专用端点。 使用私有端点，您可以设置绕过公共Internet的连接和数据流，从而增强敏感数据的安全性和网络隔离。 对[!DNL Azure Private Links]的支持可用于以下源： <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> 有关详细信息，请阅读[[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md)上的指南。 |
| [!DNL Azure Blob Storage]的增强型身份验证 | 您现在可以使用基于服务主体的身份验证将[!DNL Azure Blob Storage]源连接到Experience Platform。 使用基于服务主体的身份验证增强安全性、更轻松的凭据轮换以及更精细的帐户访问控制。 有关详细信息，请参阅 [[!DNL Azure Blob Storage]  概述](../../sources/connectors/cloud-storage/blob.md)。 |

有关更多信息，请阅读[来源概述](../../sources/home.md)。