---
title: 受众API端点
description: 使用Adobe Experience Platform分段服务API中的受众端点，以编程方式创建、管理和更新贵组织的受众。
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 3%

---

# 受众端点

受众是指具有相似行为和/或特征的人群。 这些人员集合可以通过使用Adobe Experience Platform或从外部源生成。 您可以使用 `/audiences` 分段API中的端点，允许您以编程方式检索、创建、更新和删除受众。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索受众列表 {#list}

您可以通过向以下网站发出GET请求，检索贵组织所有受众的列表： `/audiences` 端点。

**API格式**

此 `/audiences` 端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数，以帮助在列出资源时减少昂贵的开销。 如果您在不使用参数的情况下调用此端点，则将检索对您的组织可用的所有受众。 可以包含多个参数，以&amp;分隔(`&`)。

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

在检索受众列表时，可以使用以下查询参数：

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `start` | 指定返回受众的起始偏移。 | `start=5` |
| `limit` | 指定每页返回的最大受众数。 | `limit=10` |
| `sort` | 指定排序结果的顺序。 这是以格式编写的 `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | 允许您指定受众的过滤器 **完全匹配** 匹配属性的值。 这是以格式编写的 `property=` | `property=audienceId==test-audience-id` |
| `name` | 允许您指定其名称的受众的过滤器 **contain** 提供的值。 此值不区分大小写。 | `name=Sample` |
| `description` | 允许您指定其描述的受众的过滤器 **contain** 提供的值。 此值不区分大小写。 | `description=Test Description` |

**请求**

以下请求将检索在您的组织中创建的最后两个受众。

+++用于检索受众列表的示例请求。

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含您的组织中创建为JSON的受众列表。

+++一个示例响应，其中包含最后两个创建的属于您组织的受众

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| 属性 | 受众类型 | 描述 |
| -------- | ------------- | ----------- | 
| `id` | 两者 | 系统生成的受众只读标识符。 |
| `audienceId` | 两者 | 如果受众是平台生成的受众，则此值与 `id`. 如果受众是外部生成的，则此值由客户端提供。 |
| `schema` | 两者 | 受众的体验数据模型(XDM)架构。 |
| `imsOrgId` | 两者 | 受众所属的组织的ID。 |
| `sandbox` | 两者 | 有关受众所属的沙盒的信息。 有关沙箱的详细信息，请参阅 [沙盒概述](../../sandboxes/home.md). |
| `name` | 两者 | 受众的名称。 |
| `description` | 两者 | 受众的描述。 |
| `expression` | 平台生成 | 受众的个人资料查询语言(PQL)表达式。 有关PQL表达式的更多信息，请参见 [PQL表达式指南](../pql/overview.md). |
| `mergePolicyId` | 平台生成 | 受众关联的合并策略的ID。 有关合并策略的更多信息，请参阅 [合并策略指南](../../profile/api/merge-policies.md). |
| `evaluationInfo` | 平台生成 | 显示评估受众的方式。 可能的评估方法包括批处理、同步（流）或连续（边缘）。 有关评估方法的更多信息，请参阅 [分段概述](../home.md) |
| `dependents` | 两者 | 依赖于当前受众的受众ID数组。 如果您创建的受众是区段的区段，则会使用此字段。 |
| `dependencies` | 两者 | 受众所依赖的受众ID数组。 如果您创建的受众是区段的区段，则会使用此字段。 |
| `type` | 两者 | 一个系统生成的字段，用于显示受众是平台生成的还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中生成的受众，而 `ExternalSegment` 引用了未在Platform中生成的受众。 |
| `originName` | 两者 | 引用受众来源名称的字段。 对于平台生成的受众，此值将为 `REAL_TIME_CUSTOMER_PROFILE`. 对于在Audience Orchestration中生成的受众，此值将为 `AUDIENCE_ORCHESTRATION`. 对于在Adobe Audience Manager中生成的受众，此值将为 `AUDIENCE_MANAGER`. 对于其他外部生成的受众，此值将为 `CUSTOM_UPLOAD`. |
| `createdBy` | 两者 | 创建受众的用户的ID。 |
| `labels` | 两者 | 与受众相关的对象级别数据使用和基于属性的访问控制标签。 |
| `namespace` | 两者 | 受众所属的命名空间。 可能的值包括 `AAM`， `AAMSegments`， `AAMTraits`、和 `AEPSegments`. |
| `linkedAudienceRef` | 两者 | 包含其他受众相关系统标识符的对象。 |

+++

## 创建新受众 {#create}

您可以通过向以下对象发出POST请求来创建新受众： `/audiences` 端点。

**API格式**

```http
POST /audiences
```

**请求**

>[!BEGINTABS]

>[!TAB 平台生成的受众]

+++ 用于创建平台生成受众的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ],
        "ttlInDays": 60
    }'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `name` | 受众的名称。 |
| `description` | 受众的描述。 |
| `type` | 一个字段，用于显示受众是平台生成的受众还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中生成的受众，而 `ExternalSegment` 引用了未在Platform中生成的受众。 |
| `expression` | 受众的个人资料查询语言(PQL)表达式。 有关PQL表达式的更多信息，请参见 [PQL表达式指南](../pql/overview.md). |
| `schema` | 受众的体验数据模型(XDM)架构。 |
| `labels` | 与受众相关的对象级别数据使用和基于属性的访问控制标签。 |
| `ttlInDays` | 表示受众的数据过期值（以天为单位）。 |

+++

>[!TAB 外部生成的受众]

+++ 用于创建外部生成受众的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "audienceId":"test-external-audience-id",
        "name":"externalAudience",
        "namespace":"aam",
        "description":"Last 30 days",
        "type":"ExternalSegment",
        "originName":"CUSTOM_UPLOAD",
        "lifecycleState":"published",
        "datasetId":"6254cf3c97f8e31b639fb14d",
        "labels":[
            "core/C1"
        ],
        "linkedAudienceRef":{
            "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `audienceId` | 用户为受众提供的ID。 |
| `name` | 受众的名称。 |
| `namespace` | 受众的命名空间。 |
| `description` | 受众的描述。 |
| `type` | 一个字段，用于显示受众是平台生成的受众还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中生成的受众，而 `ExternalSegment` 引用了未在Platform中生成的受众。 |
| `originName` | 受众来源的名称。 对于外部生成的受众，此参数的默认值为 `CUSTOM_UPLOAD`. 其他支持的值包括 `REAL_TIME_CUSTOMER_PROFILE`， `CUSTOM_UPLOAD`， `AUDIENCE_ORCHESTRATION`、和 `AUDIENCE_MATCH`. |
| `lifecycleState` | 一个可选字段，可确定您尝试创建的受众的初始状态。 支持的值包括 `draft`， `published`、和 `inactive`. |
| `datasetId` | 可在其中找到包含受众的数据的数据集的ID。 |
| `labels` | 与受众相关的对象级别数据使用和基于属性的访问控制标签。 |
| `audienceMeta` | 属于外部生成的受众的元数据。 |
| `linkedAudienceRef` | 包含其他受众相关系统标识符的对象。 这可能包括以下内容： <ul><li>`flowId`：此ID用于将受众连接到用于引入受众数据的数据流。 有关所需ID的更多信息，请参阅 [创建数据流指南](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`：此ID用于将受众连接到相关的Audience Orchestration合成。&lt;/li/> <li>`payloadFieldGroupRef`：此ID用于引用描述受众结构的XDM字段组架构。 有关此字段值的更多信息，请参见 [XDM字段组端点指南](../../xdm/api/field-groups.md).</li><li>`audienceFolderId`：此ID用于引用Adobe Audience Manager中受众的文件夹ID。 有关此API的更多信息，请参阅 [Adobe Audience Manager API指南](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API).</ul> |

+++

>[!ENDTABS]

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的受众的信息。

>[!BEGINTABS]

>[!TAB 平台生成的受众]

+++创建平台生成的受众时的示例响应。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB 外部生成的受众]

