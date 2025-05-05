---
title: Adobe Experience Platform 发行说明（2023 年 3 月）
description: Adobe Experience Platform 的 2023 年 3 月发行说明。
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 97%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 3 月 29 日**

Adobe Experience Platform 中现有功能的更新：

- [仪表板](#dashboards)
- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的仪表板 | 现在，在小组件中添加属性之前，您可以在用户定义的仪表板小组件编辑器中&#x200B;**对属性值进行采样**。创建小组件时，该属性列中的一些示例值可用于各个属性。<br>您现在可以使用交换轴按钮&#x200B;**交换小组件上的 X 轴和 Y 轴**。在向小组件中添加属性时，这可以节省时间并提供更符合人体工程学的体验。这样就无需在属性面板中再次查找这两个属性。<br>您现在可以在小组件中&#x200B;**更改图例的位置和标题**。在小组件上出现图例后，您可以将该图例重新定位在图表上的任何位置，还可以重新命名图例标题，就像重命名轴标记和小组件标题一样。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Meta Conversions API 新的快速启动工作流程 (Beta) | 从数据收集主屏幕访问“开始使用”下新的快速启动工作流程！[Meta Conversions API 快速启动工作流程](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)使客户能够快速收集事件数据并将其从服务器端转发到 Meta，只需几个简单的步骤即可实现广告转换。 |
| Mobile SDK 新的快速启动工作流程 (Beta) | 从数据收集主屏幕访问“开始使用”下新的快速启动工作流程！[Mobile SDK 的快速启动工作流程](https://developer.adobe.com/client-sdks/documentation/)使您只需几个简单的步骤即可快速实施 Mobile SDK 并验证基本移动事件。 |
| [!DNL Braze] 事件转发扩展 | [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)事件转发扩展允许您利用 Adobe Experience Platform Edge Network 中捕获的数据，并使用 [!DNL Braze] User Track API 以服务器端事件的形式将其发送到 [!DNL Braze]。 |
| [!DNL Epsilon] 事件转发扩展 | [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 扩展允许您利用事件转发功能在 Adobe Experience Platform Edge Network 中捕获事件信息，并使用[!DNL Epsilon] Event API 将其发送给 [!DNL Epsilon]。 |
| [!DNL Mixpanel] 事件转发扩展 | [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 扩展允许客户利用事件转发功能在 Adobe Experience Platform Edge Network 中捕获事件信息，并使用 Track Events API 将其发送给 Mixpanel。 |

{style="table-layout:auto"}

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics 数据过滤功能全面可用 | 现在，您可以使用数据准备功能应用规则和条件来过滤您的 Analytics 数据，然后再将其引入实时客户轮廓。有关更多信息，请阅读有关[筛选 Analytics 数据以引入轮廓](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile)的指南。 |
| 用于编码和解码 URL 字符串的新函数 | <ul><li>该`get_url_encoded`函数将 URL 作为输入，并用 ASCII 字符替换或编码特殊字符。</li><li>该`get_url_decoded`函数将 URL 作为输入，并将 ASCII 字符解码为特殊字符。</li></ul> 有关详细信息，请阅读[数据准备函数指南](../../data-prep/functions.md)。有关保留字符及其相应编码字符的综合列表，请阅读有关[特殊字符](../../data-prep/functions.md#special-characters)的指南。 |

有关数据准备的详细信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**{#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 连接 GA](../../destinations/catalog/personalization/adobe-commerce.md) | [!DNL Adobe Commerce]目标连接器（现已全面可用）可让您选择一个或多个 Real-Time CDP 受众，以激活您的 [!DNL Adobe Commerce] 帐户，为购物者提供动态的个性化体验。 |
| [[!DNL Snap Inc] 连接 GA](../../destinations/catalog/advertising/snap-inc.md) | [!DNL Snap Inc]目标连接器（现已全面可用）允许营销人员将在 Experience Platform 中创建的用户区段导入到 [!DNL Snapchat Ads]，并使用它们来定位广告。 |
| [(API) Oracle Eloqua 连接](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 使用基于 API 的与 [!DNL Oracle Eloqua] 的连接规划和执行活动，同时为 [!DNL Oracle Eloqua] 中的潜在客户提供个性化的客户体验。 |
| [(Beta) [!DNL Amazon Ads] 连接](../../destinations/catalog/advertising/amazon-ads.md) | [!DNL Amazon Ads]与 Adobe Experience Platform 的集成可为 [!DNL Amazon Ads] 产品（包括 [!DNL Amazon DSP (ADSP)]）提供现成的集成。使用 Adobe Experience Platform 中的 [!DNL Amazon Ads] 目标，用户可以定义广告商受众，以便在 [!DNL Amazon DSP] 上进行定位和激活。 |
| [[!DNL Marketo Measure Ultimate] 连接](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure]（以前为 Bizible）使营销人员能够洞悉哪些营销工作在为公司增加收入以及使投资回报率最大化方面最有效。该目标可使业务对业务 (B2B) 数据流能够从 Adobe Experience Platform 传输到 [!DNL Marketo Measure]。该卡仅对 [!DNL Marketo Measure Ultimate] 客户可用。 |
| [TikTok 连接](../../destinations/catalog/social/tiktok.md) | 使用您的数据在 TikTok 上构建自定义受众，以便针对您的广告营销活动进行定位。 |
| [Zendesk 连接](../../destinations/catalog/crm/zendesk.md) | 使用此目标创建和更新区段内的身份标识，作为 [!DNL Zendesk] 内的联系人。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 目标的新访问控制权限：[[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新的权限使用户可激活通往现有目标的区段，而无需显示[映射步骤](../../destinations/ui/activate-batch-profile-destinations.md#mapping)。用户可以在激活工作流程中添加和删除区段，但无法添加或删除映射的属性或身份标识。 |

{style="table-layout:auto"}

**修复和增强功能** {#destinations-fixes-and-enhancements}

我们正在为Real-Time CDP发布针对基于文件的目标中的PGP/GPG加密的错误修复。 通过此更改，当前使用加密功能的现有基于文件的目标将会生成一个扩展名与以前不同的文件名。

- 当前使用加密时的扩展名：`filename.csv`
- 未来使用加密时的扩展名：`filename.csv.gpg`

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| CSV 到架构方面的建议 | 您现在可以通过上传本地文件来创建由机器学习生成的架构，从而无需手动创建架构。在[!UICONTROL 来源]工作区内，上传 CSV 示例文件，Adobe 机器学习算法将会根据目标字段为您提供架构方面的建议。有关详细信息，请参阅[文档](../../ingestion/tutorials/map-csv/recommendations.md)。 |

{style="table-layout:auto"}

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 产品建议项目]](https://github.com/adobe/xdm/pull/1678/files) | 代表产品建议的类。 |
| 类 | [[!UICONTROL 决策项目]](https://github.com/adobe/xdm/pull/1678/files) | 可以进行决策的项目。决策过程的输出是一个或多个决策项目。 |
| 类 | [[!UICONTROL 媒体会话服务器超时]](https://github.com/adobe/xdm/pull/1676/files) | 这表示用户最后一次已知交互与会话关闭之间经过的时间量（以秒为单位）。 |
| 字段组 | [[!UICONTROL XDM 轮廓计算属性]](https://github.com/adobe/xdm/pull/1686/files) | 这会将内部 Adobe 服务的计算属性添加到传入的客户数据中。客户不应使用它来摄取数据。 |
| 数据类型 | [[!UICONTROL 退款项目]](https://github.com/adobe/xdm/pull/1685/files) | 指示退款是否与某个订单关联，并定义退款类型、金额和关联货币。 |
| 数据类型 | [[!UICONTROL 类别数据]](https://github.com/adobe/xdm/pull/1677/files) | 这个新数据类型代表产品的类别。 |
| 架构 | [[!UICONTROL Adobe Target 分类字段]](https://github.com/adobe/xdm/pull/1682/files) | 为 Target 分类数据集创建了新的 XDM 架构。它包含一组对 Target 活动和体验进行分类的元数据字段。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL 内容组件详细信息]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 已从[!UICONTROL 内容组件详细信息]中删除 |
| 字段组 | [[!UICONTROL AJO 实体标记]](https://github.com/adobe/xdm/pull/1672/files) | 将 AJO 实体标记添加到对应于历程或营销活动的 [!UICONTROL AJO 实体字段] |
| 字段组 | （多种） | 为[[!UICONTROL &#x200B; Journey Orchestration 步骤事件公共字段]](https://github.com/adobe/xdm/pull/1671/files)添加了几个字段 |
| 字段组 | （多种） | 为[!UICONTROL 媒体报告][&#128279;](https://github.com/adobe/xdm/pull/1670/files)添加了几种 XDM 事件类型。 |
| 字段组 | [!UICONTROL Workfront 变更事件] | 添加了 `Full Record` 和 `Accessor Employee Ids` 字段组。 |
| 数据类型 | [[!UICONTROL 产品列表项目]](https://github.com/adobe/xdm/pull/1685/files) | 添加了[!UICONTROL 退款金额]，以指示该商品的退款金额（如果有）。 |
| 数据类型 | [[!UICONTROL 订单]](https://github.com/adobe/xdm/pull/1685/files) | 已将[!UICONTROL 退款列表]添加到此订单的退款列表。 |
| 数据类型 | [[!UICONTROL 产品列表项目]](https://github.com/adobe/xdm/pull/1677/files) | 产品类别已添加到该产品的类别数据列表中。 |
| 数据类型 | [!UICONTROL 会话详细信息] | 添加了`pev3`字符串字段[，表示用于报告 ](https://github.com/adobe/xdm/pull/1676/files) 的媒体流类型。还添加了 `pccr` 属性，指示是否发生重定向。 |
| 数据类型 | [!UICONTROL 需求列表] | 提供[需求列表属性](https://github.com/adobe/xdm/pull/1675/files)。其中包括名称、ID 和描述。 |
| 数据类型 | [!UICONTROL Commerce] | [Commerce 数据类型已更新](https://github.com/adobe/xdm/pull/1675/files)，以包括 `requisitionListOpens`、`requisitionListAdds`、`requisitionListRemovals` 和 `requisitionList`。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请阅读[XDM系统概述](../../xdm/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以加入数据湖的任何数据集，并作为新数据集获取查询结果，以用于报表、Data Science Workspace，或将数据摄取到实时客户轮廓。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 加速存储上基于属性的访问控制功能 | 将基于属性的访问控制与数据提取器结合使用，定义加速存储上所有数据集的访问控制。这控制了对用户创建并存储在加速存储中的自定义数据模型的访问，以支持自定义仪表板。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。

## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B 版本基于 Real-Time Customer Data Platform (Real-Time CDP) 构建，专为采用业务对业务服务模式运营的营销人员而构建。它将来自多个来源的数据汇集在一起&#x200B;，并将其组合成人员和帐户轮廓的单一视图。这种统一的数据使营销人员能够精确锁定特定受众，并通过所有可用渠道吸引这些受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 错误修正 | 为了在系统中更准确地表示轮廓，系统不再在 Real-Time Customer Data Platform B2B 版的总轮廓计数或可寻址受众指标中包括内部轮廓。从今天开始，您可能会看到轮廓总数/可寻址受众指标出现一次性下降。这不会删除您的任何数据，这只是对计数的更改。如果您有任何疑问，请联系您的 Adobe 主管 |

{style="table-layout:auto"}

要详细了解 Real-Time CDP B2B 版本，请阅读 [Real-Time CDP B2B 版本概述](../../rtcdp/overview.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 轮廓指标 | 为了让您能够更准确地表示轮廓指标，我们将成员关系细分和流失指标合并起来，现在按 24 小时计算。更多信息可在[分段 UI 指南](../../segmentation/ui/overview.md#browse)中找到 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Chatlio] Beta 版本的可用性 | [!DNL Chatlio] 源当前在 Beta 中可用。使用 [!DNL Chatlio] 源将您的 [!DNL Chatlio] 事件数据流式传输到 Experience Platform。有关详细信息，请参阅 [[!DNL Chatlio]  概述](../../sources/connectors/marketing-automation/chatlio-webhook.md)。 |
| [!DNL Customer.io] Beta 版本的可用性 | [!DNL Customer.io] 源当前在 Beta 中可用。使用 [!DNL Customer.io] 源将您的客户事件数据流式传输到 Experience Platform。有关详细信息，请参阅 [[!DNL Customer.io]  概述](../../sources/connectors/marketing-automation/customerio-webhook.md)。 |
| [!DNL Pendo] Beta 版本的可用性 | [!DNL Pendo] 源当前在 Beta 中可用。使用 [!DNL Pendo] 源将您的产品分析数据流式传输到 Experience Platform。有关详细信息，请参阅 [[!DNL Pendo]  概述](../../sources/connectors/analytics/pendo-webhook.md)。 |
| 支持草稿数据流 | 您现在可以使用 Flow Service API 将数据流设置为草稿状态。起草的数据流稍后可以使用新信息进行更新和发布。若要了解更多信息，请阅读有关[将源数据流设置为草稿](../../sources/tutorials/api/draft.md)的指南。 |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
