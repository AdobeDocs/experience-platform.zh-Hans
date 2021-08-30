---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务api
solution: Experience Platform
title: '使用API管理数据使用标签 '
topic-legacy: developer guide
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# 使用API管理数据使用标签

本文档提供了有关如何使用[!DNL Policy Service] API和[!DNL Dataset Service] API管理数据使用标签的步骤。

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)提供了多个端点，允许您创建和管理贵组织的数据使用标签。

[!DNL Dataset Service] API允许您应用和编辑数据集的使用情况标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的[!DNL Catalog Service] API不同。

## 快速入门

在阅读本指南之前，请按照目录开发人员指南的[快速入门部分](../../catalog/api/getting-started.md)中概述的步骤，收集所需的凭据以调用[!DNL Platform] API。

要调用本文档中列出的[!DNL Dataset Service]端点，您必须具有特定数据集的唯一`id`值。 如果没有此值，请参阅[listing Catalog objects](../../catalog/api/list-objects.md)指南，以查找现有数据集的ID。

## 列出所有标签 {#list-labels}

使用[!DNL Policy Service] API，您可以通过分别向`/labels/core`或`/labels/custom`发出GET请求来列出所有`core`或`custom`标签。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回从系统检索的自定义标签列表。 由于上面的示例请求是向`/labels/custom`发出的，因此下面的响应仅显示自定义标签。

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

## 查找标签 {#look-up-label}

您可以在[!DNL Policy Service] API的GET请求路径中包含特定标签的`name`属性，以查找特定标签。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 要查找的自定义标签的`name`属性。 |

**请求**

以下请求会检索路径中指示的自定义标签`L2`。

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

## 创建或更新自定义标签 {#create-update-label}

要创建或更新自定义标签，必须向[!DNL Policy Service] API发出PUT请求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 自定义标签的`name`属性。 如果不存在具有此名称的自定义标签，则将创建新标签。 如果存在，则将更新该标签。 |

**请求**

以下请求会创建一个新标签`L3`，该标签旨在描述包含与客户选择的付款计划相关的信息的数据。

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
| `name` | 标签的唯一字符串标识符。 此值用于查找目的并将标签应用于数据集和字段，因此建议使用简短。 |
| `category` | 标签的类别。 虽然您可以为自定义标签创建自己的类别，但强烈建议您使用`Custom`，如果您希望该标签显示在UI中。 |
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

## 查找数据集的标签 {#look-up-dataset-labels}

您可以通过向[!DNL Dataset Service] API发出GET请求，来查找已应用于现有数据集的数据使用标签。

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

成功的响应会返回已应用于数据集的数据使用情况标签。

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
| `labels` | 已应用于数据集的数据使用情况标签列表。 |
| `optionalLabels` | 数据集中已应用数据使用标签的各个字段的列表。 需要以下子属性：<br/><br/>`option`:包含字段[!DNL Experience Data Model](XDM)属性的对象。 以下三个属性是必需的：<ul><li>`id`:与字 `$id` 段关联的架构的URI值。</li><li>`contentType`:指示架构的格式和版本。有关更多信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。</li><li>`schemaPath`:相关架构属性的路径，以JSON Pointer语 [法](../../landing/api-fundamentals.md#json-pointer) 编写。</li></ul>`labels`:要添加到字段的数据使用情况标签的列表。 |

- id:数据集所基于的XDM架构的URI $id值。
- contentType:指示架构的格式和版本。 有关更多信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。
- schemaPath:相关架构属性的路径，以[JSON Pointer](../../landing/api-fundamentals.md#json-pointer)语法编写。

## 将标签应用于数据集 {#apply-dataset-labels}

您可以为数据集创建一组标签，方法是在[!DNL Dataset Service] API的POST或PUT请求的有效负载中提供标签。 使用以下任一方法会覆盖任何现有的标签，并使用有效负载中提供的标签替换它们。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为其创建标签的数据集的唯一`id`值。 |

**请求**

以下POST请求会向数据集以及该数据集内的特定字段添加一系列标签。 有效负载中提供的字段与PUT请求所需的字段相同。

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
| `labels` | 要添加到数据集的数据使用情况标签列表。 |
| `optionalLabels` | 数据集中要向其添加标签的任意单个字段的列表。 此数组中的每个项目都必须具有以下属性：<br/><br/>`option`:包含字段[!DNL Experience Data Model](XDM)属性的对象。 以下三个属性是必需的：<ul><li>`id`:与字 `$id` 段关联的架构的URI值。</li><li>`contentType`:指示架构的格式和版本。有关更多信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。</li><li>`schemaPath`:相关架构属性的路径，以JSON Pointer语 [法](../../landing/api-fundamentals.md#json-pointer) 编写。</li></ul>`labels`:要添加到字段的数据使用情况标签的列表。 |

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

## 从数据集中删除标签 {#remove-dataset-labels}

您可以通过向[!DNL Dataset Service] API发出DELETE请求，删除应用于数据集的标签。

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

成功响应HTTP状态200（确定），表示标签已被删除。 您可以在单独的调用中[查找数据集的现有标签](#look-up-dataset-labels)以确认这一点。

## 后续步骤

通过阅读本文档，您学习了如何使用API管理数据使用标签。

在数据集和字段级别添加数据使用标签后，您可以开始将数据摄取到[!DNL Experience Platform]中。 要了解更多信息，请首先阅读[数据摄取文档](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关更多信息，请参阅[数据使用策略概述](../policies/overview.md)。

有关管理[!DNL Experience Platform]中数据集的更多信息，请参阅[数据集概述](../../catalog/datasets/overview.md)。