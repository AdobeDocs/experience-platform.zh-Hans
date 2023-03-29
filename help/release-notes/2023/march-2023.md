---
title: Adobe Experience Platform发行说明2023年2月
description: 2023年3月版Adobe Experience Platform发行说明。
source-git-commit: 44075e38664c01c64e7d09f5856353bff64becb5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 3 月 29 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [分段服务](#segmentation)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 新的元转化API（测试版）快速入门工作流 | 从数据收集主屏幕中访问位于“快速入门”下的新快速入门工作流！ 的 [元转化API快速启动工作流](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 使客户能够在服务器端快速收集和转发事件数据到元数据，以便只需几个简单的步骤即可进行广告转化。 |
| [!DNL Braze] 事件转发扩展 | 的 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件转发扩展允许您利用在Adobe Experience Platform边缘网络中捕获的数据，并将其发送到 [!DNL Braze] 以服务器端事件的形式使用 [!DNL Braze] 用户跟踪API。 |
| [!DNL Mixpanel] 事件转发扩展 | 的 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 扩展允许客户利用事件转发在Adobe Experience Platform边缘网络中捕获事件信息，并使用跟踪事件API将其发送到Mixpanel。 |

{style="table-layout:auto"}

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 用于编码和解码URL字符串的新函数 | <ul><li>的 `get_url_encoded` 函数将URL作为输入，并用ASCII字符替换或编码特殊字符。</li><li>的 `get_url_decoded` 函数将URL作为输入，并将ASCII字符解码为特殊字符。</li></ul> 有关更多信息，请阅读 [数据准备功能指南](../../data-prep/functions.md). 有关保留字符及其相应编码字符的完整列表，请阅读 [特殊字符](../../data-prep/functions.md#special-characters). |

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 配置文件量度 | 为了更准确地表示用户档案量度，会将会员资格划分和流失量度组合在一起，现在会在24小时内计算这些量度。 有关更多信息，请参阅 [分段UI指南](../../segmentation/ui/overview.md) |

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
