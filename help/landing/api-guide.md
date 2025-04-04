---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；API指南；平台API指南；平台简介；开发人员指南
solution: Experience Platform
title: Adobe Experience Platform API快速入门
description: Adobe Experience Platform提供的API服务彼此密切相关。 本指南包含有关可用服务、CRUD操作所需的标头、错误消息、Postman收藏集和示例API调用的信息。
role: Developer
feature: API
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Adobe Experience Platform API快速入门

Adobe Experience Platform是根据“API优先”的理念开发的。 使用Experience Platform API，您可以以编程方式对数据执行基本的CRUD（创建、读取、更新、删除）操作，例如配置计算属性、访问数据/实体、导出数据、删除不需要的数据或批次等。

每个Experience Platform服务的API都共享同一组身份验证标头，并对其CRUD操作使用类似的语法。 以下指南概述了Experience Platform API快速入门的必要步骤。

## 身份验证和标头

要成功调用Experience Platform端点，您需要完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为Experience Platform API调用中的每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 沙盒标头

Experience Platform中的所有资源都被隔离到特定的虚拟沙盒中。 对Experience Platform API的请求需要一个标头，该标头指定将在其中执行操作的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

有关Experience Platform中沙盒的更多信息，请参阅[沙盒概述文档](../sandboxes/home.md)。

### 内容类型标头

