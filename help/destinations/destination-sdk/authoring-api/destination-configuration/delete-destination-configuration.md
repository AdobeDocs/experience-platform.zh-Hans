---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK删除现有目标配置的API调用。
title: 删除目标配置
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---

# 删除目标配置

此页面展示了可用于使用`/authoring/destinations` API端点删除现有目标配置的API请求和有效负荷。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标配置API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 删除目标配置 {#delete}

您可以删除[现有](create-destination-configuration.md)目标服务器配置，方法是使用要删除的目标配置的`{INSTANCE_ID}`向`/authoring/destinations`端点发出`DELETE`请求。

>[!TIP]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/destinations`

要获取现有目标配置及其对应的`{INSTANCE_ID}`，请参阅有关[检索目标配置](retrieve-destination-configuration.md)的文章。

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 要删除的目标配置的`ID`。 |

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

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道如何通过Destination SDK `/authoring/destinations` API端点删除现有目标配置。

要了解有关可使用此端点执行的操作的更多信息，请参阅以下文章：

* [创建目标配置](create-destination-configuration.md)
* [检索目标配置](retrieve-destination-configuration.md)
* [更新目标配置](update-destination-configuration.md)
