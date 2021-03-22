---
keywords: 目标；目标；目标类型
title: 目标类型和类别
seo-title: 目标类型和类别
description: 了解Adobe Experience Platform中不同类型和类别的目标。
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# 目标类型和类别

阅读本页，了解Adobe Experience Platform目标的不同类型和类别。

## 目标类型

在Adobe Experience Platform中，我们区分两种目标类型 — 连接和扩展。 连接目标有两种类型：用户档案导出目标和区段导出目标。

![目标类型](./assets/destination-types/types-of-destinations.png)

## 连接 {#connections}

**[!UICONTROL Profile Export]** 和Adobe Experience Platform **[!UICONTROL Segment Export]** 中的目标捕获事件数据，将其与其他数据源组合，以形 [成实时客户用户档案](../profile/home.md)，应用细分并将细分和合格用户档案导出到目标。

## 用户档案导出目标

用户档案导出目标生成包含用户档案和/或属性的文件。 这些目标使用原始数据，通常以电子邮件地址作为主要密钥。 [Amazon S3云存储目标](./catalog/cloud-storage/amazon-s3.md)是一个目标示例，您可以在其中存放包含用户档案导出的文件。

## 区段导出目标

区段导出目标会将用户档案及其限定的区段发送到目标平台。 这些目标使用区段ID或用户ID。 广告目标（如[[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md)或[[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md)）就是这些类型目标的示例。

## 用户档案导出和区段导出目标 — 视频概述

以下视频将向您介绍两种目标类型的特殊性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 扩展 {#extensions}

平台利用Adobe Experience Platform Launch的强大功能和灵活性，在平台界面中包含Platform launch扩展。

>[!TIP]
>
>有关Adobe Experience Platform Launch扩展的详细信息（包括用例和如何在界面中查找它们），请参阅[Adobe Experience Platform Launch扩展概述](./catalog/launch-extensions/overview.md)。

platform launch扩展将原始事件数据转发到多种类型的目标。 将扩展视为目标的&#x200B;**事件转发**&#x200B;类型。 这是与目标平台的集成的一种更简单类型，目标平台仅转发原始事件数据。 这些示例包括[Gainsight个性化扩展](./catalog/personalization/gainsight.md)或[客户扩展的确认语音](./catalog/voice/confirmit-digital-feedback.md)。

![Experience Platform Launch扩展与其他目标](./assets/common/launch-and-other-destinations.png)

## 何时使用连接和扩展

作为营销人员，您可以结合使用各种连接和扩展来解决您的使用案例。

当需要利用完整的集中式客户用户档案或客户细分进行激活时，连接非常有用。 例如，如果您要从分析系统将行为数据与上传的CRM数据相连，以便在向该用户传递个性化消息之前，使用户有资格访问给定细分，则使用连接。

当使用事件数据触发操作或在外部环境中执行分段时，扩展功能非常有用。 例如，如果行为数据需要转发到外部系统而不需要连接到给定用户的文件上的其他数据源。

## 目标类别

[目标目录](https://platform.adobe.com/destination/catalog)中的连接和扩展按目标类别(**Advertising**、**Cloud存储**、**调查平台**、**电子邮件营销**&#x200B;等)分组，具体取决于它们帮助您实现的营销操作。 有关每个类别以及每个类别中包含的目标的详细信息，请参阅[目标目录文档](./catalog/overview.md)。

![目标类别](./assets/destination-types/destination-categories-menu.png)

