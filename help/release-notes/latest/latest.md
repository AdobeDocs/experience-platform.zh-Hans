---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年8月版发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4211a19bfd511c495d9efac898467230678aeb96
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 36%

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
- [Experience Data Model (XDM)](#xdm)
- [身份服务](#identity-service)
- [Segmentation Service](#segmentation)
- [源](#sources)

## Real-Time Customer Data Platform {#rtcdp}

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户配置文件。

[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户配置文件。然后，根据这些配置文件构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 智能重新参与用例指南 | 此 [智能重新参与](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 用例指南提供了有关如何重新吸引已放弃转化的客户的详细信息，这些客户随后将以智能、负责的方式完成转化。 本指南使用以下示例历程重新吸引客户： <ul><li>重新参与历程 — 定位已放弃产品浏览的客户。</li><li>放弃的购物车历程 — 定位已将产品放入购物车但尚未完成购买的客户。</li><li>订单确认历程 — 重点关注产品购买</li></ul> 请使用底部的详细反馈选项链接 [智能重新参与用例指南](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 以提供反馈。 |
| 合作伙伴数据支持 | 在Real-Time CDP中利用合作伙伴提供的潜在客户配置文件和合作伙伴ID执行漏斗上层营销，以接触新客户并丰富您的第一方数据： <ul><li>客户获取和可寻址性：利用所选数据合作伙伴提供的无Cookie标识符和经过哈希处理的PII，吸引全新客户并减少第三方Cookie依赖性。</li><li>在单个系统中实现完全的漏斗营销：在单个系统中为潜在客户和已知客户提供自助式分段、受众策划和本机激活。</li><li>信任基础：通过专利数据使用、标签、访问控制等方式，负责任地管理合作伙伴数据和配置文件，并将其推向市场。 有关更多信息，请阅读以下用例指南：现在提供了潜在客户用例指南。 阅读潜在客户用例指南，了解如何通过潜在客户用例吸引和赢取新客户：<ul><li>[潜在客户](../../rtcdp/partner-data/prospecting.md)</li><li>[现场个性化](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[补充第一方配置文件](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[激活目标客户受众](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

欲知更多信息，请阅读 [Real-Time CDP概述](../../rtcdp/overview.md).

## 基于属性的访问控制 {#abac}

基于属性的访问控制是Adobe Experience Platform的一项功能，它使注重隐私的品牌在管理用户访问方面拥有更大的灵活性。 可以将各个对象（如方案字段和区段）分配给用户角色。 通过此功能，您可以授予或撤销组织中特定Platform用户访问单个对象的权限。

通过基于属性的访问控制，贵组织的管理员可以控制用户对所有平台工作流和资源中敏感个人数据(SPD)、个人身份信息(PII)和其他自定义类型数据的访问。 管理员可以定义用户角色，这些用户角色只能访问特定字段以及与这些字段对应的数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 权限策略沙盒配置 | 新 [权限策略沙盒配置](../../access-control/abac/ui/policies.md) 功能允许您根据需求和要求，对所有或所选数量的沙盒实施基于属性的访问控制策略。 |

{style="table-layout:auto"}

有关基于属性的访问控制的详细信息，请参见 [基于属性的访问控制概述](../../access-control/abac/overview.md). 有关基于属性的访问控制工作流的全面指南，请参阅 [基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md).

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 同意分析和跟踪用例 | 了解如何通过为Real-Time CDP数据的各种营销用例构建同意仪表板 [同意分析和跟踪文档](../../dashboards/insights-use-cases/consent-analysis.md). 它详细介绍如何根据您的业务需求创建具有适当属性的受众，然后通过在Adobe Experience Platform UI中使用预配置的构件来使用洞察。 它还提供了有关如何使用用户定义的功能板构建您自己的自定义小组件的说明。 本文档涵盖同意趋势和同意重叠用例。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 标记和事件转发 | [Experience Platform标记（中国）](/help/tags/ui/publishing/premium-cdn.md) | 新的Experience Platform标记（中国）功能提高了网站的可靠性和延迟，从而缩短在中国网站上部署标记的客户响应时间。 现在，客户在中国实施网站时，可以利用标记库中的JavaScript代码。 此功能也已添加到统一配置协议(UPP)，允许产品在购买后自动部署。 |

{style="table-layout:auto"}

欲知更多信息，请阅读 [数据集合概述](../../tags/home.md).

## 数据引入 {#data-ingestion}

Adobe Experience Platform 提供了一组丰富的功能，以摄取任何类型和任何延迟的数据。您可以使用批处理或流式 API、Adobe 构建的源、数据集成合作伙伴或 Adobe Experience Platform UI 摄取数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据摄取工作流的更改 | 现在，包含的值大于指定数据类型（例如，以integer数据类型传递的长数据）的数据行将被拒绝，并且将会报告错误消息。 以前，这些行在没有警告的情况下被拒绝。 |

欲知更多信息，请阅读 [数据摄取概述](../../ingestion/home.md).

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 支持过滤次要身份 | 您现在可以使用数据准备过滤来自Adobe Analytics的身份，例如AAID和AACUSTOMID。 如果过滤掉，这些身份不会引入Real-Time Customer Profile。 未过滤的数据将继续引入数据湖。 |

{style="table-layout:auto"}

欲知更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM 单个潜在客户配置文件]](https://github.com/adobe/xdm/pull/1758/files) | 使用此类引入从数据供应商的漏斗顶部客户获取用例获得的潜在客户配置文件。请参阅 [[!UICONTROL XDM单个潜在客户配置文件]](../../xdm/classes/prospect.md) 文档，以查看示例并了解更多信息。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 扩展名([!UICONTROL Adobe Analytics ExperienceEvent完整扩展]) | [[!UICONTROL 上下文数据]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL 上下文数据] 映射对象已添加到 [!UICONTROL Adobe Analytics ExperienceEvent完整扩展] 为Adobe Analytics提供上下文数据。 |
| 字段组 | 多种 | 多个字段已添加到 [[!UICONTROL 扩充事件区段详细信息]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

欲知更多信息，请阅读 [XDM系统概述](../../xdm/home.md).

## 身份服务 {#identity-service}

Adobe Experience Platform 身份服务通过跨设备和系统桥接身份，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 更改了身份图限制 | 到9月底，身份图将更改为每个图50个身份，并将摄取最新身份。 因此，将根据摄取时间戳和身份类型删除最早的身份，并首先删除Cookie身份类型。 现在，身份图具有每个图150个身份的限制，一旦达到此限制，图形将不再更新。 如果您的生产沙盒包含： <ul><li>将人员标识符（如CRM ID）配置为Cookie/设备标识类型的自定义命名空间。</li><li>将cookie/设备标识符配置为跨设备标识类型的自定义命名空间。</li></ul> Adobe工程部门将手动处理这些请求。 欲知更多信息，请参阅 [Identity Service数据的护栏](../../identity-service/guardrails.md). |

欲知更多信息，请阅读 [Identity服务概述](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 相似受众（限量发布） | 相似受众可针对每位受众提供智能见解，利用机器学习型见解通过营销活动识别和定位高价值客户。 通过相似受众，您可以创建扩展的受众以定位与高性能受众类似的客户或以前转换的受众类似的客户。 有关相似受众的更多信息，请阅读 [相似受众概述](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

欲知更多信息，请阅读 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 正式发布 [!DNL SugarCRM] | [!DNL SugarCRM] 现已提供源。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 源将您的 [!DNL SugarCRM] 账户中的数据带到 Experience Platform。有关详细信息，请参阅 [[!DNL SugarCRM]  概述](../../sources/connectors/crm/sugarcrm.md)。 |
| 在UI中支持按需引入源数据流 | 您现在可以在UI中根据需要为现有源数据流创建流运行。 有关详细信息，请阅读上的指南 [使用UI为来源创建按需流运行](../../sources/tutorials/ui/on-demand-ingestion.md). |
| 支持新的 `correlationID` Adobe Analytics的字段 | 此 `_experience.decisioning.propositions.scopeDetails.correlationID` 字段现已在Adobe Analytics源连接器架构中可用。 此字段用于支持A4T分类，并将从2023年9月开始填充。 |

{style="table-layout:auto"}

欲知更多信息，请阅读 [源概述](../../sources/home.md).