+++创建外部生成的受众时的示例响应。

```json
{
   "id": "322f9f62-cd27-11ec-9d64-0242ac120002",
   "audienceId": "test-external-audience-id",
   "name": "externalAudience",
   "namespace": "aam",
   "imsOrgId": "{ORG_ID}",
   "sandbox":{
      "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
      "sandboxName": "prod",
      "type": "production",
      "default": true
   },
   "isSystem": false,
   "description": "Last 30 days",
   "type": "ExternalSegment",
   "originName": "CUSTOM_UPLOAD",
   "lifecycleState": "published",
   "createdBy": "{CREATED_BY_ID}",
   "datasetId": "6254cf3c97f8e31b639fb14d",
   "labels": [
      "core/C1"
   ],
   "linkedAudienceRef": {
      "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
   },
   "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
   "creationTime": 1650251290000,
   "updateEpoch": 1650251290,
   "updateTime": 1650251290000,
   "createEpoch": 1650251290
}
```

+++

## 查找指定受众 {#get}

您可以通过对以下网站发出GET请求，查找有关特定受众的详细信息 `/audiences` 端点，并提供您希望在请求路径中检索的受众ID。

**API格式**

```http
GET /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | 您尝试检索的受众ID。 请注意，这是 `id` 字段，并且是 **非** 该 `audienceId` 字段。 |

**请求**

+++用于检索受众的示例请求

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关指定受众的信息。 响应将因受众是使用Adobe Experience Platform还是外部源生成而异。

>[!BEGINTABS]

>[!TAB 平台生成的受众]

+++检索平台生成的受众时的示例响应。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB 外部生成的受众]

+++检索外部生成的受众时的示例响应。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "test-external-audience-id",
    "name": "externalAudience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

>[!ENDTABS]

## 更新受众中的字段 {#update-field}

您可以通过向以下对象发出PATCH请求来更新特定受众的字段： `/audiences` 端点并在请求路径中提供要更新的受众ID。

**API格式**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要更新的受众的ID。 请注意，这是 `id` 字段，并且是 **非** 该 `audienceId` 字段。 |

**请求**

+++更新受众中字段的示例请求。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 对于更新受众，此值始终为 `add`. |
| `path` | 要更新的字段的路径。 |
| `value` | 您希望更新字段的值。 |

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关新更新的受众的信息。

+++更新受众中的字段时的示例响应。

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## 更新受众 {#put}

您可以通过向以下对象发出PUT请求来更新（覆盖）特定受众： `/audiences` 端点并在请求路径中提供要更新的受众ID。

**API格式**

```http
PUT /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要更新的受众的ID。 请注意，这是 `id` 字段，并且是 **非** 该 `audienceId` 字段。 |

