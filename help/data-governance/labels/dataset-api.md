---
keywords: Experience Platform；主页；热门主题；数据集API；管理数据使用情况；数据使用API
solution: Experience Platform
title: '使用API管理数据集的数据使用标签 '
topic-legacy: developer guide
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 2%

---

# 使用API管理数据集的数据使用标签

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/)允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的[!DNL Catalog Service] API不同。

本文档介绍如何使用[!DNL Dataset Service API]管理数据集和字段的标签。 有关如何使用API调用管理数据使用标签本身的步骤，请参阅[!DNL Policy Service API]的[标签端点指南](../api/labels.md)。

## 快速入门

在阅读本指南之前，请按照目录开发人员指南的[快速入门部分](../../catalog/api/getting-started.md)中概述的步骤，收集所需的凭据以调用[!DNL Platform] API。

要调用本文档中列出的端点，您必须具有特定数据集的唯一`id`值。 如果没有此值，请参阅[listing Catalog objects](../../catalog/api/list-objects.md)指南，以查找现有数据集的ID。

## 查找数据集的标签 {#look-up}

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
| `optionalLabels` | 数据集中已应用数据使用标签的各个字段的列表。 |

## 将标签应用于数据集 {#apply}

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

以下PUT请求会更新数据集的现有标签以及该数据集中的特定字段。 有效负载中提供的字段与POST请求所需的字段相同。

>[!IMPORTANT]
>
>对`/datasets/{DATASET_ID}/labels`端点发出PUT请求时，必须提供有效的`If-Match`标头。 有关使用所需标头的详细信息，请参阅[附录部分](#if-match)。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
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
| `optionalLabels` | 数据集中要向其添加标签的任意单个字段的列表。 此数组中的每个项目都必须具有以下属性：<br/><br/>`option`:包含字段[!DNL Experience Data Model](XDM)属性的对象。 以下三个属性是必需的：<ul><li>id</code>:与字段关联的架构的URI $id</code>值。</li><li>contentType</code>:架构的内容类型和版本号。 这应采用有效的<a href="../../xdm/api/getting-started.md#accept">XDM查找请求的</a>接受标头之一的形式。</li><li>schemaPath</code>:数据集架构中字段的路径。</li></ul>`labels`:要添加到字段的数据使用情况标签的列表。 |

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

您可以通过向[!DNL Dataset Service] API发出DELETE请求，删除应用于数据集的标签。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要删除其标签的数据集的唯一`id`值。 |

**请求**

以下请求会删除路径中指定数据集的标签。

>[!IMPORTANT]
>
>对`/datasets/{DATASET_ID}/labels`端点发出DELETE请求时，必须提供有效的`If-Match`标头。 有关使用所需标头的详细信息，请参阅[附录部分](#if-match)。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**响应**

成功响应HTTP状态200（确定），表示标签已被删除。 您可以在单独的调用中[查找数据集的现有标签](#look-up)以确认这一点。

## 后续步骤

通过阅读本文档，您了解了如何使用[!DNL Dataset Service] API管理数据集和字段的数据使用标签。

在数据集和字段级别添加数据使用标签后，您可以开始将数据摄取到[!DNL Experience Platform]中。 要了解更多信息，请首先阅读[数据摄取文档](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关更多信息，请参阅[数据使用策略概述](../policies/overview.md)。

有关管理[!DNL Experience Platform]中数据集的更多信息，请参阅[数据集概述](../../catalog/datasets/overview.md)。

## 附录 {#appendix}

以下部分包含有关使用数据集服务API处理标签的其他信息。

### [!DNL If-Match] 标题 {#if-match}

在进行API调用以更新数据集(PUT和DELETE)的现有标签时，必须包含`If-Match`标头，指示数据集服务中数据集标签实体的当前版本。 为防止发生数据冲突，仅当包含的`If-Match`字符串与系统为该数据集生成的最新版本标记匹配时，该服务才会更新数据集实体。

>[!NOTE]
>
>如果相关数据集当前不存在标签，则只能通过POST请求添加新标签，该请求不需要`If-Match`标头。 将标签添加到数据集后，会分配一个`etag`值，该值可用于稍后更新或删除标签。

要检索最新版本的dataset-label实体，请向`/datasets/{DATASET_ID}/labels`端点发出[GET请求](#look-up)。 在响应中`etag`标头下返回当前值。 在更新现有数据集标签时，最佳做法是首先对数据集执行查询请求，以获取其最新的`etag`值，然后再在后续PUT或DELETE请求的`If-Match`标头中使用该值。
