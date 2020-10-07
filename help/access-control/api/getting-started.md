---
keywords: Experience Platform;home;popular topics;access control;api;getting started
solution: Experience Platform
title: 访问控制开发人员指南
topic: developer guide
description: Adobe Experience Platform的访问控制允许您通过使用Adobe Admin Console管理各种平台功能的角色和权限。 以下各节提供了成功调用模式注册表API所需了解的其他信息。
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---


# [!DNL Access control] 开发人员指南

[!DNL Access control] 通 [!DNL Experience Platform] 过Adobe Admin Console [管](https://adminconsole.adobe.com)。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。 有关更多 [信息](../home.md) ，请参阅访问控制概述。

此开发人员指南提供如何格式化您对[! [DNL访问控制API]的请求](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)，并涵盖以下操作：

- [列表权限和资源类型的名称](./permissions-and-resource-types.md)
- [视图当前用户的有效策略](./effective-policies.md)

## 入门指南

以下各节提供了成功调用API所需了解的其他信 [!DNL Schema Registry] 息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 后续步骤

现在您已收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的有效负载的示例请求以及成功调用的示例响应。
