---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 访问控制开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# 访问控制开发人员指南

Experience Platform的访问控制通过 [Adobe Admin Console进行管理](https://adminconsole.adobe.com)。 此功能利用Admin Console中的产品用户档案，该控制台将用户与权限和沙箱关联。 有关详细 [信息，请参阅访问控制](../home.md) 概述。

此开发人员指南提供有关如何设置您对 [访问控制API的请求的格式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)，并涵盖以下操作：

- [列表权限和资源类型的名称](./permissions-and-resource-types.md)
- [视图当前用户的有效策略](./effective-policies.md)

## 入门指南

以下各节提供了成功调用模式注册表API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 后续步骤

现在，您已经收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规 **API格式**、显示所需标头和格式正确的负载的示例 **请求** ，以及成功调用的 **示例响应** 。