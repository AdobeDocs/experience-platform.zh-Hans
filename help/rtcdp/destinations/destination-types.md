---
title: 目标类型和类别
seo-title: 目标类型和类别
description: '在Adobe实时客户数据平台中，用户档案/细分导出目标可捕获事件数据，将其与其他数据源组合，应用细分，并将细分和合格用户档案导出到目标。 启动扩展将原始事件数据转发到多种类型的目标。 '
seo-description: 在Adobe实时客户数据平台中，用户档案/细分导出目标可捕获事件数据，将其与其他数据源组合，应用细分，并将细分和合格用户档案导出到目标。 启动扩展将原始事件数据转发到多种类型的目标。
translation-type: tm+mt
source-git-commit: 617cf1934402b9001647d7704fb24d6256069ff3

---


# 目标类型和类别

阅读本页以了解Adobe实时客户数据平台目标的不同类型和类别。

## 目标类型

在Adobe实时客户数据平台中，我们区分两种目标类型——连接和扩展。 连接目标有两种类型：用户档案导出目标和区段导出目标。

![目标类型](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### 连接

**用户档案Adobe实时客** 户数据平台中的导出和细分导出目标捕获事件数据，将其与其他数据源相结合以形成实时客户用户档案 ****[](/help/profile/home.md)，应用细分并将细分和合格用户档案导出到目标。

<br> 

#### 用户档案导出目标

用户档案导出目标生成包含用户档案和／或属性的文件。 这些目标使用原始数据，通常以电子邮件地址作为主要密钥。 Amazon [S3云存储目标是一个目标示例](/help/rtcdp/destinations/amazon-s3-destination.md) ，您可以在其中存放包含用户档案导出的文件。

#### 区段导出目标

区段导出目标会将用户档案及其符合条件的区段发送到目标平台。 这些目标使用区段ID或用户ID。 Google Display &amp; Video 360 [](/help/rtcdp/destinations/google-dv360-destination.md) 或 [Google Ads](/help/rtcdp/destinations/google-ads-destination.md) 等广告目标就是这些类型的目标。

#### 用户档案导出和区段导出目标——视频概述

以下视频将向您介绍两种目标类型的特殊性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### 扩展

Adobe实时CDP利用Experience Platform Launch的强大功能和灵活性，将Launch扩展包含在Adobe实时CDP界面中。

>[!TIP]
>
>有关Experience Platform Launch扩展的详细信息（包括用例以及如何在界面中查找它们），请参阅 [Launch扩展概述](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

启动扩展将原始事件数据转发到多种类型的目标。 将扩展视为目标 **的事件转发** 类型。 这是与目标平台更简单的集成类型，目标平台仅转发原始事件数据。 这些示例包括 [Gainsight个性化扩展](/help/rtcdp/destinations/gainsight-extension.md) , [或客户扩展的确认声音](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)。

![Experience Platform Launch扩展与其他目标相比](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### 何时使用连接和扩展

作为营销人员，您可以结合使用连接和扩展来解决您的使用案例。

在需要利用完整的集中式客户用户档案或客户细分进行激活时，连接非常有用。 例如，如果您要从分析系统将行为数据与上传的CRM数据相连，以便在向该用户发送个性化消息之前使用户有资格访问给定细分。

当使用事件数据触发操作或在外部环境中执行细分时，扩展功能非常有用。 例如，如果行为数据需要转发到外部系统而不需要连接到给定用户的文件上的其他数据源。

<br> 

## 目标类别

目标目录中的连接和扩展按目标类别 [(](https://platform.adobe.com/destination/catalog) Advertising **、************** Cloud存储平台、调查平台、Email MarketingMarketingComplate等)进行分组，具体取决于您所实现的营销使用案例。 有关每个类别以及每个类别中包含的目标的详细信息，请参阅目标目 [录文档](/help/rtcdp/destinations/destinations-catalog.md)。

![目标类别](/help/rtcdp/destinations/assets/destination-categories-menu.png)

