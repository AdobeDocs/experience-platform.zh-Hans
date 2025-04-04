---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源sdk；sdk；SDK
solution: Experience Platform
title: 自助源快速入门(批处理SDK)
description: 本文档介绍了在尝试使用自助源(批处理SDK)创建新源之前需要了解的先决条件信息。
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 16%

---

# 自助源快速入门(批处理SDK)

自助式源(批处理SDK)允许您集成自己的基于REST的源，将批量数据引入到Adobe Experience Platform。 本文档介绍了在尝试调用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)之前需要了解的核心概念。

## 先决条件

要使用自助源(批处理SDK)，您必须确保您有权访问配置了Adobe Experience Platform源的组织沙盒。

此外，您还需要实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 正在读取示例 API 调用

自助式源(批处理SDK)和[!DNL Flow Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 收集所需标头的值

要调用Experience Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对Experience Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙盒的更多信息，请参阅[沙盒文档](../../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 后续步骤

要开始使用自助源(批处理SDK)创建新源，请参阅有关[创建新源](./create.md)的教程。
