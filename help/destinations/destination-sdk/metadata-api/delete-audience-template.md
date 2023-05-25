---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK删除现有受众模板的API调用。
title: 删除受众模板
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# 删除受众模板

>[!IMPORTANT]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

此页面展示了可用于删除受众模板的API请求和有效负载，使用 `/authoring/audience-templates` API端点。

有关可通过此端点配置的功能的详细说明，请参阅 [受众元数据管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 受众模板API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 删除受众模板 {#delete}

您可以删除 [现有](create-audience-template.md) 创建受众模板 `DELETE` 请求 `/authoring/audience-templates` 端点 `{INSTANCE_ID}`要删除的受众模板的。

获取现有的受众模板及其对应的 `{INSTANCE_ID}`，请参阅以下文章： [检索受众模板](retrieve-audience-template.md).

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要删除的受众模板的。 |

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应返回HTTP状态200以及空的HTTP响应。

+++

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用删除受众模板 `/authoring/audience-templates` API端点。 读取 [如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md) 以了解此步骤在配置目标的过程中所处的位置。
