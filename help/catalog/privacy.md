---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据湖中的隐私请求处理
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# 数据湖中的隐私请求处理

Adobe Experience Platform Privacy Service处理客户访问、销售或删除其个人数据的请求，这些请求由隐私法规(如《一般数据保护条例》(GDPR)和《加利福尼亚消费者隐私法》(CCPA))规定。

本文档涵盖与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。

## 入门指南

在阅读本指南之前，建议您对以下Experience Platform服务有充分的了解：

* [隐私服务](../privacy-service/home.md):管理客户跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [目录服务](home.md):Experience Platform中用于数据位置和世系的记录系统。 提供可用于更新数据集元数据的API。
* [体验数据模型(XDM)系统](../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。

## 向数据集添加隐私标签 {#privacy-labels}

要在数据湖的隐私请求中处理数据集，必须为数据集提供隐私标签。 隐私标签指示数据集关联模式中的哪些字段适用于您期望在隐私请求中发送的命名空间。

本节演示如何向数据集添加隐私标签以用于Data Lake隐私请求。 首先，请考虑以下数据集：

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

数 `schemaMetadata` 据集的属性包含一个数 `gdpr` 组，该数组当前为空。 要向数据集添加隐私标签，必须使用对 [Catalog Service API的PATCH请求更新此阵列](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

>[!NOTE] 尽管阵列已命名， `gdpr`但向其添加标签将允许GDPR和CCPA规定的隐私作业请求。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要 `id` 更新的数据集的值。 |

**请求**

在此示例中，数据集在字段中包含电子邮件地址 `personalEmail.address` 。 要使此字段用作数据湖隐私请求的标识符，必须使用未注册命名空间的标签添加到其数 `gdpr` 组。

以下请求会添加一个隐私标签，该标签将命名空间“email_label”分配给字 `personalEmail.address` 段。

>[!IMPORTANT] 对数据集的属性运行PATCH操作时，请 `schemaMetadata` 务必复制请求有效负荷内的任何现有子属性。 将任何现有值从有效负荷中排除将导致它们从数据集中删除。

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `namespace` | 列出要与中指定的字段关联的命名空间的数组 `path`。 命名空间用于在隐私服务API中提交访问 [或删除请求时识别与隐私](#submit) 相关的字段。 |
| `path` | 数据集关联模式中适用于该字段的字段路径 `namespace`。 理想情况下，隐私标签仅应用于“叶”字段（没有子字段的字段）。 |

**响应**

成功的响应会返回HTTP状态200(OK)，其ID是在有效负荷中提供的数据集。 使用ID再次查找数据集会显示已添加隐私标签。

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### 标记嵌套的映射类型字段

请注意，有两种嵌套的映射类型字段不支持隐私标签：

* 数组类型字段中的映射类型字段
* 另一个映射类型字段中的映射类型字段

上述两个示例中的任何一个的隐私作业处理最终都将失败。 因此，建议您避免使用嵌套的映射类型字段存储私人客户数据。 相关消费者ID应作为非映射数据类型存储在基于记录的数据集的字段（本身是映射类型字段）或基于时间序列的数据集的 `identityMap``endUserID` 字段中。

## 提交请求 {#submit}

>[!NOTE] 本节介绍如何设置数据湖的隐私请求的格式。 强烈建议您查看 [Privacy Service API](../privacy-service/api/getting-started.md) 或 [Privacy Service UI](../privacy-service/ui/overview.md) 文档，了解有关如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户标识数据的格式。

以下部分概述了如何使用隐私服务API或UI向数据湖发出隐私请求。

### 使用API

在API中创建作业请求时，提供的任 `userIDs` 何作业请求都必须使用特定的，并 `namespace` 且 `type` 取决于它们所应用的数据存储。 数据湖的ID必须使用“未注册”作为其 `type` 值，并且值与已添加到适用数据集的 `namespace` 隐私标签之 [一相](#privacy-labels) 匹配。

此外，请求 `include` 有效负荷的数组必须包括请求所针对的不同数据存储的产品值。 向数据湖发出请求时，数组必须包含值“aepDataLake”。

以下请求使用未注册的“email_label”命名空间为数据湖创建新的隐私作业。 它还包括数组中数据湖的产品 `include` 值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中创建作业请求时，请务必在 **Products下选择** AEP Data Lake **and/or**__ 用户档案，以便分别处理数据湖或实时客户用户档案中存储的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 删除请求处理

当Experience Platform从隐私服务收到删除请求时，平台会向隐私服务发送确认消息，确认该请求已收到且受影响的数据已被标记为删除。 然后在七天内从数据湖中删除记录。 在该七天的窗口期内，数据会被软删除，因此任何平台服务都无法访问。

在将来的版本中，平台将在数据实际删除后向隐私服务发送确认。

## 后续步骤

阅读本文档后，您便了解了处理数据湖隐私请求的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理文档商 [店隐私请求的步骤](../profile/privacy.md) ，请参阅实时客户用户档案的隐私请求处理用户档案。