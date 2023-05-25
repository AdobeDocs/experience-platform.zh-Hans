---
title: Adobe Experience Platform发行说明2023年1月
description: Adobe Experience Platform 2023年1月版发行说明。
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 1 月 25 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [数据收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [体验数据模型(XDM)](#xdm)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## 人工智能/机器学习服务 {#ai-ml}

人工智能和机器学习服务使营销分析师和从业人员能够在客户体验用例中利用AI/ML的强大功能。 这允许营销分析人员使用业务级配置针对公司需求设置预测，而无需数据科学专业知识。

### 归因人工智能

Attribution AI用于将点数归因于导致转化事件的接触点。 营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| HIPAA 准备就绪 | Healthcare Shield客户现在可以在Attribution AI和某些其他基于Experience Platform的应用程序中接收、使用、维护或传输受保护的健康信息。 Healthcare Shield适用于作为HIPAA下的受保实体或业务联系人的医疗保健客户。 有关详细信息，请阅读以下文档： [HIPAA和Adobe产品和服务](https://www.adobe.com/cn/trust/compliance/hipaa-ready.html) |
| 编辑其他得分数据集列 | 现在，您可以在编辑现有模型时添加或删除其他得分数据集列（报表列）。 这扩展了归因分数的灵活性，可在创建模型后为您提供对其他维度的洞察。 请参阅 [归因UI指南](../../intelligent-services/attribution-ai/user-guide.md) 了解更多信息。 |

{style="table-layout:auto"}

请查看 [AI/ML服务](../../intelligent-services/attribution-ai/overview.md) 概述，以了解更多信息。

### 客户人工智能

适用于Real-time Customer Data Platform的客户人工智能，用于生成自定义倾向得分，例如大规模单个用户档案的流失和转化情况。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| HIPAA 准备就绪 | Healthcare Shield客户现在可以在Customer AI中为Real-time Customer Data Platform和某些其他基于Experience Platform的应用程序接收、使用、维护或传输受保护的健康信息。 Healthcare Shield适用于作为HIPAA下的受保实体或业务联系人的医疗保健客户。 有关更多信息，请参阅以下文档： [HIPAA和Adobe产品和服务](https://www.adobe.com/cn/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

请查看 [AI/ML服务](../../intelligent-services/customer-ai/overview.md) 概述，以了解更多信息。

## Assurance {#assurance}

Adobe保证允许您检查、校对、模拟和验证在移动应用程序中收集数据或提供体验的方式。

**新增或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 验证编辑器 | 在验证编辑器中添加了新增强功能。 这些增强功能包括验证列、新的代码构建工具和改进的视图。 |

{style="table-layout:auto"}

欲知Assurance的详情，请阅读 [保证文档](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| 新主屏幕 | 数据收集UI的主页已更新，包含有用的载入信息和简化生产力的链接。 这包括：<ol><li>开始使用的文档和推荐的工作流</li><li>最近的属性、规则和数据元素</li><li>常用扩展</li><li>包含快速安装功能的新扩展更新</li></ol> |
| 将数据发送到 [!DNL Google Ads] 使用事件转发 | 您现在可以使用 [[!DNL Google Ads Enhanced Conversions] API扩展](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 用于事件转发，与 [Google Oauth 2密钥](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，以安全地向发送服务器端数据 [!DNL Google Ads] 实时。 |

{style="table-layout:auto"}

## 目标（更新日期：2月2日） {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud Audiences连接](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL (Beta) Adobe Experience Cloud受众] 用于将区段从Experience Platform共享到各种Experience Platform解决方案(如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo)的连接。 |
| [Pega配置文件连接](../../destinations/catalog/personalization/pega-profile.md) | 使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中创建到 [!DNL Amazon] S3存储，用于定期将配置文件数据从Adobe Experience Platform导出到CSV文件，并存储到您自己的S3存储桶中。 In [!DNL Pega Customer Decision Hub]，您可以安排数据作业以从S3存储中导入此配置文件数据以更新 [!DNL Pega Customer Decision Hub] 个人资料。 |
| [(Beta)交易台CRM EU连接](../../destinations/catalog/advertising/tradedesk-emails.md) | 随着EUID (European Unified ID)的发布，您现在可以看到两个 [!DNL The Trade Desk - CRM] 中的目标 [目标目录](/help/destinations/catalog/overview.md). <ul><li> 如果您从欧盟地区获取数据，请使用 **[!DNL The Trade Desk - CRM (EU)]** 目标。</li><li> 如果您在APAC或NAMER地区获取数据，请使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目标。 </li></ul> |

**新增或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 增强了付费媒体同意策略，以便与流目标集成 | An [增强同意政策的执行](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 日期 [流式目标](/help/destinations/destination-types.md#streaming-destinations) 适用于付费媒体激活用例。 当配置文件不再符合同意策略的条件时，Experience Platform现在会主动将其策略退出告知流目标。 <br> <b>注释</b>：此功能仅适用于以下客户： **[!UICONTROL 隐私和安全防护板]**，以及 **[!UICONTROL Health Shield]**. |
| Beta版云存储目标连接器的新分隔符选项 | 三个新的分隔符选项（冒号） `:`，竖线，分号 `;`)现在可用于新的测试版云存储目标 —  [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)， [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [(Beta)数据登陆区](/help/destinations/catalog/cloud-storage/data-landing-zone.md)， [（测试版） Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)， [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> 阅读有关支持的 [文件格式选项](/help/destinations/ui/batch-destinations-file-formatting-options.md) 用于基于文件的目标。 |
| 新的可选参数，可在 [客户数据字段](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) 中的配置 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`：当您需要创建客户数据字段时，使用此参数，该字段的值必须在由用户组织设置的所有目标数据流中唯一。 <br> 例如， **[!UICONTROL 集成别名]** 中的字段 [[!UICONTROL 自定义个性化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 目标必须是唯一的，这意味着流向此目标的两个单独数据流不能具有此字段的相同值。 |

**修复和增强功能** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>修复或增强功能</b></td>
        <td><b>描述</b></td>
    </tr>
    <tr>
        <td>更新了导出到基于文件的目标的行为(PLAT-123316)</td>
        <td>我们修复了以下行为中的一个问题： <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">必需属性</a> 将数据文件导出到批处理目标时。 <br> 以前，已验证输出文件中的每个记录都包含以下两项： <ol><li>的非null值 <code>mandatoryField</code> 列和</li><li>至少一个其他非必填字段上的非空值。</li></ol> 第二个条件已被删除。 因此，导出的数据文件中可能会显示更多的输出行，如下例所示：<br> <b> 2023年1月版本之前的示例行为 </b> <br> 必填字段： <code>emailAddress</code> <br> <b>输入数据以激活</b> <br><table><thead><tr><th>名字</th><th>电子邮件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>激活输出</b> <br><table><thead><tr><th>名字</th><th>电子邮件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023年1月版本之后的示例行为 </b> <br> <b>激活输出</b> <br> <table><thead><tr><th>名字</th><th>电子邮件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>验证所需映射和重复映射的UI和API (PLAT-123316)</td>
        <td>现在，当UI和API中出现以下情况时，将强制进行验证 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">映射字段</a> 在激活目标工作流中：<ul><li><b>必需的映射</b>：如果目标开发人员已使用所需的映射(例如， <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google广告管理器360</a> 之后，在激活指向目标的数据时，用户需要添加这些所需的映射。 </li><li><b>复制映射</b>：在激活工作流的映射步骤中，您可以在源字段中添加重复值，但不能在目标字段中添加。 有关允许和禁止的映射组合的示例，请参见下表。 <br><table><thead><tr><th>允许/禁止</th><th>源字段</th><th>目标字段</th></tr></thead><tbody><tr><td>允许</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>电子邮件别名2</li></ul></td></tr><tr><td>禁止</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| 架构树显示名称改进 | 以前，字段名称显示在UI中，但现在，架构画布上的架构字段显示名称更易于阅读。 |

**新XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 转化]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 用于跟踪货币兑换等兑换数据的类。 |
| 字段组 | [[!UICONTROL 货币兑换率详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 的字段组 [!UICONTROL 转化] 类，捕获与货币兑换相关的其他详细信息。 |
| 字段组 | [[!UICONTROL 同意策略评估结果与元数据映射]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 捕获多个同意政策的评估结果的详细信息，包括关于同意政策进入和存在的元数据信息。 |

**更新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL 广告详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 此 `ID` 字段已重命名为 `name`，以及上一个 `name` 字段为现在 `friendlyName`. |
| 数据类型 | [[!UICONTROL 决策建议详细信息]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 添加了 `selectionStrategy` 捕获选择策略详细信息的字段。 |
| 字段组 | [[!UICONTROL 体验事件 — 建议交互]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 字段组现在与 [!UICONTROL 历程步骤事件] 类。 |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 此 `ID` 字段已重命名为 `name`. |
| 数据类型 | [[!UICONTROL 媒体信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 将模式更改还原为视频区段属性。 |
| 数据类型 | [[!UICONTROL Qoe数据详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 已删除 `droppedFrameCount` 字段。 |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已重命名 `isAuthorized` 字段至 `authorized`，并更新了 `type` 以前是布尔值时的字符串。 |
| 数据类型 | [[!UICONTROL 配送]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 添加了多个新字段： `shipDate`， `trackingNumber`、和 `trackingURL`. |
| 字段组 | [[!UICONTROL AJO实体字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 添加了多个新字段： `journeyNodeID`， `journeyNodeName`、和 `journeyModeType`. |
| 字段组 | [[!UICONTROL 使用者体验事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 字段组现在也与 [!UICONTROL 摘要量度] 类。 |
| 字段组 | [[!UICONTROL 产品触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 此 `productTriggers` 字段现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL 相对触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 此 `relativeTriggers` 字段现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL 严重触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `severeTriggers` 字段现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL 天气触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `weatherTriggers` 字段现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL XDM相关业务帐户]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 字段组现在处于稳定状态。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 实时客户资料 {#profile}

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 用户档案允许您将客户数据整合到一个统一的视图中，并提供每个客户互动的可操作、带时间戳的帐户。

**即将弃用** {#deprecation}

为了消除区段成员资格生命周期中的冗余， `Existing` 状态将从 [区段成员资格分布图](../../xdm/field-groups/profile/segmentation.md) 2023年3月底。 后续公告将包含确切的弃用日期。

弃用后，区段中符合条件的用户档案将表示为 `Realized` 并且不符合资格的用户档案将继续显示为 `Exited`. 这将带来与基于文件的目标之间的对等性， `Active` 和 `Expired` 区段状态。

如果您使用的是 [企业目标](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure事件中心、HTTP API)，并已基于 `Existing` 状态。 如果您遇到这种情况，请查看您的下游集成。 如果您想在某个特定时间后确定新符合条件的用户档案，请考虑结合使用 `Realized` 状态和 `lastQualificationTime` 区段会员资格映射中的区段名称。 有关更多信息，请联系您的Adobe代表。

要了解有关Real-time Customer Profile的更多信息，包括有关使用用户档案数据的教程和最佳实践，请从阅读 [Real-time Customer Profile概述](../../profile/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 在区段生成器中导入批量值 | 区段生成器现在支持通过上传CSV或TSV文件或手动插入逗号分隔值来导入多个值。 欲知更多信息，请参见 [Segment Builder指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| 外部受众成员资格过期 | 默认情况下，外部受众成员资格将保留30天。 要将其保留更长时间，请使用 `validUntil` 在摄取受众数据期间的字段。 |
| 平台生成的区段成员资格到期 | 中的任何区段成员资格 `Exited` 表示超过30天，基于 `lastQualificationTime` 字段将被删除。 |

{style="table-layout:auto"}

有关的详细信息 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

| 功能 | 描述 |
| --- | --- |
| 允许用户访问云存储源的子文件夹 | 现在，您可以在创建新帐户时定义对云存储源的特定子文件夹的访问权限。 创建后，用户将只能访问允许的子文件夹中的数据。 此功能适用于以下云存储源： [Azure Blob存储](../../sources/connectors/cloud-storage/blob.md)， [Google云存储](../../sources/connectors/cloud-storage/google-cloud-storage.md)， [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)、和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 的Beta版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 源现已推出beta版。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 从您的网站获取数据的源 [!DNL SugarCRM] 帐户到Experience Platform。 有关详细信息，请阅读 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md). |
