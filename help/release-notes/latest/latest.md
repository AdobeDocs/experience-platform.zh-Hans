---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年7月版发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 134c18822350a0032bb9957e6e0d1ab888c6b289
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 33%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 7 月 26 日**

Adobe Experience Platform 中现有功能的更新：

- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 标记和事件转发 | 数据收集审核日志 | 您现在可以看到何时执行了某个操作，以及谁在标记和事件转发中执行了此操作。 这有助于产品故障排除、正确治理和内部审计活动。 此审核数据通过上下文中的滑出菜单显示，这些菜单还包括快速操作和资源状态更新。 可在标记和事件转发 UI 中的以下屏幕上看到这些数据：<br><ul><li>[属性概述](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[规则](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[数据元素](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[扩展](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[库审核](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[库上次构建和发布](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| 数据流 | [地理查找](../../datastreams/configure.md#advanced-options) | 您现在可以为数据流配置地理位置和网络查找以包含以下信息： <ul><li>国家/地区</li><li>邮政编码</li><li>省/市/自治区</li><li>DMA</li><li>城市</li><li>纬度 </li><li>经度</li><li>运营商</li><li>Domain</li><li>ISP</li></ul> 您有责任确保已获得适用法律和法规规定的收集、处理和传输个人数据（包括精确的地理位置信息）所需的所有必要权限、同意、许可和授权。 <br> 您的IP地址模糊处理选择不会影响将从IP地址派生并发送到配置的Adobe解决方案的地理位置信息级别。 必须单独限制或禁用地理位置查找。 <br> 请参阅 [数据流文档](../../datastreams/configure.md#advanced-options) 以了解更多详细信息。 |

{style="table-layout:auto"}

欲知有关数据收集的更多信息，请阅读 [数据集合概述](../../tags/home.md).

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 新的映射器函数 | 现在，在数据准备中映射对象时，可以使用以下函数： <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> 有关这些功能的详细信息，请参阅 [数据准备函数指南](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

有关数据准备的详细信息，请阅读[数据准备概述](../../data-prep/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在以下位置的数据分段： [!DNL Experience Platform] 将个人（如客户、潜在客户、用户或组织）关联到受众中的活动。 您可以通过区段定义创建受众，或从以下来源创建受众： [!DNL Real-Time Customer Profile] 数据。 这些受众可在以下位置集中配置和维护： [!DNL Platform]和可供任何Adobe解决方案轻松访问。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| Audience 门户 | Audience Portal提供了新的浏览体验，可用于在Adobe Experience Platform中访问、创建和管理受众。 在Audience Portal中，您可以查看平台生成和外部生成的受众；通过筛选、文件夹和标记提高工作效率；创建平台生成的受众；以及通过CSV文件导入外部生成的受众。 欲知受众门户的更多信息，请阅读 [分段服务UI指南](../../segmentation/ui/overview.md). |
| 受众组合 | 受众构成提供了一个易于使用的工作区，通过用来表示不同操作的块来构建和编辑受众。 有关受众构图的更多信息，请参阅 [受众合成UI指南](../../segmentation/ui/audience-composition.md). |

有关的详细信息 [!DNL Segmentation Service]，请阅读 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | 您现在可以使用 [[!DNL SAP Commerce] 源](../../sources/connectors/ecommerce/sap-commerce.md) 将订阅账单数据从贵机构的 [!DNL SAP Commerce] 帐户到Experience Platform。 |
| 支持 [!DNL Phoenix] | 您现在可以使用 [[!DNL Phoenix] 源](../../sources/connectors/databases/phoenix.md) 以从您的 [!DNL Phoenix] Experience Platform数据库。 |
| 身份验证更新 [!DNL Salesforce] 和 [!DNL Salesforce Service Cloud] | 您现在可以指定的API版本 [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 和 [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) 使用Experience PlatformUI或验证新帐户时的来源 [!DNL Flow Service] API。 |

{style="table-layout:auto"}

欲知关于来源的更多信息，请阅读 [源概述](../../sources/home.md).
