---
keywords: Experience Platform；主页；热门主题；基于属性的访问控制；基于属性的访问控制
title: 基于属性的访问控制快速入门
description: 基于属性的访问控制允许您以编程方式管理Adobe Experience Platform中的角色和策略。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 4%

---

# 基于属性的访问控制快速入门

本开发人员指南提供了一些步骤，帮助您使用基于属性的访问控制来管理Adobe Experience Platform中的角色、产品、权限类别和权限集，并包含用于执行各种操作的示例API调用。

## 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅 [如何阅读示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

## 收集所需标题的值

本指南要求您完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以成功调用Platform API。 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

除了身份验证标头之外，所有请求都需要一个标头来指定操作将在其中执行的沙盒名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT和PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

## 后续步骤

现在，您已收集所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的负载的示例请求，以及成功调用的示例响应。

请参阅以下API教程，以开始调用基于属性的访问控制API:

* [角色端点](./roles.md)
* [产品端点](./products.md)
