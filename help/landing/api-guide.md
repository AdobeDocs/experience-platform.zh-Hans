---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform;API指南；平台API指南；平台简介；开发人员指南
solution: Experience Platform
title: 开始使用Adobe Experience Platform API
topic-legacy: api guide
description: Adobe Experience Platform提供彼此紧密关联的API服务。 本指南包含有关可用服务、CRUD操作所需标头、错误消息、Postman集合和示例API调用的信息。
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# 开始使用Adobe Experience Platform API

Adobe Experience Platform是按照“API优先”的理念开发的。 使用Platform API，您可以以编程方式对数据执行基本的CRUD（创建、读取、更新、删除）操作，例如配置计算属性、访问数据/实体、导出数据、删除不需要的数据或批次等。

每个Experience Platform服务的API都共享相同的身份验证标头集，并对其CRUD操作使用相似的语法。 以下指南概述了开始使用Platform API的必要步骤。

## 身份验证和标头

要成功调用Platform端点，您需要完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供Experience PlatformAPI调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 沙盒标头

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对Platform API的请求需要一个标头来指定操作将在其中进行的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

有关Platform中沙箱的更多信息，请参阅 [沙盒概述文档](../sandboxes/home.md).

### 内容类型标题

请求正文中具有有效负载的所有请求(例如POST、PUT和PATCH调用)都必须包含 `Content-Type` 标题。 接受的值特定于每个API端点。 如果 `Content-Type` 端点需要值，其值将显示在由提供的示例API请求中 [适用于各个Platform服务的API指南](#api-guides).

## Experience PlatformAPI基础知识

Adobe Experience Platform API使用了一些对于有效管理平台资源非常重要的底层技术和语法。

要详细了解Platform利用的基础API技术（包括示例JSON模式对象），请访问 [Experience PlatformAPI基础知识](api-fundamentals.md) 的双曲余切值。

## PostmanExperience PlatformAPI的收藏集

Postman是一个API开发协作平台，它允许您使用预设变量设置环境、共享API收藏集、简化CRUD请求等。 大多数Platform API服务都有Postman集合，可用于协助进行API调用。

要详细了解Postman，包括如何设置环境、可用收藏集列表以及如何导入收藏集，请访问 [Platform Postman文档](postman.md).

## 读取示例API调用 {#sample-api}

请求格式因使用的平台API而异。 了解如何构建API调用的最佳方法是，遵循文档中为您所使用的特定平台服务提供的示例。

的文档 [!DNL Experience Platform] 以两种不同的方式显示API调用示例。 首先，在 **API格式**，只显示操作(GET、POST、PUT、PATCH、DELETE)和正在使用的端点的模板表示形式(例如， `/global/classes`)。 某些模板还显示变量的位置，以帮助说明如何构建调用，例如 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

然后，调用将在 **请求**，包括成功与API交互所需的必需标头和完整“基本路径”。 基本路径应预先附加到所有端点。 例如，上述 `/global/classes` 终结点变成 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. 在整个文档中，您将看到API格式/请求模式，在对Platform API进行自己调用时，您应使用示例请求中显示的完整路径。

### API请求示例

以下是一个API请求示例，用于演示文档中将遇到的格式。

**API格式**

API格式显示操作(GET)和正在使用的端点。 变量以大括号表示(在本例中， `{CONTAINER_ID}`)。

```http
GET /{CONTAINER_ID}/classes
```

**请求**

在此示例请求中，API格式的变量在请求路径中给定实际值。 此外，所有必需的标头都显示为示例标头值或应包含敏感信息（如安全令牌和访问ID）的变量。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应说明了在成功调用API后，根据发送的请求将收到什么内容。 有时，响应的空间会被截断，这意味着您可能会看到示例中显示的更多信息或其他信息。

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

的 [平台疑难解答指南](troubleshooting.md#errors-and-troubleshooting) 提供在使用任何Experience Platform服务时可能遇到的错误列表。

有关单个Platform服务的疑难解答指南，请参阅 [服务疑难解答目录](troubleshooting.md#service-troubleshooting-directory).

有关Platform API中特定端点（包括所需的标头和请求主体）的更多信息，请参阅 [平台API指南](#api-guides).

## 平台API指南 {#api-guides}

| API指南 | 描述 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | 的 [!DNL Access Control] API端点可以检索对指定沙盒内的给定资源上的用户生效的当前策略。 所有其他访问控制功能均通过 [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [批量摄取API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API允许您将数据作为批处理文件导入到平台中。 摄取的数据可以是CRM系统中平面文件（如Parquet文件）中的配置文件数据，也可以是符合架构注册表中已知架构(XDM)的数据。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | 的 [!DNL Catalog Service] API允许开发人员在Adobe Experience Platform中管理数据集元数据。 这包括数据位置、处理阶段、处理过程中发生的错误以及数据报表。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | 的 [!DNL Data Access] API允许开发人员检索有关Experience Platform内摄取的数据集的信息。 这包括访问和下载数据集文件、检索标题信息、列出失败和成功的批次，以及下载预览CSV/Parquet文件。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | 的 [!DNL Identity Service] API允许开发人员使用Adobe Experience Platform中的身份图来管理客户的跨设备、跨渠道和近乎实时的标识。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights] 是一个RESTful API，它允许开发人员在Adobe Experience Platform中显示关键可观测性量度。 这些量度提供对平台使用情况统计数据的分析、平台服务的运行状况检查、历史趋势以及各种平台功能的性能指标。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （数据管理） | 的 [!DNL Policy Service] API允许您创建和管理数据使用标签和策略，以确定可以对包含某些数据使用标签的数据执行哪些营销操作。 要将标签应用于数据集和字段，请参阅 [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) 指南 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | 的 [!DNL Privacy Service] API允许开发人员创建和管理客户请求，以跨Experience Cloud应用程序访问或删除其个人数据，这符合法律隐私法规。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | 的 [!DNL Query Service] API允许开发人员使用标准SQL查询其Adobe Experience Platform数据。 |
| [[!DNL Real-Time Customer Profile] API指南](.././profile/api/overview.md) | 实时客户配置文件API允许开发人员探索和使用配置文件数据，包括查看配置文件、创建和更新合并策略、导出或采样配置文件数据，以及删除不再需要或错误添加的配置文件数据。 |
| [沙盒API指南](.././sandboxes/api/getting-started.md) | 沙盒API允许开发人员以编程方式管理Adobe Experience Platform中的独立虚拟沙盒环境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | 的 [!DNL Schema Registry] API允许开发人员以编程方式管理Adobe Experience Platform中的所有模式和相关的Experience Data Model(XDM)资源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | 的 [!DNL Segmentation Service] API允许开发人员以编程方式管理Adobe Experience Platform中的分段操作。 这包括构建区段并根据实时客户资料数据生成受众。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> （数据科学工作区） | 的 [!DNL Sensei Machine Learning] API为数据科学家提供了一种机制，用于组织和管理机器学习(ML)服务，从算法载入、实验到服务部署。 |

有关每项服务可用的特定端点和操作的更多信息，请参阅 [API参考文档](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

## 后续步骤

本文档介绍了所需的标头、可用指南，并提供了一个示例API调用。 现在，您已拥有在Adobe Experience Platform上进行API调用所需的标头值，接下来请选择您希望从 [平台API指南表](#api-guides).

有关常见问题解答的解答，请参阅 [平台疑难解答指南](troubleshooting.md).

要设置Postman环境并浏览可用的Postman收藏集，请参阅 [Platform Postman指南](postman.md).
