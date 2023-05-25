---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK删除现有目标配置的API调用。
title: 删除目标配置
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---


# 删除目标配置

本页举例说明了可用于删除现有目标配置的API请求和有效负载，使用 `/authoring/destinations` API端点。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 目标配置API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 删除目标配置 {#delete}

您可以删除 [现有](create-destination-configuration.md) 目标服务器配置，方法是 `DELETE` 请求 `/authoring/destinations` 端点 `{INSTANCE_ID}`要删除的目标配置的ID。

>[!TIP]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/destinations`

获取现有目标配置及其相应的配置 `{INSTANCE_ID}`，请参阅以下文章： [检索目标配置](retrieve-destination-configuration.md).

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要删除的目标配置的ID。 |

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++响应

成功的响应返回HTTP状态200以及空的HTTP响应。


## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤

阅读本文档后，您现在知道如何通过Destination SDK删除现有目标配置 `/authoring/destinations` API端点。

要了解有关可使用此端点执行的操作的更多信息，请参阅以下文章：

* [创建目标配置](create-destination-configuration.md)
* [检索目标配置](retrieve-destination-configuration.md)
* [更新目标配置](update-destination-configuration.md)

