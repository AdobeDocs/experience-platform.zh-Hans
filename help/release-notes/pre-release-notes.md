---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9b191535ba96c8791a4528361a1945ae27c6456c
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 21%

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

**发行日期： 2026年4月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [查询服务](#query-service)
- [Real-Time CDP](#rtcdp)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Microsoft广告客户匹配](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | 按电子邮件地址匹配客户并在[!DNL Microsoft Advertising Network]中重新与客户互动，包括搜索和受众广告。 将您的[!DNL Microsoft Advertising]帐户关联到Real-Time CDP，以直接从Experience Platform自动创建和管理客户匹配列表。 要获取访问权限，请联系您的Adobe客户经理。 |
| [!BADGE Beta]{type=Informative} [Reddit自定义受众](../destinations/catalog/advertising/reddit-custom-audience.md) | 将受众从Experience Platform发送到[!DNL Reddit Ads]。 连接您的[!DNL Reddit]帐户、映射身份并激活受众以联系在[!DNL Reddit]上积极探索其兴趣的人员。 |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2]是所有新[!DNL Amazon Ads]连接的当前目标。 如果您现有[（旧版） [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md)连接，则它将继续运行，而不需要任何更改。 [!DNL Amazon Ads v2]连接到[!DNL Ads Data Manager]，后者支持扩展身份类型、与地址相关的字段以及跨[!DNL Amazon Ads]产品的数据共享，与[（旧版） [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md)相比，提高了定位和受众匹配率。 |
| [!DNL Rokt] | 使用[!DNL Rokt]将Experience Platform受众关联到AI驱动的实时决策，通过更精确的定位、抑制和个性化来提高营销活动性能。 |
| [Criteo](../destinations/catalog/advertising/criteo.md)的外部受众支持 | 将受众从分段服务以外的源激活到[!DNL Criteo]，包括自定义上传受众（从CSV导入）、相似受众、联合受众和在其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中创建的受众。 有关详细信息，请参阅[支持的受众](../destinations/catalog/advertising/criteo.md#supported-audiences)部分。 |
| [Acxiom受众连接](../destinations/catalog/advertising/acxiom-audience-connection.md) | [!DNL Acxiom Audience Connection]目标现已正式可用。 使用它通过[!DNL Acxiom's Real ID]技术增强受众并将它们激活到其他平台，包括[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]、[!DNL Cox]、[!DNL LG Ads]、[!DNL Spectrum]和[!DNL Viant]。 |
| [Acxiom Real ID受众连接](../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | [!DNL Acxiom Real ID Audience Connection]目标现已正式可用。 使用它激活受众，将[!DNL Acxiom's Real ID]用作同一组受支持平台中的匹配键，包括[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]、[!DNL Cox]、[!DNL LG Ads]、[!DNL Spectrum]和[!DNL Viant]。 |

{style="table-layout:auto"}

**修复和改进**

| 修复 | 描述 |
| --- | --- |
| 自定义Personalization监控支持 | 目标的监视仪表板现在支持[!DNL Custom Personalization]目标。 已移除从监视中排除[!DNL Custom Personalization]的限制说明。 |
| 激活审核中的配置文件计数 | 激活审核步骤现在显示已激活受众的个人资料计数。 还显示流式目标（而不仅仅是批处理目标）的配置文件计数。 |
| [!DNL Pinterest]令牌到期可见性 | [!DNL Pinterest]目标现在显示直接从[!DNL Pinterest]返回的令牌过期时间，以便您查看何时需要重新身份验证。 |
| 现在已为无效计划禁用导出文件 | 当受众计划无效或过期时，**[!UICONTROL Export file now]**&#x200B;操作现在被禁用。 工具提示将说明操作不可用的原因。 |
| 修复了激活工作流中的列可见性 | 修复了一个问题，该问题导致更改一个表中的可见列错误地影响激活工作流中的其他表。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM是一个开源规范，为引入Experience Platform的数据提供通用结构和定义（架构）。 通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供洞察。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 字段组架构使用可见性 | 从详细信息页面查看哪些架构使用字段组，并在包含架构元数据的可排序对话框中浏览它们。 这有助于您快速评估依赖项和影响，而不会偏离正轨。 |

{style="table-layout:auto"}

有关详细信息，请阅读[XDM系统概述](../xdm/home.md)。

## 查询服务 {#query-service}

使用查询服务在Adobe Experience Platform [!DNL Data Lake]中使用标准SQL查询数据。 加入[!DNL Data Lake]中的任何数据集，并将查询结果捕获为新数据集，以用于报表、数据科学Workspace或将其摄取到实时客户个人资料中。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据Distiller加速器 | 在查询服务UI中运行并计划Adobe管理的参数化SQL模板，以执行常见分析而不编写SQL。 这有助于您标准化分析工作流程并在整个组织中重复使用受信任的查询逻辑。 |

{style="table-layout:auto"}

有关详细信息，请阅读[查询服务概述](../query-service/home.md)。

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP]通过跨多个渠道实时摄取、处理和激活数据，提供统一的可操作客户配置文件。 借助Real-Time CDP，组织可以从Experience Platform中连接现有数据源、构建和激活丰富受众，并确保跨目标激活符合隐私要求。 这使营销人员、分析人员和IT团队能够通过无缝、跨渠道的营销活动，为其客户提供高度个性化、及时的体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Real-Time CDP MCP (Beta) | 使用Real-Time CDP MCP将Real-Time CDP引入到AI代理和与MCP兼容的客户端中，使您能够通过本机LLM体验直接与Real-Time CDP工具交互。 通过将与MCP兼容的客户端（例如Claude、ChatGPT、Claude Code、Codex、Cursor或VS Code）连接到Adobe代表提供的端点，您可以使用自然语言检查受众、目标配置和激活运行历史记录，而无需编写Experience Platform REST API调用或导航多个UI工作流。 完成基于浏览器的Adobe登录后，您将拥有对工具的只读访问权限，包括： <ul><li>搜索现有受众</li><li>预览受众成员资格</li><li>列出目标类型</li><li>列出已配置的帐户</li><li>列出已配置的目标</li><li>列出Source连接</li><li>列出目标连接</li><li>检查激活运行</li></ul>. 每个请求都需要`imsOrgId`和`sandboxName`参数，以确保操作范围限定在您的组织和沙盒中。 请注意，此Beta版本不支持写入操作。 |

{style="table-layout:auto"}

有关详细信息，请阅读[Real-Time CDP概述](../rtcdp/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。 公司通常并行运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 快速复制 | 通过[沙盒工具UI](/help/sandboxes/ui/sandbox-tooling.md#express-copy)的单个操作，使用Express Copy将对象复制到目标沙盒。 系统会自动检测依赖对象，并在目标沙盒中创建这些对象，如果它们已存在，则重复使用这些对象。 |

{style="table-layout:auto"}

有关详细信息，请阅读[沙盒概述](../sandboxes/home.md)。

## Segmentation Service {#segmentation-service}

在Experience Platform中，使用分段服务根据客户数据创建受众并管理其整个生命周期。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 流式分段监控 | 在沙盒、数据集和区段级别实时监视评估率、摄取延迟和数据质量量度的流分段。 查看量度，包括评估率、P95摄取延迟、接收的记录、评估的记录、失败的记录和跳过的记录。 还可以查看每个区段符合条件或不符合条件的新配置文件净值。 使用这些见解在容量违规和摄取问题影响您的数据之前确定它们。 |

{style="table-layout:auto"}

有关详细信息，请阅读[受众概述](../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| 自动数据流禁用 | 自动禁用连续30天失败的源摄取数据流，这有助于揭示不健康的数据流并减少重复的失败运行。 |
| [!DNL Delta Sharing] | 您可以使用[!DNL Delta Sharing]源通过安全、开放的数据共享协议将Delta表引入Experience Platform。 在配置[!DNL Delta Sharing]连接并选择要摄取的共享和表后，Platform会自动将该数据引入数据集，以便您将其用于分析、分段和激活。 |
| [!DNL Meta Ads] (Beta) | 您可以使用源工作区中的[!DNL Meta Ads]源连接器(Beta)向[!DNL Meta]进行身份验证，选择您的广告帐户，并计划将[!DNL Meta Ads]营销活动和性能数据摄取到Experience Platform数据集。 |
| [!DNL Talon.One] | 您现在可以使用新的[!DNL Talon.One]批次和流源将Experience Platform连接到[!DNL Talon.One]。 使用新源将忠诚度配置文件数据以及交易和忠诚度活动事件摄取到Experience Platform。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../sources/home.md)。
