---
title: 使用流服务API创建Microsoft Dynamics基本连接
description: 了解如何使用流服务API将Experience Platform连接到Microsoft Dynamics帐户。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API将[!DNL Microsoft Dynamics]连接到Experience Platform

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Microsoft Dynamics]源连接到Adobe Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

以下部分提供了使用[!DNL Flow Service] API成功将Experience Platform连接到Dynamics帐户所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到[!DNL Dynamics]，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 基本身份验证]

| 凭据 | 描述 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的密码。 |

>[!TAB 服务主体和密钥身份验证]

| 凭据 | 描述 |
| --- | --- |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

>[!ENDTABS]

有关入门的详细信息，请参阅[此 [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 创建基本连接

>[!TIP]
>
>创建后，无法更改[!DNL Dynamics]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Dynamics]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用基本身份验证创建[!DNL Dynamics]基本连接，请在提供连接的`serviceUri`、`username`和`password`的值时向[!DNL Flow Service] API发出POST请求。

**请求**

以下请求使用基本身份验证为[!DNL Dynamics]源创建基本连接。

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUri` | 与您的[!DNL Dynamics]实例关联的服务URI。 |
| `auth.params.username` | 与您的[!DNL Dynamics]帐户关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Dynamics]帐户关联的密码。 |
| `connectionSpec.id` | [!DNL Dynamics]连接规范ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**响应**

成功的响应返回新创建的基本连接，包括其唯一标识符(`id`)。

+++选择以查看响应示例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 基于服务主体密钥的身份验证]

要使用基于服务主体密钥的身份验证创建[!DNL Dynamics]基本连接，请在提供连接的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`的值时向[!DNL Flow Service] API发出POST请求。

**请求**

以下请求使用基于基本服务主体密钥的身份验证为[!DNL Dynamics]源创建基本连接。

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUri` | 与您的[!DNL Dynamics]实例关联的服务URI。 |
| `auth.params.servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `auth.params.servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |
| `connectionSpec.id` | [!DNL Dynamics]连接规范ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**响应**

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。

+++选择以查看响应示例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## 浏览您的数据表

要浏览[!DNL Dynamics]数据表，请向`/connections/{BASE_CONNECTION_ID}/explore`端点发出GET请求，并提供您的基本连接ID作为查询参数的一部分。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 查询参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基本连接的ID。 使用此ID浏览源的内容和结构。 |

**请求**

以下请求检索具有基础连接ID的[!DNL Dynamics]源的可用表和视图列表： `dd668808-25da-493f-8782-f3433b976d1e`。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应返回根级别的[!DNL Dynamics]表和视图目录。

+++选择以查看响应示例

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### 使用主键优化数据探索

>[!NOTE]
>
>在使用主键方法进行优化时，只能使用非查找属性。

通过将`primaryKey`作为查询参数的一部分提供，您可以优化浏览查询。 将`primaryKey`作为查询参数加入时，必须指定[!DNL Dynamics]表的主键。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| 查询参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基本连接的ID。 使用此ID浏览源的内容和结构。 |
| `preview` | 启用数据预览的布尔值。 |
| `{OBJECT}` | 要浏览的[!DNL Dynamics]对象。 |
| `{OBJECT_TYPE}` | 对象的类型。 |
| `previewCount` | 一种限制，将返回的预览限制为仅特定数量的记录。 |
| `{PRIMARY_KEY}` | 要检索以进行预览的表的主键。 |

**请求**

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## 检查表的结构

要检查特定表的结构，请向`/connections/{BASE_CONNECTION_ID}/explore`发出GET请求，并将特定表的路径作为查询参数提供。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| 查询参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基本连接的ID。 使用此ID浏览源的内容和结构。 |
| `{TABLE_PATH}` | 要浏览的特定表的路径。 |

**请求**

以下请求检索路径为`workflowdependency`的[!DNL Dynamics]表的结构和内容。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应返回路径`workflowdependency`的内容。

+++选择以查看响应示例

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## 检查视图的结构

在[!DNL Dynamics]中，视图是指要显示的列、每列的宽度、对记录列表进行排序的默认系统以及应用于限制列表中将显示哪些记录的默认筛选器。

要检查视图的结构，请向`/connections/{BASE_CONNECTION_ID}/explore`发出GET请求，并在查询参数中指定视图路径。 此外，您必须将`objectType`指定为`view`。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| 查询参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基本连接的ID。 使用此ID浏览源的内容和结构。 |
| `{VIEW_PATH}` | 要检查的视图的路径。 |

**请求**

以下请求检索`accountView1`。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应返回`accountView1`的结构。

+++选择以查看响应示例

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## 预览实体类型视图

要预览视图的内容，请向`/connections/{BASE_CONNECTION_ID}/explore`发出GET请求，并在查询参数中包含视图路径和`preview=true`。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| 查询参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基本连接的ID。 使用此ID浏览源的内容和结构。 |
| `{VIEW_PATH}` | 要检查的视图的路径。 |


**请求**

以下请求预览`accountView1`的内容。

+++选择以查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应返回`accountView1`的内容。

+++选择以查看响应示例

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## 创建源连接以摄取视图

要创建源连接并摄取视图，请对`/sourceConnections`端点发出POST请求，提供表名称，并在请求正文中将`entityType`指定为`view`。

**API格式**

```http
POST /sourceConnections
```

**请求**

以下请求创建[!DNL Dynamics]源连接并摄取视图。

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**响应**

成功的响应会返回新生成的源连接ID及其相应的电子标记。

+++选择以查看响应示例

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### 使用主密钥优化数据流

您还可以通过指定主键作为请求正文参数的一部分来优化[!DNL Dynamics]数据流。

**API格式**

```http
POST /sourceConnections
```

**请求**

将主键指定为`contactid`时，以下请求创建[!DNL Dynamics]源连接。

+++选择以查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `baseConnectionId` | 基本连接的ID。 |
| `data.format` | 数据的格式。 |
| `params.tableName` | [!DNL Dynamics]中表的名称。 |
| `params.primaryKey` | 将优化查询的表的主键。 |
| `connectionSpec.id` | 与[!DNL Dynamics]源对应的连接规范ID。 |

+++

**响应**

成功的响应会返回新生成的源连接ID及其相应的电子标记。

+++选择以查看响应示例

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Microsoft Dynamics]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将CRM数据引入Experience Platform](../../collect/crm.md)
