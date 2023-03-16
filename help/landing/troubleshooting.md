---
keywords: Experience Platform；主页；热门主题；API错误代码；API错误代码；错误代码API；错误代码API;API请求错误；API疑难解答；API错误
solution: Experience Platform
title: Adobe Experience Platform常见问题解答和疑难解答指南
description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
landing-page-description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
short-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: b21367814e38fb5ee017709a29b39de982d59d24
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 3%

---

# [!DNL Platform] 常见问题解答和疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答，以及针对任何 [!DNL Experience Platform] API。 有关各个的故障诊断指南 [!DNL Platform] 服务，请参阅 [服务疑难解答目录](#service-troubleshooting-directory) 下。

## 常见问题解答 {#faq}

以下是有关Adobe Experience Platform的常见问题解答列表。

## 什么是 [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] 提供了多个使用HTTP请求访问的RESTful API [!DNL Platform] 资源。 这些服务API每个都会公开多个端点，并允许您执行以下操作：列出(GET)、查找(GET)、编辑(PUT和/或PATCH)以及删除(DELETE)资源。 有关每项服务可用的特定端点和操作的更多信息，请参阅 [API参考文档](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

## 如何设置API请求的格式？ {#how-do-i-format-an-api-request}

请求格式因 [!DNL Platform] 使用的API。 了解如何构建API调用的最佳方法是，遵循特定 [!DNL Platform] 服务。

