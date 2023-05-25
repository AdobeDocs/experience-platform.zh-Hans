---
title: Adobe Experience Platform发行说明2023年4月
description: Adobe Experience Platform 2023年4月版发行说明。
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

>[!IMPORTANT]
>
>自2023年5月15日起， `Existing` 为了消除区段成员资格生命周期中的冗余，区段成员资格映射中的状态将被弃用。 进行此更改后，区段中符合条件的用户档案将表示为 `Realized` 并且不符合资格的用户档案将继续显示为 `Exited`. 有关此更改的详细信息，请阅读 [“分段服务”部分](#segmentation).

**发布日期：2023 年 4 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过该功能板查看有关贵组织数据的重要见解，如在每日快照期间捕获的数据。

**新增或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的仪表板 | 您现在可以 **筛选历史数据** 使用最近的数据或自定义分析时段。 请参阅 [用户定义的功能板指南](../../dashboards/user-defined-dashboards.md#filter-historical-data) 了解更多信息。<br>您现在还可以 **复制现有构件**. 通过自定义副本并编辑其属性，您可以避免在创建新的唯一构件时从头重新启动。 阅读 [构件复制指南](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) 了解更多信息。 |

{style="table-layout:auto"}

有关仪表板的更多信息，包括如何授予访问权限和创建自定义小组件，请从阅读 [功能板概述](../../dashboards/home.md).

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证数据到体验数据模型(XDM)以及从中转换和验证数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 更新了非生产沙盒中Adobe Analytics的回填时段 | 非生产沙盒中Adobe Analytics的回填期限已缩短为三个月。 生产沙盒的回填在13个月后保持不变。 此更改仅适用于新流，不会影响现有流。 有关详细信息，请阅读 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 用于将FPID字符串转换为ECID的新映射器函数 | 使用 `fpid_to_ecid` 函数将FPID字符串转换为ECID，以用于Experience Platform和Experience Cloud应用程序。 有关详细信息，请阅读 [数据准备函数指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| 数据流的IP地址模糊处理 | 您现在可以在中定义部分或完整数据流级别的IP模糊处理选项 [数据流配置Ui](../../edge/datastreams/configure.md). <br><br>数据流级别的IP模糊处理设置优先于Adobe Target和Audience Manager中配置的任何IP模糊处理。 <br><br>发送到Adobe Analytics的数据不受数据流级别的影响 [!UICONTROL IP模糊处理] 设置。 Adobe Analytics当前接收未经模糊处理的IP地址。 要让Analytics接收模糊处理的IP地址，您必须在Adobe Analytics中单独配置IP模糊处理。 此行为将在未来版本中更新。<br><br> 有关IP模糊处理的更多详细信息以及如何配置它的说明，请参阅 [数据流配置文档](../../edge/datastreams/configure.md#advanced-options). |
| [数据流配置覆盖](../../edge/datastreams/overrides.md) | 您现在可以为数据流定义其他配置选项，您可以使用这些选项覆盖特定设置，例如事件数据集、Target属性令牌、ID同步容器和Analytics报表包。 <br><br>覆盖数据流配置是一个两步过程： <ol><li>首先，您必须在以下位置定义数据流配置覆盖 [数据流配置页面](../../edge/datastreams/configure.md).</li><li>然后，您必须通过Web SDK命令或使用Web SDK将覆盖发送到Edge Network [标记扩展](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT密码 | 此 [OAuth JWT密码](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 允许客户使用Adobe和Google服务令牌在事件转发中支持服务器到服务器交互。 |
| [!DNL Pinterest Conversions API] 扩展 | 此 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件转发扩展允许您利用Adobe Experience Platform Edge Network中捕获的数据并将其发送至 [!DNL Pinterest] 以服务器端事件的形式使用 [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新目标** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 连接](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用SalesforceMarketing Cloud客户参与（以前称为Pardot）目标来捕获、跟踪、评分和评级潜在客户。 将此目标用于涉及多个部门和决策者（需要较长的销售和决策周期）的B2B用例。 |

{style="table-layout:auto"}

**新增或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 数据流监控 [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目标 | <p> 您现在可以看到以下项的激活量度 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md)， [自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 和 [使用属性进行自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 连接。 </p> <p>![Adobe Commerce图像](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce量度"){width="100" zoomable="yes"}</p>  参见 [监视目标工作区中的数据流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 了解更多详细信息。 |
| 新 **[!UICONTROL 将区段ID附加到区段名称]** 的字段 [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目标 | <p>现在，您可以在中保留区段名称 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 包括来自Experience Platform的区段ID，如下所示： `Segment Name (Segment ID)`.</p><p>![附加区段ID图像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "将新区段ID附加到区段名称字段 "){width="100" zoomable="yes"}</p> |
| 计划的受众回填 | <p>对于 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 目标，计划在首次将区段映射到目标连接后24-48小时内激活到目标的受众回填。 此更新是为了响应Google等待24小时直到摄取数据的策略，并将提高Real-time CDP与之间的匹配率 [!DNL Google Display & Video 360].</p> <p>请注意，这是只适用于此目标的后端配置，与UI中任何客户可配置的计划选项无关。</p> |

{style="table-layout:auto"}

**修复和增强功能** {#destinations-fixes-and-enhancements}

- 我们已经修复了中的一个问题 **身份已排除** 基于文件的目标导出的报表量度。 客户正按预期从激活的导出中接收所有导出的ID。 但是， **身份已排除** 由于错误地计数了绝不应该导出的身份，UI中的报表量度错误地显示了大量被排除的身份。 (PLAT-149774)
- 我们已经修复了中的一个问题 **计划** 激活工作流的步骤。 对于需要映射ID的目标，客户无法为添加到现有目标连接的区段添加映射ID。 (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 显示名称切换 | 架构编辑器现在提供切换功能，以便在原始字段名称和更易于用户识别的显示名称之间更改。<br>![突出显示显示名称切换的架构编辑器。](../../xdm/images/ui/resources/schemas/display-name-toggle.png "架构编辑器显示名称切换"){width="100" zoomable="yes"}<br>这种灵活性可提高字段可发现性和架构的编辑。 标准字段组的显示名称由系统生成，但也可以根据需要通过UI进行自定义。 请阅读 [显示名称切换文档](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) 了解更多信息。 |

{style="table-layout:auto"}

**新XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 架构 | [[!UICONTROL Adobe Target分类字段]](https://github.com/adobe/xdm/pull/1719/files) | 目标分类数据集的新XDM架构包含一组用于分类Target活动和体验的元数据字段。 |

{style="table-layout:auto"}

**更新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL Adobe统一配置文件服务帐户合并扩展]](https://github.com/adobe/xdm/pull/1696/files) | 为Real-time Customer Profile添加了account-extension字段组，该字段组允许用户在帐户合并中添加区段成员资格。 |
| 架构 | [[!UICONTROL 计算属性系统架构]](https://github.com/adobe/xdm/pull/1696/files) | 实时客户档案使用的计算属性字段组已更新为系统只读全局架构。 |
| 字段组 | 多个 | 添加了多个事件作为字段 [[!UICONTROL 时间序列架构]](https://github.com/adobe/xdm/pull/1718/files). |
| 字段组 | 个人资料忠诚度详细信息 | [修复了标题](https://github.com/adobe/xdm/pull/1717/files) 对象 `xdm:upgradeDate` 从“计划名称”更改为“升级日期”。 |
| 字段组 | 多个 | 中的多个字段 [[!UICONTROL 决策项目]](https://github.com/adobe/xdm/pull/1714/files) 已更新以删除双重嵌套层次结构。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md).

## Real-Time Customer Data Platform

Real-time Customer Data Platform ()构建于Experience Platform之上[!DNL Real-Time CDP])帮助公司整合已知和未知数据，在整个客户历程中通过智能决策激活客户档案。 [!DNL Real-Time CDP] 可合并多个企业数据源以实时创建客户配置文件。 根据这些配置文件构建的区段随后可以发送到下游目标，以便在所有渠道和设备中提供一对一的个性化客户体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的Real-Time CDP主页 | 此 [Real-Time CDP主页](https://experience.adobe.com) 已得到增强，其外观更新并提高了性能。 主页现在具有权限感知功能，并且会显示与您有权访问的功能相关的构件。 有关详细信息，请阅读 [Real-Time CDP主页功能板概述](../../rtcdp/home-page-dashboards.md). |
| 自我识别调查 | 自我识别调查是在Adobe Experience Platform UI主页中提供的简短调查问卷。 使用自我识别调查构建您的Experience Platform个人资料，并根据您的选择接收量身定制的指南。 有关详细信息，请阅读 [自我识别调查概述](../../landing/self-identification.md). |

有关的详细信息 [!DNL Real-Time CDP]，请参见 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md).

## 实时客户资料 {#profile}

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 用户档案允许您将客户数据整合到一个统一的视图中，并提供每个客户互动的可操作、带时间戳的帐户。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 假名配置文件数据到期 | 假名配置文件数据到期现已正式可用！ 此版本将在启用后不断从Experience Platform实例中删除过时的假名配置文件。 要了解有关此功能及假名配置文件的更多信息，请阅读 [假名配置文件数据过期指南](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 区段成员资格分布图 | 作为先前于2023年2月15日宣布的后续行动， `Existing` 为了消除区段成员资格生命周期中的冗余，区段成员资格映射中的状态将被弃用。 进行此更改后，区段中符合条件的用户档案将表示为 `Realized` 并且不符合资格的用户档案将继续显示为 `Exited`.<br/><br/> 此更改可能会影响您，如果您使用 [企业目标](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure事件中心、HTTP API)，并且可能已基于以下路径部署了自动化下游进程 `Existing` 状态。 如果您属于这种情况，请检查您的下游集成。 如果您想在某个特定时间后确定新符合条件的用户档案，请考虑结合使用 `Realized` 状态和 `lastQualificationTime` 区段会员资格映射中的区段名称。 有关更多信息，请联系您的Adobe代表。 |

{style="table-layout:auto"}

有关的详细信息 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| API支持筛选Salesforce CRM源的行级数据。 | 使用逻辑运算符和比较运算符筛选Salesforce CRM源的行级数据。 阅读以下内容中的指南： [使用API筛选源的数据](../../sources/tutorials/api/filter.md) 了解更多信息。 |
| Shopify Streaming的Beta版本 | 此 [Shopify流源](../../sources/connectors/ecommerce/shopify-streaming.md) 现已推出测试版。 使用Shopify流源将数据从您的Shopify合作伙伴帐户流式传输到Experience Platform。 |
| OneTrust集成的正式发布 | 此 [OneTrust集成源](../../sources/connectors/consent-and-preferences/onetrust.md) 现在为GA。 使用OneTrust集成源将OneTrust集成帐户中的同意和偏好设置数据传送到Experience Platform。 |
| oracle服务云的正式发布 | 此 [oracle服务云源](../../sources/connectors/customer-success/oracle-service-cloud.md) 现在为GA。 使用Oracle服务云源将Oracle服务云数据引入到Experience Platform。 |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).