---
keywords: Experience Platform；主页；热门主题；流程服务；更新目标数据流
solution: Experience Platform
title: 使用流服务API更新目标数据流
type: Tutorial
description: 本教程介绍了更新目标数据流的步骤。 了解如何使用流服务API启用或禁用数据流、更新其基本信息，或添加和删除区段和属性。
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 1%

---

# 使用流服务API更新目标数据流

本教程介绍了更新目标数据流的步骤。 了解如何启用或禁用数据流、更新其基本信息，或使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 有关使用Experience PlatformUI编辑目标数据流的信息，请阅读 [编辑激活流](/help/destinations/ui/edit-activation.md).

## 快速入门 {#get-started}

本教程要求您拥有有效的流程ID。 如果您没有有效的流量ID，请从 [目标目录](../catalog/overview.md) 并按照 [连接到目标](../ui/connect-destination.md) 和 [激活数据](../ui/activation-overview.md) 在尝试本教程之前。

>[!NOTE]
>
> 术语 *流量* 和 *数据流* 在本教程中可互换使用。 在本教程的上下文中，具有相同的含义。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [目标](../home.md): [!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。
* [沙箱](../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 读取示例API调用 {#reading-sample-api-calls}

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

### 收集所需标题的值 {#gather-values-for-required-headers}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 标头未指定，请求将在 `prod` 沙盒。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找数据流详细信息 {#look-up-dataflow-details}

更新目标数据流的第一步是使用流ID检索数据流详细信息。 通过向发出GET请求，可以查看现有数据流的当前详细信息 `/flows` 端点。

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 独特 `id` 要检索的目标数据流的值。 |

**请求**

以下请求会检索有关您的流ID的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回数据流的当前详细信息，包括其版本、唯一标识符(`id`)及其他相关信息。

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## 更新数据流名称和描述 {#update-dataflow}

要更新数据流的名称和描述，请向 [!DNL Flow Service] API，同时提供您要使用的流量ID、版本和新值。

>[!IMPORTANT]
>
>的 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的数据流的唯一版本。 每次成功更新数据流时，etag值都会随之更新。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求会更新数据流的名称和描述。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 定义要更新的流程部分。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 启用或禁用数据流 {#enable-disable-dataflow}

启用后，数据流会将用户档案导出到目标。 数据流默认处于启用状态，但可以禁用它以暂停配置文件导出。

您可以通过向 [!DNL Flow Service] API和提供状态，以便您将流程更新为。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**请求**

以下请求会将数据流的状态更新为已启用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

以下请求将数据流的状态更新为已禁用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 向数据流中添加区段 {#add-segment}

要向目标数据流添加区段，请向 [!DNL Flow Service] API，同时提供流量ID、版本和要添加的区段。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求会向现有目标数据流中添加新区段。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. 要向数据流添加区段，请使用 `add` 操作。 |
| `path` | 定义要更新的流程部分。 向数据流添加区段时，请使用示例中指定的路径。 |
| `value` | 要使用更新参数的新值。 |
| `id` | 指定要添加到目标数据流的区段的ID。 |
| `name` | **(可选)**. 指定要添加到目标数据流的区段的名称。 请注意，此字段不是必填字段，您可以在不提供其名称的情况下，成功地将区段添加到目标数据流。 |
| `filenameTemplate` | 对于 *批次目标* 仅。 仅当在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中向数据流添加区段时，才需要填写此字段。 <br> 此字段确定导出到目标的文件的文件名格式。 <br> 以下选项可供使用： <br> <ul><li>`%DESTINATION_NAME%`:必选。 导出的文件包含目标名称。</li><li>`%SEGMENT_ID%`:必选。 导出的文件包含导出的区段的ID。</li><li>`%SEGMENT_NAME%`: **(可选)**. 导出的文件包含导出的区段的名称。</li><li>`DATETIME(YYYYMMdd_HHmmss)` 或 `%TIMESTAMP%`: **（可选）**. 为文件选择这两个选项之一，以包含Experience Platform生成文件的时间。</li><li>`custom-text`: **(可选)**. 将此占位符替换为要在文件名末尾附加的任何自定义文本。</li></ul> <br> 有关配置文件名的更多信息，请参阅 [配置文件名](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 章节。 |
| `exportMode` | 对于 *批次目标* 仅。 仅当在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中向数据流添加区段时，才需要填写此字段。 <br> 必选。 选择 `"DAILY_FULL_EXPORT"` 或 `"FIRST_FULL_THEN_INCREMENTAL"`。有关这两个选项的更多信息，请参阅 [导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [导出增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 批次目标激活教程中的步骤8。 |
| `startDate` | 选择区段应开始将用户档案导出到目标的日期。 |
| `frequency` | 对于 *批次目标* 仅。 仅当在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中向数据流添加区段时，才需要填写此字段。 <br> 必选。 <br> <ul><li>对于 `"DAILY_FULL_EXPORT"` 导出模式，您可以选择 `ONCE` 或 `DAILY`.</li><li>对于 `"FIRST_FULL_THEN_INCREMENTAL"` 导出模式，您可以选择 `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | 对于 *批次目标* 仅。 仅当选择 `"DAILY_FULL_EXPORT"` 模式 `frequency` 选择器。 <br> 必选。 <br> <ul><li>选择 `"AFTER_SEGMENT_EVAL"` 以使激活作业在每日Platform批量分段作业完成后立即运行。 这可确保在激活作业运行时，将最新的用户档案导出到您的目标。</li><li>选择 `"SCHEDULED"` 以在固定时间运行激活作业。 这可确保每天同时导出Experience Platform配置文件数据，但导出的配置文件可能不是最新的，具体取决于激活作业开始之前是否已完成批量分段作业。 选择此选项时，还必须添加 `startTime` 以UTC表示应在何时进行每日导出。</li></ul> |
| `endDate` | 对于 *批次目标* 仅。 仅当在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中向数据流添加区段时，才需要填写此字段。 <br> 在选择 `"exportMode":"DAILY_FULL_EXPORT"` 和 `"frequency":"ONCE"`. <br> 设置区段成员停止导出到目标的日期。 |
| `startTime` | 对于 *批次目标* 仅。 仅当在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中向数据流添加区段时，才需要填写此字段。 <br> 必选。 选择生成包含区段成员的文件并将其导出到目标的时间。 |

**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 从数据流中删除区段 {#remove-segment}

要从现有目标数据流中删除区段，请向 [!DNL Flow Service] API，以及要删除的区段的索引选择器。 索引始于 `0`. 例如，下面的示例请求会从数据流中删除第一和第二段。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求会从现有目标数据流中删除两个区段。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. 要从数据流中删除区段，请使用 `remove` 操作。 |
| `path` | 根据区段选择器的索引，指定应从目标数据流中删除的现有区段。 要检索数据流中区段的顺序，请对 `/flows` 端点并检查 `transformations.segmentSelectors` 属性。 要删除数据流中的第一个区段，请使用 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 更新数据流中区段的组件 {#update-segment}

您可以更新现有目标数据流中区段的组件。 例如，您可以更改导出频率，也可以编辑文件名模板。 为此，请对 [!DNL Flow Service] API，以及要更新的区段的流量ID、版本和索引选择器。 索引始于 `0`. 例如，以下请求更新数据流中的第九个区段。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

在现有目标数据流中更新区段时，您应首先执行GET操作，以检索要更新的区段的详细信息。 然后，在有效负载中提供所有区段信息，而不仅仅是要更新的字段。 在以下示例中，在文件名模板的末尾添加自定义文本，并且导出计划频率从6小时更新为12小时。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

有关有效负载中属性的描述，请参阅章节 [向数据流中添加区段](#add-segment).


**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

有关可在数据流中更新的区段组件的更多示例，请参阅以下示例。

## 将区段的导出模式从计划更新为评估区段后的模式 {#update-export-mode}

+++ 单击可查看相关示例，其中区段导出从在指定时间的每天激活更新为在Platform批量分段作业完成后的每天激活。

区段每天16:00 UTC时导出。

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

该区段在每日批量分段作业完成后每天导出。

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## 更新文件名模板，以在文件名中包含其他字段 {#update-filename-template}

+++ 单击可查看更新了文件名模板以在文件名中包含其他字段的示例

导出的文件包含目标名称和Experience Platform区段ID

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

导出的文件包含目标名称、Experience Platform区段ID、Experience Platform生成文件的日期和时间，以及文件末尾附加的自定义文本。


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## 向数据流添加配置文件属性 {#add-profile-attribute}

要向目标数据流添加配置文件属性，请向 [!DNL Flow Service] API，以及要添加的流量ID、版本和配置文件属性。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求会向现有目标数据流添加新配置文件属性。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. 要向数据流添加配置文件属性，请使用 `add` 操作。 |
| `path` | 定义要更新的流程部分。 向数据流添加配置文件属性时，请使用示例中指定的路径。 |
| `value.path` | 要添加到数据流的配置文件属性的值。 |

**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 从数据流中删除配置文件属性 {#remove-profile-attribute}

要从现有目标数据流中删除配置文件属性，请对 [!DNL Flow Service] API，同时提供您要删除的配置文件属性的流程ID、版本和索引选择器。 索引始于 `0`. 例如，下面的示例请求会从数据流中删除第五个配置文件属性。


**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求会从现有目标数据流中删除配置文件属性。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. 要从数据流中删除区段，请使用 `remove` 操作。 |
| `path` | 根据区段选择器的索引，指定应从目标数据流中删除的现有配置文件属性。 要检索数据流中配置文件属性的顺序，请对 `/flows` 端点并检查 `transformations.profileSelectors` 属性。 要删除数据流中的第一个区段，请使用 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**响应**

成功的响应会返回您的流量ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规的Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) ，以了解有关解释错误响应的更多信息。

## 后续步骤 {#next-steps}

通过阅读本教程，您学习了如何更新目标数据流的各个组件，如使用 [!DNL Flow Service] API。 有关目标的更多信息，请参阅 [目标概述](../home.md).
