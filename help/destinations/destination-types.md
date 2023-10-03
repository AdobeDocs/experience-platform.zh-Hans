---
keywords: 目标；目标；目标类型
title: 目标类型和类别
description: 了解Adobe Experience Platform中目标的各种类型和类别。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# 目标类型和类别

请阅读本页，了解Adobe Experience Platform目标的各种类型和类别。

## 目标类型 {#destination-types}

在Adobe Experience Platform中，我们会区分不同的目标类型，即连接、数据集导出和扩展。 有多种类型的连接目标，允许您将数据导出到基于API的目标。

最后，还可以区分目标目录中所有组织内可用的公共目标与Real-Time CDP Ultimate客户为满足其特定导出用例而可以创建的专用目标。

![目标图类型。](./assets/destination-types/types-of-destinations-no-highlight.png)

## 连接 {#connections}

**[!UICONTROL 配置文件导出]**， **[!UICONTROL 流受众导出]**、和 **[!DNL Edge Personalization]** Adobe Experience Platform中的目标会捕获事件数据，并将其与其他数据源结合以形成 [Real-time Customer Profile](../profile/home.md)，应用分段，并将受众和符合条件的配置文件导出到目标。

## 配置文件导出目标 {#profile-export}

配置文件导出目标会接收原始数据，通常使用电子邮件地址作为主键。 Experience Platform当前支持两种类型的配置文件导出目标：

* [流配置文件导出目标（企业目标）](#streaming-profile-export)
* [批处理（基于文件）目标](#file-based)

### 流配置文件导出目标（企业目标） {#streaming-profile-export}

>[!IMPORTANT]
>
>企业目标或流配置文件导出目标可用于 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 仅限客户。

使用企业目标Data Connectors近乎实时地将Adobe Real-time Customer Data Platform配置文件交付到内部系统或其他第三方系统，以便进行数据同步、分析和进一步扩充配置文件用例。

这些目标将接收受众和配置文件数据作为Experience Platform数据流。

企业目标包括：

* [HTTP API目标](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure事件中心](catalog/cloud-storage/azure-event-hubs.md)

### 批处理（基于文件）目标 {#file-based}

基于文件的目标将接收 `.csv` 包含配置文件和/或属性的文件。 [Amazon S3](catalog/cloud-storage/amazon-s3.md) 是一个目标示例，您可以在其中导出包含配置文件导出的文件。

## 流受众导出目标 {#streaming-destinations}

受众导出目标接收Experience Platform的受众数据。 这些目标使用受众ID或用户ID。 广告和社交目标，如 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md)， [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)，或 [facebook](catalog/social/facebook.md) 是此类目标的示例。

## Edge个性化目标 {#edge-personalization-destinations}

Experience Platform中的边缘个性化目标包括 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化目标](/help/destinations/catalog/personalization/custom-personalization.md). 通过使用这些目标，您可以为客户启用同一页面和下一页面个性化用例。

详细了解如何 [为同一页面和下一页面个性化配置个性化目标](/help/destinations/ui/activate-edge-personalization-destinations.md).

## 配置文件导出和受众导出目标 — 视频概述 {#video}

以下视频介绍这两种类型目标的特性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 数据集导出目标 {#dataset-export-destinations}

目标目录中的某些云存储目标支持数据集导出。 使用这些目标可将原始数据集导出到云存储位置。

详细了解如何 [导出数据集](/help/destinations/ui/export-datasets.md).

## 扩展 {#extensions}

Platform利用标记管理的强大功能和灵活性，允许您在UI中配置标记扩展。

>[!TIP]
>
>有关标记扩展的详细信息（包括用例以及如何在界面中查找它们），请参阅 [标记扩展概述](./catalog/launch-extensions/overview.md).

标记扩展可将原始事件数据转发到多种类型的目标。 将扩展视为 **事件转发** 目标的类型。 这是一种与目标平台更简单的集成，目标平台仅转发原始事件数据。 这些示例包括 [Gainsight个性化扩展](./catalog/personalization/gainsight.md) 或 [确认客户分机的声音](./catalog/voice/confirmit-digital-feedback.md).

![将标记扩展与其他目标进行比较](./assets/common/launch-and-other-destinations.png)

## 何时使用连接和扩展 {#when-to-use}

作为营销人员，您可以结合使用连接和扩展来解决用例问题。

当需要利用完整的集中式客户配置文件或客户受众进行激活时，连接会很有用。 例如，如果要将来自分析系统的行为数据与上传的CRM数据联接，则使用连接来使用户符合给定受众的资格，然后再向该用户投放个性化消息。

当使用事件数据来触发操作或在外部环境中进行分段时，扩展很有用。 例如，如果需要将行为数据转发到外部系统，而无需将其连接到给定用户的文件上的其他数据源。

## 目标类别 {#categories}

中的连接和扩展 [目标目录](https://platform.adobe.com/destination/catalog) 按目标类别分组(**广告**， **云存储**， **调查平台**， **电子邮件营销**&#x200B;等)，具体取决于他们帮助您实现的营销活动。 有关每个类别以及每个类别中包含的目标的详细信息，请参阅 [目标目录文档](./catalog/overview.md).

![目录页面中高亮显示的目标类别。](./assets/destination-types/destination-categories-menu.png)
