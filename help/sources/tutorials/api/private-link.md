---
title: 源中的专用链接支持
description: 了解如何为Adobe Experience Platform源创建和使用该专用链接
badge: Beta 版
hide: true
hidefromtoc: true
source-git-commit: 4c91ffc60a2537fcc76ce935bf3b163984fdc5e4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 5%

---

# 源中的专用链接支持

>[!AVAILABILITY]
>
>此功能处于“有限可用”状态，当前仅受以下源支持：
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

阅读本指南，了解如何通过专用链接建立与基于Azure的源的专用端点连接，并为您的数据提供更安全的传输机制。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个[!DNL Platform]实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../landing/api-guide.md)指南。

## 创建专用端点 {#create-private-endpoint}

要创建专用端点，请向`/privateEndpoints`发出POST请求。

**API格式**

```http
POST /privateEndpoints
```

**请求**

以下请求创建一个专用端点：

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 专用端点的名称。 |
| `subscriptionId` | 与您的[!DNL Azure]订阅关联的ID。 有关详细信息，请参阅[上的[!DNL Azure]指南，从 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)中检索您的订阅和租户ID。 |
| `resourceGroupName` | [!DNL Azure]上资源组的名称。 资源组包含[!DNL Azure]解决方案的相关资源。 有关详细信息，请阅读有关[管理资源组](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)的[!DNL Azure]指南。 |
| `resourceName` | 资源的名称。 在[!DNL Azure]中，资源引用虚拟机、Web应用和数据库等实例。 有关详细信息，请阅读[上的[!DNL Azure]指南，以了解 [!DNL Azure] 资源管理器](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
| `fqdns` | 源的全限定域名。 仅当使用[!DNL Snowflake]源时，才需要此属性。 |
| `connectionSpec.id` | 您正在使用的源的连接规范ID。 |
| `connectionSpec.version` | 您正在使用的连接规范ID的版本。 |

+++

**响应**

成功的响应会返回以下内容：

+++选择以查看响应示例

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 新创建的专用端点的ID。 |
| `name` | 专用端点的名称。 |
| `subscriptionId` | 与您的[!DNL Azure]订阅关联的ID。 有关详细信息，请参阅[上的[!DNL Azure]指南，从 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)中检索您的订阅和租户ID。 |
| `resourceGroupName` | [!DNL Azure]上资源组的名称。 资源组包含[!DNL Azure]解决方案的相关资源。 有关详细信息，请阅读有关[管理资源组](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)的[!DNL Azure]指南。 |
| `resourceName` | 资源的名称。 在[!DNL Azure]中，资源引用虚拟机、Web应用和数据库等实例。 有关详细信息，请阅读[上的[!DNL Azure]指南，以了解 [!DNL Azure] 资源管理器](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
| `fqdns` | 源的全限定域名。 仅当使用[!DNL Snowflake]源时，才需要此属性。 |
| `connectionSpec.id` | 您正在使用的源的连接规范ID。 |
| `connectionSpec.version` | 您正在使用的连接规范ID的版本。 |
| `state` | 私有端点的当前状态。 有效状态包括： <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## 检索专用端点列表 {#retrieve-private-endpoints}

要从您组织中的给定沙盒检索专用端点列表，请向`/privateEndpoints`发出GET请求。

**API格式**

```http
GET /privateEndpoints
```

**请求**

以下请求检索您组织中存在的所有专用端点的列表。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应将返回贵组织中的专用端点列表。

+++选择以查看响应示例

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## 检索给定源的专用端点列表 {#retrieve-private-endpoints-by-source}

要检索与特定源对应的私有端点的列表，请向`/privateEndpoints`端点发出GET请求并提供源的`connectionSpec.id`。

**API格式**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| 查询参数 | 描述 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 要搜索专用端点的源的连接规范ID。 |

**请求**

以下请求检索与具有连接规范ID的源对应的所有专用端点的列表： `4c10e202-c428-4796-9208-5f1f5732b1cf`。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应将返回与连接规范ID为`4c10e202-c428-4796-9208-5f1f5732b1cf`的源对应的所有专用端点的列表。

+++选择以查看响应示例

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## 检索专用端点 {#retrieve-specific-private-endpoint}

要检索特定的专用端点，请向`/privateEndpoints`发出GET请求，并提供要检索的专用端点的ID。

**API格式**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| 查询参数 | 描述 |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | 要检索的私有端点的ID。 |

**请求**

以下请求检索ID为`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`的专用终结点。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应返回了ID为`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`的专用终结点

+++选择以查看响应示例

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## 解析专用端点 {#resolve-private-endpoint}

**API格式**

```http
GET /privateEndpoints?op=autoResolve
```

**请求**

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**响应**

+++选择以查看响应示例

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## 启用交互式创作 {#enable-interactive-authoring}

交互式创作用于探索连接或帐户以及预览数据等功能。 要启用交互式创作，请向`/privateEndpoints/interactiveAuthoring`发出POST请求，并在查询参数中将`enable`指定为运算符。

**API格式**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| 查询参数 | 描述 |
| --- | --- |
| `op` | 要执行的操作。 要启用交互式创作，请将`op`值设置为`enable`。 |

**请求**

以下请求启用私有端点的交互式创作，并将TTL设置为60分钟。

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| 属性 | 描述 |
| --- | --- |
| `autoTerminationMinutes` | 交互式创作TTL（存留时间）（以分钟为单位）。 交互式创作用于探索连接或帐户以及预览数据等功能。 您最多可以设置120分钟的TTL。 默认TTL为60分钟。 |

+++

**响应**

成功的响应返回HTTP状态202（已接受）。

## 检索交互式创作状态 {#retrieve-interactive-authoring-status}

要查看专用端点的交互式创作的当前状态，请向`/privateEndpoints/interactiveAuthoring`发出GET请求。

**API格式**

```http
GET /privateEndpoints/interactiveAuthoring
```

**请求**

以下请求检索交互式创作状态：

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

+++选择以查看响应示例

```json
{
    "status": "Disabled"
}
```

| 属性 | 描述 |
| --- | --- |
| `status` | 交互式创作的状态。 有效值包括： `disabled`、`enabling`、`enabled`。 |

+++

## 删除专用端点 {#delete-private-endpoint}

要删除您的专用端点，请向`/privateEndpoints`发出DELETE请求，并提供要删除的端点的ID。

**API格式**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| 查询参数 | 描述 |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | 要删除的私有端点的ID。 |

**请求**

以下请求删除ID为`02a74b31-a566-4a86-9cea-309b101a7f24`的专用终结点。

+++选择以查看请求示例

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应返回HTTP状态200（成功）。 您可以通过向`/privateEndpoints`发出GET请求并提供已删除的ID作为查询参数来验证删除操作。

## 流程服务 {#flow-service}

请阅读以下各节，以了解如何将私有端点与[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)结合使用。

### 创建与专用端点的连接 {#create-base-connection}

要在Experience Platform中创建与私有端点的连接，请对[!DNL Flow Service] API的`/connections`端点发出POST请求。

**API格式**

```http
POST /connections/
```

**请求**

以下请求为[!DNL Snowflake]创建经过身份验证的基本连接，同时使用专用端点。

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 |
| `description` | （可选）提供有关连接的附加信息的描述。 |
| `auth.specName` | 用于将源连接到Experience Platform的身份验证。 |
| `auth.params.connectionString` | [!DNL Snowflake]连接字符串。 有关详细信息，请阅读[[!DNL Snowflake] API身份验证指南](../api/create/databases/snowflake.md)。 |
| `auth.params.usePrivateLink` | 一个布尔值，用于确定您是否使用私有端点。 如果您使用专用终结点，则将此值设置为`true`。 |
| `connectionSpec.id` | 连接规范ID [!DNL Snowflake]。 |
| `connectionSpec.version` | [!DNL Snowflake]连接规范ID的版本。 |

+++

**响应**

成功的响应将返回新生成的基本连接ID和etag。

+++选择以查看响应示例

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### 检索与给定私有端点关联的连接 {#retrieve-connections-by-endpoint}

要检索与特定私有端点关联的连接，请向`/connections`端点发出GET请求，并提供私有端点的ID作为查询参数。

**API格式**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| 查询参数 | 描述 |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | 与要检索的连接关联的私有端点的ID。 |

**请求**

以下请求检索绑定到ID为`02a74b31-a566-4a86-9cea-309b101a7f24`的私有端点的现有连接。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应将返回与查询的私有端点关联的连接列表。

+++选择以查看响应示例

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### 检索与任何专用端点关联的连接 {#retrieve-connections}

要检索与任何专用端点关联的连接，请向`/connections`端点发出GET请求，并提供`property=auth.params.usePrivateLink==true`作为查询参数。

**API格式**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**请求**

以下请求将检索贵组织中使用私有端点的所有连接。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应将返回与私有端点绑定的所有连接。

+++选择以查看响应示例

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++