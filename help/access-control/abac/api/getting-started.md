---
keywords: Experience Platform；主页；热门主题；基于属性的访问控制；基于属性的访问控制
title: 基于属性的访问控制API快速入门
description: 基于属性的访问控制API允许您以编程方式管理Adobe Experience Platform中的角色和访问策略。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 54e15234d1b1050ea2cdb8b7d37c79a133a339f1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# 基于属性的访问控制API快速入门

本开发人员指南提供了一些步骤，可帮助您使用基于属性的访问控制API来管理Adobe Experience Platform中的角色、产品、权限类别和权限集，并且包括用于执行各种操作的示例API调用。

## 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何读取示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

## 收集所需标题的值

本指南要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功调用平台API。 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

除了身份验证标头之外，所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

包含有效负载(POST、PUT和PATCH)的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 后续步骤

现在您已经收集了所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分都提供了有关其端点的重要信息，并演示了用于执行CRUD操作的示例API调用。 每个调用都包含常规API格式、一个示例请求（显示所需的标头和格式正确的负载），以及一个成功调用的示例响应。

请参阅以下API教程，开始调用基于属性的访问控制API：

* [角色端点](./roles.md)
* [产品端点](./products.md)
