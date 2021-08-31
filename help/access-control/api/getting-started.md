---
keywords: Experience Platform；主页；热门主题；访问控制；API；快速入门
solution: Experience Platform
title: Access Control API指南
topic-legacy: developer guide
description: 通过Adobe Experience Platform中的访问控制，您可以使用Adobe Admin Console管理各种平台功能的角色和权限。 以下部分提供了开发人员成功调用架构注册表API所需了解的其他信息。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 2a73571d806f1653dad29d2c0b0067c5ce63e0e7
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# [!DNL Access Control] API指南

[!DNL Access control]  [!DNL Experience Platform] 通过Adobe Admin Console [管理](https://adminconsole.adobe.com)。此功能可利用Admin Console中的产品配置文件，将用户与权限和沙箱相关联。 有关更多信息，请参阅[访问控制概述](../home.md)。

本开发人员指南提供了有关如何设置[[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)请求的格式的信息，并涵盖以下操作：

- [权限和资源类型的列表名称](./permissions-and-resource-types.md)
- [查看当前用户的有效策略](./effective-policies.md)

## 快速入门

以下部分提供了成功调用[!DNL Schema Registry] API所需了解的其他信息。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

## 后续步骤

现在，您已收集所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的负载的示例请求，以及成功调用的示例响应。
