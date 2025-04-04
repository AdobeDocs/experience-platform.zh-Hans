---
title: 使用流服务API更新帐户
description: 本教程涵盖了使用流服务API更新帐户详细信息和凭据的步骤。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---

# 使用流服务API更新帐户

在某些情况下，可能需要更新现有基本连接的详细信息。 [!DNL Flow Service]允许您添加、编辑和删除现有批次或流连接的详细信息，包括其名称、描述和凭据。

本教程介绍使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新连接的详细信息和凭据的步骤。

>[!TIP]
>
>当需要更新时，您不需要创建新的基本连接。 对基本连接所做的任何更改都会反映在关联的数据流中。

## 快速入门

本教程要求您拥有现有连接和有效连接ID。 如果您没有现有连接，请从[源概述](../../home.md)中选择您选择的源，并按照尝试本教程之前概述的步骤操作。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

## 查找连接详细信息

更新连接的第一步是使用连接ID检索其详细信息。 要检索您连接的当前详细信息，请在提供要更新的连接的连接ID的同时向[!DNL Flow Service] API发出GET请求。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要检索的连接唯一`id`值。 |

**请求**

以下请求将检索有关您的连接的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回您连接的当前详细信息，包括其凭据、唯一标识符(`id`)和版本。 更新连接时需要版本值。

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## 更新连接

要更新连接的名称、描述和凭据，请对[!DNL Flow Service] API执行PATCH请求，同时提供您的连接ID、版本以及要使用的新信息。

>[!IMPORTANT]
>
>发出PATCH请求时需要使用`If-Match`标头。 此标头的值是您要更新的连接的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要更新的连接的唯一`id`值。 |

**请求**

以下请求提供了新名称和描述以及一组新凭据，用于更新您的连接。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| 参数 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新连接所需的操作的操作调用。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 要更新的参数的路径。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的连接ID和更新的电子标记。 您可以在提供连接ID的同时，通过向[!DNL Flow Service] API发出GET请求来验证更新。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 后续步骤

通过学习本教程，您已更新与使用[!DNL Flow Service] API的连接关联的凭据和信息。 有关使用源连接器的更多信息，请参阅[源概述](../../home.md)。
