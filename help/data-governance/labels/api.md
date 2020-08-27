---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api
solution: Experience Platform
title: '使用API管理数据使用标签 '
topic: developer guide
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的Catalog Service API分开。
translation-type: tm+mt
source-git-commit: 4096a7c1ec2b3640886d3a8c69b578987fe96dd4
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 3%

---


# 使用API管理数据使用标签

此文档提供了如何使用API和API管理数据使用 [!DNL Policy Service] 标签的 [!DNL Dataset Service] 步骤。

[! [DNL策略服务API]提供了多个端点](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) ，允许您创建和管理组织的数据使用标签。

API [!DNL Dataset Service] 允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元 [!DNL Catalog Service] 数据的API相分离。

## 入门指南

在阅读本指南之前，请按照目录开发人 [员指南](../../catalog/api/getting-started.md) “入门”部分中概述的步骤收集所需凭据以调用 [!DNL Platform] API。

要调用此文档中概 [!DNL Dataset Service] 述的端点，您必须具有特定数 `id` 据集的唯一值。 如果没有此值，请参阅列出目录对 [象的指南](../../catalog/api/list-objects.md) ，以查找现有数据集的ID。

## 列表所有标签 {#list-labels}

使用 [!DNL Policy Service] API，您可以通过分别向 `core` 或 `custom` 发出GET请求来列表所 `/labels/core` 有或 `/labels/custom`标签。

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

## 查找标签 {#look-up-label}

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

## 创建或更新自定义标签 {#create-update-label}

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

## 查找数据集的标签 {#look-up-dataset-labels}

您可以通过向API发出GET请求来查找已应用于现有数据集的数据使用标 [!DNL Dataset Service] 签。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找 `id` 其标签的数据集的唯一值。 |

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

成功的响应会返回已应用于数据集的数据使用标签。

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
| `labels` | 应用于数据集的列表数据使用标签。 |
| `optionalLabels` | 列表数据集中已应用数据使用标签的各个字段。 |

## 将标签应用于数据集 {#apply-dataset-labels}

您可以通过在POST或PUT请求的有效负荷中提供数据集的标签集来为API创建一组标 [!DNL Dataset Service] 签。 使用以下任一方法将覆盖任何现有标签，并用有效负荷中提供的标签替换它们。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为 `id` 其创建标签的数据集的唯一值。 |

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
| `optionalLabels` | 列表数据集中要添加标签的任何单个字段。 此数组中的每个项目都必须具有以下属性： <br/><br/>`option`:包含字段 [!DNL Experience Data Model] (XDM)属性的对象。 以下三个属性是必需的：<ul><li>id</code>:与字段关联的</code> 模式的URI $id值。</li><li>contentType</code>:模式的内容类型和版本号。 这应采用XDM查找请求的有效 <a href="../../xdm/api/look-up-resource.md">接受标头</a> 之一的形式。</li><li>schemaPath</code>:数据集模式中字段的路径。</li></ul>`labels`:要添加到字段的列表数据使用标签。 |

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

您可以通过向API发出DELETE请求来删除应用于数据集的标 [!DNL Dataset Service] 签。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要删除 `id` 其标签的数据集的唯一值。 |

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

成功响应HTTP状态200(OK)，表示标签已被删除。 您可以 [在单独的调用中查找](#look-up-dataset-labels) 数据集的现有标签以确认这一点。

## 后续步骤

通过阅读此文档，您学习了如何使用API管理数据使用标签。

在数据集和字段级别添加数据使用标签后，您可以开始将数据收集到中 [!DNL Experience Platform]。 要了解更多信息，请阅读开始 [获取文档](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关详细信息，请参阅 [数据使用策略概述](../policies/overview.md)。

有关管理中数据集的更 [!DNL Experience Platform]多信息，请参 [阅数据集概述](../../catalog/datasets/overview.md)。