---
keywords: Experience Platform；主页；热门主题；API错误代码；API错误代码；错误代码API；错误代码API；API请求错误；API疑难解答；API错误
solution: Experience Platform
title: Adobe Experience Platform常见问题解答和疑难解答指南
description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
landing-page-description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
short-description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 4%

---

# [!DNL Platform] 常见问题和疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答，以及有关在任何环境中可能遇到的常见错误的高级故障排除指南 [!DNL Experience Platform] API。 有关单个的故障诊断指南 [!DNL Platform] 服务，请参见 [服务疑难解答目录](#service-troubleshooting-directory) 下面的。

## 常见问题解答 {#faq}

以下是有关Adobe Experience Platform的常见问题解答列表。

## 什么是 [!DNL Experience Platform] API？ {#what-are-experience-platform-apis}

[!DNL Experience Platform] 提供多个使用HTTP请求访问的RESTful API [!DNL Platform] 资源。 这些服务API都公开多个端点，并允许您执行列出(GET)、查找(GET)、编辑(PUT和/或PATCH)以及删除(DELETE)资源的操作。 欲了解每项服务可用的特定端点和操作的更多信息，请参阅 [API参考文档](https://www.adobe.com/go/platform-api-reference-en) 在Adobe I/O时。

## 如何设置API请求的格式？ {#how-do-i-format-an-api-request}

请求格式因 [!DNL Platform] 正在使用的API。 了解如何构建API调用的最佳方法是遵循特定文档提供的示例 [!DNL Platform] 您正在使用的服务。

有关格式化API请求的更多信息，请访问Platform API快速入门指南 [读取示例API调用](./api-guide.md#sample-api) 部分。

## 我的组织是什么？ {#what-is-my-ims-organization}

组织是客户的Adobe表示形式。 任何许可的Adobe解决方案都与此客户公司集成。 当组织有权享有 [!DNL Experience Platform]，可向开发人员分配访问权限。 组织ID (`x-gw-ims-org-id`)表示应为其执行API调用的组织，因此需要将其作为所有API请求中的标头。 此ID可通过 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui)：在 **集成** 选项卡，导航到 **概述** 部分，以查找ID **客户端凭据**. 有关如何在中进行身份验证的分步说明 [!DNL Platform]，请参见 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 在哪里可以找到我的API密钥？ {#where-can-i-find-my-api-key}

在所有API请求中，都需要API密钥作为标头。 可通过 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui). 在控制台的 **集成** 选项卡，导航到 **概述** 部分，您将找到位于下的键 **客户端凭据**. 有关如何向进行身份验证的分步说明 [!DNL Platform]，请参见 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 如何获取访问令牌？ {#how-do-i-get-an-access-token}

所有API调用的Authorization标头中都需要访问令牌。 它们可以使用CURL命令生成，前提是您有权访问组织的集成。 访问令牌仅在24小时内有效，之后必须生成新令牌才能继续使用API。 有关生成访问令牌的详细信息，请参阅 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 如何使用查询参数？ {#how-do-i-user-query-parameters}

部分 [!DNL Platform] API端点接受查询参数以定位特定信息并筛选响应中返回的结果。 查询参数被附加到带有问号(`?`)符号，后跟一个或多个使用格式的查询参数 `paramName=paramValue`. 在单个调用中组合多个参数时，必须使用&amp;符号(`&`)以分隔各个参数。 以下示例演示了使用多个查询参数的请求在文档中的表示方式。

常用查询参数的示例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有关哪些查询参数可用于特定服务或端点的详细信息，请查看特定于服务的文档。

## 如何在PATCH请求中指定要更新的JSON字段？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

中的许多PATCH操作 [!DNL Platform] API使用 [JSON指针](https://tools.ietf.org/html/rfc6901) 用于指示要更新的JSON属性的字符串。 这些通常包含在请求有效负载中，使用 [JSON修补程序](https://tools.ietf.org/html/rfc6902) 格式。 请参阅 [API基础知识指南](api-fundamentals.md) 以了解有关这些技术所需语法的详细信息。

## 我能否使用Postman调用 [!DNL Platform] API？ {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 是一个用于可视化对RESTful API的调用的有用工具。 此 [Platform API入门指南](api-guide.md) 包含有关导入Postman收藏集的视频和说明。 此外，还提供每个服务的Postman收藏集列表。

## 系统要求是什么 [!DNL Platform]？ {#what-are-the-system-requirements-for-platform}

根据您使用的是UI还是API，将应用以下系统要求：

**对于基于UI的操作：**
- 标准的新式Web浏览器。 而最新版本的 [!DNL Chrome] 建议当前和以前的主要版本 [!DNL Firefox]， [!DNL Internet Explorer]还支持、和Safari。
   - 每次发布新的主要版本时， [!DNL Platform] 开始支持最新版本，而不再支持第三个最新版本。
- 所有浏览器都必须启用Cookie和JavaScript。

**对于API和开发人员交互：**
- 为REST、流和Webhook集成开发的开发环境。

## 错误和疑难解答 {#errors-and-troubleshooting}

以下是使用任意 [!DNL Experience Platform] 服务。 有关单个的故障诊断指南 [!DNL Platform] 服务，请参见 [服务疑难解答目录](#service-troubleshooting-directory) 下面的。

## API状态代码 {#api-status-codes}

在任意 [!DNL Experience Platform] API。 每一种情况都有各种原因，因此本节中给出的解释具有一般性。 有关单个错误的特定错误的详细信息 [!DNL Platform] 服务，请参阅 [服务疑难解答目录](#service-troubleshooting-directory) 下面的。

| 状态代码 | 描述 | 可能的原因 |
|--- | --- | ---|
| 400 | 错误请求 | 请求构造不正确、缺少关键信息和/或包含不正确的语法。 |
| 401 | 身份验证失败 | 请求未通过身份验证检查。 您的访问令牌可能缺失或无效。 请参阅 [OAuth令牌错误](#oauth-token-is-missing) 部分，以了解更多详细信息。 |
| 403 | 禁止 | 找到了资源，但您没有查看该资源的正确凭据。 |
| 404 | 未找到 | 在服务器上找不到请求的资源。 该资源可能已被删除，或者所请求的路径输入不正确。 |
| 500 | 内部服务器错误 | 这是服务器端错误。 如果您同时进行多次调用，则可能已达到API限制，需要筛选结果。 (请参阅 [!DNL Catalog Service] 上的API开发人员指南子指南 [筛选数据](../catalog/api/filter-data.md) 以了解详情。) 在重试您的请求之前，请等待片刻，如果问题仍然存在，请联系您的管理员。 |

## 请求标头错误 {#request-header-errors}

中的所有API调用 [!DNL Platform] 需要特定的请求标头。 要查看各个服务所需的标头，请参阅 [API参考文档](https://www.adobe.com/go/platform-api-reference-en). 要查找所需身份验证标头的值，请参阅 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 如果在进行API调用时缺少这些标头中的任何一个或这些标头无效，则可能会出现以下错误。

### OAuth令牌缺失 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

出现以下错误消息时 `Authorization` api请求中缺少标头。 在重试之前，请确保授权标头包含有效访问令牌。

### OAuth令牌无效 {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

当提供的访问令牌位于以下位置时，显示此错误消息： `Authorization` 标头无效。 确保已正确输入令牌，或 [生成新令牌](https://www.adobe.com/go/platform-api-authentication-en) 在Adobe I/O控制台中。

### 需要API密钥 {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

当API密钥标头(`x-api-key`API请求中缺少)。 在重试之前，请确保标头包含有效的API密钥。

### API密钥无效 {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

当提供的API密钥标头的值(`x-api-key`)无效。 在重试之前，请确保已正确输入密钥。 如果您不知道自己的API密钥，可以在 [Adobe I/O控制台](https://console.adobe.io)：在 **集成** 选项卡，导航到 **概述** 部分，了解特定集成的API密钥，位于 **客户端凭据**.

### 缺少标头 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

当组织标头(`x-gw-ims-org-id`API请求中缺少)。 在重试之前，请确保标头包含在组织的ID中。

### 配置文件无效 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

当用户或Adobe I/O集成(由 [访问令牌](#how-do-i-get-an-access-token) 在 `Authorization` 标头)无权调用 [!DNL Experience Platform] 中提供的组织API `x-gw-ims-org-id` 标头。 在重试之前，请确保已在标头中为您的组织提供了正确的ID。 如果您不知道自己的组织ID，可以在 [Adobe I/O控制台](https://console.adobe.io)：在 **集成** 选项卡，导航到 **概述** 部分，以便在其中查找ID **客户端凭据**.

### 刷新etag错误 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

如果其他API调用方更改了任何源或目标实体（如流、连接、源连接器或目标连接），您可能会收到etag错误。 由于版本不匹配，您尝试进行的更改将不会应用于实体的最新版本。

要解决此问题，需要再次获取实体，确保更改与实体的新版本兼容，然后将新电子标签放入 `If-Match` 标头，最后进行API调用。

### 未指定有效的内容类型 {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

当POST、PUT或PATCH请求无效或缺失时，显示此错误消息 `Content-Type` 标头。 确保请求中包含标头，且其值为 `application/json`.

### 缺少用户区域 {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

以下两种情况之一会显示此错误消息：
- 当组织ID标头不正确或格式不正确时(`x-gw-ims-org-id`)在API请求中传递。 在重试之前，请确保包含组织的正确ID。
- 当您的帐户（由提供的身份验证凭据表示）未与Experience Platform的产品配置文件关联时。 按照上的步骤操作 [生成访问凭据](./api-authentication.md#authentication-for-each-session) 在Platform API身份验证教程中，将Platform添加到您的帐户并相应地更新身份验证凭据。

## 服务疑难解答目录 {#service-troubleshooting-directory}

以下列出了针对的疑难解答指南和API参考文档 [!DNL Experience Platform] API。 每个故障排除指南都提供常见问题的解答以及特定于个人的问题的解决方法 [!DNL Platform] 服务。 API参考文档为每个服务的所有可用端点提供了全面的指南，并显示您可能收到的请求正文、响应和错误代码示例。

| 服务 | API 参考 | 故障排除 |
| --- | --- | --- |
| 访问控制 | [访问控制API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [访问控制疑难解答指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform数据引入 | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [批量摄取疑难解答指南](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform数据引入 | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [流摄取疑难解答指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform数据科学工作区 | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑难解答指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform数据管理 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 疑难解答指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查询服务 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 疑难解答指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform区段 | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] 常见问题和疑难解答指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 疑难解答指南](../profile/troubleshooting.md) |
| 沙盒 | [沙盒API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [沙盒疑难解答指南](../sandboxes/troubleshooting-guide.md) |
