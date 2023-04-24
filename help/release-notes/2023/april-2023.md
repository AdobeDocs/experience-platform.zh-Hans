---
title: Adobe Experience Platform发行说明2023年4月
description: 2023年4月的Adobe Experience Platform发行说明。
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 4 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据准备](#data-prep)
- [源](#sources)

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 更新了非生产沙箱中Adobe Analytics的回填期 | 非生产沙箱中Adobe Analytics的回填期已缩短为三个月。 生产沙箱的回填在13个月内保持不变。 此更改仅适用于新流量，不会影响现有流量。 有关更多信息，请阅读 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 用于将FPID字符串转换为ECID的新映射器函数 | 使用 `fpid_to_ecid` 函数将FPID字符串转换为ECID，以用于Experience Platform和Experience Cloud应用程序。 有关更多信息，请阅读 [数据准备功能指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

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
