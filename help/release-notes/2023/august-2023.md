---
title: Adobe Experience Platform 发行说明（2023 年 8 月）
description: Adobe Experience Platform 的 2023 年 8 月发行说明。
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 89%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 8 月 23 日**

Adobe Experience Platform 中现有功能的更新：

- [Real-Time Customer Data Platform](#rtcdp)
- [基于属性的访问控制](#abac)
- [仪表板](#dashboards)
- [数据收集](#data-collection)
- [数据引入](#data-ingestion)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [身份标识服务](#identity-service)
- [Segmentation Service](#segmentation)
- [源](#sources)

## Real-Time Customer Data Platform {#rtcdp}

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户轮廓。

[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户轮廓。然后，根据这些轮廓构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 智能重新参与用例指南 | [智能重新参与用例指南](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)详细介绍了如何以智能和负责任的方式重新吸引在完成转化之前放弃转化的客户的详细信息。本指南使用以下示例历程来重新吸引客户： <ul><li>重新参与历程 - 针对已放弃浏览产品的客户。</li><li>已放弃的购物车历程 - 针对已将产品放入购物车但尚未完成购买的客户。</li><li>订购确认历程 - 聚焦产品订购</li></ul> 请使用[智能重新参与用例指南](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)底部的详细反馈选项链接提供反馈。 |
| 合作伙伴数据支持 | 在 Real-Time CDP 中执行漏斗上层营销，利用合作伙伴提供的潜在客户轮廓和合作伙伴 ID 来吸引新客户，并丰富您的第一方数据： <ul><li>客户获取和可寻址性：利用所选数据合作伙伴的无 cookie 标识符和散列 PII 来吸引新客户，并减少对第三方 cookie 的依赖。</li><li>单一系统中的完整漏斗营销：在单一系统中对潜在客户和已知客户进行自助分段、受众管理和本地激活。</li><li>信任基础：通过获得专利的数据使用、标签、访问控制等管理合作伙伴数据和轮廓，以负责任的方式营销。请阅读以下用例指南以获取更多信息：现在可以获得潜在客户用例指南。请阅读潜在客户用例指南，以了解如何利用潜在客户用例吸引和获得新客户：<ul><li>[潜在用户](../../rtcdp/partner-data/prospecting.md)</li><li>[现场个性化](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[补充第一方轮廓](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[激活潜在客户受众](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

有关更多信息，请参阅[&#x200B; Real-Time CDP 概述](../../rtcdp/overview.md)。

## 基于属性的访问控制 {#abac}

基于属性的访问控制是 Adob&#x200B;&#x200B;e Experience Platform 的一项功能，它为注重隐私的品牌在管理用户访问权限方面提供了更大的灵活性。可以将架构字段和区段等单个对象分配给用户角色。通过此功能，您可以授予或撤销组织中特定Experience Platform用户访问单个对象的权限。

通过基于属性的访问控制，贵组织的管理员可以控制用户对所有Experience Platform工作流和资源中的敏感个人数据(SPD)、个人身份信息(PII)和其他自定义类型数据的访问。 管理员可以定义只能访问特定字段以及与这些字段对应的数据的用户角色。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 权限策略沙盒配置 | 新的[权限策略沙盒配置](../../access-control/abac/ui/policies.md)功能允许您根据您的需要和要求，对所有或选定数量的沙盒实施基于属性的访问控制策略。 |

{style="table-layout:auto"}

有关基于属性的访问控制的详细信息，请参阅[基于属性的访问控制概述](../../access-control/abac/overview.md)。有关基于属性的访问控制工作流程的综合指南，请阅读[基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md)。

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 同意分析和跟踪用例 | 了解如何使用[同意分析和跟踪文档](../../dashboards/insights-use-cases/consent-analysis.md)为Real-Time CDP数据的各种营销用例构建同意仪表板。 它详细介绍了如何创建具有适合您业务需求的属性的受众，然后通过使用 Adob&#x200B;&#x200B;e Experience Platform UI 中的预配置小组件来使用这些见解。它还提供了有关如何使用用户定义的仪表板功能构建您自己的自定义小组件的说明。本文档涵盖同意趋势和同意重叠用例。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 标记和事件转发 | [Experience Platform 标记（中国）](/help/tags/ui/publishing/premium-cdn.md) | 新的 Experience Platform 标记（中国）功能提高了网站可靠性和延迟，从而为在中国网站上部署标记的客户提供更快的响应时间。现在，客户在中国实施网站时可以使用标记库中的 JavaScript 代码。此功能也已添加到“统一配置协议” (UPP) 中，并允许在购买后自动进行产品部署。 |

{style="table-layout:auto"}

有关更多信息，请参阅[数据收藏集概述](../../tags/home.md)。

## 数据引入 {#data-ingestion}

Adobe Experience Platform 提供了一组丰富的功能，以摄取任何类型和任何延迟的数据。您可以使用批处理或流式 API、Adobe 构建的源、数据集成合作伙伴或 Adobe Experience Platform UI 摄取数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据摄取工作流程的更改 | 现在，包含大于指定数据类型的值的数据行（例如，作为整数数据类型传递的长数据）将会被拒绝，并会报告错误消息。以前，这些行会在没有警告的情况下遭到拒绝。 |

有关更多信息，请参阅[数据摄取概述](../../ingestion/home.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 支持过滤辅助身份标识 | 您现在可以使用“数据准备”功能来过滤来自 Adob&#x200B;&#x200B;e Analytics 的身份标识，例如 AAID 和 AACUSTOMID。如果被过滤掉，则这些身份标识将不会被纳入实时客户轮廓中。未经过滤的数据仍会被摄入到数据湖中。 |

{style="table-layout:auto"}

有关更多信息，请参阅[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能**{#destinations-new-updated-functionality}

- 您现在可以[将潜在客户受众](../../destinations/ui/activate-prospect-audiences.md)激活到云存储目标。
- 每个沙盒最多100个目标的常规[激活护栏](../../destinations/guardrails.md#general-activation-guardrails)已更新为&#x200B;_硬限制_。

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM 单个潜在客户轮廓]](https://github.com/adobe/xdm/pull/1758/files) | 使用此类引入来自数据供应商最顶层的客户获取用例的潜在客户配置文件。 请参阅[[!UICONTROL XDM个人潜在客户配置文件]](../../xdm/classes/prospect.md)文档，查看示例并了解更多信息。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 扩展([!UICONTROL Adobe Analytics ExperienceEvent完整扩展]) | [[!UICONTROL 上下文数据]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL 上下文数据]映射对象已添加到[!UICONTROL Adobe Analytics ExperienceEvent完整扩展]，以提供Adobe Analytics的上下文数据。 |
| 字段组 | 多种 | 多个字段已添加到[[!UICONTROL 扩充事件区段详细信息]](https://github.com/adobe/xdm/pull/1760/files)。 |

{style="table-layout:auto"}

若要了解更多信息，请阅读[XDM 系统概述](../../xdm/home.md)。

## 身份标识服务 {#identity-service}

Adobe Experience Platform 身份标识服务通过跨设备和系统桥接身份标识，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 身份标识图形限制的更改 | 到 9 月底，身份标识图形将会更改为每个图形 50 个身份标识，并且会摄取最新的身份标识。因此，届时将会根据摄取时间戳和身份标识类型删除最旧的身份标识，其中会首先删除 cookie 身份标识类型。如今，身份标识图形的每个图型均有 150 个身份标识的限制，一旦达到此限制，图形就不会再更新。如果您的生产沙盒包含以下内容，请联系您的客户代表请求更改身份标识类型： <ul><li>自定义命名空间，其中人员身份标识符（例如 CRM ID）会被配置为 cookie/设备身份标识类型。</li><li>自定义命名空间，其中 cookie/设备身份标识符会被配置为跨设备身份标识类型。</li></ul> Adobe 工程人员会手动处理这些请求。若要了解更多信息，请阅读[身份标识服务数据的护栏](../../identity-service/guardrails.md)。 |

有关更多信息，请参阅[身份标识服务概述](../../identity-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Experience Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 相似的受众（可用性有限） | 相似受众可以提供有关每个受众的智能见解，并利用基于机器学习的见解来识别和锁定营销活动的高价值客户。通过相似受众，您可以创建扩展受众，以与高绩效受众类似的目标客户或与之前转化的受众类似的目标客户为目标。有关相似受众的更多信息，请阅读[相似受众概述](../../segmentation/types/account-audiences.md)。 |

{style="table-layout:auto"}

有关更多信息，请参阅[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL SugarCRM] 全面可用 | [!DNL SugarCRM] 源当前可用。使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 源将您的 [!DNL SugarCRM] 账户中的数据带到 Experience Platform。有关详细信息，请参阅 [[!DNL SugarCRM]  概述](../../sources/connectors/crm/sugarcrm.md)。 |
| 支持 UI 中的源数据流按需摄取 | 现在，您可以在 UI 中按需为现有源数据流创建流运行。若要了解更多信息，请阅读有关[使用 UI 为源创建按需流运行](../../sources/tutorials/ui/on-demand-ingestion.md)的指南。 |
| 支持 Adobe Analytics 的新 `correlationID` 字段 | `_experience.decisioning.propositions.scopeDetails.correlationID` 字段现在在 Adob&#x200B;&#x200B;e Analytics 源连接器架构中可用。该字段用于支持 A4T 分类，并将会于 2023 年 9 月开始填充。 |

{style="table-layout:auto"}

有关更多信息，请参阅[源概述](../../sources/home.md)。
