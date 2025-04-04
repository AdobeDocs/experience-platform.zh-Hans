---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: Real-Time Customer Profile API入门
type: Documentation
description: 配置文件API快速入门指南概述了要使用实时客户配置文件API端点对配置文件数据执行基本CRUD操作，您需要了解的关键概念和基本功能。
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 6%

---

# [!DNL Real-Time Customer Profile] API快速入门 {#getting-started}

使用实时客户个人资料API端点，您可以对个人资料数据执行基本CRUD操作，例如配置计算属性、访问实体、导出个人资料数据以及删除不需要的数据集或批次。

使用开发人员指南需要对使用[!DNL Profile]数据时涉及的各种Adobe Experience Platform服务有一定的了解。 在开始使用[!DNL Real-Time Customer Profile] API之前，请查看以下服务的文档：

* [[!DNL Real-Time Customer Profile]](../home.md)：根据来自多个源的汇总数据，实时提供统一的客户个人资料。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解您的客户及其行为。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md)：允许您从实时客户档案数据构建受众。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用[!DNL Profile] API端点需要了解的其他信息。

## 正在读取示例 API 调用

[!DNL Real-Time Customer Profile] API文档提供了示例API调用，以演示如何正确设置请求的格式。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 必需的标头

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Experience Platform]端点。 完成身份验证教程将提供[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的请求需要一个标头，该标头指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有在请求正文中具有有效负载的请求(如POST、PUT和PATCH调用)都必须包含`Content-Type`标头。 调用参数中提供了特定于每个调用的接受值。

## 后续步骤

要开始使用[!DNL Real-Time Customer Profile] API进行调用，请选择一个可用的端点指南。