有关创建API请求的更多信息，请访问Platform API快速入门指南 [读取示例API调用](./api-guide.md#sample-api) 中。

## 我的IMS组织是什么？ {#what-is-my-ims-organization}

IMS组织是Adobe的表示形式。 任何经许可的Adobe解决方案均与此客户组织集成。 当IMS组织有权 [!DNL Experience Platform]，它可以向开发人员分配访问权限。 IMS组织ID(`x-gw-ims-org-id`)表示应为执行API调用的组织，因此需要作为所有API请求中的标头。 可以通过 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui):在 **集成** 选项卡，导航到 **概述** 部分，以查找 **客户端凭据**. 有关如何在 [!DNL Platform]，请参阅 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 在哪里可以找到我的API密钥？ {#where-can-i-find-my-api-key}

所有API请求中都需要API密钥作为标头。 可通过 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui). 在控制台中， **集成** 选项卡，导航到 **概述** 部分，您将在 **客户端凭据**. 有关如何验证的分步说明 [!DNL Platform]，请参阅 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 如何获取访问令牌？ {#how-do-i-get-an-access-token}

所有API调用的授权标头中都需要使用访问令牌。 它们可以使用 `curl` 命令，前提是您有权访问IMS组织的集成。 访问令牌仅在24小时内有效，在此之后必须生成新令牌才能继续使用API。 有关生成访问令牌的详细信息，请参阅 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

## 如何使用查询参数？ {#how-do-i-user-query-parameters}

部分 [!DNL Platform] API端点接受查询参数以查找特定信息并筛选响应中返回的结果。 查询参数会附加到带有问号(`?`)符号，后跟一个或多个使用格式的查询参数 `paramName=paramValue`. 在单次调用中组合多个参数时，必须使用与号(`&`)来分隔各个参数。 以下示例演示了如何使用多个查询参数的请求在文档中的表示方式。

常用查询参数的示例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有关哪些查询参数可用于特定服务或端点的详细信息，请查阅特定于服务的文档。

## 如何在PATCH请求中指示要更新的JSON字段？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

中的许多PATCH操作 [!DNL Platform] API使用 [JSON指针](https://tools.ietf.org/html/rfc6901) 用于指示要更新的JSON属性的字符串。 这些负载通常使用 [JSON修补程序](https://tools.ietf.org/html/rfc6902) 格式。 请参阅 [API基础知识指南](api-fundamentals.md) 有关这些技术所需语法的详细信息。

## 我能否使用Postman [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 是一种将对RESTful API的调用可视化的有用工具。 的 [Platform API快速入门指南](api-guide.md) 包含有关导入Postman收藏集的视频和说明。 此外，还提供每项服务的Postman集合列表。

## 的系统要求 [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

根据您使用的是UI还是API，系统要求如下：

**对于基于UI的操作：**
- 现代化的标准Web浏览器。 而 [!DNL Chrome] 建议当前和以前的主要版本 [!DNL Firefox], [!DNL Internet Explorer]、和Safari也受支持。
   - 每次发布新的主版本时， [!DNL Platform] 开始支持最新版本，同时放弃对最新版本的支持。
- 所有浏览器都必须启用Cookie和JavaScript。

**对于API和开发人员交互：**
- 用于为REST、流和Webhook集成开发的开发环境。

## 错误和疑难解答 {#errors-and-troubleshooting}

以下是在使用任何 [!DNL Experience Platform] 服务。 有关各个的故障诊断指南 [!DNL Platform] 服务，请参阅 [服务疑难解答目录](#service-troubleshooting-directory) 下。

## API状态代码 {#api-status-codes}

可能会在任何 [!DNL Experience Platform] API。 各种原因各有不同，因此本节所作的解释一般性。 有关单个 [!DNL Platform] 服务，请参阅 [服务疑难解答目录](#service-troubleshooting-directory) 下。

| 状态代码 | 描述 | 可能的原因 |
|--- | --- | ---|
| 400 | 错误请求 | 请求构造不正确、缺少关键信息和/或包含错误语法。 |
| 401 | 身份验证失败 | 请求未通过身份验证检查。 您的访问令牌可能缺失或无效。 请参阅 [OAuth令牌错误](#oauth-token-is-missing) 部分以了解更多详细信息。 |
| 403 | 禁止 | 已找到资源，但您没有查看该资源的正确凭据。 |
| 404 | 未找到 | 在服务器上找不到请求的资源。 资源可能已删除，或请求的路径输入错误。 |
| 500 | 内部服务器错误 | 这是服务器端错误。 如果您同时进行多个调用，则可能已达到API限制，并且需要过滤结果。 (请参阅 [!DNL Catalog Service] 关于的API开发人员指南子指南 [过滤数据](../catalog/api/filter-data.md) 了解更多。) 再次尝试请求前等待片刻，如果问题仍然存在，请与管理员联系。 |

## 请求标头错误 {#request-header-errors}

中的所有API调用 [!DNL Platform] 需要特定的请求标头。 要了解各个服务需要哪些标头，请参阅 [API参考文档](https://www.adobe.com/go/platform-api-reference-en). 要查找所需身份验证标头的值，请参阅 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 如果在进行API调用时这些标头中的任何一个缺失或无效，则可能会发生以下错误。

### 缺少OAuth令牌 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

当 `Authorization` API请求中缺少标头。 再次尝试之前，请确保授权标头包含有效的访问令牌。

### OAuth令牌无效 {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

当 `Authorization` 标头无效。 确保令牌已正确输入，或 [生成新令牌](https://www.adobe.com/go/platform-api-authentication-en) Adobe I/O控制台中。

### 需要API密钥 {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

当API密钥标头(`x-api-key`)。 在重试之前，请确保标头包含有效的API密钥。

### API密钥无效 {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

当提供的API密钥标头的值(`x-api-key`)无效。 再次尝试之前，请确保已正确输入密钥。 如果您不知道自己的API密钥，可以在 [Adobe I/O控制台](https://console.adobe.io):在 **集成** 选项卡，导航到 **概述** 部分，用于查找下的API密钥 **客户端凭据**.

### 缺少标头 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

当IMS组织标头(`x-gw-ims-org-id`)。 再次尝试之前，请确保标头包含在IMS组织的ID中。

### 配置文件无效 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

当用户或Adobe I/O集成(由 [访问令牌](#how-do-i-get-an-access-token) 在 `Authorization` 头)无权对 [!DNL Experience Platform] 中提供的IMS组织的API `x-gw-ims-org-id` 标题。 再次尝试之前，请确保您在标头中为IMS组织提供了正确的ID。 如果您不知道自己的组织ID，可以在 [Adobe I/O控制台](https://console.adobe.io):在 **集成** 选项卡，导航到 **概述** 部分，以查找 **客户端凭据**.

### 刷新etag错误 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

如果其他API调用方对任何源实体或目标实体（如流、连接、源连接器或目标连接）进行了更改，则可能会收到etag错误。 由于版本不匹配，您尝试进行的更改将不会应用于实体的最新版本。

要解决此问题，您需要再次获取实体，确保所做的更改与实体的新版本兼容，然后将新标记放在 `If-Match` 头，最后进行API调用。

### 未指定有效的content-type {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

当POST、PUT或PATCH请求无效或缺失时，将显示此错误消息 `Content-Type` 标题。 确保标头包含在请求中，并且其值为 `application/json`.

### 用户区域缺失 {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

以下两种情况中的一种情况会显示此错误消息：
- 当IMS组织标头不正确或格式错误时(`x-gw-ims-org-id`)在API请求中传递。 再次尝试之前，请确保包含您的IMS组织的正确ID。
- 当您的帐户（由提供的身份验证凭据表示）与产品配置文件无关联以进行Experience Platform时。 按照 [生成访问凭据](./api-authentication.md#authentication-for-each-session) 在Platform API身份验证教程中，将Platform添加到您的帐户并相应地更新您的身份验证凭据。

## 服务疑难解答目录 {#service-troubleshooting-directory}

以下是疑难解答指南和API参考文档的列表 [!DNL Experience Platform] API。 每个故障诊断指南都提供了针对特定问题的常见问题解答和解决方案 [!DNL Platform] 服务。 API参考文档为每项服务的所有可用端点提供了全面的指南，并显示您可能收到的示例请求主体、响应和错误代码。

| 服务 | API 参考 | 故障排除 |
| --- | --- | --- |
| 访问控制 | [访问控制API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [访问控制疑难解答指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform数据摄取 | [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) | [批量摄取疑难解答指南](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[流摄取疑难解答指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform数据科学工作区 | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑难解答指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform数据管理 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 疑难解答指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查询服务 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 疑难解答指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentation | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] 常见问题解答和疑难解答指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 疑难解答指南](../profile/troubleshooting.md) |
| 沙盒 | [沙盒API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [沙箱疑难解答指南](../sandboxes/troubleshooting-guide.md) |
