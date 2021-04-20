---
keywords: Experience Platform；主页；热门主题；API错误代码；API错误代码；错误代码API；错误代码API;API请求错误；API疑难解答；API错误
solution: Experience Platform
title: Adobe Experience Platform常见问题解答和疑难解答指南
description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
landing-page-description: 查找常见问题的解答以及 Experience Platform 中常见错误的疑难解答指南。
topic: getting started
type: Documentation
translation-type: tm+mt
source-git-commit: 83cc3ddbf067f413cb524a3a685d985d5853eafd
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 4%

---


# [!DNL Platform] 常见问题解答和疑难解答指南

本文档提供有关Adobe Experience Platform的常见问题解答，以及针对任何[!DNL Experience Platform] API中可能遇到的常见错误的高级疑难解答指南。 有关各个[!DNL Platform]服务的疑难解答指南，请参阅以下[服务疑难解答目录](#service-troubleshooting-directory)。

## 常见问题解答 {#faq}

以下是有关Adobe Experience Platform的常见问题解答列表。

## 什么是[!DNL Experience Platform] API?{#what-are-experience-platform-apis}

[!DNL Experience Platform] 优惠使用HTTP请求访问资源的多个RESTful  [!DNL Platform] API。这些服务API每个都公开多个端点，并允许您对列表(GET)、查找(GET)、编辑(PUT和/或PATCH)和删除(DELETE)资源执行操作。 有关每个服务可用的特定端点和操作的详细信息，请参阅有关Adobe I/O的[API参考文档](http://www.adobe.com/go/platform-api-reference-en)。

## 如何设置API请求的格式？{#how-do-i-format-an-api-request}

请求格式因使用的[!DNL Platform] API而异。 了解如何构造API调用的最佳方式是按照您所使用的特定[!DNL Platform]服务文档中提供的示例进行操作。

有关创建API请求的详细信息，请访问平台API快速入门指南[阅读示例API调用](./api-guide.md#sample-api)部分。

## 我的IMS组织是什么？{#what-is-my-ims-organization}

IMS组织是Adobe的代表。 任何许可的Adobe解决方案都与此客户组织集成。 当IMS组织有权访问[!DNL Experience Platform]时，它可以将访问权限分配给开发人员。 IMS组织ID(`x-gw-ims-org-id`)表示应执行API调用的组织，因此在所有API请求中都要求作为头。 可通过[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)找到此ID:在&#x200B;**集成**&#x200B;选项卡中，导航至任何特定集成的&#x200B;**概述**&#x200B;部分，以在&#x200B;**客户端凭据**&#x200B;下查找ID。 有关如何验证到[!DNL Platform]的分步演练，请参阅[验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 在哪里可以找到我的API密钥？{#where-can-i-find-my-api-key}

所有API请求中都需要API密钥作为头。 它可以通过[Adobe开发者控制台](https://www.adobe.com/go/devs_console_ui)找到。 在控制台中，在&#x200B;**Integrations**&#x200B;选项卡上，导航到特定集成的&#x200B;**Overview**&#x200B;部分，您将在&#x200B;**Client Credentials**&#x200B;下找到密钥。 有关如何验证到[!DNL Platform]的分步演练，请参阅[验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何获得访问令牌?{#how-do-i-get-an-access-token}

访问令牌在所有API调用的“授权”标头中是必需的。 如果您有权访问IMS组织的集成，则可使用`curl`命令生成这些组件。 访问令牌仅在24小时内有效，此后必须生成新令牌才能继续使用API。 有关生成访问令牌的详细信息，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何使用查询参数？{#how-do-i-user-query-parameters}

某些[!DNL Platform] API端点接受查询参数以查找特定信息并过滤响应中返回的结果。 查询参数用问号(`?`)符号附加到请求路径，后跟使用格式`paramName=paramValue`的一个或多个查询参数。 在单个调用中组合多个参数时，必须使用&amp;符号(`&`)分隔单个参数。 以下示例演示了如何使用多个查询参数的请求在文档中的表示方式。

常用查询参数的示例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有关特定服务或端点可使用哪些查询参数的详细信息，请查阅特定于服务的文档。

## 如何在PATCH请求中指示要更新的JSON字段？{#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

[!DNL Platform] API中的许多PATCH操作使用[JSON指针](https://tools.ietf.org/html/rfc6901)字符串指示要更新的JSON属性。 这些值通常包含在使用[JSON Patch](https://tools.ietf.org/html/rfc6902)格式的请求负载中。 有关这些技术所需语法的详细信息，请参阅[API基础指南](api-fundamentals.md)。

## 我是否可以使用Postman对[!DNL Platform] API进行调用？{#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 是一个用于对RESTful API进行可视化调用的有用工具。[平台API快速入门指南](api-guide.md)包含有关导入Postman集合的视频和说明。 此外，还为每项服务提供邮递员集合列表。

## [!DNL Platform]有哪些系统要求？{#what-are-the-system-requirements-for-platform}

根据您是使用UI还是API，系统要求如下：

**对于基于UI的操作：**
- 现代、标准的Web浏览器。 虽然建议使用[!DNL Chrome]的最新版本，但还支持[!DNL Firefox]、[!DNL Internet Explorer]和Safari的当前版本和以前的主要版本。
   - 每次发布新的主要版本时，[!DNL Platform]支持最新版本的开始将被放弃，而支持第三个最新版本。
- 所有浏览器都必须启用Cookie和JavaScript。

**对于API和开发人员交互：**
- 用于为REST、流和Webhook集成进行开发的开发环境。

## {#errors-and-troubleshooting}错误和疑难解答

以下是使用任何[!DNL Experience Platform]服务时可能遇到的错误列表。 有关各个[!DNL Platform]服务的疑难解答指南，请参阅以下[服务疑难解答目录](#service-troubleshooting-directory)。

## API状态代码{#api-status-codes}

在任何[!DNL Experience Platform] API上都可能遇到以下状态代码。 每种解释都有各种原因，因此本节中的解释是一般性的。 有关单个[!DNL Platform]服务中的特定错误的详细信息，请参见下面的[服务疑难解答目录](#service-troubleshooting-directory)。

| 状态代码 | 描述 | 可能的原因 |
--- | --- | ---
| 400 | 错误请求 | 请求构造不正确、缺少关键信息和/或包含不正确的语法。 |
| 401 | 身份验证失败 | 请求未通过身份验证检查。 您的访问令牌可能缺失或无效。 有关更多详细信息，请参阅下面的[OAuth令牌错误](#oauth-token-is-missing)部分。 |
| 403 | 禁止 | 已找到该资源，但您没有正确的凭据来视图它。 |
| 404 | 未找到 | 在服务器上找不到请求的资源。 资源可能已删除，或请求的路径输入不正确。 |
| 500 | 内部服务器错误 | 这是服务器端错误。 如果您同时发出多个调用，则可能达到API限制，并需要过滤结果。 （有关详细信息，请参阅[筛选数据](../catalog/api/filter-data.md)上的[!DNL Catalog Service] API开发人员指南子指南。） 请稍等片刻，然后再次尝试您的请求，如果问题仍然存在，请与管理员联系。 |

## 请求标头错误{#request-header-errors}

[!DNL Platform]中的所有API调用都需要特定的请求标头。 要查看各个服务需要哪些标头，请参阅[API参考文档](http://www.adobe.com/go/platform-api-reference-en)。 要查找所需身份验证头的值，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 如果在进行API调用时，这些标头中的任何标头缺失或无效，则可能会发生以下错误。

### 缺少{#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

当API请求中缺少`Authorization`标头时，将显示此错误消息。 在重试之前，请确保授权标头包含有效访问令牌。

### OAuth令牌无效

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

当`Authorization`标头中提供的访问令牌无效时，将显示此错误消息。 确保已正确输入令牌，或者[在Adobe I/O控制台中生成新令牌](https://www.adobe.com/go/platform-api-authentication-en)。

### 需要API密钥

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

当API请求中缺少API密钥头(`x-api-key`)时，将显示此错误消息。 在重试之前，请确保标头包含有效的API密钥。

### API密钥无效

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

当提供的API密钥头(`x-api-key`)的值无效时，将显示此错误消息。 请确保在重试之前输入了正确的密钥。 如果您不知道您的API密钥，可以在[Adobe I/O控制台](https://console.adobe.io)中找到它：在&#x200B;**集成**&#x200B;选项卡中，导航至&#x200B;**概述**&#x200B;部分，以查找特定集成，以在&#x200B;**客户端凭据**&#x200B;下查找API密钥。


### 缺少标题

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

当API请求中缺少IMS组织头(`x-gw-ims-org-id`)时，将显示此错误消息。 在重试之前，请确保头包含在IMS组织的ID中。

### 用户档案无效

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

当用户或Adobe I/O集成(由`Authorization`标头中的[访问令牌](#how-do-i-get-an-access-token)标识)无权对`x-gw-ims-org-id`标头中提供的IMS组织调用[!DNL Experience Platform] API时，将显示此错误消息。 在重试之前，请确保已在标头中为您的IMS组织提供了正确的ID。 如果您不知道您的组织ID，可以在[Adobe I/O控制台](https://console.adobe.io)中找到它：在&#x200B;**集成**&#x200B;选项卡中，导航至&#x200B;**概述**&#x200B;部分，以查找特定集成，以在&#x200B;**客户端凭据**&#x200B;下查找ID。

### 未指定有效的内容类型

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

当POST、PUT或PATCH请求的标头无效或缺少`Content-Type`标头时，将显示此错误消息。 请确保请求中包含标头，并且其值为`application/json`。


## 服务疑难解答目录{#service-troubleshooting-directory}

以下是[!DNL Experience Platform] API的疑难解答指南和API参考文档的列表。 每个故障排除指南都针对特定于单个[!DNL Platform]服务的常见问题和问题提供解答。 API参考文档为每个服务的所有可用端点提供了全面指南，并显示您可能收到的示例请求主体、响应和错误代码。

| 服务 | API 参考 | 故障诊断 |
| --- | --- | --- |
| 访问控制 | [访问控制 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [访问控制疑难解答指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform数据摄取 | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [批量摄取疑难解答](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[指南流式摄取疑难解答指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑难解答指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform Data Governance | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] 疑难解答指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查询服务 | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] 疑难解答指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentation | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] 常见问题解答和疑难解答指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] 疑难解答指南](../profile/troubleshooting.md) |
| 沙盒 | [沙箱API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [沙箱疑难解答指南](../sandboxes/troubleshooting-guide.md) |

