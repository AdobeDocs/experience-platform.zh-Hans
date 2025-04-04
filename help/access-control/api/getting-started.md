---
keywords: Experience Platform；主页；热门主题；访问控制；API；快速入门
solution: Experience Platform
title: Access Control API指南
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种Experience Platform功能的角色和权限。 以下部分提供了开发人员成功调用架构注册表API时需要了解的其他信息。
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 20%

---

# [!DNL Access Control] API指南

[!DNL Experience Platform]的[!DNL Access control]通过[Adobe Admin Console](https://adminconsole.adobe.com)进行管理。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。 有关详细信息，请参阅[访问控制概述](../home.md)。

此开发人员指南提供了有关如何格式化对[[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)的请求的信息，并涵盖了以下操作：

- [权限和资源类型的列表名称](./permissions-and-resource-types.md)
- [查看当前用户的有效访问策略](./effective-policies.md)

## 快速入门

以下部分提供成功调用[!DNL Access Control] API所需了解的其他信息。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

- Content-Type： application/json

## 后续步骤

现在您已经收集了所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分都提供了有关其端点的重要信息并演示了用于执行CRUD操作的示例API调用。 每个调用都包含常规API格式、一个示例请求（显示所需的标头和格式正确的负载），以及一个成功调用的示例响应。
