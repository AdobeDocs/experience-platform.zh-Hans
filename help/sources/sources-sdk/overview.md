---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 自助源（批量SDK）概述
description: Adobe Experience Platform自助源(Batch SDK)是一组配置API，允许您使用流量服务API集成基于REST API的源，以将数据引入Experience Platform。
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 自助源（批量SDK）概述

Adobe Experience Platform自助源（批量SDK）是一个框架，允许您使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 自助源（批量SDK）提供了一组配置API，用于构建您自己的源并将批量数据Experience Platform。

使用自助源（批量SDK），您可以：

* 使用配置新源并将其集成到Experience Platform目录 [!DNL Flow Service] API。
* 为源定义规范，包括与支持的身份验证类型以及如何获取资源数据有关的信息。
* 为新源创建面向用户的文档。

自助源文档提供了配置、测试和发布基于REST API的源与Experience Platform集成的说明，并让您的源成为不断增长的源目录的一部分。

![目录](./assets/catalog.png)

## 了解源

Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

有关源的详细信息，以及要查看当前支持的不同源的列表，请参阅Experience Platform [源概述](../home.md).

## 创建源

通过自助源，您可以集成自己的基于REST API的源，并将数据Experience Platform到 [!DNL Flow Service]. 您可以通过创建、配置和提交新的连接规范，将源集成到Experience Platform源目录中 [!DNL Flow Service] API。

请参阅 [创建新连接规范](./api/api-overview.md) 以了解有关如何将新源集成到Experience Platform的信息。

## 记录源

创建源后，请参阅 [文档指南](./documentation/doc-overview.md) 有关如何通过 [!DNL GitHub] Web界面或通过您自己的文本编辑器。

## 高级流程

在Experience Platform中配置源的分步流程如下所示：

* 阅读 [自助源（批量SDK）API指南](./api/api-overview.md).
   * 阅读 [入门指南](./api/getting-started.md).
   * 请阅读本教程 [创建新连接规范](./api/create.md).
   * 请阅读本教程 [更新连接规范](./api/update-connection-specs.md).
   * 请阅读本教程 [将新的连接规范ID添加到流量规范](./api/update-flow-specs.md)
   * [提交新来源](./api/submit.md).
* 要更好地了解连接规范的结构和属性，请阅读 [自助源（批处理SDK）的配置选项](./config/config.md).
   * 阅读 [配置身份验证规范](./config/authspec.md) 以便更好地了解可用于源的不同身份验证类型。
   * 阅读 [配置源规范](./config/sourcespec.md) 有关可以为源配置的不同分页类型、计划格式和自定义架构的信息。
   * 阅读 [配置浏览规范](./config/explorespec.md) 有关如何定义浏览和检查源中包含的对象所需的参数的信息。
* 要开始记录源，请阅读 [自助源创建文档概述](./documentation/doc-overview.md)
   * 您可以使用此 [源API文档模板](./documentation/template.md) 来构建API文档。
   * 您可以使用此 [源UI文档模板](./documentation/ui-template.md) 以构建UI文档。
   * 请参阅 [使用GitHub Web界面](./documentation/github.md) 有关如何使用GitHub创建文档的步骤。
   * 请参阅 [使用文本编辑器](./documentation/text-editor.md) 有关如何使用本地计算机创建文档的步骤。
