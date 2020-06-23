---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 评估区段
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 1%

---


# 评估和访问区段结果

本文档提供了一个教程，用于使用分段API评估区段和访问 [区段结果](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

## 入门指南

本教程需要对创建Adobe Experience Platform段时涉及的各种受众服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [实时客户用户档案](../../profile/home.md): 根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [Adobe Experience Platform分段服务](../home.md): 允许您根据实时受众数据构建用户档案细分。
- [体验数据模型(XDM)](../../xdm/home.md): Platform组织客户体验数据的标准化框架。
- [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

### 所需的标题

本教程还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用PlatformAPI。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对PlatformAPI的请求需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关Platform中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有POST、PUT和PATCH请求都需要额外的标头：

- 内容类型： application/json

## 评估区段

开发、测试和保存区段定义后，您便可以通过计划评估或按需评估来评估区段。

[计划评估](#scheduled-evaluation) （也称为“计划细分”）允许您创建在特定时间运行导出作业的循环计划，而 [点播评估](#on-demand-evaluation) （按需评估）涉及创建区段作业以立即构建受众。 下面列出了每个步骤。

如果您尚未使用实时 [客户用户档案API教程创建区段](./create-a-segment.md) ，或者使用区段生成器创建 [了区段定义](../ui/overview.md)，请在继续本教程前执行此操作。

## 计划评估 {#scheduled-evaulation}

通过计划的评估，您的IMS组织可以创建循环计划以自动运行导出作业。

>[!NOTE] 对于XDM单个用户档案，最多可以为五(5)个合并策略的沙箱启用计划评估。 如果您的组织在单个沙箱用户档案内有五个以上的XDM单个环境的合并策略，您将无法使用计划的评估。

### 创建计划

通过向端点发出POST请 `/config/schedules` 求，您可以创建计划并包含应触发计划的特定时间。

**API格式**

```http
POST /config/schedules
```

**请求**

以下请求根据有效负荷中提供的规范创建新计划。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | **(必需** )计划名称。 必须是字符串。 |
| `type` | **（必需）** 字符串格式的作业类型。 支持的类型有 `batch_segmentation` 和 `export`。 |
| `properties` | **(必需** )包含与计划相关的其他属性的对象。 |
| `properties.segments` | **(等于时需`type`要)`batch_segmentation`使用** , `["*"]` 确保包括所有区段。 |
| `schedule` | **（必需）** 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着在24小时内不能将作业计划为多次运行。 显示的示例(`0 0 1 * * ?`)表示作业每天在1:00:00 UTC时触发。 有关详细信息，请查阅 [cron表达式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 文档。 |
| `state` | *（可选）包含计划状态的字符串* 。 可用值： `active` 和 `inactive`。 默认值为 `inactive`。IMS组织只能创建一个计划。 更新计划的步骤将在本教程的稍后部分提供。 |

**响应**

成功的响应会返回新创建计划的详细信息。

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### 启用计划

默认情况下，创建计划时处于非活动状态，除 `state` 非属性设置 `active` 为创建(POST)请求主体中。 您可以通过向端点发出PATCH请求并在路 `state` 径中包 `active``/config/schedules` 含计划的ID来启用计划（将设置为）。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使 [用JSON修补程](http://jsonpatch.com/) 序格式，以将 `state` 计划更新为 `active`。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**响应**

成功的更新返回空的响应正文和HTTP状态204（无内容）。

同一操作可用于禁用计划，方法是将上一个请求中的“值”替换为“非活动”。

### 更新计划时间

计划定时可以通过向端点发出PATCH请求并 `/config/schedules` 在路径中包含计划的ID来更新。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使 [用JSON修补程](http://jsonpatch.com/) 序格式以更 [新计划](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 的cron表达式。 在此示例中，计划现在将在UTC 10:15:00触发。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**响应**

成功的更新返回空的响应正文和HTTP状态204（无内容）。

## 按需评估

按需评估允许您创建区段作业，以便根据需要生成受众区段。 与计划评估不同，仅当请求时才会发生，且不再重复。

### 创建区段作业

段作业是创建新受众段的异步进程。 它引用细分定义以及任何合并策略，控制实时客户用户档案如何合并用户档案片段中重叠的属性。 当区段作业成功完成时，您可以收集有关区段的各种信息，如处理过程中可能发生的任何错误以及受众的最终大小。

您可以通过在实时客户用户档案API中向终 `/segment/jobs` 结点发出POST请求来创建新细分作业。

**API格式**

```http
POST /segment/jobs
```

**请求**

以下请求根据有效负荷中提供的两个区段定义创建新区段作业。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentId` | 要从中构建受众的区段定义的标识符。 负载阵列中必须至少提供一个段ID。 |

**响应**

成功的响应会返回新创建的区段作业的详细信息， `id`包括该区段作业的只读、系统生成的值，该值是此区段作业特有的。

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 用于查找目的的新段作业的标识符。 |
| `status` | 区段作业的当前状态。 在处理完成之前，将为“PROCESSING”（处理），此时它将变为“SUCCEEDED”（成功）或“FAILED”（失败）。 |

### 查找区段作业状态

您可以使用 `id` 特定段作业的查找请求(GET)来视图作业的当前状态。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | 要访 `id` 问的区段作业的值。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回分段作业的详细信息，并根据作业的当前状态提供不同的信息。 您可以重复查找请求，直 `status` 到达“SUCCEEDED”（成功），此时可以将区段导出到数据集。


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentedProfileCounter` | 符合该区段资格的合并用户档案总数。 |
| `segmentedProfileByNamespaceCounter` | 按身份用户档案代码细分符合区段条件的命名空间。 身份命名空间代码的列表可在身份命名空间概 [述中找到](../../identity-service/namespaces.md)。 |

## 解释区段结果

成功运行区段作业时，将 `segmentMembership` 更新区段中包含的每个用户档案的映射。 `segmentMembership` 还存储任何被引入Platform的预评估受众细分，允许与Adobe Audience Manager等其他解决方案集成。

以下示例显示了各个 `segmentMembership` 用户档案记录的属性的外观：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `lastQualificationTime` | 断言区段成员身份和用户档案进入或退出区段的时间戳。 |
| `status` | 作为当前请求一部分的区段参与状态。 必须等于以下已知值之一： <ul><li>`existing`: 实体继续在分部中。</li><li>`realized`: 实体正在输入区段。</li><li>`exited`: 实体正在退出区段。</li></ul> |

## 访问区段结果

区段作业的结果可通过以下两种方式之一进行访问： 您可以访问单个用户档案或将整个受众导出到数据集。

以下各节将更详细地介绍这些选项。

## 查找用户档案

如果您知道要访问的特定用户档案，则可以使用实时客户用户档案API进行访问。 使用用户档案API教程访问实时客户 [用户档案数据中提供了访问各个用户档案的完整步骤](../../profile/api/entities.md) 。

## 导出区段 {#export}

分段作业成功完成后(属性的 `status` 值为“SUCCEEDED”)，您可以将受众导出到数据集，在该数据集中可以访问并执行操作。

导出受众需要执行以下步骤：

- [创建目标数据集](#create-a-target-dataset) -创建数据集以容纳受众成员。
- [在数据集中生成受众用户档案](#generate-profiles-for-audience-members) -根据区段作业的结果，用XDM单个用户档案填充数据集。
- [监视导出进度](#monitor-export-progress) -检查导出过程的当前进度。
- [读取受众](#next-steps) -检索表示受众成员的结果XDM单个用户档案。

### 创建目标数据集

导出受众时，必须先创建目标数据集。 必须正确配置数据集以确保导出成功。

一个主要考虑事项是数据集所基于的模式(在`schemaRef.id` 下面的API示例请求中)。 要导出区段，数据集必须基于XDM个人用户档案合并模式(`https://ns.adobe.com/xdm/context/profile__union`)。 合并模式是系统生成的只读模式，它聚合共享同一类的模式的字段，在本例中为XDM个人用户档案类。 有关合并视图模式的更多信息，请参 [阅模式注册开发人员指南的实时客户用户档案部分](../../xdm/api/getting-started.md)。

有两种方法可创建必需的数据集：

- **使用API:** 本教程中遵循的步骤概述了如何使用目录API创建引用XDM单个用户档案合并模式的数据集。
- **使用UI:** 要使用Adobe Experience Platform用户界面创建引用合并模式的数据集，请按照 [UI教程中的步骤](../ui/overview.md) ，然后返回本教程，继续执行生成 [受众用户档案的步骤](#generate-xdm-profiles-for-audience-members)。

如果您已经有一个兼容数据集并且知道其ID，则可以直接继续执行生成受众 [用户档案的步骤](#generate-xdm-profiles-for-audience-members)。

**API格式**

```http
POST /dataSets
```

**请求**

以下请求将创建新数据集，在有效负荷中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 数据集的描述性名称。 |
| `schemaRef.id` | 合并集将与之关联的视图(模式)的ID。 |
| `fileDescription.persisted` | 一个布尔值，当设置为 `true`时，它使数据集在合并视图中保持。 |

**响应**

成功的响应会返回一个数组，其中包含新创建数据集的只读、系统生成的唯一ID。 要成功导出受众成员，需要正确配置的数据集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 为用户档案成员生成受众

一旦有合并持久数据集，您可以创建一个导出作业，通过在实时用户档案API中向端点发出POST请求并提供要导出的区段的数据集ID和区段信息，将受众成员保留到数据集。 `/export/jobs`

**API格式**

```http
POST /export/jobs
```

**请求**

以下请求将创建新的导出作业，在有效负荷中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `fields` | *（可选）* 将要包含在导出中的数据字段限制为仅包含在此参数中的字段。 创建区段时也可以使用相同的参数，因此区段中的字段可能已过滤。 忽略此值将导致导出数据中包含所有字段 |
| `mergePolicy` | *（可选）* 指定用于管理导出数据的合并策略。 当导出多个段时，请包含此参数。 忽略此值将导致导出服务使用段提供的合并策略。 |
| `mergePolicy.id` | 合并策略的ID |
| `mergePolicy.version` | 要使用的合并策略的特定版本。 忽略此值将默认为最新版本。 |
| `filter` | *（可选）* 指定在导出前应用于区段的以下一个或多个过滤器: |
| `filter.segments` | *（可选）* 指定要导出的段。 忽略此值将导致导出所有用户档案的所有数据。 接受段对象的数组，每个对象都包含以下字段： |
| `filter.segments.segmentId` | **(使用时需`segments`要** )要导出的用户档案的段ID。 |
| `filter.segments.segmentNs` | *(可选* )给定的区段命名空间 `segmentID`。 |
| `filter.segments.status` | *（可选）* 提供状态过滤器的字符串数组 `segmentID`。 默认情 `status` 况下，该 `["realized", "existing"]` 值将表示当前时间属于区段的所有用户档案。 可能的值包括： `"realized"`、 `"existing"`和 `"exited"`。 |
| `filter.segmentQualificationTime` | *（可选）根据* “区段限定时间”进行筛选。 可以提供开始时间和／或结束时间。 |
| `filter.segmentQualificationTime.startTime` | *（可选）* ，给定状态的区段ID的区段资格开始时间。 它未提供，将不会对区段ID资格的开始时间进行筛选。 时间戳必须以RFC 3339 [格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.segmentQualificationTime.endTime` | *（可选）* ，给定状态的区段ID的区段资格结束时间。 它未提供，在区段ID资格的结束时间上将没有过滤器。 时间戳必须以RFC 3339 [格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp` | *（可选）* 将导出的用户档案限制为仅包括在此时间戳后更新的那些。 时间戳必须以RFC 3339 [格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp` **用户档案**，如果提供 | 包括所有合并用户档案，其中合并的更新时间戳大于给定时间戳。 支持操 `greater_than` 作数。 |
| `filter.fromTimestamp` 针对事件 | 在此时间戳之后摄取的所有事件都将与生成的用户档案结果相对应地导出。 这不是事件本身，而是事件的摄取时间。 |
| `filter.emptyProfiles` | *（可选）* Boolean。 用户档案可以包含用户档案记录和／或ExperienceEvent记录。 没有用户档案记录且只有ExperienceEvent记录的用户档案称为“emptyProfiles”。 要导出用户档案商店中的所有用户档案（包括“emptyProfiles”），请将值 `emptyProfiles` 设置为 `true`。 如果 `emptyProfiles` 设置为 `false`，则只会导出存储中具有用户档案记录的用户档案。 默认情况下，如 `emptyProfiles` 果不包括属性，则只导出包含用户档案记录的用户档案。 |
| `additionalFields.eventList` | *（可选）通过* 提供以下一个或多个设置，控制为子对象或关联对象导出的时间序列事件字段： |
| `additionalFields.eventList.fields` | 控制要导出的字段。 |
| `additionalFields.eventList.filter` | 指定限制关联对象中包含的结果的条件。 需要导出所需的最小值，通常为日期。 |
| `additionalFields.eventList.filter.fromIngestTimestamp` | 过滤器时间序列事件到在提供的时间戳后已收录的时间序列。 这不是事件本身，而是事件的摄取时间。 |
| `destination` | **（必需）导出** 数据的目标信息 |
| `destination.datasetId` | **(必需** )要导出数据的数据集的ID。 |
| `destination.segmentPerBatch` | *(可选* )布尔值，如果未提供，则默认为 `false`。 值将所 `false` 有段ID导出为单个批ID。 值将一个 `true` 段ID导出为一个批ID。 请注意，将值设置为可能 `true` 会影响批量导出性能。 |
| `schema.name` | **(必需** )与要导出数据的数据集关联的模式的名称。 |

**响应**

成功的响应会返回一个数据集，其中填充的用户档案符符合区段作业上次完成运行的条件。 之前可能存在于数据集中但在上次完成的区段作业运行期间没有资格访问区段的任何用户档案已被删除。

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

如 `destination.segmentPerBatch` 果请求中未包含(如果不存在，则默认为 `false`)或将值设置为 `false`，则上述响应中的对象将不包含数组，而只 `destination` 包含一个，如 `batches``batchId`下所示。 该单个批将包括所有段ID，而上述响应显示每个批ID的单个段ID。

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### 列表所有导出作业

通过对端点执行GET请求，可以返回特定IMS组织的所有导出作业的列表 `export/jobs` 符。 该请求还支持查询参 `limit` 数 `offset`和，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| 属性 | 描述 |
| -------- | ----------- |
| `limit` | 指定要返回的记录数。 |
| `offset` | 按提供的数字偏移要返回的结果页。 |


**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

该响应包含 `records` 一个对象，其中包含由IMS组织创建的导出作业。

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### 监视导出进度

作为导出作业进程，您可以通过向端点发出GET请求并在路 `/export/jobs` 径中包含导 `id` 出作业的状态来监视其状态。 一旦字段返回值“SUCCEEDED”, `status` 导出作业即完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要 `id` 访问的导出作业。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `batchId` | 从成功导出创建的批的标识符，用于读取受众数据时的查找目的。 |

## 后续步骤

成功完成导出后，您的数据即可在Experience Platform的数据湖中使用。 然后，您可以使用 [数据访问](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) API，使用与导出 `batchId` 关联的数据访问数据。 根据区段的大小，数据可能以块为单位，而批可能由多个文件组成。

有关如何使用数据访问API访问和下载批处理文件的分步说明，请遵循数据 [访问教程](../../data-access/tutorials/dataset-data.md)。

您还可以使用Adobe Experience Platform查询服务访问成功导出的段数据。 查询服务使用UI或RESTful API，允许您对数据湖中的数据编写、验证和运行查询。

有关如何查询受众数据的更多信息，请查阅 [查询服务文档](../../query-service/home.md)。
