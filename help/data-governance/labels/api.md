---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务api
solution: Experience Platform
title: '使用API管理数据使用标签 '
topic-legacy: developer guide
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# 使用API管理数据使用标签

本文档提供了有关如何使用 [!DNL Policy Service] API和 [!DNL Dataset Service] API。

的 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 提供了多个端点，允许您为贵组织创建和管理数据使用标签。

的 [!DNL Dataset Service] API允许您应用和编辑数据集的使用情况标签。 它是Adobe Experience Platform数据目录功能的一部分，但与 [!DNL Catalog Service] 管理数据集元数据的API。

## 快速入门

在阅读本指南之前，请先执行 [入门部分](../../catalog/api/getting-started.md) ，以收集所需的凭据来调用 [!DNL Platform] API。

为了调用 [!DNL Dataset Service] 端点，则您必须具有 `id` 值。 如果没有此值，请参阅 [列出目录对象](../../catalog/api/list-objects.md) 以查找现有数据集的ID。

## 列出所有标签 {#list-labels}

使用 [!DNL Policy Service] API，您可以列出所有 `core` 或 `custom` 通过向发送GET请求 `/labels/core` 或 `/labels/custom`，分别为。

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

## 查找标签 {#look-up-label}

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

## 创建或更新自定义标签 {#create-update-label}

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

## 查找数据集的标签 {#look-up-dataset-labels}

您可以通过向 [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 独特 `id` 要查找其标签的数据集的值。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回已应用于数据集的数据使用情况标签。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
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
| `optionalLabels` | 数据集中已应用数据使用标签的各个字段的列表。 需要以下子属性：<br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)字段的属性。 以下三个属性是必需的：<ul><li>`id`:URI `$id` 与字段关联的架构的值。</li><li>`contentType`:指示架构的格式和版本。 请参阅 [模式版本控制](../../xdm/api/getting-started.md#versioning) ，以了解更多信息。</li><li>`schemaPath`:相关架构属性的路径，写入 [JSON指针](../../landing/api-fundamentals.md#json-pointer) 语法。</li></ul>`labels`:要添加到字段的数据使用情况标签的列表。 |

- id:数据集所基于的XDM架构的URI $ID值。
- contentType:指示架构的格式和版本。 请参阅 [模式版本控制](../../xdm/api/getting-started.md#versioning) ，以了解更多信息。
- schemaPath:相关架构属性的路径，写入 [JSON指针](../../landing/api-fundamentals.md#json-pointer) 语法。

## 将标签应用于数据集 {#apply-dataset-labels}

您可以为数据集创建一组标签，方法是在POST或PUT请求的有效负荷中向提供标签 [!DNL Dataset Service] API。 使用以下任一方法会覆盖任何现有的标签，并使用有效负载中提供的标签替换它们。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 独特 `id` 要为其创建标签的数据集的值。 |

**请求**

以下POST请求会向数据集以及该数据集内的特定字段添加一系列标签。 有效负载中提供的字段与PUT请求所需的字段相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optionalLabels` | 数据集中要向其添加标签的任意单个字段的列表。 此数组中的每个项目都必须具有以下属性：<br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)字段的属性。 以下三个属性是必需的：<ul><li>`id`:URI `$id` 与字段关联的架构的值。</li><li>`contentType`:指示架构的格式和版本。 请参阅 [模式版本控制](../../xdm/api/getting-started.md#versioning) ，以了解更多信息。</li><li>`schemaPath`:相关架构属性的路径，写入 [JSON指针](../../landing/api-fundamentals.md#json-pointer) 语法。</li></ul>`labels`:要添加到字段的数据使用情况标签的列表。 |

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

您可以通过向 [!DNL Dataset Service] API。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 独特 `id` 要删除其标签的数据集的值。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应HTTP状态200（确定），表示标签已被删除。 您可以 [查找现有标签](#look-up-dataset-labels) ，以在单独的调用中确认此操作。

## 后续步骤

通过阅读本文档，您学习了如何使用API管理数据使用标签。

在数据集和字段级别添加数据使用情况标签后，您可以开始将数据摄取到 [!DNL Experience Platform]. 要了解更多信息，请首先阅读 [数据获取文档](../../ingestion/home.md).

您现在还可以根据已应用的标签定义数据使用策略。 有关更多信息，请参阅 [数据使用策略概述](../policies/overview.md).

有关管理 [!DNL Experience Platform]，请参阅 [数据集概述](../../catalog/datasets/overview.md).