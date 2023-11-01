---
description: Adobe Experience Platform Destination SDK是一组配置API，允许您为Experience Platform配置目标集成模式，以根据所选的数据和身份验证格式将受众和配置文件数据传送到端点或存储位置。 配置存储在Experience Platform中，可以通过API检索以获取其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 4%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK是一套配置API，允许您配置目标集成模式以便Experience Platform根据所选的数据和身份验证格式将受众和配置文件数据传送到端点或存储位置。 配置存储在Experience Platform中，可以通过API检索以获取其他更新。

该Destination SDK文档为您提供了相关说明，指导您使用Adobe Experience Platform Destination SDK配置、测试和发布与Adobe Experience Platform的生产化目标集成，并让您的目标成为不断增长的目标目录的一部分。 通过使用Destination SDK，您还可以创建自己的自定义专用目标，以导出根据您的需求定制的数据。

![Experience PlatformUI的屏幕快照，显示目标目录](assets/destinations-catalog-overview.png)

## 生产和自定义集成 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 创建专用自定义目标的此功能仅适用于 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

作为Destination SDK合作伙伴，您可以通过将按产品划分的目标添加到 [Experience Platform目录](../catalog/overview.md)：

1. 使用预配置的参数标准化跨客户的集成配置并简化客户的设置体验。
2. 在Experience Platform目标目录中引入品牌目标卡，以简化客户设置和意识。
3. 作为与Adobe Experience Platform和Adobe Real-time Customer Data Platform的产品化目标集成而受到追捧。

作为Experience Platform客户，您还可以创作自己的专用自定义目标，这最适合您的激活需求。

![概览图显示了目标开发人员如何与Destination SDK进行交互，以及Real-Time CDP客户如何从生产目标和私有目标中受益。](assets/destination-sdk-visual.png)

## 支持的集成类型 {#supported-integration-types}

### 实时（流）集成 {#real-time-integrations}

通过Destination SDK，Adobe Experience Platform支持与具有REST API端点的目标的实时（也称为流）集成。 与Experience Platform的实时集成支持以下功能：

* 报文转换和聚合
* 配置文件回填
* 可配置的元数据集成可初始化受众设置和数据传输
* 可配置的身份验证
* 一套测试和验证API，可供您测试和迭代目标配置

### 基于文件的集成 {#file-based-integrations}

通过Destination SDK，您还可以设置集成，以定期将文件导出到您选择的存储位置。 基于文件与Experience Platform的集成支持以下功能：

* 以多种支持的格式(CSV、Parquet、JSON)导出文件
* 可配置的文件格式选项，利用这些选项可构建导出文件的格式以满足下游需求。

在中阅读有关目标方面的技术要求 [集成先决条件](integration-prerequisites.md) 文章并阅读 [配置选项](functionality/configuration-options.md) 文章

## 获取对Destination SDK的访问权限 {#get-access}

Destination SDK访问权限因您作为合作伙伴或Experience Platform、Real-Time CDP客户的身份而异。 有关更多信息，请参阅下表。

| 合作伙伴或客户的类型 | 如何访问Destination SDK |
---------|----------|
| 独立软件供应商(ISV) | 加入 [Adobe技术合作伙伴计划](https://partners.adobe.com/technologyprogram/experiencecloud.html) 并请求配置一个Experience Platform沙盒以访问Destination SDK。 |
| 系统集成商(SI) | 您需要在 [Adobe解决方案合作伙伴计划](https://solutionpartners.adobe.com/home.html)，您将获得配置的Experience Platform沙盒以及对Destination SDK的访问权限。 |
| Experience Platform客户于 [Real-Time CDP Ultimate包](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 默认情况下，您有权访问Experience Platform沙盒和Destination SDK，从而允许您为组织构建专用目标。 |

{style="table-layout:auto"}

## 高级流程 {#process}

在Experience Platform中配置目标的过程概述如下：

1. 如果您是ISV或SI，请参见 [获取访问权限](#get-access) 的信息。 [Real-Time CDP Ultimate包](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户可跳过此步骤。
2. [请求配置Experience Platform沙盒](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 并启用目标创作权限。
3. 构建集成。 按照产品文档中的说明进行配置 [流目标](guides/configure-destination-instructions.md) 或 [基于文件的目标](guides/configure-file-based-destination-instructions.md).
4. 测试您的集成。 按照产品文档中的说明进行测试 [流目标](testing-api/streaming-destinations/streaming-destination-testing-overview.md) 或 [基于文件的目标](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. 如果您是ISV或SI，请创建 [产品化集成](./overview.md#productized-custom-integrations)， [提交集成](guides/submit-destination.md) Adobe的审查（标准响应时间为五个工作日）。
6. 如果您是创建产品化集成的ISV或SI，请使用 [自助式文档流程](docs-framework/documentation-instructions.md) 创建产品文档页面，了解目标的Experience League。
7. 对于产品化集成，一经Adobe批准，您的集成将显示在 [Experience Platform目录](../catalog/overview.md).
8. 如果要更新集成，请按照相同的流程操作。

## 参考 {#reference}

Adobe建议您阅读并了解以下Experience Platform文档：

* [Adobe Experience Platform目标概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=zh-Hans)
* [XDM模式组合的基础](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans)
* [身份命名空间概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)
