---
keywords: Experience Platform；主页；热门主题；流服务；更新帐户
solution: Experience Platform
title: 使用流服务API更新帐户
type: Tutorial
description: 本教程介绍了使用流服务API更新帐户详细信息和凭据的步骤。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 使用流服务API更新帐户

在某些情况下，可能需要更新现有源连接的详细信息。 [!DNL Flow Service] 允许您添加、编辑和删除现有批处理或流连接的详细信息，包括其名称、描述和凭据。

本教程介绍了使用更新连接的详细信息和凭据的步骤。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教程要求您拥有一个现有连接和一个有效的连接ID。 如果您没有现有连接，请从 [源概述](../../home.md) 并按照尝试阅读本教程之前概述的步骤操作。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 查找连接详细信息

更新连接的第一步是使用连接ID检索其详细信息。 GET要检索您连接的当前详细信息，请向 [!DNL Flow Service] 提供要更新的连接的连接ID时的API。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 唯一 `id` 要检索的连接值。 |

**请求**

以下请求检索有关您的连接的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回您连接的当前详细信息，包括其凭据、唯一标识符(`id`)和版本。 更新连接时需要版本值。

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

PATCH要更新连接的名称、描述和凭据，请向 [!DNL Flow Service] API，同时提供您的连接ID、版本以及要使用的新信息。

>[!IMPORTANT]
>
>此 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的连接的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 唯一 `id` 要更新的连接的值。 |

**请求**

以下请求提供了一个新名称和描述，以及一组用于更新您的连接的新凭据。

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
| `op` | 用于定义更新连接所需的操作的操作调用。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 要更新的参数的路径。 |
| `value` | 您希望使用更新参数的新值。 |

**响应**

成功的响应将返回您的连接ID和更新的etag。 您可以通过向以下用户发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的连接ID。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 后续步骤

在本教程之后，您已使用更新与连接关联的凭据和信息。 [!DNL Flow Service] API。 有关使用源连接器的更多信息，请参见 [源概述](../../home.md).
