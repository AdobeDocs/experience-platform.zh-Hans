---
keywords: Experience Platform;home;popular topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Adobe Experience Platform常见问题解答和疑难解答指南
description: 查找常见问题的解答以及Experience Platform中常见错误的疑难解答指南。
topic: getting started
type: Documentation
user-guide-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
translation-type: tm+mt
source-git-commit: bc7c0a5d59c666ba80fac81a859b5ecf4dd37412
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 3%

---


# [!DNL Platform] 常见问题解答和疑难解答指南

此文档提供有关Adobe Experience Platform的常见问题解答，以及针对任何API中可能遇到的常见错误的高级故障排除 [!DNL Experience Platform] 指南。 有关各项服务的疑难 [!DNL Platform] 解答指南，请参 [阅以下服务疑难解答目录](#service-troubleshooting-directory) 。

## 常见问题解答 {#faq}

以下是有关Adobe Experience Platform的常见问题的一列表解答。

## 什么是 [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] 优惠多个使用HTTP请求访问资源的RESTful [!DNL Platform] API。 这些服务API每个都公开多个端点，并允许您对列表(GET)、查找(GET)、编辑(PUT和／或PATCH)和删除(DELETE)资源执行操作。 有关每个服务可用的特定端点和操作的详细信息，请参 [阅AdobeI/O的](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) API参考文档。

## 如何设置API请求的格式？ {#how-do-i-format-an-api-request}

请求格式因所使用的 [!DNL Platform] API而异。 了解如何构建API调用的最佳方法是，按照您所使用的特定服务文档中提供的 [!DNL Platform] 示例进行操作。

### 读取示例API调用

文档以两 [!DNL Experience Platform] 种不同的方式显示示例API调用。 首先，调用以其API **格式显示**，模板表示只显示操作(GET、POST、PUT、PATCH、DELETE)和正在使用的端点(例如， `/global/classes`)。 一些模板还显示变量的位置，以帮助说明如何构建调用，例如 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`。

调用随后在请求中显示为cURL **命令**，该请求包括成功与API交互所需的必要标头和完整“基本路径”。 基本路径应预先附加到所有端点。 例如，前面提到的 `/global/classes` 端点变 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`为。 您将在整个文档中看到API格式／请求模式，在对平台API进行自己的调用时，应使用示例请求中显示的完整路径。

### 示例API请求

下面是一个API请求示例，它演示了您在文档中将遇到的格式。

**API格式**

API格式显示操作(GET)和正在使用的端点。 变量由大括号(本例中为 `{CONTAINER_ID}`)表示。

```http
GET /{CONTAINER_ID}/classes
```

**请求**

在此示例请求中，API格式的变量在请求路径中被赋予实际值。 所有必需的标头也会显示，例如，应包含敏感信息（如安全令牌和访问ID）的示例标头值或变量。

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

该响应说明了根据发送的请求，在成功调用API后您会收到什么。 有时，响应会因空间而截断，这意味着您可能会看到示例中显示的更多信息或其他信息。

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

有关平台API中特定端点（包括所需的头和请求主体）的更多信息，请参阅 [API参考文档](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)。

## 我的IMS组织是什么？ {#what-is-my-ims-organization}

IMS组织是Adobe的代表。 任何许可的Adobe解决方案都与此客户组织集成。 当IMS组织有权访问时， [!DNL Experience Platform]它可以将访问权限分配给开发人员。 IMS组织ID(`x-gw-ims-org-id`)表示应执行API调用的组织，因此作为所有API请求的头是必需的。 此ID可通过Adobe开发人 [员控制台找到](https://www.adobe.com/go/devs_console_ui):在“集 **成** ”选项卡中，导 **航至任何特定集** 成 **的“概述”部分，以在“客户端凭据”**&#x200B;下查找ID。 有关如何进行身份验证的分步演练，请参 [!DNL Platform]阅身份验证 [教程](../tutorials/authentication.md)。

## 在哪里可以找到我的API密钥？ {#where-can-i-find-my-api-key}

所有API请求中都需要API密钥作为头。 它可以通过Adobe开发 [人员控制台找到](https://www.adobe.com/go/devs_console_ui)。 在控制台中，在“集 **成** ”选项卡上，导航到特定集 **成的“概述** ”部分，您将在“客户端凭据” **下找到密钥**。 有关如何进行身份验证的分步演练，请参 [!DNL Platform]阅身份验证 [教程](../tutorials/authentication.md)。

## 如何获得访问令牌? {#how-do-i-get-an-access-token}

访问令牌在所有API调用的“授权”标头中是必需的。 如果您有权访问IMS `curl` 组织的集成，则可以使用命令生成这些组件。 访问令牌仅在24小时内有效，之后必须生成新令牌才能继续使用API。 有关生成访问令牌的详细信息，请参 [阅身份验证教程](../tutorials/authentication.md)。

## 如何使用查询参数？ {#how-do-i-user-query-parameters}

某些 [!DNL Platform] API端点接受查询参数来查找特定信息并过滤响应中返回的结果。 查询参数用问号()符号附加到请`?`求路径中，后跟一个或多个查询参数，使用格式 `paramName=paramValue`。 在单个调用中组合多个参数时，必须使用和号()`&`来分隔各个参数。 以下示例演示了如何使用多个查询参数的请求在文档中的表示方式。

常用查询参数的示例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有关特定服务或端点可使用哪些查询参数的详细信息，请查阅特定于服务的文档。

## 如何在PATCH请求中指示要更新的JSON字段？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

API中的许多PATCH [!DNL Platform] 操作 [都使用JSON指](https://tools.ietf.org/html/rfc6901) 针字符串，以指示要更新的JSON属性。 这些修补程序通常包含在使用JSON修补程 [序格式的请求负载](https://tools.ietf.org/html/rfc6902) 中。 有关这些 [技术所需语法的详](api-fundamentals.md) 细信息，请参阅API基础知识指南。

## 我是否可以使用邮递员调用 [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 是一种将对RESTful API的调用可视化的实用工具。 此 [中篇文章](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) 介绍如何设置Postman以自动执行身份验证，并使用它使用 [!DNL Experience Platform] API。

## 系统要求有哪些 [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

根据您是使用UI还是API，系统要求如下：

**对于基于UI的操作：**
- 现代、标准的Web浏览器。 虽然建议使用最 [!DNL Chrome] 新版本，但还支持当前和以前 [!DNL Firefox]的 [!DNL Internet Explorer]主要版本、Safari和Safari。
   - 每次发布新的主要版本时， [!DNL Platform] 支持最新版本的开始将被放弃，而支持第三个最新版本。
- 所有浏览器都必须启用cookie和JavaScript。

**对于API和开发人员交互：**
- 用于为REST、流和Webhook集成进行开发的开发环境。

## 错误和疑难解答 {#errors-and-troubleshooting}

以下是您在使用任何服务时可能遇到的一列表 [!DNL Experience Platform] 错误。 有关各项服务的疑难 [!DNL Platform] 解答指南，请参 [阅以下服务疑难解答目录](#service-troubleshooting-directory) 。

## API状态代码 {#api-status-codes}

在任何API上都可能遇到以下状 [!DNL Experience Platform] 态代码。 各有各种原因，因此本节所作的解释是一般性的。 有关各个服务中特定错误的更 [!DNL Platform] 多详细信息，请参 [阅以下服务疑难解答目录](#service-troubleshooting-directory) 。

| 状态代码 | 描述 | 可能的原因 |
--- | --- | ---
| 400 | 错误请求 | 请求构造不正确、缺少密钥信息和／或包含不正确的语法。 |
| 401 | 身份验证失败 | 请求未通过身份验证检查。 您的访问令牌可能缺失或无效。 有关更多详 [细信息，请参阅](#oauth-token-is-missing) 下面的OAuth令牌错误部分。 |
| 403 | 禁止 | 已找到该资源，但您没有正确的凭据来视图它。 |
| 404 | 未找到 | 在服务器上找不到请求的资源。 该资源可能已被删除，或请求的路径输入不正确。 |
| 500 | 内部服务器错误 | 这是服务器端错误。 如果您同时进行多个调用，则可能达到API限制，需要过滤结果。 (有关筛选 [!DNL Catalog Service] 数据，请参阅API开发人员指南子指 [南](../catalog/api/filter-data.md) ，了解更多信息。) 请等待片刻，然后再次尝试请求，如果问题仍然存在，请与管理员联系。 |

## 请求标题错误 {#request-header-errors}

中的所有API调用 [!DNL Platform] 都需要特定的请求标头。 要查看各个服务需要哪些标头，请参阅API [参考文档](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)。 要查找所需身份验证头的值，请参阅身份验证 [教程](../tutorials/authentication.md)。 如果在进行API调用时这些标头中的任何一个缺失或无效，则可能会发生以下错误。

### 缺少OAuth令牌 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

当API请求中缺少标 `Authorization` 头时，将显示此错误消息。 在再次尝试之前，请确保授权标头包含在有效访问令牌中。

### OAuth令牌无效

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

当标题中提供的访问令牌无效时 `Authorization` 显示此错误消息。 确保已正确输入令牌，或 [在AdobeI](../tutorials/authentication.md) /O控制台中生成新令牌。

### 需要API密钥

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

当API请求中缺少API密钥头(`x-api-key`)时，将显示此错误消息。 在再次尝试之前，请确保标头包含有效的API密钥。

### API密钥无效

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

当提供的API密钥头()的值无效时，将显`x-api-key`示此错误消息。 再次尝试之前，请确保输入的密钥正确无误。 如果您不知道您的API密钥，可以在AdobeI/O控 [制台中找到它](https://console.adobe.io):在“集 **成** ”选项卡中，导 **航到“概述** ”部分，以查找特定集成的API密钥在“客户端凭据” **下的位置**。


### 缺少标题

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

当API请求中缺少IMS组织头()`x-gw-ims-org-id`时，将显示此错误消息。 在再次尝试之前，请确保头包含在IMS组织的ID中。

### 用户档案无效

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

当用户或AdobeI/O集成(标题中的 [访问令牌](#how-do-i-get-an-access-token)`Authorization` 标识)无权调用标题中提 [!DNL Experience Platform] 供的IMS组织的API时，将显示此错 `x-gw-ims-org-id` 误消息。 在再次尝试之前，请确保已在头中为IMS组织提供了正确的ID。 如果您不知道您的组织ID，您可以在AdobeI/O控 [制台中找到它](https://console.adobe.io):在“集 **成** ”选项卡中，导 **航至“概述** ”部分，以查找特定集成的“客户端凭据 **”下的ID**。

### 未指定有效的内容类型

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

当POST、PUT或PATCH请求标头无效或缺失时，将显示此错误 `Content-Type` 消息。 确保请求中包含标题，并且其值为 `application/json`。


## 服务疑难解答目录 {#service-troubleshooting-directory}

以下是API的疑难解答指南和API参考文档的 [!DNL Experience Platform] 列表。 每个故障排除指南都提供针对特定服务的常见问题和问题的解答 [!DNL Platform] 。 API参考文档为每项服务的所有可用端点提供了全面的指南，并显示可能收到的示例请求主体、响应和错误代码。

| 服务 | API 参考 | 故障诊断 |
| --- | --- | --- |
| 访问控制 | [访问控制API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [访问控制疑难解答指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform数据摄取 | [[!DNL数据摄取API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [批量摄取疑难解答](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[指南流式摄取疑难解答指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform数据科学工作区 | [[!DNL Sensei机器学习API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑难解答指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform数据管理 | [[!DNL策略服务API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] 疑难解答指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查询处 | [[!DNL查询服务API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] 疑难解答指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform细分 | [[!DNL分段API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL目录服务API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL模式注册表API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] 常见问题解答和疑难解答指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL流服务API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL实时客户用户档案API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] 疑难解答指南](../profile/troubleshooting.md) |
| 沙盒 | [沙箱API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [沙箱疑难解答指南](../sandboxes/troubleshooting-guide.md) |

