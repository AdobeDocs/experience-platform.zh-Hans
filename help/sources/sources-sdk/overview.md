---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 源SDK概述（测试版）
topic-legacy: overview
description: Adobe Experience Platform Sources SDK是一组配置API，允许您使用流程服务API集成基于REST API的源，以将数据引入Experience Platform。
hide: true
hidefromtoc: true
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: ce902e461c748e30e0307558da894a4dbdd212a4
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 源SDK概述（测试版）

>[!IMPORTANT]
>
>Sources SDK当前处于测试阶段，您的组织可能尚未访问该SDK。 本文档中描述的功能可能会发生更改。

Adobe Experience Platform Sources SDK是一组配置API，允许您使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 将数据Experience Platform。

通过源SDK，您可以：

* 为Platform目录配置新源，以及使用 [!DNL Flow Service] API。
* 为源定义规范，包括与支持的身份验证类型以及如何获取资源数据有关的信息。
* 为新源创建面向用户的文档。

源SDK文档提供了有关使用Adobe Experience Platform源SDK配置、测试和发布基于REST API的源与平台集成的说明，并让您的源成为不断增长的源目录的一部分。

![目录](./assets/catalog.png)

## 了解源

Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

有关源的详细信息以及要查看平台上当前支持的不同源的列表，请参阅 [源概述](../home.md).

## 创建源

通过Sources SDK，您可以集成自己的基于REST API的源，并将数据导入平台 [!DNL Flow Service]. Sources SDK允许您通过以下方式将新源与平台集成：通过 [!DNL Flow Service] API。

请参阅 [创建新连接规范](./api/api-overview.md) 有关如何将新源集成到平台的信息。

## 记录源

创建源后，请参阅 [文档指南](./documentation/doc-overview.md) 有关如何通过 [!DNL GitHub] Web界面或通过您自己的文本编辑器。

## 高级流程

在Experience Platform中配置源的分步流程如下所示：

* 阅读 [源SDK API指南](./api/api-overview.md);
   * 阅读 [入门指南](./api/getting-started.md);
   * 请阅读本教程 [创建新连接规范](./api/create.md);
   * 请阅读本教程 [更新连接规范](./api/update-connection-specs.md);
   * 请阅读本教程 [将新的连接规范ID添加到流量规范](./api/update-flow-specs.md)
   * [提交新来源](./api/submit.md).
* 要更好地了解连接规范的结构和属性，请参阅 [源SDK的配置选项](./config/config.md);
   * 请参阅 [配置身份验证规范](./config/authspec.md);
   * 请参阅 [配置源规范](./config/sourcespec.md);
   * 请参阅 [配置浏览规范](./config/explorespec.md);
* 要开始记录源，请参阅 [有关为源SDK创建文档的概述](./documentation/doc-overview.md)
   * 您可以使用此 [源API文档模板](./documentation/template.md) 构建API文档；
   * 您可以使用此 [源UI文档模板](./documentation/ui-template.md) 构建用户界面文档；
   * 请参阅 [使用GitHub Web界面](./documentation/github.md) 有关如何使用GitHub创建文档的步骤；
   * 请参阅 [使用文本编辑器](./documentation/text-editor.md) 有关如何使用本地计算机创建文档的步骤。
