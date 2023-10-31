---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK删除现有目标服务器配置的API调用。
title: 删除目标服务器配置
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# 删除目标服务器配置

本页举例说明了可用于删除现有目标服务器配置的API请求和有效负载，使用 `/authoring/destination-servers` API端点。

有关可通过此端点删除的功能的详细说明，请参阅以下文章：

* [使用Destination SDK创建的目标的服务器规范](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK创建的目标模板规范](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [消息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [文件格式配置](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标服务器API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../../getting-started.md) 获取成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 删除目标服务器配置 {#delete}

您可以删除 [现有](create-destination-server.md) 目标服务器配置，方法是 `DELETE` 请求 `/authoring/destination-servers` 端点，带有 `{INSTANCE_ID}`要删除的目标服务器配置中的。

>[!TIP]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

获取现有的目标服务器配置及其相应的配置 `{INSTANCE_ID}`，请参阅关于以下内容的文章： [检索目标服务器配置](retrieve-destination-server.md).

**API格式**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要删除的目标服务器配置中的。 |

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++响应

成功的响应返回HTTP状态200以及空的HTTP响应。

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) ，位于平台疑难解答指南中。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何通过Destination SDK删除现有目标服务器 `/authoring/destination-servers` API端点。

要了解有关可使用此端点执行的操作的更多信息，请参阅以下文章：

* [创建目标服务器配置](create-destination-server.md)
* [检索目标服务器配置](retrieve-destination-server.md)
* [更新目标服务器配置](update-destination-server.md)
