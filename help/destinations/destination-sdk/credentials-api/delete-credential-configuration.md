---
description: 本页说明了用于删除凭据配置Adobe Experience Platform Destination SDK的API调用。
title: 删除凭据配置
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# 删除凭据配置

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/credentials`

本页说明了可用于使用删除凭据配置的API请求和负载 `/authoring/credentials` API端点。

## 何时使用 `/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您 ***不*** 需要使用 `/credentials` API端点。 您而是可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。
> 
>读取 [客户身份验证配置](../functionality/destination-configuration/customer-authentication.md) 以详细了解支持的身份验证类型。

仅当Adobe与目标平台之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，您必须使用 `/credentials` API端点。

使用全局身份验证系统时，必须设置 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目标投放](../functionality/destination-configuration/destination-delivery.md) 配置，当 [创建新目标配置](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 凭据API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](../getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 删除凭据配置 {#delete}

您可以删除 [现有](create-credential-configuration.md) 通过创建 `DELETE` 请求 `/authoring/credentials` 端点 `{INSTANCE_ID}`要删除的凭据配置的URL。

获取现有目标配置及其对应的 `{INSTANCE_ID}`，请参阅关于 [检索凭据配置](retrieve-credential-configuration.md).

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `ID` 要删除的凭据配置。 |

以下请求会删除由 `{INSTANCE_ID}` 参数。

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应会返回HTTP状态200以及空的HTTP响应。

+++

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用 `/authoring/credentials` API端点。 读取 [如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md) 以了解此步骤在配置目标过程中的适用位置。
