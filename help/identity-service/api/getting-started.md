---
keywords: Experience Platform；主页；热门主题；identity service api;identity service开发人员指南；区域
solution: Experience Platform
title: Identity Service API指南
topic-legacy: API guide
description: Identity Service API允许开发人员使用Adobe Experience Platform中的身份图来管理客户的跨设备、跨渠道和近乎实时的标识。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service] 在Adobe Experience Platform内称为身份图的中，管理客户的跨设备、跨渠道和近乎实时的标识。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Identity Service]](../home.md):解决了客户用户档案数据碎片化带来的根本难题。 它通过跨客户与您的品牌进行交互的设备和系统桥接身份来实现这一点。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

以下各节提供了您需要了解或掌握的其他信息，以便成功调用 [!DNL Identity Service] API。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

### 基于区域的路由

的 [!DNL Identity Service] API采用特定于区域的端点，这些端点需要包含 `{REGION}` 作为请求路径的一部分。 在配置IMS组织期间，会确定一个区域并将其存储在您的IMS组织配置文件中。 对每个端点使用正确的区域可确保使用 [!DNL Identity Service] API将被路由到相应的区域。

当前支持两个区域 [!DNL Identity Service] API:VA7和NLD2。

下表显示了使用区域的示例路径：

| 服务 | 地区：VA7 | 地区：NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>在未指定区域的情况下发出的请求可能导致呼叫路由到错误区域或导致呼叫意外失败。

如果您在IMS组织配置文件中找不到该区域，请联系您的系统管理员以获取支持。

## 使用 [!DNL Identity Service] API

这些服务中使用的身份参数可以采用两种方式之一表示；复合或XID。

复合身份是包括ID值和命名空间的构造。 使用复合标识时，命名空间可以通过以下任一名称(`namespace.code`)或ID(`namespace.id`)。

当保留身份时， [!DNL Identity Service] 生成ID并将其分配给该标识，称为本机ID或XID。 群集API和映射API的所有变体在其请求和响应中都支持复合身份和XID。 其中一个参数是必需的 —  `xid` 或组合 [`ns` 或 `nsid`] 和 `id` 以使用这些API。

为了限制响应中的有效负载，API会根据使用的身份结构类型调整其响应。 也就是说，如果传递XID，您的响应将具有XID，如果传递复合身份，则响应将遵循请求中使用的结构。

本文档中的示例不涵盖 [!DNL Identity Service] API。 有关完整的API，请参阅 [Swagger API引用](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>在请求中使用本机XID时，返回的所有身份都将采用本机XID格式。 建议使用ID/命名空间表单。 有关更多信息，请参阅 [获取XID以获取身份](./create-custom-namespace.md).

## 后续步骤

现在，您已收集所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规API格式、显示所需标头和格式正确的负载的示例请求，以及成功调用的示例响应。
