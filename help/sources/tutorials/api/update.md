---
keywords: Experience Platform；主页；热门主题；流程服务；更新帐户
solution: Experience Platform
title: 使用流服务API更新帐户
topic-legacy: overview
type: Tutorial
description: 本教程介绍了使用流量服务API更新帐户的详细信息和凭据的步骤。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 使用流量服务API更新帐户

在某些情况下，可能需要更新现有源连接的详细信息。 [!DNL Flow Service] 使您能够添加、编辑和删除现有批处理连接或流连接的详细信息，包括其名称、描述和凭据。

本教程介绍使用更新连接的详细信息和凭据的步骤 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教程要求您拥有现有连接和有效的连接ID。 如果您没有现有连接，请从 [源概述](../../home.md) ，然后按照在尝试使用本教程之前列出的步骤操作。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 查找连接详细信息

更新连接的第一步是使用连接ID检索其详细信息。 要检索连接的当前详细信息，请向 [!DNL Flow Service] 提供要更新的连接的连接ID时的API。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 独特 `id` 值。 |

**请求**

以下请求会检索与您的连接有关的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回连接的当前详细信息，包括其凭据、唯一标识符(`id`)和版本。 更新连接时需要使用版本值。

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

要更新连接的名称、说明和凭据，请向执行PATCH请求 [!DNL Flow Service] API，同时提供您要使用的连接ID、版本和新信息。

>[!IMPORTANT]
>
>的 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的连接的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 独特 `id` 值。 |

**请求**

以下请求提供了新名称和描述以及一组新的凭据，用于更新您与的连接。

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
| `op` | 操作调用，用于定义更新连接所需的操作。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的连接ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供连接ID。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 后续步骤

通过阅读本教程，您已使用更新了与连接关联的凭据和信息 [!DNL Flow Service] API。 有关使用源连接器的更多信息，请参阅 [源概述](../../home.md).
