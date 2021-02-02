---
keywords: Experience Platform；主页；热门主题；访问控制;api；入门
solution: Experience Platform
title: 访问控制开发人员指南
topic: developer guide
description: Adobe Experience Platform的访问控制允许您通过使用Adobe Admin Console管理各种平台功能的角色和权限。 以下各节提供了成功调用模式注册表API所需了解的其他信息。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---


# [!DNL Access control] 开发人员指南

[!DNL Access control] 通 [!DNL Experience Platform] 过Adobe Admin Console进 [行](https://adminconsole.adobe.com)。此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。 有关详细信息，请参阅[访问控制概述](../home.md)。

本开发人员指南提供有关如何格式化您对[[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)的请求的信息，并涵盖以下操作：

- [列表权限和资源类型的名称](./permissions-and-resource-types.md)
- [视图当前用户的有效策略](./effective-policies.md)

## 入门指南

以下各节提供了成功调用[!DNL Schema Registry] API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 后续步骤

现在您已收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的有效负载的示例请求以及成功调用的示例响应。
