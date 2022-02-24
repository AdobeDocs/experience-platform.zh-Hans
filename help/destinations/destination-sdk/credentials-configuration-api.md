---
description: 本页介绍了可使用“/authoring/credentials” API端点执行的所有API操作。
title: 凭据端点API操作
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 4%

---

# 凭据端点API操作 {#credentials}

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/credentials`

本页列出并介绍了您可以使用 `/authoring/credentials` API端点。

有关此端点支持的功能的描述，请参阅：

* [流目标配置](destination-configuration.md) 对于功能，您可以为流目标配置。
* [基于文件的目标配置](file-based-destination-configuration.md) 对于功能，您可以为基于文件的目标配置。

## 何时使用 `/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您 *不* 需要使用 `/credentials` API端点。 您而是可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。 读取 [身份验证配置](./authentication-configuration.md#when-to-use) 以了解更多信息。

使用此API端点并选择 `PLATFORM_AUTHENTICATION` 在 [目标配置](./destination-configuration.md#destination-delivery) 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 `/credentials` API端点。

## 凭据配置API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 创建凭据配置 {#create}

您可以通过向 `/authoring/credentials` 端点。

**API格式**

```http
POST /authoring/credentials
```

**请求**

以下请求会创建一个新的凭据配置，该配置由有效负载中提供的参数进行配置。 以下负载包括接受的所有参数 `/authoring/credentials` 端点。 请注意，您不必在调用中添加所有参数，并且该模板可根据您的API要求进行自定义。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `username` | 字符串 | 凭据配置登录用户名 |
| `password` | 字符串 | 凭据配置登录密码 |
| `url` | 字符串 | 授权提供程序的URL |
| `clientId` | 字符串 | 客户端/应用程序凭据的客户端ID |
| `clientSecret` | 字符串 | 客户端/应用程序凭据的客户端密钥 |
| `accessToken` | 字符串 | 授权提供程序提供的访问令牌 |
| `expiration` | 字符串 | 访问令牌的生存时间 |
| `refreshToken` | 字符串 | 授权提供程序提供的刷新令牌 |
| `header` | 字符串 | 授权所需的任何标头 |
| `accessId` | 字符串 | Amazon S3访问ID |
| `secretKey` | 字符串 | Amazon S3密钥 |
| `sshKey` | 字符串 | 用于通过SSH身份验证的SFTP的SSH密钥 |
| `tenant` | 字符串 | Azure数据湖存储租户 |
| `servicePrincipalId` | 字符串 | Azure数据湖存储的Azure服务主体ID |
| `servicePrincipalKey` | 字符串 | Azure数据湖存储的Azure服务主密钥 |
| `connectionString` | 字符串 | Azure Blob Storage连接字符串 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回HTTP状态200，其中包含新创建凭据配置的详细信息。

## 列出凭据配置 {#retrieve-list}

您可以通过向 `/authoring/credentials` 端点。

**API格式**


```http
GET /authoring/credentials
```

**请求**

以下请求将根据IMS组织和沙盒配置，检索您有权访问的凭据配置列表。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

以下响应会根据您使用的IMS组织ID和沙盒名称，返回HTTP状态200，其中包含您有权访问的凭据配置列表。 一个 `instanceId` 对应于一个凭据配置的模板。 响应因简短而被截断。

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## 更新现有凭据配置 {#update}

您可以通过向 `/authoring/credentials` 端点并提供要更新的凭据配置的实例ID。 在调用正文中，提供更新的凭据配置。

**API格式**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的凭据配置的ID。 |

**请求**

以下请求会更新现有的凭据配置，该配置由有效负载中提供的参数进行配置。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## 检索特定凭据配置 {#get}

您可以通过向 `/authoring/credentials` 端点并提供要更新的凭据配置的实例ID。

**API格式**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要检索的凭据配置的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定凭据配置的详细信息。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## 删除特定凭据配置 {#delete}

您可以通过向 `/authoring/credentials` 端点和提供您希望在请求路径中删除的凭据配置的ID。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `id` 要删除的凭据配置。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回HTTP状态200以及空的HTTP响应。

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道何时使用凭据端点以及如何使用 `/authoring/credentials` API端点或 `/authoring/destinations` 端点。 读取 [如何使用Destination SDK配置目标](./configure-destination-instructions.md) 以了解此步骤在配置目标过程中的适用位置。
