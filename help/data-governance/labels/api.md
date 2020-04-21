---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: '使用API管理数据使用标签 '
topic: developer guide
translation-type: tm+mt
source-git-commit: cac6ab568f030cf86ee68a1df9e45a3ac9d421cb

---


# 使用API管理数据使用标签

本文档提供了如何使用Catalog Service API管理数据集级和字段级的数据使用标签的步骤。

## 入门指南

在阅读本指南之前，建议您阅读目录服务概述 [](../../catalog/home.md) ，以便了解该服务的更强大的介绍。 此外，您还必须按照目录开发人员指南中 [的入门部分中所述](../../catalog/api/getting-started.md) ，收集所需凭据以调用目录API。

要调用以下各节中概述的端点，您必须具有特定数 `id` 据集的唯一值。 如果您没有此值，请参阅列出目录对象的开发人员指 [南部分](../../catalog/api/list-objects.md) ，以查找现有数据集的ID。

## 查找数据集的标签 {#lookup}

您可以通过发出GET请求来查找已应用于现有数据集的数据使用标签。

**API格式**

```http
GET /dataSets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找 `id` 其标签的数据集的唯一值。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回已应用到数据集的数据使用标签。

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
| `labels` | 已应用于数据集的数据使用标签列表。 |
| `optionalLabels` | 数据集中已应用数据使用标签的单个字段的列表。 |

## 将标签应用于数据集

您可以通过在POST或PUT请求的有效负荷中提供数据集的标签集。 使用其中任一方法将覆盖任何现有标签，并将其替换为有效负荷中提供的标签。

**API格式**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为 `id` 其创建标签的数据集的唯一值。 |

**请求**

以下POST请求向数据集中添加一系列标签以及该数据集中的特定字段。 有效负荷中提供的字段与PUT请求所需的字段相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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
| `labels` | 要添加到数据集的数据使用标签列表。 |
| `optionalLabels` | 数据集中要添加标签的任何单个字段的列表。 此数组中的每个项目都必须具有以下属性： <br/><br/>`option`:包含字段的体验数据模型(XDM)属性的对象。 以下三个属性是必需的：<ul><li>id</code>:与字段关联的模式的URI $id</code> 值。</li><li>contentType</code>:模式的内容类型和版本号。 这应采用XDM查找请求的有效接 <a href="../../xdm/api/look-up-resource.md">受头之一</a> 。</li><li>schemaPath</code>:数据集模式中字段的路径。</li></ul>`labels`:要添加到字段的数据使用标签列表。 |

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

## 删除数据集的标签

您可以通过发出DELETE请求来删除应用于数据集的标签。

>[!NOTE] 您只应在准备要删除的父数据集时使用此操作。

**API格式**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要删除 `id` 其标签的数据集的唯一值。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应HTTP状态200(OK)表示已删除标签。 您可以 [在单独的调用中查找数据集的现有标签](#lookup) ，以确认这一点。

## 后续步骤

现在，您已在数据集和字段级别添加了数据使用标签，可以开始将数据引入Experience Platform。 要了解更多信息，请阅读数据获取文 [档进行开始](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关详细信息，请参阅数 [据使用策略概述](../policies/overview.md)。