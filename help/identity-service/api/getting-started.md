---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 入门指南
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Identity Service API开发人员指南

Adobe Experience Platform Identity Service通过Adobe Experience Platform中称为“身份图”的跨设备、跨渠道和近乎实时的客户身份识别进行管理。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

- [标识服务](../home.md):解决客户用户档案数据碎片化带来的根本挑战。 它通过跨设备和系统连接客户与您品牌互动的身份来实现这一点。
- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。

以下各节提供了成功调用Identity Service API所需的或现有的其他信息。

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

### 基于区域的路由

Identity Service API采用区域特定的端点，这些端点要求将某个端点作为请 `{REGION}` 求路径的一部分包含。 在配置IMS组织期间，会确定一个区域并将其存储在IMS组织用户档案中。 将正确的区域与每个端点一起使用可确保使用Identity Service API发出的所有请求都路由到相应的区域。

Identity Service API当前支持两个区域：VA7和NLD2。

下表显示了使用区域的示例路径：

| 服务 | 地区：VA7 | 地区：NLD2 |
| ------ | -------- |--------- |
| Identity Service API | https://</span>platform-va7.adobe。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| 标识命名空间API | https://</span>platform-va7.adobe。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] 在未指定区域的情况下发出的请求可能导致调用路由到错误区域或导致调用意外失败。

如果您无法在IMS组织用户档案中找到该区域，请与系统管理员联系以获取支持。

## 使用Identity Service API

这些服务中使用的身份参数可以通过两种方式之一表示；复合或XID。

组合标识是包括ID值和命名空间的构造。 使用复合标识时，命名空间可以由名称(`namespace.code`)或ID(`namespace.id`)提供。

当标识被保留时，Identity Service将生成一个ID并将其分配给该标识，称为本机ID或XID。 群集和映射API的所有变体在其请求和响应中都支持组合标识和XID。 其中一个参数是必需的- `xid` 或者组合 [`ns` 或 `nsid`] 和使 `id` 用这些API。

要限制响应中的有效负荷，API会根据使用的标识构造类型调整其响应。 也就是说，如果您通过XID，您的答复将具有XID，如果您通过复合身份，则答复将遵循请求中使用的结构。

本文档中的示例不涵盖Identity Service API的完整功能。 有关完整的API，请参阅 [Swagger API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。

>[!NOTE] 当请求中使用本机XID时，返回的所有标识都将采用本机XID格式。 建议使用ID/命名空间表单。 有关详细信息，请参阅 [获取XID以获取标识部分](./create-custom-namespace.md)。

## 后续步骤

现在，您已经收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包括常规 **API格式**、显示所需标头和格式正确的负载的示例 **请求** ，以及成功调用的 **示例响应** 。
