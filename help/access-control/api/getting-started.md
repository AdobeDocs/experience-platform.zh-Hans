---
keywords: Experience Platform；主页；热门主题；访问控制;api；快速入门
solution: Experience Platform
title: 访问控制 API指南
topic-legacy: developer guide
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种平台功能的角色和权限。 以下各节提供开发人员成功调用模式 Registry API所需了解的其他信息。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---

# [!DNL Access Control] API指南

[!DNL Access control] for [!DNL Experience Platform] 通过Adobe Admin Console [管理](https://adminconsole.adobe.com)。此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。 有关详细信息，请参阅[访问控制概述](../home.md)。

本开发人员指南提供有关如何格式化您对[[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)的请求的信息，并涵盖以下操作：

- [列表权限和资源类型的名称](./permissions-and-resource-types.md)
- [视图当前用户的有效策略](./effective-policies.md)

## 入门指南

以下各节提供了成功调用[!DNL Schema Registry] API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：承载`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 后续步骤

现在，您已经收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和正确格式有效负载的示例请求以及成功调用的示例响应。
