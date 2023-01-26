---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 08ad27303b88826fd7e0fcc0a8b3d498de58c260
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 1 月 25 日**

Adobe Experience Platform 现有功能的更新包括：

- [Assurance](#assurance)
- [数据收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [体验数据模型(XDM)](#xdm)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## Assurance {#assurance}

Adobe保证允许您检查、校样、模拟和验证如何在移动设备应用程序中收集数据或提供体验。

**新增功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 验证编辑器 | 对验证编辑器进行了新的增强。 这些增强功能包括验证列、新的代码构建工具和改进的视图。 |

{style=&quot;table-layout:auto&quot;}

有关“Assurance（保证）”的更多信息，请阅读 [保证文档](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 新主屏幕 | 数据收集UI主页已更新，其中包含有用的入门信息和链接，可简化工作效率。 这包括：<ol><li>文档和建议的工作流以开始使用</li><li>近期属性、规则和数据元素</li><li>常用扩展</li><li>新扩展通过快速安装功能进行了更新</li></ol> |
| 将数据发送到 [!DNL Google Ads] 使用事件转发 | 您现在可以使用 [[!DNL Google Ads Enhanced Conversions] API扩展](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 对于事件转发，与 [Google Oauth 2密钥](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，以安全地将服务器端数据发送到 [!DNL Google Ads] 实时。 |

{style=&quot;table-layout:auto&quot;}

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [（测试版）Adobe Experience Cloud Audiences连接](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL （测试版）Adobe Experience Cloud受众] 可将区段从Experience Platform共享到各种Experience Platform解决方案，如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。 |
| [Pega配置文件连接](../../destinations/catalog/personalization/pega-profile.md) | 使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中创建与 [!DNL Amazon] S3存储，用于将配置文件数据定期从Adobe Experience Platform导出到CSV文件，并将其导出到您自己的S3存储段中。 在 [!DNL Pega Customer Decision Hub]，则可以计划数据作业以从S3存储导入此配置文件数据，以更新 [!DNL Pega Customer Decision Hub] 配置文件。 |
| [（测试版）交易台CRM EU连接](../../destinations/catalog/advertising/tradedesk-emails.md) | 随着EUID（欧洲统一ID）的发布，您现在会看到两个 [!DNL The Trade Desk - CRM] 目标 [目标目录](/help/destinations/catalog/overview.md). <ul><li> 如果您在欧盟地区收集数据，请使用 **[!DNL The Trade Desk - CRM (EU)]** 目标。</li><li> 如果您在APAC或NAMER地区收集数据，请使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目标。 </li></ul> |

**新增功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 测试版云存储目标连接器的新分隔符选项 | 三个新的分隔符选项（冒号） `:`，管道，分号 `;`)现已可用于新的测试版云存储目标 —  [(Beta)Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [（测试版）Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [（测试版）Azure数据湖存储第2代](/help/destinations/catalog/cloud-storage/adls-gen2.md), [（测试版）数据登陆区](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [（测试版）Google云存储](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [（测试版）SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> 了解支持的 [文件格式选项](/help/destinations/ui/batch-destinations-file-formatting-options.md) （对于基于文件的目标）。 |
| 中提供的新可选参数 [客户数据字段](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) 配置 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`:当您需要创建一个客户数据字段，该字段的值在用户组织设置的所有目标数据流中必须唯一时，请使用此参数。 <br> 例如， **[!UICONTROL 集成别名]** 字段 [[!UICONTROL 自定义个性化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 目标必须唯一，这意味着此目标的两个单独的数据流不能具有此字段的相同值。 |

**修复和增强功能** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>修复或增强功能</b></td>
        <td><b>描述</b></td>
    </tr>
    <tr>
        <td>更新了对基于文件的目标的导出行为(PLAT-123316)</td>
        <td>我们修复了 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">必需属性</a> 将数据文件导出到批处理目标时。 <br> 以前，输出文件中的每条记录都经过验证，可同时包含以下两项： <ol><li>的非空值 <code>mandatoryField</code> 列和</li><li>其他至少一个非必填字段上的非空值。</li></ol> 第二个条件已被删除。 因此，您可能会在导出的数据文件中看到更多输出行，如以下示例所示：<br> <b> 2023年1月版之前的示例行为 </b> <br> 必填字段： <code>emailAddress</code> <br> <b>要激活的输入数据</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>约翰</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>杰尼费</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>激活输出</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>约翰</td><td>john@acme.com</td></tr><tr><td>杰尼费</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023年1月版发布后的示例行为 </b> <br> <b>激活输出</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>约翰</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>杰尼费</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
</table>

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 禁用字符串字段的建议值 | 您现在可以 [禁用字符串字段的单个建议值](../../xdm/ui/fields/enum.md) 在 [!UICONTROL 模式] 工作区，包括来自标准组件的工作区。 此功能仅适用于具有建议值的字段，枚举约束不支持此功能。 |

**新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 转化]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 用于跟踪货币兑换等兑换数据的类。 |
| 字段组 | [[!UICONTROL 货币兑换率详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 的字段组 [!UICONTROL 转化] 类，捕获与货币兑换相关的其他详细信息。 |
| 字段组 | [[!UICONTROL 包含元数据的同意策略评估结果映射]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 捕获多个同意策略评估结果的详细信息，包括有关同意策略入口和存在的元数据信息。 |

**更新了XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL 广告详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 的 `ID` 字段已重命名为 `name`、和上一个 `name` 字段 `friendlyName`. |
| 数据类型 | [[!UICONTROL 决策建议详细信息]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 添加了 `selectionStrategy` 字段，用于捕获选择策略的详细信息。 |
| 字段组 | [[!UICONTROL 体验事件 — 建议交互]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 字段组现在与 [!UICONTROL 历程步骤事件] 类。 |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 的 `ID` 字段已重命名为 `name`. |
| 数据类型 | [[!UICONTROL 媒体信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 还原了对视频区段属性的模式更改。 |
| 数据类型 | [[!UICONTROL Qoe数据详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 删除了 `droppedFrameCount` 字段。 |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 重命名了 `isAuthorized` 字段 `authorized`，并更新了 `type` 字符串（当它以前为布尔值时）。 |
| 数据类型 | [[!UICONTROL 装运]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 添加了以下几个新字段： `shipDate`, `trackingNumber`和 `trackingURL`. |
| 字段组 | [[!UICONTROL AJO实体字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 添加了以下几个新字段： `journeyNodeID`, `journeyNodeName`和 `journeyModeType`. |
| 字段组 | [[!UICONTROL 消费者体验事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 字段组现在还与 [!UICONTROL 概要量度] 类。 |
| 字段组 | [[!UICONTROL 产品触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 的 `productTriggers` 字段，现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL 相对触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 的 `relativeTriggers` 字段，现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL 严重触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 的 `severeTriggers` 字段，现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL 天气触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 的 `weatherTriggers` 字段，现在嵌套在 `weather` 对象。 |
| 字段组 | [[!UICONTROL XDM相关业务帐户]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 字段组现在稳定。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将客户数据整合到统一视图中，为每次客户互动提供一个加盖时间戳的可操作帐户。

**即将弃用** {#deprecation}

为了在区段成员资格生命周期中消除冗余， `Existing` 状态将从 [区段成员资格映射](../../xdm/field-groups/profile/segmentation.md) 于2023年3月底。 后续公告将包括确切的弃用日期。

弃用后，符合区段条件的用户档案将表示为 `Realized` 取消用户档案资格的用户档案将继续以 `Exited`. 这将实现与基于文件的目标的对等性 `Active` 和 `Expired` 区段状态。

如果您使用 [企业目标](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure事件中心、HTTP API)，并且已根据 `Existing` 状态。 如果存在这种情况，请查看下游集成。 如果您有兴趣识别超过特定时间的新合格用户档案，请考虑将 `Realized` 状态和 `lastQualificationTime` 在区段成员资格映射中。 有关更多信息，请联系您的Adobe代表。

要了解有关实时客户用户档案的更多信息，包括有关使用用户档案数据的教程和最佳实践，请首先阅读 [实时客户资料概述](../../profile/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 平台生成的区段成员资格过期 | 位于 `Exited` 状态超过30天，根据 `lastQualificationTime` 字段，则该字段将被删除。 |
| 外部受众成员资格过期 | 默认情况下，外部受众成员资格将保留30天。 若要将其保留更长时间，请使用 `validUntil` 字段。 |

{style=&quot;table-layout:auto&quot;}

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| 允许用户访问云存储源的子文件夹 | 现在，您可以在创建新帐户时定义对云存储源特定子文件夹的访问权限。 创建后，用户将只能从允许的子文件夹访问数据。 此功能适用于以下云存储源： [Azure Blob存储](../../sources/connectors/cloud-storage/blob.md), [Google云存储](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 测试版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 源现在在测试版中可用。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 从 [!DNL SugarCRM] 帐户Experience Platform。 有关更多信息，请阅读 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md). |