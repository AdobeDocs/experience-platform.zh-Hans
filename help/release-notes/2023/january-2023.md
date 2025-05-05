---
title: Adobe Experience Platform 发行说明（2023 年 1 月）
description: Adobe Experience Platform 的 2023 年 1 月发行说明。
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2227'
ht-degree: 97%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 1 月 25 日**

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [数据收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 人工智能/机器学习服务 {#ai-ml}

人工智能和机器学习能够让营销分析师和从业人员利用客户体验用例中人工智能和机器学习的功能。这使得营销分析师可以使用业务级别的配置根据公司的需求设置预测，而无需数据科学专业知识。

### 归因人工智能

归因人工智能用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户历程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| HIPAA 准备就绪 | Healthcare Shield 客户现在可以在归因人工智能和某些其他基于 Experience Platform 的应用程序中接收、使用、维护或传输受保护的健康信息。Healthcare Shield 适用于 HIPAA 下的受保实体或业务伙伴的医疗保健客户。有关更多信息，请阅读有关 [HIPAA 和 Adobe 产品和服务](https://www.adobe.com/trust/compliance/hipaa-ready.html)的文档 |
| 编辑其他得分数据集列 | 现在，您可以在编辑现有模型时添加或删除其他分数数据集列（报告列）。这扩展了属性分数的灵活性，以便在创建模型后为您提供对其他维度的见解。请参阅[属性 UI 指南](../../intelligent-services/attribution-ai/user-guide.md)，了解更多信息。 |

{style="table-layout:auto"}

有关更多信息，请查看[人工智能/机器学习服务](../../intelligent-services/attribution-ai/overview.md)概述。

### 客户人工智能

面向 Real-Time Customer Data Platform 的客户人工智能用于生成自定义倾向分数，如单个轮廓大规模的流失率和转化率。这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| HIPAA 准备就绪 | Healthcare Shield 客户现在可以在面向 Real-Time Customer Data Platform 的客户人工智能和某些其他基于 Experience Platform 的应用程序中接收、使用、维护或传输受保护的健康信息。Healthcare Shield 适用于 HIPAA 下的受保实体或业务伙伴的医疗保健客户。有关更多信息，请参阅有关 [HIPAA 和 Adobe 产品和服务](https://www.adobe.com/trust/compliance/hipaa-ready.html)的文档 |

{style="table-layout:auto"}

有关更多信息，请查看[人工智能/机器学习服务](../../intelligent-services/customer-ai/overview.md)概述。

## Assurance {#assurance}

Adobe Assurance 可帮助您检查、校对、模拟和验证您在移动应用程序中收集数据或提供体验的方式。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 验证错误 | 为验证编辑器添加了新的增强功能。这些增强功能包括验证列、新的代码构建工具和改进的视图。 |

{style="table-layout:auto"}

有关 Assurance 的详细信息，请阅读 [Assurance 文档](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 新的主屏幕 | 数据收集 UI 的主页已更新，其中包含有用的入门信息和可提高生产力的链接。这包括：<ol><li>入门文档和推荐的工作流</li><li>最近的属性、规则和数据元素</li><li>热门扩展</li><li>具有快速安装功能的新扩展更新</li></ol> |
| 使用事件转发功能发送数据至[!DNL Google Ads] | 您现在可以使用 [[!DNL Google Ads Enhanced Conversions] API 扩展](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)进行事件转发，结合 [Google Oauth 2 机密](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，安全地实时将服务器端数据发送到 [!DNL Google Ads]。 |

{style="table-layout:auto"}

## 目标（2 月 2 日更新） {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud 受众连接](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL (Beta) Adobe Experience Cloud 受众]连接，共享从 Experience Platform 到各种 Experience Platform 解决方案的区段，如 Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target 或 Marketo。 |
| [Pega 轮廓连接](../../destinations/catalog/personalization/pega-profile.md) | 使用 Adobe Experience Platform 中的 [!DNL Pega Profile Connector] 创建与 [!DNL Amazon] S3 存储的实时出站连接，定期将轮廓数据从 Adobe Experience Platform 导出为CSV文件，并将其导出到您自己的 S3 存储桶中。在 [!DNL Pega Customer Decision Hub] 中，您可以安排数据作业从 S3 存储中导入该轮廓数据，以更新[!DNL Pega Customer Decision Hub]轮廓。 |
| [(Beta) Trade Desk CRM EU 连接](../../destinations/catalog/advertising/tradedesk-emails.md) | 随着 EUID (European Unified ID) 的发布，现在您在[目标目录](/help/destinations/catalog/overview.md)中会看到两个 [!DNL The Trade Desk - CRM] 目标。 <ul><li> 如果您在欧盟获取数据，请使用 **[!DNL The Trade Desk - CRM (EU)]** 目标。</li><li> 如果您在 APAC 或 NAMER 地区获取数据，请使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目标。 </li></ul> |

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 用于与流媒体目标集成的付费媒体同意策略增强功能 | 针对付费媒体激活用例，对[流媒体目标](/help/destinations/destination-types.md#streaming-destinations)的同意策略执行[&#128279;](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement)进行了增强。当轮廓不再符合同意策略时，Experience Platform 现在会主动将其策略退出通知给流媒体目标。<br> <b>注释</b>：此功能仅适用于&#x200B;**[!UICONTROL Privacy and Security Shield]**&#x200B;以及&#x200B;**[!UICONTROL Healthcare Shield]**&#x200B;的客户。 |
| 测试版云存储目标连接器的新分隔符选项 | 三个新的分隔符选项（冒号`:`、竖线、分号`;`）现在可用于新的测试版云存储目的地 - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)、[(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)、[(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)、[(Beta) 数据登陆区](/help/destinations/catalog/cloud-storage/data-landing-zone.md)、[(Beta) Google 云存储](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)、[(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md)。<br>了解基于文件的目标支持的[文件格式选项](/help/destinations/ui/batch-destinations-file-formatting-options.md)。 |
| [Destination SDK](/help/destinations/destination-sdk/overview.md) 中 [客户数据字段](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md)配置中提供的新可选参数 | `unique`：当您需要创建一个客户数据字段时，请使用此参数，该字段的值在用户组织设置的所有目标数据流中必须是唯一的。<br>例如，[[!UICONTROL 自定义个性化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters)中的&#x200B;**[!UICONTROL 集成别名]**&#x200B;字段必须是唯一的，这意味着到该目标的两个单独的数据流不能具有相同的该字段值。 |

**修复和增强功能** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>修复或增强</b></td>
        <td><b>描述</b></td>
    </tr>
    <tr>
        <td>更新了到基于文件的目标的导出行为 (PLAT-123316)</td>
        <td>我们修复了将数据文件导出到批处理目标时<a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">强制属性</a>的行为中的一个问题。<br>经过验证，以前输出文件中的每条记录都包含以下两者： <ol><li><code>mandatoryField</code> 列的非空值和</li><li>至少其中一个其他非必填字段具有非空值。</li></ol> 第二个条件已被删除。因此，您可能会在导出的数据文件中看到更多输出行，如下例所示：<br><b>推出 2023 年 1 月发布版本之前的示例行为</b><br>必填字段：<code>emailAddress</code><br><b>输入要激活的数据</b><br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br><b>激活输出</b><br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br><b>推出 2023 年 1 月发布版本后的示例行为</b><br><b>激活输出</b><br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>所需映射和重复映射的 UI 和 API 验证 (PLAT-123316)</td>
        <td>当激活目的地工作流中的<a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">映射字段</a>时，UI 和 API 中的验证现在强制如下：<ul><li><b>所需映射</b>：如果目标开发人员使用所需映射（例如，<a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a> 目标）设置了目标，则用户在向目标激活数据时需要添加这些所需映射。 </li><li><b>重复的映射</b>：在激活工作流的映射步骤中，您可以在源字段中添加重复值，但不能在目标字段中添加重复值。请参阅下表，了解允许和禁止的映射组合的示例。 <br><table><thead><tr><th>允许/禁止</th><th>源字段</th><th>目标字段</th></tr></thead><tbody><tr><td>允许</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>emailalias2</li></ul></td></tr><tr><td>禁止</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 架构树显示名称改进 | 以前，字段名称显示在 UI 中，但现在，架构画布上架构字段的显示名称更易于阅读。 |

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 转化]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 用于跟踪货币兑换等兑换数据的类。 |
| 字段组 | [[!UICONTROL 货币兑换率详情]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | [!UICONTROL 转化]类的字段组，捕获与货币转化相关的其他详细信息。 |
| 字段组 | [[!UICONTROL 带有元数据的同意策略评估结果图]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | 捕获多个同意策略评估结果的详细信息，包括有关同意策略入口和存在的元数据信息。 |

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL Advertising 详情信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 该 `ID` 字段已重命名为`name`，之前的 `name` 字段现在是 `friendlyName`。 |
| 数据类型 | [[!UICONTROL 决策提案详情]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 添加了一个捕获选择策略细节的 `selectionStrategy` 字段。 |
| 字段组 | [[!UICONTROL 体验事件 - 命题互动]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 该字段组现在与[!UICONTROL 历程步骤事件]类兼容。 |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 该`ID`字段已重命名为 `name`。 |
| 数据类型 | [[!UICONTROL 媒体信息]](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/media.schema.json) | 已将模式中的更改还原为视频区段属性。 |
| 数据类型 | [[!UICONTROL Qoe 数据详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 删除了 `droppedFrameCount` 字段。 |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 将 `isAuthorized` 字段重命名为 `authorized`，并将其 `type` 更新为以前为布尔值的字符串。 |
| 数据类型 | [[!UICONTROL 运送]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 添加了几个新字段：`shipDate`、`trackingNumber` 和 `trackingURL`。 |
| 字段组 | [[!UICONTROL AJO 实体字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 添加了几个新字段：`journeyNodeID`、`journeyNodeName` 和 `journeyModeType`。 |
| 字段组 | [[!UICONTROL 消费者体验事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 该字段组现在也与[!UICONTROL 摘要指标]类兼容。 |
| 字段组 | [[!UICONTROL 产品触发因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 该`productTriggers`字段现在嵌套在 `weather` 对象中。 |
| 字段组 | [[!UICONTROL 相对触发因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 该`relativeTriggers`字段现在嵌套在 `weather` 对象中。 |
| 字段组 | [[!UICONTROL 严重的触发因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 该`severeTriggers`字段现在嵌套在 `weather` 对象中。 |
| 字段组 | [[!UICONTROL 天气触发因素]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 该`weatherTriggers`字段现在嵌套在 `weather` 对象中。 |
| 字段组 | [[!UICONTROL XDM 相关企业账户]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 目前，字段组已稳定。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**即将弃用**{#deprecation}

为了消除区段成员关系生命周期中的冗余，在 2023 年 3 月低，[区段成员关系图](../../xdm/field-groups/profile/segmentation.md)中将会弃用 `Existing` 状态。后续公告将会包括确切的弃用日期。

启用后，一个区段中合格的轮廓将表示为 `Realized`，不合格的配置将继续表示为 `Exited`。这会为具有 `Active` 和 `Expired` 区段状态的基于文件的目标带来对等性。

如果您正在使用[企业目标](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis, Azure Event Hubs, HTTP API)，并且可能已根据 `Existing` 状态将下游流程自动化，则此更改可能会对您产生影响。如果您属于这种情况，请检查您的下游集成。如果您有兴趣在一定时间后识别新获得资格的轮廓，请考虑在您的区段成员关系图中使用 `Realized` 状态和 `lastQualificationTime` 的组合。有关更多信息，请与您的 Adobe 代表联系。

要详细了解实时客户轮廓，包括使用轮廓数据的教程和最佳实践，请首先阅读[实时客户轮廓概述](../../profile/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 在区段生成器中批量导入值 | 区段生成器现在支持通过上传 CSV 或 TSV 文件，或通过手动插入逗号分隔值来导入多个值。更多信息可以在[区段生成器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas)中找到。 |
| 外部受众成员关系过期 | 默认情况下，外部受众成员关系将会保留 30 天。若要延长保留时间，请在提取受众数据期间使用 `validUntil` 字段。 |
| Experience Platform生成的区段成员资格过期 | 基于 `lastQualificationTime` 字段，任何处于 `Exited` 状态超过 30 天的区段成员关系都会被删除。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| 允许用户访问云存储源的子文件夹 | 现在，您可以在创建新帐户时定义对云存储源的特定子文件夹的访问权限。创建后，用户将只能访问获得许可的子文件夹中的数据。此功能可用于以下云存储源：[Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md)、[Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md)、[Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md) 和 [SFTP](../../sources/connectors/cloud-storage/sftp.md)。 |
| [!DNL SugarCRM] Beta 版本的可用性 | [!DNL SugarCRM] 源当前在 Beta 中可用。使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 源将您的 [!DNL SugarCRM] 账户中的数据带到 Experience Platform。有关详细信息，请参阅 [[!DNL SugarCRM]  概述](../../sources/connectors/crm/sugarcrm.md)。 |
