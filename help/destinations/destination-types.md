---
keywords: 目标；目标类型
title: 目标类型和类别
seo-title: Destination types and categories
description: 了解Adobe Experience Platform中的不同目标类型和类别。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 08c6c2716b88180b1eb290663117e6da2d8641f0
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 目标类型和类别

请阅读本页以了解Adobe Experience Platform目标的不同类型和类别。

## 目标类型

在Adobe Experience Platform中，我们区分两种目标类型 — 连接和扩展。 有两种类型的连接目标：配置文件导出目标和区段导出目标。

![目标类型](./assets/destination-types/types-of-destinations.png)

## 连接 {#connections}

**[!UICONTROL 配置文件导出]** 和 **[!UICONTROL 流区段导出]** Adobe Experience Platform中的目标捕获事件数据，将其与其他数据源组合以形成 [实时客户资料](../profile/home.md)、应用分段，并将区段和符合条件的用户档案导出到目标。

## 配置文件导出目标

配置文件导出目标会接收原始数据，通常以电子邮件地址作为主键。 Experience Platform当前支持两种类型的配置文件导出目标：

* [流配置文件导出目标](#streaming-profile-export)
* [批量（基于文件）目标](#file-based)

### 流配置文件导出目标 {#streaming-profile-export}

流配置文件导出目标将区段和配置文件数据作为Experience Platform数据流接收。 [AmazonKinesis](catalog/cloud-storage/amazon-kinesis.md) 和 [Azure事件中心](catalog/cloud-storage/azure-event-hubs.md) 是此类目标的示例。

### 批量（基于文件）目标 {#file-based}

基于文件的目标接收 `.csv` 包含配置文件和/或属性的文件。 [Amazon S3](catalog/cloud-storage/amazon-s3.md) 是一个可导出包含配置文件导出的文件的目标示例。

## 流区段导出目标 {#streaming-destinations}

区段导出目标可接收Experience Platform区段数据。 这些目标使用区段ID或用户ID。 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)，以及此类目标的示例。

## 配置文件导出和区段导出目标 — 视频概述 {#video}

以下视频将向您介绍两种目标类型的特性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 扩展 {#extensions}

平台利用标签管理的强大功能和灵活性，允许您在数据收集UI中配置标签扩展。

>[!TIP]
>
>有关标记扩展的详细信息（包括用例以及如何在界面中查找它们），请参阅 [标记扩展概述](./catalog/launch-extensions/overview.md).

标记扩展可将原始事件数据转发到多种类型的目标。 将扩展视为 **事件转发** 目标类型。 这是与目标平台的更简单集成类型，目标平台仅转发原始事件数据。 例如 [Gainsight个性化扩展](./catalog/personalization/gainsight.md) 或 [确认客户扩展的声音](./catalog/voice/confirmit-digital-feedback.md).

![标记扩展与其他目标的比较](./assets/common/launch-and-other-destinations.png)

## 何时使用连接和扩展 {#when-to-use}

作为营销人员，您可以使用连接和扩展的组合来解决您的用例。

如果需要利用完整的集中式客户配置文件或客户区段进行激活，则连接非常有用。 例如，如果您从分析系统将行为数据与已上传的CRM数据联接在一起，以便在向该用户发送个性化消息之前，将用户限定为给定区段，则使用连接。

当事件数据用于触发操作或在外部环境中执行分段时，扩展非常有用。 例如，如果行为数据需要转发到外部系统，而不需要连接到给定用户的文件上的其他数据源。

## 目标类别 {#categories}

中的连接和扩展 [目标目录](https://platform.adobe.com/destination/catalog) 按目标类别(**广告**, **云存储**, **调查平台**, **电子邮件营销**&#x200B;等)，具体取决于他们帮助您实现的营销操作。 有关每个类别以及每个类别中包含的目标的更多信息，请参阅 [目标目录文档](./catalog/overview.md).

![目标类别](./assets/destination-types/destination-categories-menu.png)
