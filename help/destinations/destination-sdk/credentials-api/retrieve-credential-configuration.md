---
description: 本页说明了用于通过Adobe Experience Platform Destination SDK检索凭据配置的API调用。
title: 检索凭据配置
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---


# 检索凭据配置

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/credentials`

本页说明了可用于使用检索凭据配置的API请求和有效负载 `/authoring/credentials` API端点。

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

## 检索凭据配置 {#retrieve}

您可以检索 [现有](create-credential-configuration.md) 通过创建 `GET` 请求 `/authoring/credentials` 端点。

**API格式**

使用以下API格式检索您帐户的所有凭据配置。

```http
GET /authoring/credentials
```

使用以下API格式检索由 `{INSTANCE_ID}` 参数。

```http
GET /authoring/credentials/{INSTANCE_ID}
```

以下两个请求将检索您的IMS组织或特定凭据配置的所有凭据配置，具体取决于您是否传递了 `INSTANCE_ID` 参数。

选择下面的每个选项卡，以查看相应的有效负荷。

>[!BEGINTABS]

>[!TAB 检索所有凭据配置]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功响应会根据 [!DNL IMS Org ID] 和您使用的沙盒名称。 一个 `instanceId` 对应于一个凭据配置。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB 检索特定凭据配置]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要检索的凭据配置的ID。 |

+++

+++响应

成功响应会返回HTTP状态200，其中凭据配置的详细信息对应于 `instanceId` 请求提供。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用 `/authoring/credentials` API端点。 读取 [如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md) 以了解此步骤在配置目标过程中的适用位置。
