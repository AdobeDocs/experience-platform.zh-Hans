---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 入门指南
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---


# [!DNL Identity Service] API开发人员指南

Adobe Experience Platform [!DNL Identity Service] 通过Adobe Experience Platform内的“身份图”管理跨设备、跨渠道和近乎实时的客户身份识别。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

- [!DNL Identity Service](../home.md): 解决客户用户档案数据碎片化带来的根本挑战。 它通过跨设备和系统连接身份来实现这一点，客户可以与您的品牌互动。
- [!DNL Real-time Customer Profile](../../profile/home.md): 根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用API所需的或现有的其他信 [!DNL Identity Service] 息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型： application/json

### 基于区域的路由

该 [!DNL Identity Service] API采用区域特定端点，这些端点要求将 `{REGION}` 一个包含在请求路径中。 在设置IMS组织期间，将确定一个区域并存储在IMS组织用户档案中。 将正确的区域与每个端点一起使用，可确保使用API发出的所 [!DNL Identity Service] 有请求都路由到相应的区域。

API当前支持两个 [!DNL Identity Service] 区域： VA7和NLD2。

下表显示了使用区域的示例路径：

| 服务 | 地区： VA7 | 地区： NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe。</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe。</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe。</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] 在未指定区域的情况下发出的请求可能导致调用路由到错误区域或导致调用意外失败。

如果您无法在IMS组织用户档案中找到该区域，请与系统管理员联系以获得支持。

## 使用 [!DNL Identity Service] API

这些服务中使用的身份参数可以通过两种方式之一来表示； 复合或XID。

组合标识是包括ID值和命名空间的构造。 使用复合标识时，命名空间可以由名称()`namespace.code`或ID()提`namespace.id`供。

当某个标识被保留 [!DNL Identity Service] 时，将生成一个ID并为其分配一个ID，称为本机ID或XID。 群集和映射API的所有变体在其请求和响应中都支持组合标识和XID。 其中一个参数是必需的- `xid` 或者组合 [`ns` 或 `nsid`] 使用这 `id` 些API的参数。

要限制响应中的有效负荷，API会调整其响应以适应所使用的身份构造类型。 即，如果传递XID，则您的响应将具有XID，如果传递复合身份，则响应将遵循请求中使用的结构。

此文档中的示例不涵盖API的完整功 [!DNL Identity Service] 能。 有关完整的API，请参阅 [Swagger API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。

>[!NOTE] 当请求中使用本机XID时，返回的所有标识都将采用本机XID格式。 建议使用ID/命名空间表单。 有关详细信息，请参阅 [获取XID以获取身份](./create-custom-namespace.md)。

## 后续步骤

现在您已收集了所需的凭据，现在可以继续阅读开发人员指南的其余部分。 每个部分提供有关其端点的重要信息，并演示用于执行CRUD操作的示例API调用。 每个调用都包 **括常规API格式**、显示所需标头 **和格式正确** 的有效负载的示例请求以及成 **功调用的** 示例响应。
