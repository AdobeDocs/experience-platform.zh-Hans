---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年6月版发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a03d0eeab5ca42225705fdeab692020b1641395d
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 6 月 21 日**

Adobe Experience Platform 现有功能的更新包括：

- [对Experience PlatformAPI的身份验证](#authentication-platform-apis)
- [数据收集](#data-collection)
- [目标](#destinations)
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
| 标记和事件转发 | 用户归因 | 用户归因可跨以下各项提供关键活动数据： [标记](../../tags/home.md) 和 [事件转发](../../tags/ui/event-forwarding/overview.md) UI。<br><br>数据包括谁在何时做出了哪些更改。 此数据可在以下屏幕中的标记和事件转发UI中看到：<br><ul><li> 属性概述</li><li> 已安装的扩展</li><li>规则比较和审查</li><li>数据元素比较审查</li><li>扩展比较审查</li><li>库资源更改</li><li>上次生成和发布的库</li></ul> |

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
| 工作区支持 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 目标。 | 现在，在配置新的Adobe Target目标连接时，您可以选择要将受众共享到的Adobe Target工作区。 请参阅 [连接参数](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) 部分以了解更多信息。 此外，请参阅关于的教程 [配置工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) Adobe Target中的，以了解有关工作区的更多信息。 |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform数据湖中查询数据。 您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。&#x200B;
**更新的功能**
&#x200B; |功能 |描述 | | — | — | |&#x200B;内联模板 |查询服务现在支持使用引用SQL中其他模板的模板。 利用查询中的内联模板，减少工作负载并避免错误。 可以重用语句或条件，并引用嵌套模板以提高SQL的灵活性。 可存储为模板的查询大小或可从原始查询引用的模板数量没有限制。 有关详细信息，请阅读 [内联模板指南](../../query-service/essential-concepts/inline-templates.md). | |计划的查询用户界面更新 |使用，从UI中的一个位置管理所有计划查询 [[!UICONTROL “计划查询”选项卡]](../../query-service/ui/monitor-queries.md#inline-actions). 此 [!UICONTROL 计划的查询] 通过添加内联查询操作和新的查询状态列，UI已得到改进。 最近添加的功能包括启用、禁用和删除计划，或订阅即将运行的查询的警报，直接从 [!UICONTROL 计划的查询] 视图。 <p>![中突出显示的内联操作 [!UICONTROL 计划的查询] 视图。](../../query-service/images/ui/monitor-queries/disable-inline.png "中突出显示的内联操作 [!UICONTROL 计划的查询] 视图。"){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
有&#x200B;关查询服务的更多信息，请参阅 [查询服务概述](../../query-service/home.md).

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
