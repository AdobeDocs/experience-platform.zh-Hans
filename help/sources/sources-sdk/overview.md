---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源sdk；sdk；SDK
solution: Experience Platform
title: 自助式源(批处理SDK)概述
description: Adobe Experience Platform自助源(批处理SDK)是一组配置API，允许您使用流服务API集成基于REST API的源，将您的数据引入到Experience Platform。
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 3%

---

# 自助式源(批处理SDK)概述

Adobe Experience Platform自助源(批处理SDK)是一个框架，它允许您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将基于REST API的源集成到Experience Platform源目录。 自助源(批处理SDK)提供了一组配置API，用于构建您自己的源并将批量数据引入Experience Platform。

通过自助式源(批处理SDK)，您可以：

* 使用[!DNL Flow Service] API配置新源并将其集成到Experience Platform目录。
* 定义源的规范，包括与支持的身份验证类型以及如何获取资源数据相关的信息。
* 为新源创建面向用户的文档。

“自助源”文档提供了配置、测试和发布与Experience Platform的基于REST API的源集成的说明，并让您的源成为不断增长的源目录的一部分。

![目录](./assets/catalog.png)

## 了解源

Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

有关源的详细信息，以及要查看Experience Platform上当前支持的各种源的列表，请参阅[源概述](../home.md)。

## 创建源

通过自助源，您可以将自己的基于REST API的源集成到一起，并将您的数据带到Experience Platform和[!DNL Flow Service]。 您可以通过[!DNL Flow Service] API创建、配置和提交新的连接规范，将源集成到Experience Platform源目录。

有关如何将新源集成到Experience Platform的信息，请参阅[创建新连接规范](./api/api-overview.md)指南。

## 记录您的源

创建源后，请参阅[文档指南](./documentation/doc-overview.md)，获取有关如何通过[!DNL GitHub] Web界面或通过您自己的文本编辑器来记录源的说明。

## 高级流程

下面概述了在Experience Platform中配置源的分步流程：

* 阅读[自助源(批处理SDK) API指南](./api/api-overview.md)。
   * 阅读[入门指南](./api/getting-started.md)。
   * 按照有关[创建新连接规范](./api/create.md)的教程进行操作。
   * 按照有关[更新连接规范](./api/update-connection-specs.md)的教程进行操作。
   * 按照有关[将新的连接规范ID添加到流规范](./api/update-flow-specs.md)的教程进行操作
   * [提交您的新源](./api/submit.md)。
* 要更好地了解连接规范的结构和属性，请阅读关于自助源(批处理SDK)的[配置选项](./config/config.md)的指南。
   * 请阅读[配置身份验证规范](./config/authspec.md)的指南，以更好地了解可用于源的各种身份验证类型。
   * 请阅读[配置源规范](./config/sourcespec.md)的指南，以了解有关可以为源配置的不同分页类型、计划格式和自定义架构的信息。
   * 请阅读[配置浏览规范](./config/explorespec.md)的指南，以了解如何定义浏览和检查源中包含的对象所需的参数。
* 要开始记录您的源，请阅读有关创建自助源文档的[概述](./documentation/doc-overview.md)
   * 您可以使用此[源API文档模板](./documentation/template.md)来构建API文档。
   * 您可以使用此[源UI文档模板](./documentation/ui-template.md)来构造您的UI文档。
   * 有关如何使用GitHub创建文档的步骤，请参阅有关[使用GitHub Web界面](./documentation/github.md)的指南。
   * 有关如何使用本地计算机创建文档的步骤，请参阅[使用文本编辑器](./documentation/text-editor.md)上的指南。
