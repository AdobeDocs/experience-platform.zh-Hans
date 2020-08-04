---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: '使用API管理数据集的数据使用标签 '
topic: developer guide
translation-type: tm+mt
source-git-commit: 2f35765c0dfadbfb4782b6c3904e33ae7a330b2f
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---


# 使用API管理数据集的数据使用标签

使 [!DNL Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) 用，您可以应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元 [!DNL Catalog Service] 数据的API相分离。

本文档介绍如何使用管理数据集和字段的标签 [!DNL Dataset Service API]。 有关如何使用API调用管理数据使用标签本身的步骤，请参 [阅的标签端点指南](../api/labels.md) ( [!DNL Policy Service API])。

## 入门指南

在阅读本指南之前，请按照目录开发人 [员指南](../../catalog/api/getting-started.md) “入门”部分中概述的步骤收集所需凭据以调用 [!DNL Platform] API。

要调用此文档中概述的端点，您必须具有特定数 `id` 据集的唯一值。 如果没有此值，请参阅列出目录对 [象的指南](../../catalog/api/list-objects.md) ，以查找现有数据集的ID。

## 查找数据集的标签 {#look-up}

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

## 将标签应用于数据集 {#apply}

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
| `optionalLabels` | 列表数据集中要添加标签的任何单个字段。 此数组中的每个项目都必须具有以下属性： <br/><br/>`option`: 包含字段 [!DNL Experience Data Model] (XDM)属性的对象。 以下三个属性是必需的：<ul><li>id</code>: 与字段关联的</code> 模式的URI $id值。</li><li>contentType</code>: 模式的内容类型和版本号。 这应采用XDM查找请求的有效 <a href="../../xdm/api/look-up-resource.md">接受标头</a> 之一的形式。</li><li>schemaPath</code>: 数据集模式中字段的路径。</li></ul>`labels`: 要添加到字段的列表数据使用标签。 |

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

## 从数据集中删除标签 {#remove}

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

成功响应HTTP状态200(OK)，表示标签已被删除。 您可以 [在单独的调用中查找](#look-up) 数据集的现有标签以确认这一点。

## 后续步骤

通过阅读此文档，您学习了如何使用API管理数据集和字段的数据使用标 [!DNL Dataset Service] 签。

在数据集和字段级别添加数据使用标签后，您可以开始将数据收集到中 [!DNL Experience Platform]。 要了解更多信息，请阅读开始 [获取文档](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关详细信息，请参阅 [数据使用策略概述](../policies/overview.md)。

有关管理中数据集的更 [!DNL Experience Platform]多信息，请参 [阅数据集概述](../../catalog/datasets/overview.md)。