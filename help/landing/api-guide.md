---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform;api指南；平台api指南；平台简介；开发人员指南
solution: Experience Platform
title: Adobe Experience Platform API入门
topic-legacy: api guide
description: Adobe Experience Platform提供彼此紧密关联的API服务。 本指南包含有关可用服务、CRUD操作所需标头、错误消息、Postman集合和示例API调用的信息。
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Adobe Experience Platform API入门

Adobe Experience Platform是根据“API优先”理念开发的。 使用平台API，您可以对数据以编程方式执行基本的CRUD（创建、读取、更新、删除）操作，例如配置计算属性、访问数据/实体、导出数据、删除不需要的数据或批次等。

每个Experience Platform服务的API都共享同一组身份验证标头，并对其CRUD操作使用类似语法。 以下指南概述了开始使用Platform API的必要步骤。

## 身份验证和头

为了成功调用平台端点，您需要完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为Experience Platform API调用中每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### 沙箱头

Experience Platform中的所有资源都隔离到特定的虚拟沙箱。 对平台API的请求需要一个头，该头指定操作将在中进行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

有关平台中沙箱的详细信息，请参阅[沙箱概述文档](../sandboxes/home.md)。

### 内容类型标题

请求主体中具有有效负荷的所有请求(如POST、PUT和PATCH调用)都必须包含`Content-Type`头。 接受的值特定于每个API端点。 如果端点需要特定的`Content-Type`值，则其值将显示在各个平台服务](#api-guides)的[API指南提供的示例API请求中。

## Experience Platform API基础知识

Adobe Experience Platform API采用了若干重要的底层技术和语法，以便有效管理平台资源。

要进一步了解Platform使用的基础API技术(包括示例JSON模式对象)，请访问[Experience Platform API基础知识指南](api-fundamentals.md)。

## Experience PlatformAPI的邮递员集合

Postman是一个用于API开发的协作平台，它允许您使用预设变量设置环境、共享API集合、简化CRUD请求等。 大多数平台API服务都有Postman集合，可用于协助进行API调用。

要进一步了解Postman，包括如何设置环境、可用集合的列表以及如何导入集合，请访问[Platform Postman文档](postman.md)。

## 读取示例API调用{#sample-api}

请求格式因所使用的平台API而异。 了解如何构建API调用的最佳方式是跟随您所使用的特定平台服务文档中提供的示例。

[!DNL Experience Platform]的文档以两种不同的方式显示了示例API调用。 首先，调用以&#x200B;**API格式**&#x200B;显示，模板表示仅显示操作(GET、POST、PUT、PATCH、DELETE)和正在使用的端点（例如`/global/classes`）。 某些模板还显示变量的位置，以帮助说明如何构建调用，如`GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`。

然后，在&#x200B;**Request**&#x200B;中将调用显示为cURL命令，其中包括成功与API交互所需的必要标头和完整的“基本路径”。 基本路径应预置到所有端点。 例如，前面提到的`/global/classes`端点变为`https://platform.adobe.io/data/foundation/schemaregistry/global/classes`。 您将在整个文档中看到API格式/请求模式，在对平台API进行您自己的调用时，应使用示例请求中显示的完整路径。

### 示例API请求

以下是一个API请求示例，它演示了您在文档中将会遇到的格式。

**API格式**

API格式显示操作(GET)和正在使用的端点。 变量由花括号表示（在本例中为`{CONTAINER_ID}`）。

```http
GET /{CONTAINER_ID}/classes
```

**请求**

在此示例请求中，API格式的变量在请求路径中给出实际值。 此外，所有必需的标题都显示为示例标题值或应包含敏感信息（如安全令牌和访问ID）的变量。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

该响应说明了在基于发送的请求成功调用API后，您将收到什么。 有时，响应会因空间而截断，这意味着您可能会看到示例中显示的更多信息或其他信息。

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## 错误消息

[平台故障排除指南](troubleshooting.md#errors-and-troubleshooting)提供了使用任何Experience Platform服务时可能遇到的错误列表。

有关各个平台服务的疑难解答指南，请参阅[服务疑难解答目录](troubleshooting.md#service-troubleshooting-directory)。

有关平台API中特定端点（包括所需的标头和请求主体）的详细信息，请参阅[平台API指南](#api-guides)。

## 平台API指南{#api-guides}

| API指南 | 描述 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | [!DNL Access Control] API端点可以检索对指定沙箱内给定资源上的用户有效的当前策略。 所有其他访问控制功能都通过[Adobe Admin Console](https://adminconsole.adobe.com/)提供。 |
| [批处理API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API允许您将数据作为批处理文件引入平台。 所摄取的用户档案可以是来自CRM系统中的平面文件（如Parke文件）的模式数据，或符合注册表(XDM)中的已知模式的数据。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | [!DNL Catalog Service] API允许开发人员管理Adobe Experience Platform中的数据集元数据。 这包括数据位置、处理阶段、处理过程中发生的错误以及数据报告。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | [!DNL Data Access] API允许开发人员检索Experience Platform中收录的数据集的相关信息。 这包括访问和下载数据集文件、检索标题信息、列出失败和成功的批次，以及下载预览 CSV/Parke文件。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的Catalog Service API是分开的。 |
| [[!DNL Flow Service] API指南](.././sources/tutorials/api/create-dataset-base-connection.md) <br> （源和目标） | [!DNL Flow Service] API用于收集和集中来自不同来源的数据，并用于创建数据并将数据激活到Adobe Experience Platform中的不同目标。 该服务提供可连接所有受支持源的RESTful API。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | [!DNL Identity Service] API允许开发人员使用Adobe Experience Platform中的标识图管理跨设备、跨渠道和接近实时的客户标识。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights] 是一个RESTful API，它允许开发人员在Adobe Experience Platform中显示关键的可观测性指标。这些指标提供对平台使用统计数据的洞察、平台服务运行状况检查、历史趋势以及各种平台功能的性能指标。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （数据管理） | [!DNL Policy Service] API允许您创建和管理数据使用标签和策略，以确定可以对包含某些数据使用标签的数据采取哪些营销操作。 要将标签应用于数据集和字段，请参阅[[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md)指南 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | [!DNL Privacy Service] API允许开发人员创建和管理客户请求，以便跨Experience Cloud应用程序访问或删除其个人数据，这符合法律隐私法规。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | [!DNL Query Service] API允许开发人员使用标准SQL查询其Adobe Experience Platform数据。 |
| [[!DNL Real-time Customer Profile] API指南](.././profile/api/overview.md) | 实时客户用户档案API允许开发人员探索和使用用户档案数据，包括查看用户档案、创建和更新合并策略、导出或采样用户档案数据，以及删除不再需要或错误地添加的用户档案数据。 |
| [沙箱API指南](.././sandboxes/api/getting-started.md) | 沙箱API允许开发人员有计划地管理Adobe Experience Platform中的独立虚拟沙箱环境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | [!DNL Schema Registry] API允许开发人员以编程方式管理Adobe Experience Platform中的所有模式和相关体验数据模型(XDM)资源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | [!DNL Segmentation Service] API允许开发人员以编程方式管理Adobe Experience Platform中的分段操作。 这包括构建细分和根据实时客户用户档案数据生成受众。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> （数据科学工作区） | [!DNL Sensei Machine Learning] API为数据科学家提供了一个机制，用于组织和管理从算法入门、实验到服务部署的机器学习(ML)服务。 |

有关每个服务可用的特定端点和操作的详细信息，请参阅有关Adobe I/O的[API参考文档](http://www.adobe.com/go/platform-api-reference-en)。

## 后续步骤

本文档介绍了所需的标头、可用指南，并提供了一个示例API调用。 既然您拥有在Adobe Experience Platform上进行API调用所需的标头值，请从[平台API指南表](#api-guides)中选择要浏览的API端点。

有关常见问题解答的解答，请参阅[平台疑难解答指南](troubleshooting.md)。

要设置邮递环境并浏览可用的邮递员集合，请参阅[平台邮递员指南](postman.md)。
