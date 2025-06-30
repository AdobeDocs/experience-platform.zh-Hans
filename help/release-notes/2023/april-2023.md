---
title: Adobe Experience Platform 发行说明（2023 年 4 月）
description: Adobe Experience Platform 的 2023 年 4 月发行说明。
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 96%

---

# Adobe Experience Platform 发行说明

>[!IMPORTANT]
>
>自 2023 年 5 月 15 日起，将从区段成员关系图中弃用 `Existing` 状态以消除区段成员关系生命周期中的冗余。经过此更改后，在某个区段中符合条件的轮廓将表示为 `Realized`，不符合条件的配置将继续表示为 `Exited`。有关此更改的更多详细信息，请阅读[分段服务](#segmentation)部分。

**发布日期：2023 年 4 月 26 日**

Adobe Experience Platform 中现有功能的更新：

- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的仪表板 | 现在可从“见解”小组件中&#x200B;**筛选历史数据**，并使用最近的数据或自定义的分析周期。有关详细信息，请参阅[用户定义的仪表板指南](../../dashboards/standard-dashboards.md#filter-historical-data)。<br>现在还可&#x200B;**复制现有小组件**。通过自定义副本并编辑其属性，在创建新的独特小组件时可避免从头开始创建。请阅读[小组件复制指南](../../dashboards/standard-dashboards.md#duplicate-a-widget)以了解详情。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 对非生产沙盒中 Adobe Analytics 回填期的更新 | 非生产沙盒中 Adobe Analytics 的回填期已缩短至三个月。生产沙盒的回填保持在 13 个月不变。此更改仅适用于新流，不影响现有流。有关详细信息，请阅读 [Adobe Analytics 概述](../../sources/connectors/adobe-applications/analytics.md)。 |
| 新的映射器函数可将 FPID 字符串转换为 ECID | 使用 `fpid_to_ecid` 函数将 FPID 字符串转换为 ECID，以在 Experience Platform 和 Experience Cloud 应用程序中使用。有关详细信息，请阅读[数据准备函数指南](../../data-prep/functions.md)。 |

{style="table-layout:auto"}

有关数据准备的详细信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 对数据流进行 IP 地址模糊处理 | 现在可在[数据流配置 UI](../../datastreams/configure.md) 中定义部分或全部数据流级别 IP 模糊处理选项。<br><br>数据流级别 IP 模糊处理设置优先于任何在 Adobe Target 和 Audience Manager 中的任何 IP 模糊处理功能。<br><br>数据流级别 [!UICONTROL IP 模糊处理]设置不影响发送到 Adobe Analytics 的数据。Adobe Analytics 当前接收未经模糊处理的 IP 地址。要让 Analytics 接收经过模糊处理的 IP 地址，您必须在 Adobe Analytics 中单独配置 IP 模糊处理。将在后续版本中更新此行为。<br><br>有关 IP 模糊处理的更多详细信息以及有关如何配置它的说明，请参阅[数据流配置文档](../../datastreams/configure.md#advanced-options)。 |
| [数据流配置覆盖](../../datastreams/overrides.md) | 您现在可以为数据流定义其他配置选项，这些选项可用于覆盖特定设置，例如事件数据集、Target 属性令牌、ID 同步容器和 Analytics 报表包。<br><br>覆盖数据流配置是一个两步过程： <ol><li>首先，您必须在[数据流配置页面](../../datastreams/configure.md)中定义数据流配置覆盖。</li><li>然后，您必须通过 Web SDK 命令或使用 Web SDK [标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)将这些覆盖发送到 Edge Network。</li></ol> |
| OAuth JWT 机密 | 通过 [OAuth JWT 机密](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=zh-Hans)，客户可以使用 Adobe 和 Google 服务令牌在事件转发中支持服务器到服务器的交互。 |
| [!DNL Pinterest Conversions API] 扩展 | 通过 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=zh-Hans) 事件转发扩展，可利用在 Adobe Experience Platform Edge Network 中捕获的数据，并使用 [!DNL Pinterest Conversions API] 以服务器端事件的形式将数据发送到 [!DNL Pinterest]。 |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 连接](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用 Salesforce Marketing Cloud Account Engagement（以前称为 Pardot）目标捕获、跟踪潜在客户、为其评分和分类。将此目标用于涉及多个部门和决策者且需要较长销售和决策周期的 B2B 用例。 |

{style="table-layout:auto"}

**新增或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目标的数据流监控 | <p> 您现在可以看到 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md)、[自定义个性化](../../destinations/catalog/personalization/custom-personalization.md)和[带属性自定义个性化](../../destinations/catalog/personalization/custom-personalization.md)连接的激活指标。 </p> <p>![Adobe Commerce 图像](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce 指标"){width="100" zoomable="yes"}</p>  请参阅[在“目标”工作区中监视数据流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace)以了解详情。 |
| [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目标新增&#x200B;**[!UICONTROL 将区段 ID 附加到区段名称]**&#x200B;字段 | <p>您现在可以让 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 中的区段名称包含来自 Experience Platform 的区段 ID，例如：`Segment Name (Segment ID)`。</p><p>![附加区段 ID 图像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "新增的“将区段 ID 附加到区段名称”字段"){width="100" zoomable="yes"}</p> |
| 安排受众回填 | <p>对于 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 目标，安排在区段首次映射到目标连接 24 至 48 小时后激活对目标的受众回填。此更新是为了响应Google的策略而进行的，该策略等待24小时直到摄取数据，此更新将提高Real-Time CDP与[!DNL Google Display & Video 360]之间的匹配率。</p> <p>请注意，这是仅适用于该目标的后端配置，并与 UI 中任何客户可配置的计划选项无关。</p> |

{style="table-layout:auto"}

**修复和增强功能** {#destinations-fixes-and-enhancements}

- 我们已经修复了基于文件的目标导出中&#x200B;**身份标识排除**&#x200B;报告指标中的一个问题。客户按预期从激活的导出中接收到所有导出的 ID。但是，由于错误地计算了不应导出的身份标识，UI 中的&#x200B;**身份标识排除**&#x200B;报告指标错误地显示了大量排除的身份标识。(PLAT-149774)
- 我们已经修复了激活工作流程中的&#x200B;**计划**&#x200B;步骤中的一个问题。对于需要映射 ID 的目标，客户无法为添加到现有目标连接的区段添加映射 ID。(PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 显示名称切换 | 架构编辑器现在提供了一个切换功能，可以在原始字段名称和更易于理解的显示名称之间进行更改。<br>![显示名称切换高亮显示的架构编辑器。](../../xdm/images/ui/resources/schemas/display-name-toggle.png "架构编辑器显示名称切换"){width="100" zoomable="yes"}<br>这种灵活性可以提高字段发现能力和架构编辑功能。标准字段组的显示名称是由系统生成的，但如果需要，也可以通过 UI 进行自定义。请阅读[显示名称切换文档](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#display-name-toggle)，了解详情。 |

{style="table-layout:auto"}

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 架构 | [[!UICONTROL Adobe Target 分类字段]](https://github.com/adobe/xdm/pull/1719/files) | Target 分类数据集的新 XDM 架构包含一组元数据字段，用于对 Target 活动和体验进行分类。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL Adobe 联合轮廓服务帐户合并扩展]](https://github.com/adobe/xdm/pull/1696/files) | 为实时客户轮廓添加了帐户扩展字段组，使用户能够在帐户合并中添加区段成员资格。 |
| 架构 | [[!UICONTROL 计算属性系统架构]](https://github.com/adobe/xdm/pull/1696/files) | 实时客户轮廓使用的计算属性字段组已更新为系统只读全局架构。 |
| 字段组 | 多种 | 添加了几个事件作为[[!UICONTROL 时间序列架构]](https://github.com/adobe/xdm/pull/1718/files)的字段。 |
| 字段组 | 轮廓忠诚度详细信息 | [将 `xdm:upgradeDate` 的标题](https://github.com/adobe/xdm/pull/1717/files)从“程序名称”改为“升级日期”。 |
| 字段组 | 多种 | [[!UICONTROL 决策项]](https://github.com/adobe/xdm/pull/1714/files)中的几个字段已更新，以删除双重嵌套层级。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请阅读[XDM系统概述](../../xdm/home.md)。

## Real-Time Customer Data Platform

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户轮廓。[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户轮廓。然后，根据这些轮廓构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强型 Real-Time CDP 主页 | [Real-Time CDP 主页](https://experience.adobe.com)的外观焕然一新，并且性能得到了增强。主页现在具有权限感知功能，并会显示与您有权访问的功能相关的小组件。有关详细信息，请阅读 [Real-Time CDP 主页仪表板概述](../../rtcdp/home-page-dashboards.md)。 |
| 自我认同调查 | 自我认同调查是 Adobe Experience Platform UI 主页中提供的简短调查问卷。使用自我认同调查来构建您的 Experience Platform 个人轮廓，并根据您的选择接收量身定制的指南。有关详细信息，请阅读[自我认同调查概述](../../landing/self-identification.md)。 |

有关 [!DNL Real-Time CDP] 的详细信息，请参阅 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 假名轮廓数据到期 | 假名轮廓数据到期功能现已普遍可用！启用后，此版本将会持续从您的 Experience Platform 实例中删除过时的假名轮廓。要详细了解此功能和假名轮廓，请阅读[假名轮廓数据有效期限指南](../../profile/pseudonymous-profiles.md)。 |

{style="table-layout:auto"}

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 区段成员关系图 | 继 2 月的上一次公告之后，自 2023 年 5 月 15 日起，区段成员关系图中将会弃用 `Existing` 状态，以消除区段成员关系生命周期中的冗余。经过此更改后，在某个区段中符合条件的轮廓将表示为 `Realized`，不符合条件的配置将继续表示为 `Exited`。<br/><br/>如果您正在使用[企业目标](../../destinations/destination-types.md#advanced-enterprise-destinations)（Amazon Kinesis、Azure Event Hubs、HTTP API），并且可能已根据 `Existing` 状态将下游流程自动化，则此更改可能会对您产生影响。如果您属于这种情况，请检查您的下游集成。如果您有兴趣在一定时间后识别新获得资格的轮廓，请考虑在您的区段成员关系图中使用 `Realized` 状态和 `lastQualificationTime` 的组合。有关更多信息，请与您的 Adobe 代表联系。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| API 支持为 Salesforce CRM 源筛选行级数据。 | 使用逻辑和比较运算符来过滤 Salesforce CRM 源的行级数据。有关更多信息，请阅读[使用 API 过滤源数据](../../sources/tutorials/api/filter.md)的指南。 |
| Shopify Streaming 的 Beta 版可用性 | [Shopify Streaming 源](../../sources/connectors/ecommerce/shopify-streaming.md)现已推出 Beta 版。使用 Shopify Streaming 源将数据从您的 Shopify 合作伙伴帐户流式传输到 Experience Platform。 |
| OneTrust Integration 全面可用 | [OneTrust Integration 源](../../sources/connectors/consent-and-preferences/onetrust.md)现在全面可用。使用 OneTrust Integration 源将同意和偏好设置数据从您的 OneTrust Integration 帐户添加到 Experience Platform。 |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
