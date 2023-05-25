---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务api
solution: Experience Platform
title: 使用API管理数据使用标签
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# 使用API管理数据使用标签

本文档提供了有关如何使用管理数据使用标签的步骤。 [!DNL Policy Service] API和 [!DNL Dataset Service] API。

此 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 提供了多个端点，可让您为组织创建和管理数据使用标签。

此 [!DNL Dataset Service] API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与 [!DNL Catalog Service] 管理数据集元数据的API。

## 快速入门

在阅读本指南之前，请按照 [入门部分](../../catalog/api/getting-started.md) 目录开发人员指南中的，用于收集调用所需的凭据 [!DNL Platform] API。

为了调用 [!DNL Dataset Service] 本文档中概述的端点，您必须具有 `id` 特定数据集的值。 如果您没有此值，请参阅上的指南 [列出目录对象](../../catalog/api/list-objects.md) 以查找现有数据集的ID。

## 列出所有标签 {#list-labels}

使用 [!DNL Policy Service] API，您可以列出所有 `core` 或 `custom` 标签(通过向以下用户发出GET请求) `/labels/core` 或 `/labels/custom`，则不会显示任何内容。

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

成功的响应将返回从系统中检索到的自定义标签列表。 由于上述范例请求是向 `/labels/custom`，则下面的响应仅显示自定义标签。

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

您可以通过包含特定标签的 `name` GET请求路径中的属性 [!DNL Policy Service] API。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 此 `name` 要查找的自定义标签的属性。 |

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

成功的响应将返回自定义标签的详细信息。

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

PUT要创建或更新自定义标签，您必须向 [!DNL Policy Service] API。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 此 `name` 自定义标签的属性。 如果不存在具有此名称的自定义标签，则将创建新标签。 如果存在，则将更新该标签。 |

**请求**

以下请求创建一个新标签， `L3`，用于描述包含与客户所选支付计划相关的信息的数据。

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
| `name` | 标签的唯一字符串标识符。 此值用于查找目的，并将标签应用于数据集和字段，因此建议该值简短明了。 |
| `category` | 标签的类别。 虽然您可以为自定义标签创建自己的类别，但强烈建议您使用 `Custom` 是否希望标签显示在UI中。 |
| `friendlyName` | 标签的友好名称，用于显示目的。 |
| `description` | （可选）提供进一步上下文的标签描述。 |

**响应**

成功的响应将返回自定义标签的详细信息，如果更新了现有标签，则返回HTTP代码为200 （确定）；如果创建了新标签，则返回201 （创建）。

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

您可以通过对以下项发出GET请求，查找已应用于现有数据集的数据使用标签： [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 要查找其标签的数据集的值。 |

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

成功响应将返回已应用于数据集的数据使用标签。

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
| `labels` | 已应用于数据集的数据使用标签列表。 |
| `optionalLabels` | 数据集内已应用数据使用标签的单独字段列表。 需要以下子属性：<br/><br/>`option`：包含 [!DNL Experience Data Model] (XDM)字段的属性。 需要以下三个属性：<ul><li>`id`：URI `$id` 与字段关联的架构的值。</li><li>`contentType`：指示架构的格式和版本。 请参阅以下部分： [架构版本控制](../../xdm/api/getting-started.md#versioning) 有关更多信息，请参阅XDM API指南。</li><li>`schemaPath`：相关架构属性的路径，写入位置 [JSON指针](../../landing/api-fundamentals.md#json-pointer) 语法。</li></ul>`labels`：要添加到字段的数据使用标签列表。 |

- id：数据集所基于的XDM架构的URI $id值。
- contentType：指示架构的格式和版本。 请参阅以下部分： [架构版本控制](../../xdm/api/getting-started.md#versioning) 有关更多信息，请参阅XDM API指南。
- schemaPath：相关架构属性的路径，写入 [JSON指针](../../landing/api-fundamentals.md#json-pointer) 语法。

## 将标签应用于数据集 {#apply-dataset-labels}

您可以为数据集创建一组标签，方法是在POST或PUT请求的有效负荷中将这些标签提供给 [!DNL Dataset Service] API。 使用这两种方法之一会覆盖任何现有标签，并将它们替换为有效负载中提供的标签。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 您正在为其创建标签的数据集的值。 |

**请求**

以下POST请求向数据集添加了一系列标签，以及该数据集中的特定字段。 有效负载中提供的字段与PUT请求所需的字段相同。

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
| `labels` | 要添加到数据集的数据使用标签列表。 |
| `optionalLabels` | 数据集内要向其添加标签的任何单独字段的列表。 此数组中的每一项都必须具有以下属性：<br/><br/>`option`：包含 [!DNL Experience Data Model] (XDM)字段的属性。 需要以下三个属性：<ul><li>`id`：URI `$id` 与字段关联的架构的值。</li><li>`contentType`：指示架构的格式和版本。 请参阅以下部分： [架构版本控制](../../xdm/api/getting-started.md#versioning) 有关更多信息，请参阅XDM API指南。</li><li>`schemaPath`：相关架构属性的路径，写入位置 [JSON指针](../../landing/api-fundamentals.md#json-pointer) 语法。</li></ul>`labels`：要添加到字段的数据使用标签列表。 |

**响应**

成功的响应将返回已添加到数据集的标签。

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

您可以通过对数据集发出DELETE请求，删除应用于数据集的标签。 [!DNL Dataset Service] API。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 要删除其标签的数据集的值。 |

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

成功响应HTTP状态200 （正常），指示标签已被删除。 您可以 [查找现有标签](#look-up-dataset-labels) 在另一个调用中用于数据集以确认这一点。

## 后续步骤

通过阅读本文档，您已了解如何使用API管理数据使用标签。

在数据集和字段级别添加数据使用标签后，您可以开始将数据摄取到 [!DNL Experience Platform]. 要了解更多信息，请从阅读 [数据摄取文档](../../ingestion/home.md).

您现在还可以根据已应用的标签定义数据使用策略。 欲了解更多信息，请参见 [数据使用策略概述](../policies/overview.md).

有关管理中数据集的更多信息 [!DNL Experience Platform]，请参见 [数据集概述](../../catalog/datasets/overview.md).