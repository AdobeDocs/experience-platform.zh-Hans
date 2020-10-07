---
keywords: Experience Platform;home;popular topics;sandbox developer guide
solution: Experience Platform
title: 沙箱API开发人员指南
topic: developer guide
description: 此开发人员指南提供帮助您使用沙箱API管理Experience Platform中沙箱的步骤，并包含用于执行各种操作的示例API调用。
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 沙箱API开发人员指南

Adobe Experience Platform的沙箱提供独立的开发环境，使您能够测试功能、运行实验和制作自定义配置，而不会影响您的生产环境。

此开发人员指南提供帮助您使用沙箱API管理Experience Platform中沙箱的步骤，并包含用于执行各种操作的示例API调用。

## 沙箱API快速入门

要管理IMS组织的沙箱，您必须具有“沙箱管理”权限。 没有访问权限的用户只能使用端点来 [列出当前用户的活动沙箱](./list-active-sandboxes.md)。 有关如 [何为访问控制](../../access-control/home.md) 分配沙箱权限的更多信息，请参阅Experience Platform概述。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

本指南要求您完成身 [份验证教程](../../tutorials/authentication.md) ，以便成功调用平台API。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

除了身份验证标头之外，所有请求都需要一个标头来指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT和PATCH)的请求都需要附加标头：

* 内容类型：application/json

## 后续步骤

现在您已收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的有效负载的示例请求以及成功调用的示例响应。