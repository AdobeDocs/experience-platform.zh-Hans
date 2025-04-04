---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒API快速入门
description: 沙盒API允许开发人员以编程方式管理Adobe Experience Platform中的沙盒。 参阅本指南，了解如何使用 API 执行关键操作。
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 15%

---

# 沙盒API快速入门

Adobe Experience Platform中的沙盒提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验以及进行自定义配置。

本开发人员指南提供了帮助您使用沙盒API管理Experience Platform中的沙盒的步骤，包括用于执行各种操作的示例API调用。

## 先决条件

为了管理贵组织的沙盒，您必须具有沙盒管理权限。 没有访问权限的用户只能使用[可用的沙盒终结点](./available.md)列出当前用户的活动沙盒。 有关如何为Experience Platform分配沙盒权限的更多信息，请参阅[访问控制概述](../../access-control/home.md)。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

本指南要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用Experience Platform API。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

除了身份验证标头之外，所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name： `{SANDBOX_NAME}`

所有包含有效负载(POST、PUT和PATCH)的请求都需要额外的标头：

* Content-Type： application/json

## 后续步骤

现在您已经收集了所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分都提供了有关其端点的重要信息并演示了用于执行CRUD操作的示例API调用。 每个调用都包含常规API格式、一个示例请求（显示所需的标头和格式正确的负载），以及一个成功调用的示例响应。
