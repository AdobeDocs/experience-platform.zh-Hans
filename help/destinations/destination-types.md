---
keywords: 目标；目标；目标类型
title: 目标类型和类别
description: 了解Adobe Experience Platform中目标的各种类型和类别。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 1%

---

# 目标类型和类别

请阅读本页，了解Adobe Experience Platform目标的各种类型和类别。

## 目标类型 {#destination-types}

在Adobe Experience Platform中，我们会区分不同的目标类型，即连接、数据集导出和扩展。 有多种类型的连接目标，可让您将数据导出到基于API的目标、社交目标、CRM平台等。

最后，还可以区分目标目录中所有组织内可用的公共目标与Real-Time CDP Ultimate客户为满足其特定导出用例而可以创建的专用目标，这两者之间的连接。

>[!BEGINSHADEBOX]

![目标图类型。](./assets/destination-types/types-of-destinations-no-highlight.png "目标图类型。"){zoomable="yes"}

>[!ENDSHADEBOX]

## 连接 {#connections}

Adobe Experience Platform捕获事件数据中的&#x200B;**[!UICONTROL 配置文件导出]**、**[!UICONTROL 流式受众导出]**&#x200B;和&#x200B;**[!DNL Edge Personalization]**&#x200B;目标，将其与其他数据源组合以形成[实时客户配置文件](../profile/home.md)，应用分段，并将受众和符合条件的配置文件导出到目标。

## 配置文件导出目标 {#profile-export}

配置文件导出目标会接收原始数据，通常使用电子邮件地址作为主键。 Experience Platform当前支持两种类型的配置文件导出目标：

* [批处理（基于文件）目标](#file-based)
* [高级企业目标（流配置文件导出目标）](#advanced-enterprise-destinations)

### 高级企业目标（流配置文件导出目标） {#advanced-enterprise-destinations}

>[!IMPORTANT]
>
>高级企业目标或流式配置文件导出目标仅适用于[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)客户。

使用高级企业目标数据连接器近乎实时地将Adobe Real-Time Customer Data Platform配置文件交付给内部系统或其他第三方系统，以便进行数据同步、分析和进一步扩充配置文件用例。

这些目标会作为Experience Platform数据流接收受众和配置文件数据。

高级企业目标包括：

* [HTTP API目标](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure 事件中心](catalog/cloud-storage/azure-event-hubs.md)

### 批处理（基于文件）目标 {#file-based}

基于文件的目标接收包含配置文件和/或属性的`.csv`文件。 [Amazon S3](catalog/cloud-storage/amazon-s3.md)是导出包含配置文件导出的文件的目标示例。

## 流受众导出目标 {#streaming-destinations}

受众导出目标接收Experience Platform受众数据。 这些目标使用受众ID或用户ID。 Advertising和社交目标（如[[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md)、[[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)或[Facebook](catalog/social/facebook.md)）就是此类目标的示例。

## Edge个性化目标 {#edge-personalization-destinations}

Experience Platform中的Edge个性化目标包括[Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)和[自定义个性化目标](/help/destinations/catalog/personalization/custom-personalization.md)。 通过使用这些目标，您可以为客户启用同一页面和下一页面个性化用例。

阅读有关如何[为同一页面和下一页面个性化](/help/destinations/ui/activate-edge-personalization-destinations.md)配置个性化目标的更多信息。

## 配置文件导出和受众导出目标 — 视频概述 {#video}

以下视频介绍这两种类型目标的特性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 导出的受众的类型 {#exported-audiences-types}

您可以将三种类型的受众从Experience Platform导出到不同的目标：

* 人员受众
* 帐户受众
* 潜在客户受众

了解有关[各种受众类型](/help/segmentation/types/account-audiences.md#terminology)的更多信息。

目标卡上的符号显示了您可以导出到每个目标的受众类型。

![带有符号的目标卡片示例显示了可以导出的受众类型。](/help/destinations/assets/destination-types/types-of-audiences.png "带有符号的目标卡片示例显示了可以导出的受众类型。"){zoomable="yes"}


## 数据集导出目标 {#dataset-export-destinations}

目标目录中的某些云存储目标支持数据集导出。 使用这些目标可将原始数据集导出到云存储位置。

阅读有关如何[导出数据集](/help/destinations/ui/export-datasets.md)的详细信息。

## 扩展 {#extensions}

Platform利用标记管理的强大功能和灵活性，允许您在UI中配置标记扩展。

>[!TIP]
>
>有关标记扩展的详细信息，包括用例以及如何在界面中查找它们，请参阅[标记扩展概述](./catalog/launch-extensions/overview.md)。

标记扩展可将原始事件数据转发到多种类型的目标。 将扩展视为&#x200B;**事件转发**&#x200B;类型的目标。 这是一种与目标平台更简单的集成，目标平台仅转发原始事件数据。 例如，[Gainsight个性化扩展](./catalog/personalization/gainsight.md)或客户扩展的[Confirmit Voice](./catalog/voice/confirmit-digital-feedback.md)。

![标记扩展与其他目标的比较](./assets/common/launch-and-other-destinations.png)

## 何时使用连接和扩展 {#when-to-use}

作为营销人员，您可以结合使用连接和扩展来解决用例问题。

当需要利用完整的集中式客户配置文件或客户受众进行激活时，连接会很有用。 例如，如果要将来自分析系统的行为数据与上传的CRM数据联接，则使用连接来使用户符合给定受众的资格，然后再向该用户投放个性化消息。

当使用事件数据来触发操作或在外部环境中进行分段时，扩展很有用。 例如，如果需要将行为数据转发到外部系统，而无需将其连接到给定用户的文件上的其他数据源。

## 目标类别 {#categories}

[目标目录](https://platform.adobe.com/destination/catalog)中的连接和扩展按目标类别(**Advertising**、**Cloud Storage**、**调查平台**、**电子邮件营销**&#x200B;等)分组，具体取决于它们帮助您实现的营销操作。 有关每个类别以及每个类别中包含的目标的详细信息，请参阅[目标目录文档](./catalog/overview.md)。

![目录页面中突出显示的目标类别。](./assets/destination-types/destination-categories-menu.png "目录页面中突出显示的目标类别。"){zoomable="yes"}
