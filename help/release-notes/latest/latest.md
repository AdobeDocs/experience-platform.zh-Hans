---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年6月版发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a3faca5e0a711f0d4f6bafb22bf3c4770f58db8e
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 6 月 21 日**

Adobe Experience Platform 现有功能的更新包括：

- [对Experience PlatformAPI的身份验证](#authentication-platform-apis)
- [数据收集](#data-collection)
- [目标](#destinations)
- [体验数据模型(XDM)](#xdm)
- [查询服务](#query-service)
- [源](#sources)

## 对Experience PlatformAPI的身份验证 {#authentication-platform-apis}

对于Experience PlatformAPI用户，现在简化了获取进行身份验证和调用API端点所需的访问令牌的方法。 用于获取访问令牌的JWT方法已弃用，并替换为更简单的OAuth服务器到服务器身份验证方法。<p>![突出显示用于获取访问令牌的新OAuth身份验证方法。](/help/landing/images/api-authentication/oauth-authentication-method.png "突出显示用于获取访问令牌的新OAuth身份验证方法。"){width="100" zoomable="yes"}</p>

虽然使用JWT身份验证方法的现有API集成将继续工作到2025年1月1日，但Adobe强烈建议您在该日期之前将现有集成迁移到新的OAuth服务器到服务器方法。 阅读以下内容中的指南： [从服务帐户(JWT)凭据迁移到OAuth服务器到服务器凭据](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

阅读更新内容 [Experience Platform身份验证教程](/help/landing/api-authentication.md) 了解更多信息。

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

**新增或更新功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Google Cloud Platform] 事件转发扩展 | 此 [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) 事件转发扩展允许您将事件数据转发到Google以供激活，方法是： [!DNL Google Pub/Sub]. |
| 扩展 | [!DNL Cloud connector for Google Analytics 4 (ga4)] 扩展 | 此 [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) 事件转发扩展允许您通过新的 [!DNL Google Analytics 4 (ga4)] 标准。 |
| 密码 | OAuth 2 JWT密码 | 此 [OAuth 2 JWT密码](../../tags/ui/event-forwarding/secrets.md) 允许您使用Adobe和 [!DNL Google] 在事件转发中支持服务器 — 服务器交互的服务令牌。 |

{style="table-layout:auto"}

要了解有关数据收集的更多信息，请阅读 [数据收集概述](../../tags/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新的或更新后的目标** {#new-updated-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[！BADGE Beta]{type=Informational} [!DNL Amazon Ads] 连接](../../destinations/catalog/advertising/amazon-ads.md) | 此 [!DNL Amazon Ads] 与Adobe Experience Platform集成现在支持到以下各项的区域路由： [!DNL Amazon Ads] 市场。 有关更多信息，请参阅 [目标更改日志](../../destinations/catalog/advertising/amazon-ads.md#changelog). |

{style="table-layout:auto"}

**新增或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 工作区支持 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 目标。 | 现在，在配置新的Adobe Target目标连接时，您可以选择要将受众共享到的Adobe Target工作区。 请参阅 [连接参数](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) 部分以了解更多信息。 此外，请参阅关于的教程 [配置工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hans) Adobe Target中的，以了解有关工作区的更多信息。 |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 扩展（潜在客户 — 配置文件） | [[!UICONTROL Adobe统一配置文件服务潜在客户 — 配置文件合并扩展]](https://github.com/adobe/xdm/pull/1735/files) | 添加了Prospect-Profile合并架构的必填字段。 |
| 扩展 | [[!UICONTROL 决策资源]](https://github.com/adobe/xdm/pull/1732/files) | 添加数据类型以表示决策中使用的资产。 [!UICONTROL 决策资源] 提供用于呈现以下内容的资源的引用： `decisionItems`. |
| 数据类型 | [[!UICONTROL 商务]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL 商务] 存储与购买和销售活动相关的记录。 |
| 字段组 | [[!UICONTROL 配置文件合作伙伴扩充（示例）]](https://github.com/adobe/xdm/pull/1747/files) | 为配置文件合作伙伴扩充添加了一个示例架构。 |
| 字段组 | [[!UICONTROL Partner Prospect详细信息（示例）]](https://github.com/adobe/xdm/pull/1747/files) | 为数据供应商目标客户配置文件扩展添加了示例架构。 |
| 数据类型 | [[!UICONTROL 商业范围]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL 商业范围] 标识发生事件的位置。 例如，在商店视图、商店或网站中，等等。 |
| 数据类型 | [[!UICONTROL 帐单]](https://github.com/adobe/xdm/pull/1734/files) | 用于一项或多项付款的帐单信息已添加到 [!UICONTROL 商务] 架构。 |

{style="table-layout:auto"}

**更新的XDM组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL MediaAnalytics交互详细信息]](https://github.com/adobe/xdm/pull/1736/files) | 已更改 `bitrateAverageBucket` 从100到“800-899”。 |
| 数据类型 | [[!UICONTROL Qoe数据详细信息]](https://github.com/adobe/xdm/pull/1736/files) | 已更改 `bitrateAverageBucket` 数据类型转换为字符串。 |
| 字段组 | [[!UICONTROL 区段成员资格详细信息]](https://github.com/adobe/xdm/pull/1735/files) | 已添加到目标客户配置文件类。 |
| 架构 | [[!UICONTROL 计算属性系统架构]](https://github.com/adobe/xdm/pull/1735/files) | 身份映射已添加到 [!UICONTROL 计算属性系统架构]. |
| 数据类型 | [[!UICONTROL 内容交付网络]](https://github.com/adobe/xdm/pull/1733/files) | 字段已添加至 [!UICONTROL 会话详细信息] 描述使用的内容交付网络。 |
| 扩展 | [[!UICONTROL Adobe统一配置文件服务帐户合并扩展]](https://github.com/adobe/xdm/pull/1731/files) | 身份映射已添加到 [!UICONTROL Adobe统一配置文件服务帐户合并扩展]. |
| 数据类型 | [[!UICONTROL 订购]](https://github.com/adobe/xdm/pull/1730/files) | `discountAmount` 已添加至 [!UICONTROL 订购]. 这传达了正常订单价格与特殊价格之间的差异。 它应用于整个订单，而不是单个产品。 |
| 架构 | [[!UICONTROL AEP保健操作请求]](https://github.com/adobe/xdm/pull/1728/files) | 此 `targetServices` 添加了字段，以提供处理数据卫生操作的服务的名称。 |
| 数据类型 | [[!UICONTROL 配送]](https://github.com/adobe/xdm/pull/1727/files) | `currencyCode` 已添加到一个或多个产品的配送信息中。 它是用于为产品定价的ISO 4217字母货币代码。 |
| 数据类型 | [[!UICONTROL 应用程序]](https://github.com/adobe/xdm/pull/1726/files) | 此 `language` 添加了字段，以便为应用程序提供用户的语言、地理或文化偏好。 |
| 扩展 | [[!UICONTROL AJO实体字段]](https://github.com/adobe/xdm/pull/1746/files) | [!UICONTROL AJO时间戳实体] 已添加，以指示上次修改消息的时间。 |
| 数据类型 | （多个） | [删除了多个媒体详细信息](https://github.com/adobe/xdm/pull/1739/files) 跨多种数据类型实现一致性。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md)

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform数据湖中查询数据。 您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 内联模板 | 查询服务现在支持使用引用SQL中其他模板的模板。 利用查询中的内联模板，减少工作负载并避免错误。 可以重用语句或条件，并引用嵌套模板以提高SQL的灵活性。 可存储为模板的查询大小或可从原始查询引用的模板数量没有限制。 有关详细信息，请阅读 [内联模板指南](../../query-service/essential-concepts/inline-templates.md). |
| 计划的查询用户界面更新 | 使用，从UI中的某个位置管理所有计划查询 [[!UICONTROL “计划查询”选项卡]](../../query-service/ui/monitor-queries.md#inline-actions). 此 [!UICONTROL 计划的查询] 通过添加内联查询操作和新的查询状态列，UI已得到改进。 最近添加的功能包括启用、禁用和删除计划，或订阅即将运行的查询的警报，直接从 [!UICONTROL 计划的查询] 视图。 <p>![中突出显示的内联操作 [!UICONTROL 计划的查询] 视图。](../../query-service/images/ui/monitor-queries/disable-inline.png "中突出显示的内联操作 [!UICONTROL 计划的查询] 视图。"){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅 [查询服务概述](../../query-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强这些数据。 您可以从多种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics分类源数据流删除支持 | 您现在可以删除使用Adobe Analytics分类作为其源的源数据流。 下 **[!UICONTROL 源]** > **[!UICONTROL 数据流]**，选择所需的数据流，然后选择删除。 有关详细信息，请阅读以下指南： [为Adobe Analytics分类数据创建源连接](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| 过滤支持 [!DNL Microsoft Dynamics] 使用API | 使用逻辑运算符和比较运算符筛选 [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) 源。 有关详细信息，请阅读以下指南： [使用API筛选源的数据](../../sources/tutorials/api/filter.md). |
| [!BADGE 测试版]{type=Informative}[!DNL RainFocus] | 您现在可以使用 [!DNL RainFocus] 源集成，可从以下位置获取事件管理和分析数据： [!DNL RainFocus] 帐户到Experience Platform。 有关详细信息，请阅读 [[!DNL RainFocus] 源概述](../../sources/connectors/analytics/rainfocus.md). |
| 支持Adobe Commerce | 您现在可以使用Adobe Commerce源集成将Adobe Commerce帐户中的数据引入Experience Platform。 有关详细信息，请阅读 [Adobe Commerce源概述](../../sources/connectors/adobe-applications/commerce.md). |
| 支持 [!DNL Mixpanel] | 您现在可以使用 [!DNL Mixpanel] 源集成，从您的网站获取analytics数据 [!DNL Mixpanel] Experience Platform使用API或用户界面的帐户。 有关详细信息，请阅读 [[!DNL Mixpanel] 源概述](../../sources/connectors/analytics/mixpanel.md). |
| 支持 [!DNL Zendesk] | 您现在可以使用 [!DNL Zendesk] 源集成，从您的获取客户成功数据 [!DNL Zendesk] Experience Platform使用API或用户界面的帐户。 有关详细信息，请阅读 [[!DNL Zendesk] 源概述](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).
