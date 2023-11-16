---
keywords: Experience Platform；主页；热门主题；数据集api；管理数据使用情况；数据使用情况api
solution: Experience Platform
title: 使用API管理数据集的数据使用标签
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 319bcc742b09f979cd744c8d66f032886427ea9e
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 1%

---

# 使用API管理数据集的数据使用标签

此 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与 [!DNL Catalog Service] 管理数据集元数据的API。

>[!IMPORTANT]
>
>仅数据管理用例支持在数据集级别应用标签。 如果您尝试为数据创建访问策略，则必须 [将标签应用于架构](../../xdm/tutorials/labels.md) 数据集所基于的内容。 有关更多详细信息，请参阅 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解更多信息。

本文档介绍如何使用管理数据集和字段的标签 [!DNL Dataset Service API]. 有关如何使用API调用管理数据使用标签本身的步骤，请参阅 [标签端点指南](../api/labels.md) 对于 [!DNL Policy Service API].

## 快速入门

在阅读本指南之前，请按照 [快速入门部分](../../catalog/api/getting-started.md) ，以收集进行调用所需的凭据 [!DNL Platform] API。

要调用本文档中概述的端点，您必须具有 `id` 特定数据集的值。 如果您没有此值，请参阅上的指南 [列出目录对象](../../catalog/api/list-objects.md) 以查找现有数据集的ID。

## 查找数据集的标签 {#look-up}

您可以通过对GET请求，查找已应用于现有数据集的数据使用标签 [!DNL Dataset Service] API。

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

成功的响应将返回已应用于数据集的数据使用标签。

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
| `optionalLabels` | 数据集内已应用数据使用标签的单独字段列表。 |

## 将标签应用于数据集 {#apply}

通过在POST或PUT请求的有效负荷中提供一组标签，您可以为整个数据集应用这些标签。 [!DNL Dataset Service] API。 两个调用的请求正文相同。 您无法将标签添加到单独的数据集字段。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 要为其创建标签的数据集的值。 |

**请求**

下面的示例POST请求使用更新整个数据集 `C1` 标签。 有效负载中提供的字段与PUT请求所需的字段相同。

进行更新数据集(PUT)现有标签的API调用时， `If-Match` 必须包括指示数据集服务中数据集标签实体的当前版本的标头。 为防止数据冲突，服务将只更新数据集实体（如果包含） `If-Match` 字符串匹配系统为该数据集生成的最新版本标记。

>[!NOTE]
>
>如果相关数据集当前存在标签，则只能通过PUT请求添加新标签，这需要一个 `If-Match` 标题。 将标签添加到数据集后，最近的 `etag` 稍后需要使用此值来更新或删除标签<br>在执行PUT方法之前，必须对数据集标签执行GET请求。 确保仅更新请求中要修改的特定字段，而其余字段保持不变。 此外，确保PUT调用维护与GET调用相同的父实体。 任何差异都会导致客户出错。

要检索最新版本的dataset-label实体，请生成 [GET请求](#look-up) 到 `/datasets/{DATASET_ID}/labels` 端点。 当前值在响应中返回到 `etag` 标题。 更新现有数据集标签时，最佳做法是首先执行数据集的查找请求，以获取其最新数据 `etag` 值之前，在中使用该 `If-Match` 后续PUT请求的标题。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
            {
              "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
              "type": "schema",
              "namespace": "AEP"
            }
        ]
      } '
```

| 属性 | 描述 |
| --- | --- |
| `entityId` | 这将标识要更新的特定数据集实体。 |
| `entityId.namespace` | 用于避免ID冲突。 此 `namespace` 是 `AEP`. |
| `entityId.id` | 要更新的资源的ID。 此名称是指 `datasetId`. |
| `entityId.type` | 正在更新的资源的类型。 这将永远是 `dataset`. |
| `labels` | 要添加到整个数据集的数据使用标签列表。 |
| `parents` | 此 `parents` 数组包含列表 `entityId`此数据集将从中继承标签的内容。 数据集可以从架构和/或数据集继承标签。 |

**响应**

成功的响应将返回数据集的更新标签集。

>[!IMPORTANT]
>
>此 `optionalLabels` 已弃用资产以用于POST请求。 无法再将数据标签添加到数据集字段。 POST如果 `optionalLabel` 值存在。 但是，您可以使用PUT请求和从各个字段删除标签 `optionalLabels` 属性。 有关详细信息，请参阅 [从数据集中删除标签](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## 从数据集中删除标签 {#remove}

您可以通过更新现有的字段标签来移除任何以前应用的字段标签 `optionalLabels` 具有现有字段标签子集的值，或要完全删除它们的空列表。 向发出PUT请求 [!DNL Dataset Service] 用于更新或删除以前应用的标签的API。

**API格式**

```http
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 要为其创建标签的数据集的值。 |

**请求**

应用PUT操作的以下数据集的properties/person/properties/address字段上具有C1 optionalLabel，而/properties/person/properties/name/properties/fullName字段上具有C1， C2 optionalLabels。 在put操作之后，第一字段将没有标签（C1标签被删除），而第二字段将只有C1标签（C2标签被删除）

在下面的示例场景中，PUT请求用于移除添加到单个字段的标签。 在提出请求之前， `fullName` 字段具有 `C1` 和 `C2` 已应用标签，并且 `address` 字段已具有 `C1` 已应用标签。 PUT请求覆盖现有标签 `C1, C2` 标签来自 `fullName` 带有以下内容的字段 `C1` 标签使用 `optionalLabels.labels` 参数。 该请求还将覆盖 `C1` 标签来自 `address` 字段标签集为空的字段。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| 参数 | 描述 |
| --- | --- |
| `entityId` | 这将标识要更新的特定数据集实体。 此 `entityId` 必须包括以下三个值：<br/><br/>`namespace`：用于避免ID冲突。 此 `namespace` 是 `AEP`.<br/>`id`：要更新的资源的ID。 此名称是指 `datasetId`.<br/>`type`：正在更新的资源的类型。 这将永远是 `dataset`. |
| `labels` | 要添加到整个数据集的数据使用标签列表。 |
| `parents` | 此 `parents` 数组包含列表 `entityId`此数据集将从中继承标签的内容。 数据集可以从架构和/或数据集继承标签。 |
| `optionalLabels` | 此参数用于移除先前应用于数据集字段的标签。 数据集中要从中删除标签的任何单独字段的列表。 此数组中的每一项都必须具有以下属性： <br/><br/>`option`：包含 [!DNL Experience Data Model] (XDM)字段的属性。 需要以下三个属性：<ul><li><code>id</code>：URI <code>$id</code> 与字段关联的架构的值。</li><li><code>contentType</code>：架构的内容类型和版本号。 这应该采用有效形式之一 <a href="../../xdm/api/getting-started.md#accept">接受标头</a> ，以获取XDM查找请求。</li><li><code>架构路径</code>：数据集架构中字段的路径。</li></ul>`labels`：此值必须包含应用的现有字段标签的子集，或为空以删除所有现有字段标签。 PUT或POST方法现在会返回错误，如果 `optionalLabels` 字段具有任何新标签或修改的标签。 |

**响应**

成功的响应将返回数据集的更新标签集。

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## 后续步骤

通过阅读本文档，您已了解如何使用 [!DNL Dataset Service] API。 您现在可以定义 [数据使用策略](../policies/overview.md) 和 [访问控制策略](../../access-control/abac/ui/policies.md) 基于您应用的标签。

有关管理中数据集的更多信息 [!DNL Experience Platform]，请参见 [数据集概述](../../catalog/datasets/overview.md).