**请求**

+++更新整个受众的示例请求。

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| 属性 | 描述 |
| -------- | ----------- | 
| `audienceId` | 受众的ID。 对于外部生成的受众，此值可由用户提供。 |
| `name` | 受众的名称。 |
| `namespace` | 受众的命名空间。 |
| `description` | 受众的描述。 |
| `type` | 一个系统生成的字段，用于显示受众是平台生成的还是外部生成的受众。 可能的值包括 `SegmentDefinition` 和 `ExternalSegment`. A `SegmentDefinition` 指在Platform中生成的受众，而 `ExternalSegment` 引用了未在Platform中生成的受众。 |
| `lifecycleState` | 受众的状态。 可能的值包括 `draft`， `published`、和 `inactive`. `draft` 表示创建受众的时间， `published` 发布受众的时间，以及 `inactive` 受众不再处于活动状态时。 |
| `datasetId` | 可找到受众数据的数据集的ID。 |
| `labels` | 与受众相关的对象级别数据使用和基于属性的访问控制标签。 |

+++

**响应**

成功的响应返回HTTP状态200以及新更新受众的详细信息。 请注意，您的受众详细信息将有所不同，具体取决于它是平台生成的受众还是外部生成的受众。

+++更新整个受众时的示例响应。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## 删除受众 {#delete}

您可以通过向以下对象发出DELETE请求来删除特定受众： `/audiences` 端点并在请求路径中提供要删除的受众ID。

**API格式**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{AUDIENCE_ID}` | 要删除的受众ID。 请注意，这是 `id` 字段，并且是 **非** 该 `audienceId` 字段。 |

**请求**

+++ 删除受众的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态204，但不返回消息。

## 检索多个受众 {#bulk-get}

您可以通过向以下网站发出POST请求来检索多个受众： `/audiences/bulk-get` 端点，并提供要检索的受众的ID。

**API格式**

```http
POST /audiences/bulk-get
```

**请求**

+++ 用于检索多个受众的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**响应**

成功的响应会返回HTTP状态207，其中包含您请求的受众的信息。

+++ 检索多个受众时的示例响应。

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "ttlInDays": 30,
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## 后续步骤

阅读本指南后，您现在可以更好地了解如何使用Adobe Experience Platform API创建、管理和删除受众。 有关使用UI进行受众管理的更多信息，请参阅 [分段UI指南](../ui/overview.md).
