---
keywords: Experience Platform；主页；热门主题；沙箱开发人员指南
solution: Experience Platform
title: 沙箱API指南
topic-legacy: developer guide
description: 沙箱API允许开发人员有序管理Adobe Experience Platform中的沙箱。 请按照本指南学习如何使用API执行关键操作。
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# 沙箱API指南

Adobe Experience Platform中的沙箱提供独立的开发环境，使您能够测试功能、运行实验和制作自定义配置，而不会影响您的制作环境。

此开发人员指南提供了帮助您使用沙箱API管理Experience Platform中沙箱的步骤，并包含用于执行各种操作的示例API调用。

## 沙箱API入门

要管理IMS组织的沙箱，您必须具有“沙箱管理”权限。 没有访问权限的用户只能使用[的端点，列出当前用户](./list-active-sandboxes.md)的活动沙箱。 有关如何为Experience Platform分配沙箱权限的详细信息，请参阅[访问控制概述](../../access-control/home.md)。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

本指南要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以成功调用平台API。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：承载`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

除了身份验证标头之外，所有请求都需要一个标头来指定操作将在中执行的沙箱的名称：

* x-sandbox-name:`{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT和PATCH)的请求都需要附加标头：

* 内容类型：application/json

## 后续步骤

现在，您已经收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和正确格式有效负载的示例请求以及成功调用的示例响应。
