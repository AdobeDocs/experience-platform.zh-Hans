---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 数据摄取API快速入门
type: Documentation
description: 数据摄取API快速入门指南概述了在使用API将数据摄取到Experience Platform中之前，您需要了解的关键概念和基本功能。
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 数据摄取API快速入门 {#getting-started}

使用数据摄取API端点，您可以执行基本的CRUD操作，以便在Adobe Experience Platform中摄取数据。

使用API指南需要实际了解与处理数据有关的多个Adobe Experience Platform服务。 在使用数据摄取API之前，请查看以下服务的文档：

* [批量摄取](./overview.md)：允许您将数据作为批处理文件摄取到Adobe Experience Platform。
* [[!DNL Real-Time Customer Profile]](../home.md)：根据来自多个来源的汇总数据实时提供统一的客户用户档案。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform用于组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功调用时需要了解的其他信息 [!DNL Profile] api端点。

## 正在读取示例API调用

数据摄取API文档提供了示例API调用，以演示如何正确设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 必需的标头

此API文档还要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] 端点。 完成身份验证教程将为中的每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

请求正文中具有有效负载的所有请求(例如POST、PUT和PATCH调用)必须包含 `Content-Type` 标头。 调用参数中提供了特定于每个调用的接受值。

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).
