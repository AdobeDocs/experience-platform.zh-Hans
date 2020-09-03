---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 标签端点
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 3%

---


# 标签端点

数据使用标签允许您根据可能适用于该数据的使用策略对数据进行分类。 中的 `/labels` 端点允许您 [!DNL Policy Service API] 以编程方式管理体验应用程序中的数据使用标签。

>[!NOTE]
>
>端点 `/labels` 仅用于检索、创建和更新数据使用标签。 有关如何使用API调用向数据集和字段添加标签的步骤，请参阅《管理数据集标签 [指南》](../labels/dataset-api.md)。

## 入门指南

本指南中使用的API端点是[[!DNL策略服务API]的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在继续之前，请查 [看入门指南](getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 检索标签列表 {#list}

您可以通过分别 `core` 向或 `custom` 者发出列表请求来GET所 `/labels/core` 有或 `/labels/custom`标签。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**请求**

以下请求将列表在您的组织下创建的所有自定义标签。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回从系统检索的一列表自定义标签。 由于上面的示例请求是向 `/labels/custom`的，因此下面的响应仅显示自定义标签。

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

通过在向API请求GET的路径中包 `name` 含该标签的属性，可以查找特定 [!DNL Policy Service] 标签。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 要 `name` 查找的自定义标签的属性。 |

**请求**

以下请求将检索自定 `L2`义标签，如路径所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

要创建或更新自定义标签，您必须向API发出PUT [!DNL Policy Service] 请求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 自 `name` 定义标签的属性。 如果不存在具有此名称的自定义标签，则将创建新标签。 如果存在，则该标签将更新。 |

**请求**

以下请求创建新标签， `L3`该标签旨在描述包含与客户所选付款计划相关的信息的数据。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 标签的唯一字符串标识符。 此值用于查找目的并将标签应用于数据集和字段，因此建议它简短而简明。 |
| `category` | 标签的类别。 虽然您可以为自定义标签创建自己的类别，但强烈建议您 `Custom` 在UI中显示标签时使用。 |
| `friendlyName` | 用于显示目的的标签的友好名称。 |
| `description` | （可选）用于提供更多上下文的标签描述。 |

**响应**

成功的响应会返回自定义标签的详细信息，如果更新了现有标签，则返回HTTP代码200（确定）；如果创建了新标签，则返回201（已创建）。

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

本指南介绍了在策略服 `/labels` 务API中端点的使用。 有关如何将标签应用到数据集和字段的步骤，请参阅数 [据集标签API指南](../labels/dataset-api.md)。
