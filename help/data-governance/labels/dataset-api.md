---
keywords: Experience Platform；主页；热门主题；数据集API；管理数据使用情况；数据使用API
solution: Experience Platform
title: 使用API管理数据集的数据使用标签
description: 数据集服务API允许您应用和编辑数据集的使用标签。 它是Adobe Experience Platform数据目录功能的一部分，但与管理数据集元数据的目录服务API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 1%

---

# 使用API管理数据集的数据使用标签

的 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 允许您应用和编辑数据集的使用情况标签。 它是Adobe Experience Platform数据目录功能的一部分，但与 [!DNL Catalog Service] 管理数据集元数据的API。

>[!IMPORTANT]
>
>仅支持在数据集级别应用标签用于数据管理用例。 如果您尝试为数据创建访问策略，则必须 [将标签应用到架构](../../xdm/tutorials/labels.md) 数据集所基于的信息。 请参阅 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解更多信息。

本文档介绍如何使用 [!DNL Dataset Service API]. 有关如何使用API调用管理数据使用情况标签本身的步骤，请参阅 [标签端点指南](../api/labels.md) 对于 [!DNL Policy Service API].

## 快速入门

在阅读本指南之前，请先执行 [入门部分](../../catalog/api/getting-started.md) ，以收集所需的凭据来调用 [!DNL Platform] API。

要调用本文档中概述的端点，您必须具有 `id` 值。 如果没有此值，请参阅 [列出目录对象](../../catalog/api/list-objects.md) 以查找现有数据集的ID。

## 查找数据集的标签 {#look-up}

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
| `optionalLabels` | 数据集中已应用数据使用标签的各个字段的列表。 |

## 将标签应用于数据集 {#apply}

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

以下示例PUT请求更新了数据集的现有标签以及该数据集中的特定字段。 有效负载中提供的字段与POST请求所需的字段相同。

在进行API调用以更新数据集(PUT)的现有标签时， `If-Match` 表示数据集服务中必须包含数据集标签实体的当前版本的标头。 为防止发生数据冲突，该服务仅在包含的 `If-Match` 字符串匹配由系统为该数据集生成的最新版本标记。

>[!NOTE]
>
>如果相关数据集当前不存在标签，则只能通过POST请求添加新标签，该请求不需要 `If-Match` 标题。 将标签添加到数据集后， `etag` 值已分配，可用于稍后更新或删除标签。

要检索数据集标签实体的最新版本，请 [GET请求](#look-up) 到 `/datasets/{DATASET_ID}/labels` 端点。 在响应中的 `etag` 标题。 更新现有数据集标签时，最佳做法是首先对数据集执行查找请求，以获取其最新版本 `etag` 值，然后在 `If-Match` 后续PUT请求的标头。

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
| `optionalLabels` | 数据集中要向其添加标签的任意单个字段的列表。 此数组中的每个项目都必须具有以下属性： <br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)字段的属性。 以下三个属性是必需的：<ul><li>id</code>:URI $id</code> 与字段关联的架构的值。</li><li>contentType</code>:架构的内容类型和版本号。 这应采用有效 <a href="../../xdm/api/getting-started.md#accept">接受标头</a> 的XDM查询请求。</li><li>schemaPath</code>:数据集架构中字段的路径。</li></ul>`labels`:要添加到字段的数据使用情况标签的列表。 |

**响应**

成功的响应会返回数据集的更新标签集。

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

## 后续步骤

通过阅读本文档，您了解了如何使用 [!DNL Dataset Service] API。 您现在可以定义 [数据使用策略](../policies/overview.md) 和 [访问控制策略](../../access-control/abac/ui/policies.md) 基于您应用的标签。

有关管理 [!DNL Experience Platform]，请参阅 [数据集概述](../../catalog/datasets/overview.md).