所有在请求正文中具有有效负载的请求(如POST、PUT和PATCH调用)都必须包含`Content-Type`标头。 接受的值特定于每个API端点。 如果端点需要特定`Content-Type`值，其值将显示在[API指南为各个Experience Platform服务](#api-guides)提供的示例API请求中。

## Experience Platform API基础

Adobe Experience Platform API使用多种底层技术和语法，这些技术和语法对于有效管理Experience Platform资源非常重要，需要了解。

要了解有关Experience Platform使用的基础API技术（包括示例JSON模式对象）的更多信息，请访问[Experience Platform API基础知识](api-fundamentals.md)指南。

## Experience Platform API的Postman收藏集

Postman是API开发的协作平台，允许您使用预设变量设置环境、共享API收藏集、简化CRUD请求等。 大多数Experience Platform API服务都具有Postman收藏集，这些收藏集可用于协助进行API调用。

要了解有关Postman的更多信息（包括如何设置环境、可用收藏集列表以及如何导入收藏集），请访问[Experience Platform Postman文档](postman.md)。

## 正在读取示例 API 调用 {#sample-api}

请求格式因使用的Experience Platform API而异。 了解如何构建API调用结构的最佳方法是，遵循文档中为您使用的特定Experience Platform服务提供的示例。

[!DNL Experience Platform]的文档以两种不同的方式显示示例API调用。 首先，调用以其&#x200B;**API格式**&#x200B;呈现，此模板表示仅显示操作(GET、POST、PUT、PATCH、DELETE)和正在使用的端点（例如`/global/classes`）。 某些模板还显示变量的位置，以帮助说明应如何制定调用，如`GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`。

然后，这些调用在&#x200B;**请求**&#x200B;中显示为cURL命令，其中包括成功与API交互所需的必要标头和完整的“基本路径”。 基本路径应预先附加到所有端点。 例如，前面提到的`/global/classes`端点变为`https://platform.adobe.io/data/foundation/schemaregistry/global/classes`。 您将在整个文档中看到API格式/请求模式，并在对Experience Platform API进行您自己的调用时，应使用示例请求中显示的完整路径。

### 示例API请求

以下是一个API请求示例，用于演示将在文档中遇到的格式。

**API格式**

API格式显示了操作(GET)和正在使用的端点。 变量用大括号指示（在本例中为`{CONTAINER_ID}`）。

```http
GET /{CONTAINER_ID}/classes
```

**请求**

在此示例请求中，API格式的变量在请求路径中给定实际值。 此外，所有必需的标头都会显示为标头值示例或变量，其中应包含敏感信息（例如安全令牌和访问ID）。

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

响应将基于发送的请求说明在成功调用API后您会收到什么内容。 有时，响应会截断空格，这意味着您可能会看到示例中显示的详细信息或附加信息。

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

[Experience Platform疑难解答指南](troubleshooting.md#errors-and-troubleshooting)提供了您在使用任何Experience Platform服务时可能遇到的错误列表。

有关单个Experience Platform服务的故障排除指南，请参阅[服务故障排除目录](troubleshooting.md#service-troubleshooting-directory)。

有关Experience Platform API中特定端点的更多信息，包括所需的标头和请求正文，请参阅[Experience Platform API指南](#api-guides)。

## Experience Platform API指南 {#api-guides}

| API指南 | 描述 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | [!DNL Access Control] API终结点可以在指定沙盒内的给定资源上检索某个用户有效的当前策略。 所有其他访问控制功能均通过[Adobe Admin Console](https://adminconsole.adobe.com/)提供。 |
| [批次摄取API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API允许您将数据作为批处理文件摄取到Experience Platform中。 所摄取的数据可以是来自CRM系统中平面文件（如Parquet文件）的配置文件数据，也可以是与架构注册表(XDM)中的已知架构相符的数据。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | [!DNL Catalog Service] API允许开发人员在Adobe Experience Platform中管理数据集元数据。 这包括数据位置、处理阶段、处理期间发生的错误和数据报表。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | [!DNL Data Access] API允许开发人员检索Experience Platform中已摄取的数据集的信息。 这包括访问和下载数据集文件、检索标头信息、列出失败和成功的批处理，以及下载预览CSV/Parquet文件。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。 |
| [[!DNL Data Hygiene API guide]](../hygiene/api/overview.md) | [!DNL Data Hygiene] API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据，以及安排数据集的到期日期。 |
| [[!DNL Edge Network Server] API指南](../server-api/overview.md) | [!DNL Edge Network Server API]可用于各种数据收集、个性化、广告和营销用例。 [!DNL Server API]可用于服务器、[!DNL IoT]设备、机顶盒和其他各种设备。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | [!DNL Identity Service] API允许开发人员使用Adobe Experience Platform中的标识图管理客户的跨设备、跨渠道和近乎实时的身份识别。 |
| [[!DNL MTLS Service API guide]](../data-governance/mtls-api/overview.md) | [!DNL MTLS Service] API允许您安全地检索Adobe为您的组织颁发的公共证书。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights]是一个RESTful API，它允许开发人员在Adobe Experience Platform中公开关键可观察性指标。 这些指标可深入分析Experience Platform使用统计数据、Experience Platform服务的运行状况检查、历史趋势和各种Experience Platform功能的性能指标。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （数据管理） | [!DNL Policy Service] API允许您创建和管理数据使用标签和策略，以确定可以对包含特定数据使用标签的数据执行哪些营销操作。 要将标签应用于数据集和字段，请参阅[[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md)指南 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | [!DNL Privacy Service] API允许开发人员创建和管理客户请求，以访问或删除他们在Experience Cloud应用程序中的个人数据，从而符合隐私法规。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | [!DNL Query Service] API允许开发人员使用标准SQL查询其Adobe Experience Platform数据。 |
| [[!DNL Real-Time Customer Profile] API指南](.././profile/api/overview.md) | 实时客户个人资料API允许开发人员探索和使用个人资料数据，包括查看个人资料、创建和更新合并策略、导出或取样个人资料数据，以及删除不再需要或添加错误的个人资料数据。 |
| [沙盒API指南](.././sandboxes/api/getting-started.md) | 沙盒API允许开发人员以编程方式管理Adobe Experience Platform中的独立虚拟沙盒环境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | [!DNL Schema Registry] API允许开发人员以编程方式管理Adobe Experience Platform中的所有架构和相关体验数据模型(XDM)资源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | [!DNL Segmentation Service] API允许开发人员以编程方式管理Adobe Experience Platform中的分段操作。 这包括从实时客户档案数据构建区段和生成受众。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> (数据科学Workspace) | [!DNL Sensei Machine Learning] API为数据科学家提供了一种机制，可用于组织和管理机器学习(ML)服务，从算法载入、实验到服务部署。 |

有关每个服务可用的特定端点和操作的更多信息，请参阅Adobe I/O上的[API参考文档](https://www.adobe.com/go/platform-api-reference-en)。

## 后续步骤

本文档介绍了所需的标头、可用的指南，并提供了一个示例API调用。 现在您已具有在Adobe Experience Platform上进行API调用所需的标头值，请从[Experience Platform API指南表](#api-guides)中选择要探索的API端点。

有关常见问题的解答，请参阅[Experience Platform疑难解答指南](troubleshooting.md)。

要设置Postman环境并浏览可用的Postman收藏集，请参阅[Experience Platform Postman指南](postman.md)。
