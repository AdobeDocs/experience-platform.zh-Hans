---
keywords: Experience Platform；主页；热门主题；API错误代码；API错误代码；错误代码API；错误代码API；API请求错误；API疑难解答；API错误
solution: Experience Platform
title: Adobe Experience Platform常见问题解答和疑难解答指南
description: 查找常见问题的解答以及 Adobe Experience Platform 中常见错误的疑难解答指南。
landing-page-description: 查找常见问题的解答以及 Adobe Experience Platform 中常见错误的疑难解答指南。
short-description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
type: Documentation
role: Developer
feature: API, Audiences, Data Ingestion, Datasets, Destinations, Privacy, Queries, Schemas, Sandboxes, Sources
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 4%

---

# [!DNL Experience Platform]常见问题解答和疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答，以及有关在任何[!DNL Experience Platform] API中可能遇到的常见错误的高级故障排除指南。 有关单个[!DNL Experience Platform]服务的故障排除指南，请参阅下面的[服务故障排除目录](#service-troubleshooting-directory)。

## 常见问题解答 {#faq}

以下是有关Adobe Experience Platform的常见问题解答列表。

## 什么是[!DNL Experience Platform] API？ {#what-are-experience-platform-apis}

[!DNL Experience Platform]提供多个RESTful API，它们使用HTTP请求访问[!DNL Experience Platform]资源。 这些服务API每个都会公开多个端点，并允许您执行列出(GET)、查找(GET)、编辑(PUT和/或PATCH)和删除(DELETE)资源的操作。 有关每个服务可用的特定端点和操作的更多信息，请参阅Adobe I/O上的[API参考文档](https://www.adobe.com/go/platform-api-reference-en)。

## 如何设置API请求的格式？ {#how-do-i-format-an-api-request}

请求格式因使用的[!DNL Experience Platform] API而异。 要了解如何构建API调用，最好的方法是，按照文档中为您使用的特定[!DNL Experience Platform]服务提供的示例进行操作。

有关格式化API请求的更多信息，请访问Experience Platform API快速入门指南[阅读示例API调用](./api-guide.md#sample-api)部分。

## 我的组织是什么？ {#what-is-my-ims-organization}

组织是客户的Adobe表示形式。 任何许可的Adobe解决方案均与此客户组织集成。 当组织有权使用[!DNL Experience Platform]时，它可以向开发人员分配访问权限。 组织ID (`x-gw-ims-org-id`)表示应为其执行API调用的组织，因此需要将其作为所有API请求中的标头。 可以通过[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)找到此ID：在&#x200B;**集成**&#x200B;选项卡中，导航到任何特定集成的&#x200B;**概述**&#x200B;部分，以在&#x200B;**客户端凭据**&#x200B;下查找此ID。 有关如何向[!DNL Experience Platform]进行身份验证的分步说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 在哪里可以找到我的API密钥？ {#where-can-i-find-my-api-key}

在所有API请求中，都需要API密钥作为标头。 可以通过[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)找到它。 在控制台的&#x200B;**集成**&#x200B;选项卡上，导航到特定集成的&#x200B;**概述**&#x200B;部分，您将在&#x200B;**客户端凭据**&#x200B;下找到密钥。 有关如何向[!DNL Experience Platform]进行身份验证的分步说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何获取访问令牌？ {#how-do-i-get-an-access-token}

所有API调用的Authorization标头中都需要访问令牌。 只要您有权访问组织的集成，就可以使用CURL命令生成这些区段。 访问令牌仅在24小时内有效，之后必须生成新令牌以继续使用API。 有关生成访问令牌的详细信息，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何使用查询参数？ {#how-do-i-user-query-parameters}

某些[!DNL Experience Platform] API端点接受查询参数以定位特定信息并筛选响应中返回的结果。 查询参数被附加到带有问号(`?`)的请求路径中，后跟一个或多个使用格式`paramName=paramValue`的查询参数。 在单个调用中组合多个参数时，必须使用&amp;符号(`&`)来分隔各个参数。 以下示例演示了文档如何表示使用多个查询参数的请求。

常用查询参数的示例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有关哪些查询参数适用于特定服务或端点的详细信息，请查看特定于服务的文档。

## 如何在PATCH请求中指定要更新的JSON字段？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

[!DNL Experience Platform] API中的许多PATCH操作都使用[JSON指针](https://tools.ietf.org/html/rfc6901)字符串来指示要更新的JSON属性。 这些通常包含在使用[JSON Patch](https://tools.ietf.org/html/rfc6902)格式的请求负载中。 有关这些技术所需语法的详细信息，请参阅[API基础指南](api-fundamentals.md)。

## 我可以使用Postman调用[!DNL Experience Platform] API吗？ {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/)是一种用于可视化对RESTful API的调用的有用工具。 [Experience Platform API快速入门指南](api-guide.md)包含有关导入Postman收藏集的视频和说明。 此外，还提供了每个服务的Postman收藏集列表。

## [!DNL Experience Platform]的系统要求是什么？ {#what-are-the-system-requirements-for-platform}

根据您使用的是UI还是API，将应用以下系统要求：

**对于基于UI的操作：**

- 一种现代化的标准网络浏览器。 虽然建议使用最新版本的[!DNL Chrome]，但也支持[!DNL Firefox]、[!DNL Internet Explorer]和Safari的当前和以前的主要版本。

   - 每次发布新的主要版本时，[!DNL Experience Platform]开始支持最新版本，而不再支持第三个最新版本。

- 所有浏览器都必须启用Cookie和JavaScript。

**对于API和开发人员交互：**

- 要为REST、流和Webhook集成开发的开发环境。

## 错误和故障排除 {#errors-and-troubleshooting}

以下是使用任何[!DNL Experience Platform]服务时可能遇到的错误列表。 有关单个[!DNL Experience Platform]服务的故障排除指南，请参阅下面的[服务故障排除目录](#service-troubleshooting-directory)。

## API状态代码 {#api-status-codes}

在任何[!DNL Experience Platform] API上可能会遇到以下状态代码。 每种原因都各不相同，因此本节中给出的解释具有一般性。 有关单个[!DNL Experience Platform]服务中特定错误的更多详细信息，请参阅下面的[服务疑难解答目录](#service-troubleshooting-directory)。

| 状态代码 | 描述 | 可能的原因 |
|--- | --- | ---|
| 400 | 请求无效 | 请求构造不正确、缺少关键信息和/或包含不正确的语法。 |
| 401 | 身份验证失败 | 请求未通过身份验证检查。 您的访问令牌可能缺失或无效。 有关更多详细信息，请参阅下面的[OAuth令牌错误](#oauth-token-is-missing)部分。 |
| 403 | 禁止 | 已找到该资源，但您没有查看该资源的正确凭据。 <br>导致此错误的可能原因是您可能没有访问或编辑资源所需的[访问控制权限](/help/access-control/home.md)。 了解如何[获取必要的基于属性的访问控制权限](/help/landing/api-authentication.md#get-abac-permissions)以使用Experience Platform API。 </p> |
| 404 | 未找到 | 在服务器上找不到请求的资源。 该资源可能已被删除，或者所请求的路径输入不正确。 |
| 500 | 内部服务器错误 | 这是服务器端错误。 如果您同时发起多个调用，则可能会达到API限制，需要筛选结果。 （请参阅[!DNL Catalog Service]过滤数据[上的](../catalog/api/filter-data.md) API开发人员指南子指南以了解详情。） 在重试您的请求之前，请等待片刻，如果问题仍然存在，请联系您的管理员。 |

## 请求标头错误 {#request-header-errors}

[!DNL Experience Platform]中的所有API调用都需要特定的请求标头。 要查看各个服务所需的标头，请参阅[API参考文档](https://www.adobe.com/go/platform-api-reference-en)。 要查找所需身份验证标头的值，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 如果在进行API调用时这些标头中有任何标头缺失或无效，则可能会出现以下错误。

### OAuth令牌缺失 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

当API请求中缺少`Authorization`标头时，显示此错误消息。 在重试之前，请确保授权标头包含有效访问令牌。

### OAuth令牌无效 {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

当`Authorization`标头中提供的访问令牌无效时，将显示此错误消息。 请确保已正确输入令牌，或[在Adobe I/O控制台中生成新令牌](https://www.adobe.com/go/platform-api-authentication-en)。

### 需要API密钥 {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

当API请求中缺少API密钥标头(`x-api-key`)时，显示此错误消息。 在重试之前，请确保标头包含有效的API密钥。

### API密钥无效 {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

当提供的API密钥标头(`x-api-key`)的值无效时，将显示此错误消息。 在重试之前，请确保已正确输入密钥。 如果您不知道自己的API密钥，可以在[Adobe I/O控制台](https://console.adobe.io)中找到它：在&#x200B;**集成**&#x200B;选项卡中，导航到&#x200B;**概述**&#x200B;部分以获取特定集成，从而在&#x200B;**客户端凭据**&#x200B;下查找API密钥。

### 缺少标头 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

当API请求中缺少组织标头(`x-gw-ims-org-id`)时，显示此错误消息。 在重试之前，请确保标头包含在组织的ID中。

### 配置文件无效 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

当用户或Adobe I/O集成（由[标头中的](#how-do-i-get-an-access-token)访问令牌`Authorization`标识）无权为[!DNL Experience Platform]标头中提供的组织调用`x-gw-ims-org-id` API时，将显示此错误消息。 在重试之前，请确保已在标头中为您的组织提供了正确的ID。 如果您不知道自己的组织ID，可以在[Adobe I/O控制台](https://console.adobe.io)中找到它：在&#x200B;**集成**&#x200B;选项卡中，导航到&#x200B;**概述**&#x200B;部分以进行特定集成，从而在&#x200B;**客户端凭据**&#x200B;下找到该ID。

### 刷新etag错误 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

如果其他API调用方更改了任何源或目标实体（如流、连接、源连接器或目标连接），您可能会收到etag错误。 由于版本不匹配，您尝试进行的更改将不会应用于实体的最新版本。

要解决此问题，需要再次获取实体，确保更改与实体的新版本兼容，然后将新etag放置在`If-Match`标头中，最后进行API调用。

### 未指定有效的内容类型 {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

当POST、PUT或PATCH请求的`Content-Type`标头无效或缺失时，显示此错误消息。 确保请求中包含标头且其值为`application/json`。

### 缺少用户区域 {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

此错误消息在以下两种情况之一中显示：

- 在API请求中传递不正确或格式错误的组织ID标头(`x-gw-ims-org-id`)时。 在重试之前，请确保包含组织的正确ID。
- 当您的帐户（由提供的身份验证凭据表示）未与Experience Platform的产品配置文件关联时。 按照Experience Platform API身份验证教程中[生成访问凭据](./api-authentication.md#authentication-for-each-session)的步骤操作，将Experience Platform添加到您的帐户并相应地更新身份验证凭据。

## 服务疑难解答目录 {#service-troubleshooting-directory}

以下是[!DNL Experience Platform] API的疑难解答指南和API参考文档列表。 每个疑难解答指南都提供常见问题的解答以及单个[!DNL Experience Platform]服务特有的问题的解决方案。 API参考文档为每个服务的所有可用端点提供全面的指南，并显示您可能收到的请求正文、响应和错误代码示例。

| 服务 | API 参考 | 故障排除 |
| --- | --- | --- |
| 访问控制 | [访问控制API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [访问控制疑难解答指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform数据摄取 | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [批处理摄取疑难解答指南](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform数据摄取 | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [流式摄取疑难解答指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform数据科学Workspace | [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) | [[!DNL Data Science Workspace] 疑难解答指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform数据管理 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform 身份标识服务 | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 疑难解答指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查询服务 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 疑难解答指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform区段 | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] 常见问题解答和疑难解答指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] （[!DNL Sources]和[!DNL Destinations]） | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 疑难解答指南](../profile/troubleshooting.md) |
| 沙盒 | [沙盒API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [沙盒疑难解答指南](../sandboxes/troubleshooting-guide.md) |
