---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: 准备要在智能服务中使用的数据
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1d827d1637da05d3d2afc338f48911bb23039949

---


# 准备要在智能服务中使用的数据

为了让智能服务从您的营销事件数据中发掘洞察，数据必须在语义上得到丰富并以标准结构进行维护。 智能服务利用体验数据模型(XDM)模式来实现这一点。 具体而言，智能服务中使用的所有数据集必须符合消费者体 **验事件(CEE)** XDM模式。

本文档提供有关将营销事件数据从多个渠道映射到本模式的一般指导，概述有关该模式中重要字段的信息，以帮助您确定如何将数据有效地映射到其结构。

## 了解CEE模式

消费者体验事件模式描述个人的行为，因为它与数字营销事件（Web或移动）以及在线或离线商务活动相关。 智能服务需要使用此模式，因为其语义上定义良好的字段（列），从而避免了任何未知名称，否则这些名称会使数据变得不那么清晰。

与所有XDM模式一样，CEE mixin是可扩展的。 换句话说，可以向CEE mixin添加其他字段，如果需要，可以在多个模式中包含不同的变体。

可以在公共XDM存储库中找到混音的完整示例 [](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)，并应用作以下部分概述的关键字段的引用。

### 关键字段

下表突出显示了CEE Mix中应用的关键字段，以便智能服务生成有用的洞察，包括说明和指向参考文档的链接，以便进一步示例。

| XDM字段 | 描述 | 参考 |
| --- | --- | --- |
| `xdm:channel` | 与ExperienceEvent相关的营销渠道。 该字段包含有关渠道类型、媒体类型和位置类型的信息。 **必须提&#x200B;_供此字段_，才能让归因AI处理您的数据**。 有关某些 [示例映射](#example-channels) ，请参阅下表。 | [体验渠道模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | 代表客户选择的产品的一组项目，包括产品SKU、名称、价格和数量。 | [商务详细信息模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | 包含有关ExperienceEvent的商务特定信息，包括采购订单编号和付款信息。 | [商务详细信息模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | 表示与ExperienceEvent相关的Web详细信息，如交互、页面详细信息和推荐人。 | [ExperienceEvent Web详细信息模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### 示例渠道 {#example-channels}

该字 `xdm:channel` 段表示与ExperienceEvent相关的营销渠道。 下表提供了映射到XDM的营销渠道的一些示例：

| Channel | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | 付费 | 搜索 | 单击 |
| 社交——营销 | 免费 | 社交 | 单击 |
| 显示 | 付费 | 显示 | 单击 |
| 电子邮件 | 付费 | 电子邮件 | 单击 |
| 内部推荐人 | 自有 | 直接 | 单击 |
| 显示浏览 | 付费 | 显示 | 印象 |
| QR码重定向 | 自有 | 直接 | 单击 |
| SMS文本消息 | 自有 | SMS | 单击 |
| 移动设备 | 自有 | 移动 | 单击 |

## 映射和摄取数据

一旦您确定时间序列数据是否可以映射到CEE模式，您就可以开始将数据引入智能服务的过程。 联系Adobe咨询服务，帮助将数据映射到模式并将其引入服务。

如果您拥有Adobe Experience Platform订阅并希望自己映射和摄取数据，请按照以下部分中所述的步骤操作。

### 使用Adobe Experience Platform

>[!NOTE] 以下步骤需要订阅到Experience Platform。 如果您无权访问平台，请跳到下一步 [部分](#next-steps) 。

本节概述了将数据映射到Experience Platform以用于智能服务的工作流程，包括指向教程的详细步骤链接。

#### 创建CEE模式和数据集

当您准备好开始准备数据以进行摄取时，第一步是创建一个使用CEE混音的新XDM模式。 以下教程将逐步介绍在UI或API中创建新模式的过程：

* [在UI中创建模式](../xdm/tutorials/create-schema-ui.md)
* [在API中创建模式](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] 以上教程遵循了创建模式的通用工作流程。 为模式选择类时，必须使用 **XDM ExperienceEvent类**。 选择此类后，您可以将CEE混音添加到模式。

在将CEE混音添加到模式后，您可以根据数据中其他字段的需要添加其他混音。

创建并保存模式后，您可以基于该模式创建新数据集。 以下教程将逐步介绍在UI或API中创建新数据集的过程：

* [在UI中创建数据集](../catalog/datasets/user-guide.md#create) (按照工作流使用现有模式)
* [在API中创建数据集](../catalog/datasets/create.md)

#### 映射和摄取数据

创建CEE模式和数据集后，您可以开始将数据表映射到模式，并将该数据引入平台。 有关如何在UI [中执行此操作的步骤](../ingestion/tutorials/map-a-csv-file.md) ，请参阅有关将CSV文件映射到XDM模式的教程。 在填充数据集后，可以使用同一数据集摄取其他数据文件。

## 后续步骤 {#next-steps}

本文档为准备要在智能服务中使用的数据提供了一般指导。 如果您需要根据您的用例进行其他咨询，请联系Adobe咨询支持。

成功填充包含客户体验数据的数据集后，您便可以使用Intelligent Services生成洞察。 请参阅以下文档以开始：

* [归因人工智能概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
