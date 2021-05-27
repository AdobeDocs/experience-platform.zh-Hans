---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒API指南
topic-legacy: developer guide
description: 沙盒API允许开发人员以编程方式管理Adobe Experience Platform中的沙箱。 请阅读本指南，了解如何使用API执行关键操作。
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# 沙盒API指南

Adobe Experience Platform中的沙箱提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验和进行自定义配置。

本开发人员指南提供了一些步骤来帮助您使用沙盒API管理Experience Platform中的沙箱，其中还包含用于执行各种操作的示例API调用。

## 沙盒API快速入门

要为IMS组织管理沙箱，您必须具有沙盒管理权限。 没有访问权限的用户只能使用[可用沙箱端点](./available.md)来列出当前用户的活动沙箱。 有关如何分配沙盒权限以进行Experience Platform的更多信息，请参阅[访问控制概述](../../access-control/home.md)。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

本指南要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)才能成功调用Platform API。 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：载体`{ACCESS_TOKEN}`
* x-api密钥：`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

除了身份验证标头之外，所有请求都需要一个标头来指定操作将在其中执行的沙盒名称：

* x-sandbox-name:`{SANDBOX_NAME}`

所有包含有效负载(POST、PUT和PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## 后续步骤

现在，您已收集所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的负载的示例请求，以及成功调用的示例响应。
