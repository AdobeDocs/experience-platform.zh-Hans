---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 标签API端点
topic-legacy: developer guide
description: 了解如何使用策略服务API在Experience Platform中管理数据使用标签。
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# 标签端点

数据使用标签允许您根据可能应用于该数据的使用策略对数据进行分类。 的 `/labels` 的端点 [!DNL Policy Service API] 允许您以编程方式管理体验应用程序中的数据使用情况标签。

>[!NOTE]
>
>的 `/labels` 端点仅用于检索、创建和更新数据使用情况标签。 有关如何使用API调用向数据集和字段添加标签的步骤，请参阅 [管理数据集标签](../labels/dataset-api.md).

## 快速入门

本指南中使用的API端点是 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在继续之前，请查看 [入门指南](getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 检索标签列表 {#list}

您可以列出所有 `core` 或 `custom` 通过向发送GET请求 `/labels/core` 或 `/labels/custom`，分别为。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**请求**

以下请求列出了在您的组织下创建的所有自定义标签。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回从系统检索的自定义标签列表。 由于上述示例请求是 `/labels/custom`，则下面的响应仅显示自定义标签。

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## 查找标签 {#look-up}

您可以通过包含该标签的 `name` 属性(在GET请求的路径中) [!DNL Policy Service] API。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 的 `name` 要查找的自定义标签的属性。 |

**请求**

以下请求检索自定义标签 `L2`，如路径中所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回自定义标签的详细信息。

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## 创建或更新自定义标签 {#create-update}

要创建或更新自定义标签，您必须向 [!DNL Policy Service] API。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 的 `name` 自定义标签的属性。 如果不存在具有此名称的自定义标签，则将创建新标签。 如果存在，则将更新该标签。 |

**请求**

以下请求会创建新标签， `L3`，旨在描述包含与客户选择的支付计划相关信息的数据。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 标签的唯一字符串标识符。 此值用于查找目的并将标签应用于数据集和字段，因此建议使用简短。 |
| `category` | 标签的类别。 虽然您可以为自定义标签创建自己的类别，但强烈建议您使用 `Custom` 如果您希望标签显示在UI中，请执行以下操作： |
| `friendlyName` | 标签的易记名称，用于显示。 |
| `description` | （可选）用于提供更多上下文的标签描述。 |

**响应**

成功的响应会返回自定义标签的详细信息，如果更新了现有标签，则返回HTTP代码为200(OK)；如果创建了新标签，则返回201（已创建）。

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## 后续步骤

本指南介绍了 `/labels` 策略服务API中的端点。 有关如何将标签应用于数据集和字段的步骤，请参阅 [数据集标签API指南](../labels/dataset-api.md).
