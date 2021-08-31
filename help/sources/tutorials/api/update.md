---
keywords: Experience Platform；主页；热门主题；流程服务；更新帐户
solution: Experience Platform
title: 使用流服务API更新帐户
topic-legacy: overview
type: Tutorial
description: 本教程介绍了使用流量服务API更新帐户的详细信息和凭据的步骤。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 2%

---

# 使用流量服务API更新帐户

在某些情况下，可能需要更新现有源连接的详细信息。 [!DNL Flow Service] 使您能够添加、编辑和删除现有批处理连接或流连接的详细信息，包括其名称、描述和凭据。

本教程介绍了使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新连接的详细信息和凭据的步骤。

## 快速入门

本教程要求您拥有现有连接和有效的连接ID。 如果您没有现有连接，请从[源概述](../../home.md)中选择您选择的源，然后按照列出的步骤操作，然后再尝试本教程。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功更新连接所需了解的其他信息。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中[如何阅读示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找连接详细信息

更新连接的第一步是使用连接ID检索其详细信息。 要检索连接的当前详细信息，请在提供要更新的连接的连接ID时向[!DNL Flow Service] API发出GET请求。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要检索的连接的唯一`id`值。 |

**请求**

以下请求会检索与您的连接有关的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回连接的当前详细信息，包括其凭据、唯一标识符(`id`)和版本。 更新连接时需要使用版本值。

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

要更新连接的名称、说明和凭据，请在提供连接ID、版本和要使用的新信息时，向[!DNL Flow Service] API执行PATCH请求。

>[!IMPORTANT]
>
>发出PATCH请求时需要`If-Match`标头。 此标头的值是要更新的连接的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要更新的连接的唯一`id`值。 |

**请求**

以下请求提供了新名称和描述以及一组新的凭据，用于更新您与的连接。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | 操作调用，用于定义更新连接所需的操作。 操作包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的连接ID和更新的标记。 在提供连接ID的同时，您可以通过向[!DNL Flow Service] API发出GET请求来验证更新。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 后续步骤

在本教程之后，您已使用[!DNL Flow Service] API更新了与连接相关的凭据和信息。 有关使用源连接器的更多信息，请参阅[源概述](../../home.md)。
