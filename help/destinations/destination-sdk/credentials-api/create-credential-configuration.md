---
description: 本页举例说明了用于创建凭据配置Adobe Experience Platform Destination SDK的API调用。
title: 创建凭据配置
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 8%

---

# 创建凭据配置

>[!IMPORTANT]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/credentials`

本页举例说明了可用于创建凭据配置的API请求和有效负载，使用 `/authoring/credentials` API端点。

## 何时使用 `/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您 ***不要*** 需要使用 `/credentials` API端点。 您而是可以通过配置目标的身份验证信息 `customerAuthenticationConfigurations` 的参数 `/destinations` 端点。
> 
>读取 [客户身份验证配置](../functionality/destination-configuration/customer-authentication.md) 以了解有关支持的身份验证类型的详细信息。

只有在Adobe和目标平台之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，您必须使用创建凭据配置 `/credentials` API端点。

在使用全局身份验证系统时，必须设置 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目标投放](../functionality/destination-configuration/destination-delivery.md) 配置，时间 [创建新的目标配置](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 凭据API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../getting-started.md) 获取成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 创建凭据配置 {#create}

您可以通过创建 `POST` 请求 `/authoring/credentials` 端点。

**API格式**

```http
POST /authoring/credentials
```

以下请求创建新的凭据配置，这些配置由有效负载中提供的参数定义。

选择下面的每个选项卡以查看相应的有效负载。

>[!BEGINTABS]

>[!TAB 基本]

**创建基本凭据配置**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `url` | 字符串 | 授权提供程序的URL |
| `username` | 字符串 | 凭据配置登录用户名 |
| `password` | 字符串 | 凭据配置登录密码 |

{style="table-layout:auto"}

+++

+++响应

成功的响应返回HTTP状态200以及新创建的凭据配置的详细信息。

+++

>[!TAB Amazon S3]

**创建 [!DNL Amazon S3] 凭据配置**

+++**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `accessId` | 字符串 | [!DNL Amazon S3] 访问ID |
| `secretKey` | 字符串 | [!DNL Amazon S3] 密钥 |

{style="table-layout:auto"}

+++

+++响应

成功的响应返回HTTP状态200以及新创建的凭据配置的详细信息。

+++

>[!TAB SSH]

**创建SSH凭据配置**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `username` | 字符串 | 凭据配置登录用户名 |
| `sshKey` | 字符串 | 用于采用SSH身份验证的SFTP的SSH密钥 |

{style="table-layout:auto"}

+++

+++响应

成功的响应返回HTTP状态200以及新创建的凭据配置的详细信息。

+++

>[!TAB Azure数据湖存储]

**创建 [!DNL Azure Data Lake Storage] 凭据配置**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `url` | 字符串 | 授权提供程序的URL |
| `tenant` | 字符串 | Azure Data Lake存储租户 |
| `servicePrincipalId` | 字符串 | Azure Data Lake Storage的Azure服务主体ID |
| `servicePrincipalKey` | 字符串 | 用于Azure Data Lake存储的Azure服务主体密钥 |

{style="table-layout:auto"}

+++

+++响应

成功的响应返回HTTP状态200以及新创建的凭据配置的详细信息。

+++

>[!TAB Azure Blob 存储]

**创建 [!DNL Azure Blob Storage] 凭据配置**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `connectionString` | 字符串 | [!DNL Azure Blob Storage] 连接字符串 |

{style="table-layout:auto"}

+++

+++响应

成功的响应返回HTTP状态200以及新创建的凭据配置的详细信息。

+++

>[!ENDTABS]

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) ，位于平台疑难解答指南中。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道何时使用凭据端点以及如何使用设置凭据配置 `/authoring/credentials` API端点读取 [如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md) 以了解此步骤在配置目标的过程中所处的位置。
