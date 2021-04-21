---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务api
solution: Experience Platform
title: '使用API管理数据使用标签 '
topic-legacy: developer guide
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的Catalog Service API是分开的。
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 2%

---


# 使用API管理数据使用标签

本文档提供了有关如何使用[!DNL Policy Service] API和[!DNL Dataset Service] API管理数据使用标签的步骤。

[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)提供了多个端点，允许您创建和管理组织的数据使用标签。

[!DNL Dataset Service] API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的[!DNL Catalog Service] API分开。

## 入门指南

在阅读本指南之前，请按照目录开发人员指南中[入门部分](../../catalog/api/getting-started.md)中概述的步骤收集所需凭据以调用[!DNL Platform] API。

要调用此文档中概述的[!DNL Dataset Service]终结点，您必须具有特定数据集的唯一`id`值。 如果没有此值，请参阅[列表目录对象](../../catalog/api/list-objects.md)的指南，以查找现有数据集的ID。

## 列表所有标签{#list-labels}

使用[!DNL Policy Service] API，您可以通过分别向`/labels/core`或`/labels/custom`发出GET请求来列表所有`core`或`custom`标签。

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

成功的响应返回从系统检索的自定义标签的列表。 由于以上示例请求是向`/labels/custom`发出的，因此下面的响应仅显示自定义标签。

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

## 查找标签{#look-up-label}

您可以通过在GET请求到[!DNL Policy Service] API的路径中包含该标签的`name`属性来查找特定标签。

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

## 创建或更新自定义标签{#create-update-label}

要创建或更新自定义标签，必须向[!DNL Policy Service] API发出PUT请求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 自定义标签的`name`属性。 如果不存在具有此名称的自定义标签，则将创建新标签。 如果确实存在，该标签将更新。 |

**请求**

以下请求创建新标签`L3`，旨在描述包含与客户所选付款计划相关信息的数据。

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
| `name` | 标签的唯一字符串标识符。 此值用于查找目的并将标签应用于数据集和字段，因此建议它简短和简洁。 |
| `category` | 标签的类别。 虽然您可以为自定义标签创建自己的类别，但强烈建议您使用`Custom`（如果希望标签显示在UI中）。 |
| `friendlyName` | 用于显示目的的标签的易记名称。 |
| `description` | （可选）用于提供更多上下文的标签描述。 |

**响应**

成功的响应会返回自定义标签的详细信息，如果更新了现有标签，则返回HTTP代码为200（确定）；如果创建了新标签，则返回201（已创建）。

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

## 查找数据集{#look-up-dataset-labels}的标签

您可以通过向[!DNL Dataset Service] API发出GET请求来查找已应用于现有数据集的数据使用标签。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找其标签的数据集的唯一`id`值。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回已应用于数据集的数据使用标签。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `labels` | 已应用于数据集的列表数据使用标签。 |
| `optionalLabels` | 列表数据集中应用了数据使用标签的各个字段。 需要以下子属性：<br/><br/>`option`:包含字段的[!DNL Experience Data Model](XDM)属性的对象。 以下三个属性是必需的：<ul><li>`id`:与字 `$id` 段关联的模式的URI值。</li><li>`contentType`:指示模式的格式和版本。有关详细信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。</li><li>`schemaPath`:所述模式属性的路径，用JSON Pointer语法 [编](../../landing/api-fundamentals.md#json-pointer) 写。</li></ul>`labels`:要添加到字段的数据使用标签列表。 |

- id:数据集所基于的XDM模式的URI $id值。
- contentType:指示模式的格式和版本。 有关详细信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。
- schemaPath:所述模式属性的路径，以[JSON Pointer](../../landing/api-fundamentals.md#json-pointer)语法编写。

## 将标签应用于数据集{#apply-dataset-labels}

您可以通过在POST或PUT请求[!DNL Dataset Service] API的负载中提供数据集的标签来为数据集创建一组标签。 使用以下任一方法将覆盖任何现有标签，并将其替换为有效负荷中提供的标签。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为其创建标签的数据集的唯一`id`值。 |

**请求**

以下POST请求会向数据集添加一系列标签以及该数据集中的特定字段。 有效负荷中提供的字段与PUT请求所需的字段相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `labels` | 要添加到数据集的列表数据使用标签。 |
| `optionalLabels` | 列表数据集中要添加标签的任何单个字段。 此数组中的每个项都必须具有以下属性：<br/><br/>`option`:包含字段的[!DNL Experience Data Model](XDM)属性的对象。 以下三个属性是必需的：<ul><li>`id`:与字 `$id` 段关联的模式的URI值。</li><li>`contentType`:指示模式的格式和版本。有关详细信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。</li><li>`schemaPath`:所述模式属性的路径，用JSON Pointer语法 [编](../../landing/api-fundamentals.md#json-pointer) 写。</li></ul>`labels`:要添加到字段的数据使用标签列表。 |

**响应**

成功的响应会返回已添加到数据集的标签。

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## 从数据集{#remove-dataset-labels}中删除标签

可以通过向[!DNL Dataset Service] API发出DELETE请求来删除应用于数据集的标签。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要删除其标签的数据集的唯一`id`值。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应HTTP状态200(OK)，表示标签已被删除。 您可以在单独的调用中查找数据集的现有标签](#look-up-dataset-labels)以确认这一点。[

## 后续步骤

通过阅读此文档，您学习了如何使用API管理数据使用标签。

在数据集和字段级别添加数据使用标签后，即可开始将数据收录到[!DNL Experience Platform]中。 要了解更多信息，请阅读[开始获取文档](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关详细信息，请参阅[数据使用策略概述](../policies/overview.md)。

有关管理[!DNL Experience Platform]中的数据集的详细信息，请参阅[数据集概述](../../catalog/datasets/overview.md)。