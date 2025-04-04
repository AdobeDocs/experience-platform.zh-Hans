---
keywords: Experience Platform；主页；热门主题；identity service api；identity service开发人员指南；区域
solution: Experience Platform
title: Identity Service API指南
description: Identity Service API允许开发人员使用Adobe Experience Platform中的身份图管理客户的跨设备、跨渠道和近乎实时的身份识别。 参阅本指南，了解如何使用 API 执行关键操作。
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 14%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service]通过Adobe Experience Platform中称为“身份图”的方式管理客户的跨设备、跨渠道和近乎实时的身份识别。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [[!DNL Identity Service]](../home.md)：解决客户个人资料数据碎片化带来的基本挑战。 它通过在客户与您的品牌互动的设备和系统中桥接身份来实现这一点。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，实时提供统一的使用者配置文件。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。

以下部分提供了您需要了解或拥有的其他信息，以便成功调用[!DNL Identity Service] API。

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

### 基于区域的工艺路线

[!DNL Identity Service] API使用特定于区域的端点，这些端点要求将`{REGION}`作为请求路径的一部分包含。 在您的组织配置过程中，会确定一个区域并将其存储在您的组织配置文件中。 对每个端点使用正确的区域可确保使用[!DNL Identity Service] API发出的所有请求都被路由到适当的区域。

[!DNL Identity Service] API当前支持两个区域：VA7和NLD2。

下表显示了使用区域的示例路径：

| 服务 | 地区： VA7 | 区域： NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>在不指定区域的情况下发出的请求可能会导致呼叫路由到不正确的区域，或导致呼叫意外失败。

如果您无法在组织配置文件中找到该区域，请联系您的系统管理员寻求支持。

## 使用[!DNL Identity Service] API

这些服务中使用的标识参数可以采用以下两种方式之一来表示：复合或XID。

复合身份是包括ID值和命名空间在内的结构。 使用复合标识时，命名空间可由名称(`namespace.code`)或ID (`namespace.id`)提供。

当保留某个标识时，[!DNL Identity Service]会生成一个ID并将其分配给该标识，称为本机ID或XID。 群集和映射API的所有变体在其请求和响应中支持复合身份和XID。 需要使用其中一个参数 — `xid`或[`ns`或`nsid`]和`id`的组合才能使用这些API。

为了限制响应中的有效负载，API会根据使用的身份构造类型调整其响应。 也就是说，如果传递XID，您的响应将具有XID；如果传递复合身份，则响应将遵循请求中使用的结构。

本文档中的示例不涉及[!DNL Identity Service] API的完整功能。 有关完整的API，请参阅[Swagger API引用](https://www.adobe.io/experience-platform-apis/references/identity-service)。

>[!NOTE]
>
>在请求中使用本机XID时，返回的所有标识都将采用本机XID格式。 建议使用ID/命名空间表单。 有关详细信息，请参阅[获取标识的XID](./create-custom-namespace.md)一节。

## 后续步骤

现在您已经收集了所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分都提供了有关其端点的重要信息并演示了用于执行CRUD操作的示例API调用。 每个调用都包含常规API格式、一个示例请求（显示所需的标头和格式正确的负载），以及一个成功调用的示例响应。
