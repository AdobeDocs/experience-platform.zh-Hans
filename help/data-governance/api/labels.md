---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 标签端点
topic: developer guide
description: 了解如何使用策略服务API在Experience Platform中管理数据使用标签。
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---


# 标签端点

数据使用标签允许您根据可能适用于该数据的使用策略对数据进行分类。 [!DNL Policy Service API]中的`/labels`端点允许您以编程方式管理体验应用程序中的数据使用标签。

>[!NOTE]
>
>`/labels`端点仅用于检索、创建和更新数据使用标签。 有关如何使用API调用向数据集和字段添加标签的步骤，请参阅[管理数据集标签](../labels/dataset-api.md)上的指南。

## 入门指南

本指南中使用的API端点是[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 检索标签列表{#list}

您可以通过分别向`/labels/core`或`/labels/custom`发出列表请求，来GET所有`core`或`custom`标签。

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

成功的响应返回从系统检索的一列表自定义标签。 由于以上示例请求是向`/labels/custom`发出的，因此下面的响应只显示自定义标签。

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

## 查找标签{#look-up}

通过将该标签的`name`属性包含在[!DNL Policy Service] API的GET请求路径中，可以查找特定标签。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 要查找的自定义标签的`name`属性。 |

**请求**

以下请求将检索自定义标签`L2`，如路径中所示。

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

## 创建或更新自定义标签{#create-update}

要创建或更新自定义标签，您必须向[!DNL Policy Service] API发出PUT请求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 自定义标签的`name`属性。 如果不存在具有此名称的自定义标签，则将创建新标签。 如果存在，则该标签将更新。 |

**请求**

以下请求将创建一个新标签`L3`，该标签旨在描述包含与客户所选付款计划相关的信息的数据。

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
| `category` | 标签的类别。 虽然您可以为自定义标签创建自己的类别，但强烈建议您使用`Custom`（如果希望标签显示在UI中）。 |
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

本指南介绍了在策略服务API中使用`/labels`端点的情况。 有关如何将标签应用到数据集和字段的步骤，请参阅[数据集标签API指南](../labels/dataset-api.md)。