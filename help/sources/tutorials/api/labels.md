---
title: 应用访问标签以管理用户对使用API的源数据流的访问
description: 了解如何使用流服务API来应用访问标签和管理用户对您的源数据流的访问。
exl-id: 572d6838-3e4c-4fd5-89fa-32cad6280325
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 3%

---

# 应用访问标签以管理用户对使用API的源数据流的访问

您可以使用Real-Time CDP中由[基于属性的访问控制](../../../access-control/abac/overview.md)提供的功能将标签应用于源数据流。 利用此功能，您可以确保组织中只有一部分用户有权访问特定源数据流。

向特定数据流添加访问标签时，只有对分配了该标签的角色具有访问权限的用户才能查看和编辑该数据流。 如果源数据流未标记任何标签，则它对于属于您组织的所有用户都可见。 例如，如果将C12标签应用于数据流，则分配到没有C12标签的角色的用户将无法查看和编辑具有C12标签的数据流。

有关如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将访问标签应用于源数据流的信息，请阅读本指南。

## 快速入门

在使用访问控制标签之前，请确保您首先要熟悉基于属性的访问控制的功能。 有关详细信息，请阅读以下文档：

* [基于属性的访问控制概述](../../../access-control/abac/overview.md)
* [基于属性的访问控制端到端指南](../../../access-control/abac/end-to-end-guide.md)
* [基于属性的访问控制API指南](../../../access-control/abac/api/overview.md)
* [数据使用标签词汇表](../../../data-governance/labels/reference.md)

## 将访问标签应用于源数据流

>[!NOTE]
>
>* 不能将标签应用于流运行。 但是，流运行会继承您应用于父数据流的任意标签。
>
>* 如果您没有数据流的查看访问权限，则也无法查看其对应的流运行。

若要向数据流添加标签，请向`/flows`端点发出PATCH请求，并提供要更新的数据流的ID。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{FLOW_ID}` | 要更新的数据流的ID。 |

**请求**

>[!TIP]
>
>要发出PATCH请求，请提供要作为`if-match`标头参数更新的数据流版本/etag。

以下请求将C12标签添加到ID为`84224def-1e2a-4d95-9ea2-132d697ed2aa`的数据流。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 要更新的数据流部分。 |
| `value` | 要用于更新属性的新值。 |



**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

成功配置数据流访问标签后，任何无权访问该标签的用户将无法再检索数据流。 例如，如果未配置C12标签的用户发出GET请求以检索ID为`84224def-1e2a-4d95-9ea2-132d697ed2aa`的数据流，他们将收到以下响应：

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

同样，无权访问C12标签的用户将无法针对更新的数据流发起任何PATCH或DELETE请求，并将收到以下响应：

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## 后续步骤

您现在知道如何将访问标签应用于源数据流。 现在，您可以确保只有贵组织中的特定用户组才能访问特定源数据流。 有关其他信息，请阅读以下文档：

* [将访问标签应用于UI中的源数据流](../ui/labels.md)
* [访问控制概述](../../../access-control/home.md)
