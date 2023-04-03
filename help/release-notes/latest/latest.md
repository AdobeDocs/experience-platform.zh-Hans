---
title: Adobe Experience Platform 发行说明
description: 2023年3月版Adobe Experience Platform发行说明。
source-git-commit: 1ead97aa9b197cd1c046175bdcd06c03fd35ac17
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 3 月 29 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [分段服务](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关组织数据的重要分析（在每日快照中捕获）。

**新增功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的功能板 | 您现在可以 **示例属性值** 在用户定义的功能板小组件编辑器中向小组件添加属性之前，请执行以下操作： 创建小组件时，该属性列中的一些示例值可用于单个属性。<br>您现在可以 **交换X和Y轴** 在带交换轴按钮的小组件上。 这样可节省时间，并在向小组件添加属性时提供更符合人体工程学的体验。 这样保存后，需要从“属性”面板中再次查找这两个属性。<br>您现在可以 **更改图例的位置和标题** 在小组件中。 在小组件上出现图例后，您可以将该图例重新定位到图表周围的任意位置，还可以重新命名图例标题，就像使用轴标签和小组件标题一样。 |

{style="table-layout:auto"}

有关功能板的更多信息（包括如何授予访问权限和创建自定义小组件），请首先阅读 [功能板概述](../../dashboards/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 新的元转化API（测试版）快速入门工作流 | 从数据收集主屏幕中访问位于“快速入门”下的新快速入门工作流！ 的 [元转化API快速启动工作流](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 使客户能够在服务器端快速收集和转发事件数据到元数据，以便只需几个简单的步骤即可进行广告转化。 |
| [!DNL Braze] 事件转发扩展 | 的 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件转发扩展允许您利用在Adobe Experience Platform边缘网络中捕获的数据，并将其发送到 [!DNL Braze] 以服务器端事件的形式使用 [!DNL Braze] 用户跟踪API。 |
| [!DNL Epsilon] 事件转发扩展 | 的 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 扩展允许您利用事件转发在Adobe Experience Platform边缘网络中捕获事件信息，并将其发送到 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。 |
| [!DNL Mixpanel] 事件转发扩展 | 的 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 扩展允许客户利用事件转发在Adobe Experience Platform边缘网络中捕获事件信息，并使用跟踪事件API将其发送到Mixpanel。 |

{style="table-layout:auto"}

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 筛选Adobe Analytics数据的一般可用性 | 现在，您可以使用数据准备功能来应用规则和条件，以便在将Analytics数据摄取到实时客户资料之前对其进行过滤。 有关更多信息，请阅读 [过滤用于配置文件摄取的Analytics数据](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| 用于编码和解码URL字符串的新函数 | <ul><li>的 `get_url_encoded` 函数将URL作为输入，并用ASCII字符替换或编码特殊字符。</li><li>的 `get_url_decoded` 函数将URL作为输入，并将ASCII字符解码为特殊字符。</li></ul> 有关更多信息，请阅读 [数据准备功能指南](../../data-prep/functions.md). 有关保留字符及其相应编码字符的完整列表，请阅读 [特殊字符](../../data-prep/functions.md#special-characters). |

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新目标** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 连接GA](../../destinations/catalog/personalization/adobe-commerce.md) | 的 [!DNL Adobe Commerce] 目标连接器（现在通常可用）允许您选择一个或多个要激活到您的Real-Time CDP受众 [!DNL Adobe Commerce] 帐户为购物者提供动态个性化体验。 |
| [[!DNL Snap Inc] 连接GA](../../destinations/catalog/advertising/snap-inc.md) | 的 [!DNL Snap Inc] 目标连接器（现在通常可用）允许营销人员将在Experience Platform中创建的用户区段导入 [!DNL Snapchat Ads] 并用于定位其广告。 |
| [(API)OracleEloqua连接](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 使用基于API的连接到 [!DNL Oracle Eloqua] 在为潜在客户提供个性化客户体验的同时，在 [!DNL Oracle Eloqua]. |
| [（测试版） [!DNL Amazon Ads] 连接](../../destinations/catalog/advertising/amazon-ads.md) | 的 [!DNL Amazon Ads] 与Adobe Experience Platform集成提供与 [!DNL Amazon Ads] 产品，包括 [!DNL Amazon DSP (ADSP)]. 使用 [!DNL Amazon Ads] 目标中，用户能够定义广告商受众，以在上定位和激活 [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] 连接](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] （以前称为Bizible）使营销人员能够洞悉哪些营销工作在增加收入和为公司实现投资回报方面最有效。 该目标支持从Adobe Experience Platform到 [!DNL Marketo Measure]. 该卡仅供 [!DNL Marketo Measure Ultimate] 客户。 |
| [TikTok连接](../../destinations/catalog/social/tiktok.md) | 在TikTok上使用您的数据构建自定义受众，以便通过广告营销活动进行定位。 |
| [Zendesk连接](../../destinations/catalog/crm/zendesk.md) | 使用此目标可在区段内创建和更新身份，以作为 [!DNL Zendesk]. |

{style="table-layout:auto"}

**新增功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 目标的新访问控制权限： [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新权限允许用户将区段激活到现有目标，而不显示 [映射步骤](../../destinations/ui/activate-batch-profile-destinations.md#mapping). 用户可以在激活工作流中添加和删除区段，但无法添加或删除映射的属性或标识。 |

{style="table-layout:auto"}

**修复和增强功能** {#destinations-fixes-and-enhancements}

我们将针对实时CDP的基于文件的目标中的PGP/GPG加密发布错误修复。 根据这项更改，当前使用加密的基于文件的现有目标将生成一个扩展名与之前不同的文件名。

- 使用加密时的当前扩展： `filename.csv`
- 使用加密时的未来扩展： `filename.csv.gpg`

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| CSV模式推荐 | 您现在可以上传本地文件来创建机器学习生成的架构，从而无需手动创建架构。 从 [!UICONTROL 源] 工作区、上传CSV文件示例，Adobe机器学习算法将根据目标字段为您建议一种模式。 请参阅 [文档](../../ingestion/tutorials/map-csv/recommendations.md) ”。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以加入来自数据湖的任何数据集，并作为新数据集捕获查询结果，以用于报表、Data Science Workspace或将其摄取到实时客户资料中。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 基于属性的加速存储访问控制 | 结合使用基于属性的访问控制和数据Distiller，对加速存储上的所有数据集定义访问控制。 这可控制对用户创建并存储在加速存储中的自定义数据模型的访问，以支持自定义功能板。 |

{style="table-layout:auto"}

有关查询服务的更多信息，请参阅 [查询服务概述](../../query-service/home.md).

## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B Edition基于Real-time Customer Data Platform(Real-Time CDP)而构建，专为以企业对企业服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其整合为人员和帐户配置文件的单一视图。 通过这种统一的数据，营销人员可以准确定位特定受众并在所有可用渠道中吸引这些受众。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 错误修复 | 为了在系统中更准确地表示用户档案，在Real-time Customer Data Platform B2B Edition的总用户档案计数或可寻址受众量度中，系统不再包含内部用户档案。 从今天开始，您可能会看到配置文件计数/可寻址受众量度总数出现一次性下降。 您的任何数据都未被擦除，这只是对计数的更改。 如有任何疑问，请联系您的Adobe主管 |

{style="table-layout:auto"}

要了解有关Real-Time CDP B2B Edition的更多信息，请阅读 [Real-Time CDP B2B版概述](../../rtcdp/overview.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 配置文件量度 | 为了更准确地表示用户档案量度，会将会员资格划分和流失量度组合在一起，现在会在24小时内计算这些量度。 有关更多信息，请参阅 [分段UI指南](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 测试版可用性 [!DNL Chatlio] | 的 [!DNL Chatlio] 来源现已在测试版中提供。 使用 [!DNL Chatlio] 流源 [!DNL Chatlio] 事件数据Experience Platform。 有关更多信息，请阅读 [[!DNL Chatlio] 概述](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 测试版可用性 [!DNL Customer.io] | 的 [!DNL Customer.io] 来源现已在测试版中提供。 使用 [!DNL Customer.io] 用于将客户事件数据流式传输到Experience Platform的源。 有关更多信息，请阅读 [[!DNL Customer.io] 概述](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 测试版可用性 [!DNL Pendo] | 的 [!DNL Pendo] 来源现已在测试版中提供。 使用 [!DNL Pendo] 来源将产品分析数据流化到Experience Platform。 有关更多信息，请阅读 [[!DNL Pendo] 概述](../../sources/connectors/analytics/pendo-webhook.md). |
| 支持草稿数据流 | 您现在可以使用流服务API将数据流设置为草稿状态。 起草的数据流稍后可以更新并发布，以包含新信息。 有关更多信息，请阅读 [将源数据流设置为草稿](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

要进一步了解来源，请阅读 [源概述](../../sources/home.md).
