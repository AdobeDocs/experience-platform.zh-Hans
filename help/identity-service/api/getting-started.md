---
keywords: Experience Platform；主页；热门主题；identity service api；identity service开发人员指南；区域
solution: Experience Platform
title: Identity Service API指南
description: Identity Service API允许开发人员在Adobe Experience Platform中使用身份图管理客户的跨设备、跨渠道和近乎实时的身份识别。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service] 通过Adobe Experience Platform中称为“身份图”的方式管理客户的跨设备、跨渠道和近乎实时的身份识别。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Identity Service]](../home.md)：解决客户个人资料数据碎片化带来的根本挑战。 它通过在客户与您品牌互动的设备和系统之间桥接身份来实现这一点。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的聚合数据实时提供统一的用户配置文件。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

以下部分提供了您需要了解或拥有的其他信息，以便成功调用 [!DNL Identity Service] API。

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type： application/json

### 基于区域的工艺路线

此 [!DNL Identity Service] API采用特定于区域的端点，这些端点需要包含 `{REGION}` 作为请求路径的一部分。 在您的组织配置过程中，会确定一个区域并将其存储在您的组织配置文件中。 对每个端点使用正确的区域可确保使用发出的所有请求 [!DNL Identity Service] API被路由到适当的区域。

目前支持两个区域 [!DNL Identity Service] API： VA7和NLD2。

下表显示了使用区域的示例路径：

| 服务 | 地区： VA7 | 区域： NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>在不指定区域的情况下发出的请求可能会导致呼叫路由到不正确的区域，或导致呼叫意外失败。

如果您在组织配置文件中找不到该区域，请联系您的系统管理员寻求支持。

## 使用 [!DNL Identity Service] API

这些服务中使用的身份参数可以用以下两种方式之一表示：复合或XID。

复合身份是包含ID值和命名空间的结构。 使用复合身份时，命名空间可由任一名称(`namespace.code`)或ID (`namespace.id`)。

当一个身份持续存在时， [!DNL Identity Service] 生成一个ID并将其分配给该标识，称为本机ID或XID。 Cluster和Mapping API的所有变体都在其请求和响应中支持复合身份和XID。 需要以下参数之一 —  `xid` 或以下项的组合 [`ns` 或 `nsid`] 和 `id` 以使用这些API。

为了限制响应中的有效负载，API根据使用的身份构造类型调整其响应。 也就是说，如果传递XID，则响应将具有XID；如果传递复合身份，则响应将遵循请求中使用的结构。

本文档中的示例不包括 [!DNL Identity Service] API。 有关完整的API，请参阅 [Swagger API参考](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>在请求中使用本机XID时，返回的所有标识都将采用本机XID格式。 建议使用ID/命名空间表单。 有关更多信息，请参阅以下部分： [获取标识的XID](./create-custom-namespace.md).

## 后续步骤

现在您已经收集了所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分都提供了有关其端点的重要信息，并演示了用于执行CRUD操作的示例API调用。 每个调用都包含常规API格式、一个示例请求（显示所需的标头和格式正确的负载），以及一个成功调用的示例响应。
