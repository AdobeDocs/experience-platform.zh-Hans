---
keywords: Experience Platform；主页；热门主题；数据集api；管理数据使用情况；数据使用情况api
solution: Experience Platform
title: 使用API管理数据集的数据使用标签
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

---

# 使用API管理数据集的数据使用标签

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/)允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的[!DNL Catalog Service] API不同。

>[!IMPORTANT]
>
>仅数据管理用例支持在数据集级别应用标签。 如果尝试创建数据的访问策略，则必须[将标签应用于数据集所基于的架构](../../xdm/tutorials/labels.md)。 有关详细信息，请参阅[基于属性的访问控制](../../access-control/abac/overview.md)的概述。

本文档介绍如何使用[!DNL Dataset Service API]管理数据集和字段的标签。 有关如何使用API调用管理数据使用标签本身的步骤，请参阅[!DNL Policy Service API]的[标签端点指南](../api/labels.md)。

## 快速入门

在阅读本指南之前，请按照《目录开发人员指南》的[入门部分](../../catalog/api/getting-started.md)中所述的步骤来收集调用[!DNL Experience Platform] API所需的凭据。

要调用本文档中概述的端点，您必须具有特定数据集的唯一`id`值。 如果没有此值，请参阅[列出目录对象](../../catalog/api/list-objects.md)上的指南以查找现有数据集的ID。

## 查找数据集的标签 {#look-up}

您可以通过向[!DNL Dataset Service] API发出GET请求，查找已应用于现有数据集的数据使用标签。

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

通过在POST或PUT请求的有效负荷中向[!DNL Dataset Service] API提供一组标签，您可以将一组标签应用于整个数据集。 两个调用的请求正文相同。 您无法将标签添加到单独的数据集字段。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 您为其创建标签的数据集的唯一`id`值。 |

**请求**

下面的示例POST请求使用`C1`标签更新整个数据集。 有效负载中提供的字段与PUT请求所需的字段相同。

当进行更新数据集(PUT)的现有标签的API调用时，必须包括一个`If-Match`标头，以指示数据集服务中数据集标签实体的当前版本。 为避免数据冲突，仅当包含的`If-Match`字符串与系统为该数据集生成的最新版本标记匹配时，服务才会更新数据集实体。

>[!NOTE]
>
>如果相关数据集当前存在标签，则只能通过PUT请求添加新标签，该请求需要`If-Match`标头。 将标签添加到数据集后，以后需要最新的`etag`值来更新或删除标签<br>在执行PUT方法之前，必须对数据集标签执行GET请求。 确保仅更新请求中要修改的特定字段，而其余字段保持不变。 此外，确保PUT调用维护与GET调用相同的父实体。 任何差异都会导致客户出错。

要检索最新版本的dataset-label实体，请向`/datasets/{DATASET_ID}/labels`端点发出[GET请求](#look-up)。 当前值在`etag`标头下的响应中返回。 更新现有数据集标签时，最佳实践是先对数据集执行查找请求，以获取其最新的`etag`值，然后再在后续PUT请求的`If-Match`标头中使用该值。

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
        "parents": []
      } '
```

| 属性 | 描述 |
| --- | --- |
| `entityId` | 这将标识要更新的特定数据集实体。 |
| `entityId.namespace` | 用于避免ID冲突。 `namespace`是`AEP`。 |
| `entityId.id` | 要更新的资源的ID。 这是对`datasetId`的引用。 |
| `entityId.type` | 正在更新的资源的类型。 这将始终为`dataset`。 |
| `labels` | 要添加到整个数据集的数据使用标签列表。 |
| `parents` | `parents`数组包含此数据集将继承其标签的`entityId`的列表。 数据集可以从架构和/或数据集继承标签。 |

**响应**

成功的响应将返回数据集的更新标签集。

>[!IMPORTANT]
>
>`optionalLabels`属性已弃用以便与POST请求一起使用。 无法再将数据标签添加到数据集字段。 如果存在`optionalLabel`值，则POST操作将引发错误。 但是，您可以使用PUT请求和`optionalLabels`属性从各个字段删除标签。 有关详细信息，请参阅[从数据集](#remove)中删除标签一节。

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

您可以通过更新具有现有字段标签子集的现有`optionalLabels`值，或通过使用空列表完全删除它们，来删除任何以前应用的字段标签。 向[!DNL Dataset Service] API发出PUT请求以更新或删除以前应用的标签。

>[!NOTE]
>
>通过为`labels`参数提供空列表，可以完全删除数据集的标签。 数据集不必保留任何标签。

**API格式**

```http
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 您为其创建标签的数据集的唯一`id`值。 |

**请求**

应用PUT操作的以下数据集的properties/person/properties/address字段上具有C1 optionalLabel，而/properties/person/properties/name/properties/fullName字段上具有C1， C2 optionalLabels。 在put操作之后，第一字段将没有标签（C1标签被删除），而第二字段将只有C1标签（C2标签被删除）

在以下示例场景中，PUT请求用于删除添加到各个字段的标签。 在发出请求之前，`fullName`字段已应用`C1`和`C2`标签，并且`address`字段已应用`C1`标签。 PUT请求使用`optionalLabels.labels`参数覆盖具有`C1`标签的`fullName`字段中的现有标签`C1, C2`标签。 该请求还会使用一组空的字段标签覆盖`address`字段中的`C1`标签。

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
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
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
| `entityId` | 这将标识要更新的特定数据集实体。 `entityId`必须包括以下三个值：<br/><br/>`namespace`：用于避免ID冲突。 `namespace`是`AEP`。<br/>`id`：正在更新的资源的ID。 这是对`datasetId`的引用。<br/>`type`：正在更新的资源的类型。 这将始终为`dataset`。 |
| `labels` | 要添加到整个数据集的数据使用标签列表。 |
| `parents` | `parents`数组包含此数据集将继承其标签的`entityId`的列表。 数据集可以从架构和/或数据集继承标签。 |
| `optionalLabels` | 此参数用于移除先前应用于数据集字段的标签。 数据集中要从中删除标签的任何单独字段的列表。 此数组中的每个项都必须具有以下属性： <br/><br/>`option`：包含字段的[!DNL Experience Data Model] (XDM)属性的对象。 需要以下三个属性：<ul><li><code>id</code>： URI <code>$id</code> 与字段关联的架构的值。</li><li><code>内容类型</code>：架构的内容类型和版本号。 这应该采用XDM查找请求的有效<a href="../../xdm/api/getting-started.md#accept">接受标头</a>的形式。</li><li><code>架构路径</code>：数据集架构中字段的路径。</li></ul>`labels`：此值必须包含应用的现有字段标签的子集，或者为空以删除所有现有字段标签。 如果`optionalLabels`字段具有任何新标签或修改的标签，则PUT或POST方法现在会返回错误。 |

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

通过阅读本文档，您已了解如何使用[!DNL Dataset Service] API管理数据集和字段的数据使用标签。 您现在可以根据已应用的标签定义[数据使用策略](../policies/overview.md)和[访问控制策略](../../access-control/abac/ui/policies.md)。

有关管理[!DNL Experience Platform]中数据集的详细信息，请参阅[数据集概述](../../catalog/datasets/overview.md)。
