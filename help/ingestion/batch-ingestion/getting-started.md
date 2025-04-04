---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 数据摄取API快速入门
type: Documentation
description: 数据摄取API快速入门指南概述了在使用API将数据摄取到Experience Platform之前需要了解的关键概念和基本功能。
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 6%

---

# 数据摄取API快速入门 {#getting-started}

使用数据摄取API端点，您可以执行基本的CRUD操作，以便在Adobe Experience Platform中摄取数据。

使用API指南需要实际了解与数据处理有关的多个Adobe Experience Platform服务。 在使用数据摄取API之前，请查看以下服务的文档：

* [批量摄取](./overview.md)：允许您将数据作为批处理文件摄取到Adobe Experience Platform中。
* [[!DNL Real-Time Customer Profile]](../home.md)：根据来自多个源的汇总数据，实时提供统一的客户个人资料。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用[!DNL Profile] API端点需要了解的其他信息。

## 正在读取示例 API 调用

数据摄取API文档提供了示例API调用，以演示如何正确设置请求的格式。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 必需的标头

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Experience Platform]端点。 完成身份验证教程将提供[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

所有在请求正文中具有有效负载的请求(如POST、PUT和PATCH调用)都必须包含`Content-Type`标头。 调用参数中提供了特定于每个调用的接受值。

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的请求需要一个标头，该标头指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。
