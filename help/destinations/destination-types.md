---
keywords: 目标；目标；目标类型
title: 目标类型和类别
seo-title: 目标类型和类别
description: 了解Adobe Experience Platform的不同类型和类别目的地。
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# 目标类型和类别

阅读本页，了解Adobe Experience Platform目标的不同类型和类别。

## 目标类型

在Adobe Experience Platform，我们区分两种目标类型——连接和扩展。 连接目标有两种类型：用户档案导出目标和段导出目标。

![目标类型](./assets/destination-types/types-of-destinations.png)

### 连接 {#connections}

**[!UICONTROL 用户档案]** 出 **[!UICONTROL 口和]** 细分Adobe Experience Platform的出口目标捕获事件数据，将其与其他数据源相结合，构成实 [时客户用户档案](../profile/home.md)，应用细分并将细分和合格用户档案导出到目标。

#### 用户档案导出目标

用户档案导出目标生成包含用户档案和／或属性的文件。 这些目标使用原始数据，通常以电子邮件地址作为主要密钥。 [AmazonS3云存储目标](./catalog/cloud-storage/amazon-s3.md)是可以存放包含用户档案导出的文件的目标示例。

#### 区段导出目标

区段导出目标会将用户档案及其符合条件的区段发送到目标平台。 这些目标使用区段ID或用户ID。 [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md)或[[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md)等广告目标就是这些类型目标的示例。

#### 用户档案导出和细分导出目标——视频概述

以下视频将介绍两种目标类型的特点：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### 扩展 {#extensions}

平台利用Adobe Experience Platform Launch的强大功能和灵活性，将Platform Launch扩展包含在平台界面中。

>[!TIP]
>
>有关Adobe Experience Platform Launch扩展的详细信息，包括使用案例以及如何在界面中查找这些扩展，请参阅[Adobe Experience Platform Launch扩展概述](./catalog/launch-extensions/overview.md)。

Platform Launch扩展将原始事件数据转发到几种类型的目标。 将扩展视为&#x200B;**事件转发**&#x200B;类型的目标。 这是与目标平台的集成的一种更简单类型，目标平台仅转发原始事件数据。 这些示例包括[Gainsight个性化扩展](./catalog/personalization/gainsight.md)或[客户扩展的确认语音](./catalog/voice/confirmit-digital-feedback.md)。

![Experience Platform Launch扩展与其他目标](./assets/common/launch-and-other-destinations.png)

### 何时使用连接和扩展

作为营销人员，您可以结合使用连接和扩展来解决您的使用案例。

在需要利用完整的集中式客户用户档案或客户细分进行激活时，连接非常有用。 例如，如果您要从分析系统将行为数据与已上传的CRM数据相结合，以在向该用户发送个性化消息之前，使用连接来确定特定细分的用户资格。

当事件数据用于触发操作或在外部环境中执行细分时，扩展功能非常有用。 例如，如果行为数据需要转发到外部系统而不需要连接到给定用户的文件上的其他数据源。

## 目标类别

[目标目录](https://platform.adobe.com/destination/catalog)中的连接和扩展按目标类别(**广告**、**云存储**、**调查平台**、**电子邮件营销**&#x200B;等)进行分组，具体取决于它们有助于您实现的营销用例。 有关每个类别以及每个类别中包含的目标的详细信息，请参阅[目标目录文档](./catalog/overview.md)。

![目标类别](./assets/destination-types/destination-categories-menu.png)

