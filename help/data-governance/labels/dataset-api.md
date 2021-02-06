---
keywords: Experience Platform；主页；热门主题；数据集api；管理数据使用；数据使用api
solution: Experience Platform
title: '使用API管理数据集的数据使用标签 '
topic: developer guide
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的Catalog Service API分开。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---


# 使用API管理数据集的数据使用标签

[[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml)允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的[!DNL Catalog Service] API分开。

此文档介绍如何使用[!DNL Dataset Service API]管理数据集和字段的标签。 有关如何使用API调用管理数据使用标签本身的步骤，请参阅[!DNL Policy Service API]的[标签端点指南](../api/labels.md)。

## 入门指南

在阅读本指南之前，请按照目录开发人员指南中[快速入门部分](../../catalog/api/getting-started.md)中概述的步骤收集所需的凭据以调用[!DNL Platform] API。

要调用此文档中概述的端点，您必须具有特定数据集的唯一`id`值。 如果没有此值，请参阅[列表目录对象](../../catalog/api/list-objects.md)上的指南，以查找现有数据集的ID。

## 查找数据集{#look-up}的标签

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

## 将标签应用于数据集{#apply}

您可以通过将数据集的标签集提供到[!DNL Dataset Service] API的POST或PUT请求的有效负荷中来为数据集创建标签集。 使用以下任一方法将覆盖任何现有标签，并用有效负荷中提供的标签替换它们。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为其创建标签的数据集的唯一`id`值。 |

**请求**

以下PUT请求更新数据集的现有标签以及该数据集中的特定字段。 有效负荷中提供的字段与POST请求所需的字段相同。

>[!IMPORTANT]
>
>向`/datasets/{DATASET_ID}/labels`端点发出PUT请求时，必须提供有效的`If-Match`头。 有关使用所需标题的详细信息，请参见[附录部分](#if-match)。

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
| `labels` | 要添加到数据集的列表数据使用标签。 |
| `optionalLabels` | 列表数据集中要添加标签的任何单个字段。 此数组中的每个项目都必须具有以下属性：<br/><br/>`option`:包含字段[!DNL Experience Data Model](XDM)属性的对象。 以下三个属性是必需的：<ul><li>id</code>:与字段关联的模式的URI $id</code>值。</li><li>contentType</code>:模式的内容类型和版本号。 对于XDM查找请求，应采用有效<a href="../../xdm/api/getting-started.md#accept">接受标头</a>的形式。</li><li>schemaPath</code>:数据集模式中字段的路径。</li></ul>`labels`:要添加到字段的列表数据使用标签。 |

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

## 从数据集{#remove}中删除标签

可以通过向[!DNL Dataset Service] API发出DELETE请求来删除应用于数据集的标签。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要删除其标签的数据集的唯一`id`值。 |

**请求**

以下请求将删除路径中指定的数据集的标签。

>[!IMPORTANT]
>
>向`/datasets/{DATASET_ID}/labels`端点发出DELETE请求时，必须提供有效的`If-Match`头。 有关使用所需标题的详细信息，请参见[附录部分](#if-match)。

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

成功响应HTTP状态200(OK)，表示标签已被删除。 您可以在单独的调用中[查找数据集的现有标签](#look-up)以确认这一点。

## 后续步骤

通过阅读此文档，您学习了如何使用[!DNL Dataset Service] API管理数据集和字段的数据使用标签。

在数据集和字段级别添加数据使用标签后，您可以开始将数据引入[!DNL Experience Platform]。 要了解更多信息，请阅读[开始获取文档](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关详细信息，请参阅[数据使用策略概述](../policies/overview.md)。

有关管理[!DNL Experience Platform]中的数据集的详细信息，请参阅[数据集概述](../../catalog/datasets/overview.md)。

## 附录 {#appendix}

以下部分包含有关使用Dataset Service API处理标签的其他信息。

### [!DNL If-Match] 标题  {#if-match}

在发出更新数据集(PUT和DELETE)现有标签的API调用时，必须包含一个`If-Match`头，指示数据集服务中数据集标签实体的当前版本。 为防止数据冲突，仅当包含的`If-Match`字符串与系统为该数据集生成的最新版本标签相匹配时，服务才会更新数据集实体。

>[!NOTE]
>
>如果当前不存在相关数据集的标签，则只能通过POST请求添加新标签，该请求不需要`If-Match`标头。 将标签添加到数据集后，会分配一个`etag`值，用于在以后更新或删除标签。

要检索dataset-label实体的最新版本，请向`/datasets/{DATASET_ID}/labels`端点发出[GET请求](#look-up)。 当前值在`etag`标头下的响应中返回。 更新现有数据集标签时，最佳做法是首先对数据集执行查找请求，以在后续PUT或DELETE请求的`If-Match`标头中使用最新`etag`值。