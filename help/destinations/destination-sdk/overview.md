---
description: Adobe Experience Platform Destination SDK是一组配置API，允许您配置目标集成模式，以便Experience Platform根据所选的数据和身份验证格式将受众和配置文件数据交付到端点。 这些配置存储在Experience Platform中，可通过API进行检索以进行其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: abc9b9857e4a93a334440e855ca0ae562c695df1
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 3%

---

# Adobe Experience Platform Destination SDK

## 概述 {#destinations-sdk}

Adobe Experience Platform Destination SDK是一组配置API，允许您配置目标集成模式，以便Experience Platform根据所选的数据和身份验证格式将受众和配置文件数据交付到端点。 这些配置存储在Experience Platform中，可通过API进行检索以进行其他更新。

本Destination SDK文档提供了相关说明，供您使用这些Adobe Experience Platform Destination SDK配置、测试和发布与Adobe Experience Platform的已产品化目标集成，并让您的目标成为不断增长的目标目录的一部分。

![目标目录概述](./assets/destinations-catalog-overview.png)

## 产品化和自定义集成 {#productized-custom-integrations}

作为Destination SDK合作伙伴，您可以从将按产品分类的目标添加到 [Experience Platform目录](/help/destinations/catalog/overview.md):
1. 通过预配置的参数跨客户标准化集成配置，并简化客户的设置体验。
2. 在Experience Platform目标目录中引入品牌目标卡，以简化客户设置和意识。
3. 作为与Adobe Experience Platform和Real-time Customer Data Platform的产品化目标集成。

作为Experience Platform客户，您可以创建自己的专用自定义目标，最适合您的激活需求。

![Destination SDK可视化图表](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## 支持的集成类型 {#supported-integration-types}

通过Destination SDK,Adobe Experience Platform支持与具有REST API端点的目标进行实时集成。 与Experience Platform的实时集成支持以下功能：
* 报文转换和聚合
* 用户档案回填
* 可配置的元数据集成，用于初始化受众设置和数据传输
* 可配置身份验证
* 一套测试和验证API，可供您测试和迭代目标配置

请阅读 [集成先决条件](./integration-prerequisites.md) 文章。


## 获取Destination SDK {#get-access}

Destination SDK访问权限因您作为合作伙伴或Experience Platform客户的状态而异。 有关详细信息，请参阅下表。


| 合作伙伴或客户的类型 | 如何访问Destination SDK |
---------|----------|
| 独立软件供应商(ISV) | 加入 [Adobe交换计划](https://partners.adobe.com/exchangeprogram/experiencecloud.html) 和请求，以便配置Experience Platform沙盒以访问Destination SDK。 |
| 系统集成商(SI) | 您需要在 [Adobe解决方案合作伙伴计划](https://solutionpartners.adobe.com/home.html)，您将获得一个Experience Platform沙盒，并有权访问Destination SDK。 |
| Experience Platform客户 [激活包](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | 默认情况下，您可以访问Experience Platform沙箱和Destination SDK。 |
| Experience Platform客户 [Real-time CDP Ultimate软件包](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 您无权访问Destination SDK，但有权访问由其他使用Destination SDK的公司配置并在Experience Platform组织中发布的所有产品化目标。 |

{style=&quot;table-layout:auto&quot;}

## 高级流程 {#process}

在Experience Platform中配置目标的过程如下所述：

1. 如果您是ISV或SI，请参阅上述部分中的获取访问信息。 [Adobe Experience Platform激活](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) 客户可以跳过此步骤。
2. [请求配置Experience Platform沙盒](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 并启用目标创作权限。
3. [构建集成](./configure-destination-instructions.md) 遵循产品文档。
4. [测试集成](./test-destination.md) 遵循产品文档。
5. [提交集成](./submit-destination.md) 供Adobe审阅（标准响应时间为五个工作日）。
6. 如果您是ISV或SI创建 [产品化集成](./overview.md#productized-custom-integrations)，则使用 [自助文档流程](./docs-framework/documentation-instructions.md) 在Experience League上为您的目标创建产品文档页面。
7. 获得Adobe批准后，您的集成将显示在 [Experience Platform目录](/help/destinations/catalog/overview.md).
8. 如果您想要更新集成，请遵循相同的流程。

## 参考 {#reference}

Adobe建议您阅读并了解以下Experience Platform文档：

* [Adobe Experience Platform目标概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM架构组合的基础](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans)
* [身份命名空间概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)
