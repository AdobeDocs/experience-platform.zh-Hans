---
title: Adobe Experience Platform 发行说明
description: 2023年3月版Adobe Experience Platform发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 4 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [Experience Data Model](#xdm)
- [实时客户资料](#profile)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关组织数据的重要分析（在每日快照中捕获）。

**新增功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的功能板 | 您现在可以 **过滤历史数据** ，并使用近期数据或自定义分析时段。<br>您现在也可以 **复制现有小组件**. 通过自定义副本并编辑其属性，可避免在创建新的独特小组件时从头开始重新启动。 |

{style="table-layout:auto"}

有关功能板的更多信息（包括如何授予访问权限和创建自定义小组件），请首先阅读 [功能板概述](../../dashboards/home.md).

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 更新了非生产沙箱中Adobe Analytics的回填期 | 非生产沙箱中Adobe Analytics的回填期已缩短为三个月。 生产沙箱的回填在13个月内保持不变。 此更改仅适用于新流量，不会影响现有流量。 有关更多信息，请阅读 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 用于将FPID字符串转换为ECID的新映射器函数 | 使用 `fpid_to_ecid` 函数将FPID字符串转换为ECID，以用于Experience Platform和Experience Cloud应用程序。 有关更多信息，请阅读 [数据准备功能指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 显示名称切换 | 模式编辑器现在提供了一个切换开关，用于在原始字段名称和更易读的显示名称之间进行更改。 这种灵活性可改进字段发现和编辑架构。 标准字段组的显示名称是系统生成的，但也可以根据需要通过UI进行自定义。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将客户数据整合到统一视图中，为每次客户互动提供一个加盖时间戳的可操作帐户。

**更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 匿名用户档案数据到期 | 现在，通常可以使用假名用户档案数据到期！ 此版本将在启用后，从您的Experience Platform实例中持续删除旧用户档案。 要了解有关此功能和假名用户档案的更多信息，请阅读 [匿名用户档案数据过期指南](../../profile/pseudonymous-profiles.md). |

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持过滤Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud的行级数据的API | 使用逻辑和比较运算符过滤Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud源的行级数据。 阅读 [使用API过滤源的数据](../../sources/tutorials/api/filter.md) 以了解更多信息。 |
| Shopify Streaming的测试版可用性 | 的 [Shopify流源](../../sources/connectors/ecommerce/shopify-streaming.md) 现已在测试版中提供。 使用Shopify流源从Shopify合作伙伴帐户流式传输数据以Experience Platform。 |
| OneTrust集成的一般可用性 | 的 [OneTrust集成源](../../sources/connectors/consent-and-preferences/onetrust.md) 现在为GA。 使用OneTrust集成源将OneTrust集成帐户中的同意和首选项数据Experience Platform。 |
| oracle服务云的正式发布 | 的 [Oracle服务云源](../../sources/connectors/customer-success/oracle-service-cloud.md) 现在为GA。 使用Oracle服务云源将Oracle服务云数据引入Experience Platform。 |

{style="table-layout:auto"}

要进一步了解来源，请阅读 [源概述](../../sources/home.md).