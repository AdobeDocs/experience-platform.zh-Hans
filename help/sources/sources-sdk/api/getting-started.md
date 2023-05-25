---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
solution: Experience Platform
title: 自助式源快速入门(Batch SDK)
description: 本文档介绍了在尝试使用自助源(Batch SDK)创建新源之前需要了解的先决条件信息。
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 2a5d545db18a5dd33c5ff2ac5c543ec35db4ca00
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 自助式源快速入门(Batch SDK)

自助式源（批处理SDK）允许您集成自己的基于REST的源，将批量数据引入到Adobe Experience Platform。 本文档介绍了在尝试调用 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 先决条件

要使用自助式源（批处理SDK），您必须确保您有权访问配置了Adobe Experience Platform源的组织沙盒。

本指南还需要深入了解Adobe Experience Platform的以下组件：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 正在读取示例API调用

自助式源(Batch SDK)和 [!DNL Flow Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

## 收集所需标题的值

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Platform中的所有资源，包括属于 [!DNL Flow Service]，与特定的虚拟沙盒隔离。 对Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙盒的更多信息，请参阅 [沙盒文档](../../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 后续步骤

要开始使用自助源(Batch SDK)创建新源，请参阅关于的教程 [创建新源](./create.md).
