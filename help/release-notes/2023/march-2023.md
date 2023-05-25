---
title: Adobe Experience Platform发行说明2023年3月
description: Adobe Experience Platform 2023年3月版发行说明。
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
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

Adobe Experience Platform提供了多个功能板，您可以通过该功能板查看有关贵组织数据的重要见解，如在每日快照期间捕获的数据。

**新增或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的仪表板 | 您现在可以 **示例属性值** 将属性添加到用户定义的功能板构件编辑器中的构件之前。 创建构件时，该属性列中的几个示例值可用于单个属性。<br>您现在可以 **交换X轴和Y轴** 用交换轴按钮替换构件。 这可以节省时间，并在向构件添加属性时提供更符合人体工学的体验。 此保存操作需要再次从属性面板中查找这两个属性。<br> 您现在可以 **更改图例的位置和标题** 在你的小组件中。 在小组件上显示图例后，您可以将该图例重新定位到图表周围的任何位置，还可以重新命名图例标题，就像使用轴标签和小组件标题一样。 |

{style="table-layout:auto"}

有关仪表板的更多信息，包括如何授予访问权限和创建自定义小组件，请从阅读 [功能板概述](../../dashboards/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| 元转化API（测试版）的新快速入门工作流 | 从数据收集主屏幕访问“快速入门”下的新快速入门工作流！ 此 [元转化API的快速启动工作流](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 使客户能够快速收集和转发事件数据，只需几个简单的步骤即可从服务器端到元进行广告转化。 |
| Mobile SDK的新快速入门工作流（测试版） | 从数据收集主屏幕访问“快速入门”下的新快速入门工作流！ 此 [Mobile SDK快速入门工作流](https://developer.adobe.com/client-sdks/documentation/) 使您能够通过几个简单的步骤快速实施Mobile SDK并验证基本移动事件。 |
| [!DNL Braze] 事件转发扩展 | 此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件转发扩展允许您利用Adobe Experience Platform Edge Network中捕获的数据并将其发送至 [!DNL Braze] 以服务器端事件的形式使用 [!DNL Braze] 用户跟踪API。 |
| [!DNL Epsilon] 事件转发扩展 | 此 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 扩展允许您利用事件转发捕获Adobe Experience Platform Edge Network中的事件信息并将其发送给 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。 |
| [!DNL Mixpanel] 事件转发扩展 | 此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 扩展允许客户利用事件转发捕获Adobe Experience Platform Edge Network中的事件信息，并使用“跟踪事件API”将其发送到Mixpanel。 |

{style="table-layout:auto"}

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证数据到体验数据模型(XDM)以及从中转换和验证数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics数据过滤的正式发布 | 您现在可以使用数据准备功能来应用规则和条件，以便在将Analytics数据摄取到实时客户档案中之前对其进行筛选。 有关详细信息，请阅读以下指南： [筛选Analytics数据以进行配置文件摄取](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| 用于编码和解码URL字符串的新函数 | <ul><li>此 `get_url_encoded` 函数将URL作为输入，并使用ASCII字符替换或编码特殊字符。</li><li>此 `get_url_decoded` 函数以URL作为输入，并将ASCII字符解码为特殊字符。</li></ul> 有关详细信息，请阅读 [数据准备函数指南](../../data-prep/functions.md). 有关保留字符及其相应编码字符的完整列表，请阅读 [特殊字符](../../data-prep/functions.md#special-characters). |

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新目标** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 连接GA](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL Adobe Commerce] 目标连接器（现已正式可用）允许您选择一个或多个要激活到的Real-Time CDP受众 [!DNL Adobe Commerce] 帐户，为购物者提供动态的个性化体验。 |
| [[!DNL Snap Inc] 连接GA](../../destinations/catalog/advertising/snap-inc.md) | 此 [!DNL Snap Inc] 目标连接器（现已正式可用）允许营销人员将Experience Platform中创建的用户区段导入 [!DNL Snapchat Ads] 用它们来定位他们的广告。 |
| [(API)OracleEloqua连接](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 将基于API的连接用于 [!DNL Oracle Eloqua] 计划和执行活动，同时为潜在客户提供个性化的客户体验，包括 [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] 连接](../../destinations/catalog/advertising/amazon-ads.md) | 此 [!DNL Amazon Ads] 与Adobe Experience Platform集成提供了到 [!DNL Amazon Ads] 产品，包括 [!DNL Amazon DSP (ADSP)]. 使用 [!DNL Amazon Ads] 目标：在Adobe Experience Platform中，用户能够定义广告商受众，以便在 [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] 连接](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] （以前称为Bizible）可让营销人员深入了解哪些营销工作在为公司增加收入和最大化投资回报方面最有效。 该目标支持企业到企业(B2B)数据从Adobe Experience Platform流入 [!DNL Marketo Measure]. 此卡仅适用于 [!DNL Marketo Measure Ultimate] 客户。 |
| [TikTok连接](../../destinations/catalog/social/tiktok.md) | 使用您的数据在TikTok上构建自定义受众，以便通过广告营销活动进行定位。 |
| [Zendesk连接](../../destinations/catalog/crm/zendesk.md) | 使用此目标可在区段中作为联系人创建和更新身份 [!DNL Zendesk]. |

{style="table-layout:auto"}

**新增或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 目标的新访问控制权限： [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新权限让用户能够将区段激活到现有目标，而无需显示 [映射步骤](../../destinations/ui/activate-batch-profile-destinations.md#mapping). 用户可以在激活工作流中添加和删除区段，但无法添加或删除映射的属性或标识。 |

{style="table-layout:auto"}

**修复和增强功能** {#destinations-fixes-and-enhancements}

我们正在针对Real-time CDP基于文件的目标中的PGP/GPG加密发布错误修复。 通过这项更改，当前正在使用加密的现有基于文件的目标将生成一个与以前扩展名不同的文件名。

- 使用加密时的当前扩展： `filename.csv`
- 使用加密时的未来扩展： `filename.csv.gpg`

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| CSV到架构推荐 | 您现在可以上传本地文件以创建机器学习生成的架构，而无需手动创建架构。 从 [!UICONTROL 源] 工作区、上传示例CSV文件以及Adobe机器学习算法将根据目标字段为您建议架构。 请参阅 [文档](../../ingestion/tutorials/map-csv/recommendations.md) 了解更多信息。” |

{style="table-layout:auto"}

**新XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 优惠项目]](https://github.com/adobe/xdm/pull/1678/files) | 表示选件的类。 |
| 类 | [[!UICONTROL 决策项目]](https://github.com/adobe/xdm/pull/1678/files) | 可进行决策的项目。 决策过程的输出是一个或多个决策项目。 |
| 类 | [[!UICONTROL 媒体会话服务器超时]](https://github.com/adobe/xdm/pull/1676/files) | 这指示用户最后一次已知交互和会话关闭之间经过的时间（以秒为单位）。 |
| 字段组 | [[!UICONTROL XDM配置文件计算属性]](https://github.com/adobe/xdm/pull/1686/files) | 这会将Adobe内部服务的计算属性添加到传入的客户数据。 客户不应使用此数据来摄取数据。 |
| 数据类型 | [[!UICONTROL 退款项目]](https://github.com/adobe/xdm/pull/1685/files) | 指示退款是否与订单关联，并定义退款类型、金额和相关联的货币。 |
| 数据类型 | [[!UICONTROL 类别数据]](https://github.com/adobe/xdm/pull/1677/files) | 此新数据类型表示产品的类别。 |
| 架构 | [[!UICONTROL Adobe Target分类字段]](https://github.com/adobe/xdm/pull/1682/files) | 已为目标分类数据集创建新的XDM架构。 它包含一组元数据字段，用于对Target活动和体验进行分类。 |

{style="table-layout:auto"}

**更新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL 内容组件详细信息]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 已从 [!UICONTROL 内容组件详细信息] |
| 字段组 | [[!UICONTROL AJO实体标记]](https://github.com/adobe/xdm/pull/1672/files) | 已将AJO实体标记添加到 [!UICONTROL AJO实体字段]，对应于历程或促销活动 |
| 字段组 | （多个） | 为添加了多个字段 [[!UICONTROL Journey Orchestration步骤事件常用字段]](https://github.com/adobe/xdm/pull/1671/files) |
| 字段组 | （多个） | [为添加了多个XDM事件类型 [!UICONTROL 媒体报告]](https://github.com/adobe/xdm/pull/1670/files). |
| 字段组 | [!UICONTROL Workfront更改事件] | 此 `Full Record` 和 `Accessor Employee Ids` 已添加字段组。 |
| 数据类型 | [[!UICONTROL 产品列表项]](https://github.com/adobe/xdm/pull/1685/files) | 此 [!UICONTROL 退款金额] 已添加以指示该物料的退款金额（如果有）。 |
| 数据类型 | [[!UICONTROL 订购 ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL 退款列表] 已添加到此订单的退款列表。 |
| 数据类型 | [[!UICONTROL 产品列表项 ]](https://github.com/adobe/xdm/pull/1677/files) | 已将产品类别添加到此产品的类别数据列表中。 |
| 数据类型 | [!UICONTROL 会话详细信息] | 添加了 `pev3` 字符串字段 [指示用于报告的媒体流的类型](https://github.com/adobe/xdm/pull/1676/files). 另外还添加了 `pccr` 属性指示是否发生重定向。 |
| 数据类型 | [!UICONTROL 申请列表] | 提供 [申请列表属性](https://github.com/adobe/xdm/pull/1675/files). 包括名称、ID和描述。 |
| 数据类型 | [!UICONTROL Commerce] | 此 [Commerce数据类型已更新](https://github.com/adobe/xdm/pull/1675/files) 要包含 `requisitionListOpens`， `requisitionListAdds`， `requisitionListRemovals`、和 `requisitionList`. |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 加速存储上基于属性的访问控制 | 结合使用基于属性的访问控制与数据Distiller来定义对加速存储上所有数据集的访问控制。 这控制对用户创建并存储在加速存储中的自定义数据模型的访问，以支持自定义仪表板。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅 [查询服务概述](../../query-service/home.md).

## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B版构建于Real-time Customer Data Platform (Real-Time CDP)之上，专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其合并到人员和帐户配置文件的单一视图中。 此统一数据允许营销人员准确地定位特定受众，并在所有可用渠道中吸引这些受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 错误修复 | 为了更准确地表示您系统中的配置文件，系统不再将内部配置文件包含在Real-time Customer Data Platform B2B版本的总配置文件计数或可寻址受众指标中。 从今天开始，您可能会看到配置文件总数/可寻址受众量度出现一次性下降。 您的所有数据均未被清除，这只是对计数的更改。 如有任何问题，请联系您的Adobe主管 |

{style="table-layout:auto"}

要了解有关Real-Time CDP B2B版本的更多信息，请阅读 [Real-Time CDP B2B版本概述](../../rtcdp/overview.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件量度 | 为了让您更准确地表示用户档案指标，成员资格划分和流失指标正在进行合并，现在计算时间是24小时。 欲知更多信息，请参见 [分段UI指南](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

有关的详细信息 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 的Beta版可用性 [!DNL Chatlio] | 此 [!DNL Chatlio] 源现已推出beta版。 使用 [!DNL Chatlio] 源以流式传输 [!DNL Chatlio] 要Experience Platform的事件数据。 有关详细信息，请阅读 [[!DNL Chatlio] 概述](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 的Beta版可用性 [!DNL Customer.io] | 此 [!DNL Customer.io] 源现已推出beta版。 使用 [!DNL Customer.io] 源，用于将您的客户事件数据流式传输到Experience Platform。 有关详细信息，请阅读 [[!DNL Customer.io] 概述](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 的Beta版可用性 [!DNL Pendo] | 此 [!DNL Pendo] 源现已推出beta版。 使用 [!DNL Pendo] 源，用于将您的产品分析数据流式传输到Experience Platform。 有关详细信息，请阅读 [[!DNL Pendo] 概述](../../sources/connectors/analytics/pendo-webhook.md). |
| 支持草稿数据流 | 您现在可以使用流服务API将数据流设置为草稿状态。 草拟的数据流稍后可以更新并发布新信息。 有关详细信息，请阅读以下指南： [将源数据流设置为草稿](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).
