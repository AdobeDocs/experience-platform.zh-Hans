---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 数据摄取API快速入门
type: Documentation
description: 数据摄取API入门指南概述了在使用API将数据摄取到Experience Platform之前您需要了解的关键概念和基本功能。
source-git-commit: 19837e820ab3abdaa0bc8569ad78ce51dec1d21e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 数据摄取API快速入门 {#getting-started}

使用数据摄取API端点，您可以执行基本的CRUD操作，以便在Adobe Experience Platform中摄取数据。

使用API指南需要对处理数据涉及的多项Adobe Experience Platform服务有一定的了解。 在使用数据摄取API之前，请查阅以下服务的文档：

* [批量摄取](./overview.md):允许您将数据作为批处理文件导入到Adobe Experience Platform中。
* [[!DNL Real-time Customer Profile]](../home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用来组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用[!DNL Profile] API端点所需了解的其他信息。

## 读取示例API调用

数据摄取API文档提供了示例API调用，以演示如何正确设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

## 必需标题

API文档还要求您已完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Platform]端点。 完成身份验证教程将提供[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

请求正文中具有有效负载的所有请求(例如POST、PUT和PATCH调用)都必须包含`Content-Type`标头。 调用参数中提供了特定于每个调用的已接受值。

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的请求需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。
