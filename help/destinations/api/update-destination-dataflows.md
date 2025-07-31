---
keywords: Experience Platform；主页；热门主题；流服务；更新目标数据流
solution: Experience Platform
title: 使用流服务API更新目标数据流
type: Tutorial
description: 本教程介绍了更新目标数据流的步骤。 了解如何使用流服务API启用或禁用数据流、更新其基本信息或添加和删除受众和属性。
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 3%

---

# 使用流服务API更新目标数据流

本教程介绍了更新目标数据流的步骤。 了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)启用或禁用数据流、更新其基本信息或添加和删除受众和属性。 有关使用Experience Platform UI编辑目标数据流的信息，请阅读[编辑激活流](/help/destinations/ui/edit-activation.md)。

## 快速入门 {#get-started}

本教程要求您拥有有效的流ID。 如果您没有有效的流ID，请从[目标目录](../catalog/overview.md)中选择您选择的目标，然后按照列出的步骤[连接到目标](../ui/connect-destination.md)和[激活数据](../ui/activation-overview.md)，然后再尝试本教程。

>[!NOTE]
>
> 在本教程中，术语&#x200B;*流*&#x200B;和&#x200B;*数据流*&#x200B;可互换使用。 在本教程的上下文中，它们具有相同的含义。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations]是预先构建的与目标平台的集成，可无缝激活Adobe Experience Platform中的数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。
* [沙盒](../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用[!DNL Flow Service] API成功更新数据流。

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值 {#gather-values-for-required-headers}

要调用Experience Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对Experience Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果未指定`x-sandbox-name`标头，则在`prod`沙盒下解析请求。

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的媒体类型标头：

* `Content-Type: application/json`

## 查找数据流详细信息 {#look-up-dataflow-details}

更新目标数据流的第一步是使用流ID检索数据流详细信息。 通过向`/flows`端点发出GET请求，可查看现有数据流的当前详细信息。

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要检索的目标数据流的唯一`id`值。 |

**请求**

以下请求可检索有关您的流量ID的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回数据流的当前详细信息，包括其版本、唯一标识符(`id`)和其他相关信息。

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

要更新数据流的名称和描述，请对[!DNL Flow Service] API执行PATCH请求，同时提供您的流ID、版本以及要使用的新值。

>[!IMPORTANT]
>
>发出PATCH请求时需要使用`If-Match`标头。 此标头的值是要更新的数据流的唯一版本。 每次成功更新数据流时，etag值都会更新。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求将更新数据流的名称和描述。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 启用或禁用数据流 {#enable-disable-dataflow}

启用后，数据流会将配置文件导出到目标。 数据流默认处于启用状态，但可以禁用以暂停配置文件导出。

通过向[!DNL Flow Service] API发出POST请求并提供要更新流的状态，可以启用或禁用现有目标数据流。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**请求**

以下请求会将您的数据流状态更新为“已启用”。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

以下请求会将您的数据流状态更新为已禁用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 将受众添加到数据流 {#add-segment}

要将受众添加到目标数据流，请在提供您的流ID、版本和要添加的受众的同时对[!DNL Flow Service] API执行PATCH请求。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求会将新受众添加到现有目标数据流。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 要将受众添加到数据流，请使用`add`操作。 |
| `path` | 定义要更新的流部分。 将受众添加到数据流时，请使用示例中指定的路径。 |
| `value` | 要用于更新参数的新值。 |
| `id` | 指定要添加到目标数据流的受众的ID。 |
| `name` | **（可选）**。 指定要添加到目标数据流的受众的名称。 请注意，此字段不是必填字段，您无需提供名称即可将受众成功添加到目标数据流。 |
| `filenameTemplate` | 仅适用于&#x200B;*批次目标*。 只有在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中将受众添加到数据流时，才需要使用此字段。 <br>此字段确定导出到目标的文件的文件名格式。 <br>以下选项可用： <br> <ul><li>`%DESTINATION_NAME%`：必填。 导出的文件包含目标名称。</li><li>`%SEGMENT_ID%`：必填。 导出的文件包含导出受众的ID。</li><li>`%SEGMENT_NAME%`： **（可选）**。 导出的文件包含导出的受众的名称。</li><li>`DATETIME(YYYYMMdd_HHmmss)`或`%TIMESTAMP%`： **（可选）**。 为文件选择这两个选项之一，以包含Experience Platform生成文件的时间。</li><li>`custom-text`： **（可选）**。 将此占位符替换为要在文件名末尾追加的任何自定义文本。</li></ul> <br>有关配置文件名的详细信息，请参阅批量目标激活教程中的[配置文件名](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)部分。 |
| `exportMode` | 仅适用于&#x200B;*批次目标*。 只有在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中将受众添加到数据流时，才需要使用此字段。 <br>必填。 选择`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 有关这两个选项的更多信息，请参阅批处理目标激活教程中的[导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[导出增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 |
| `startDate` | 选择受众应开始将用户档案导出到目标的日期。 |
| `frequency` | 仅适用于&#x200B;*批次目标*。 只有在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中将受众添加到数据流时，才需要使用此字段。 <br>必填。<br> <ul><li>对于`"DAILY_FULL_EXPORT"`导出模式，您可以选择`ONCE`或`DAILY`。</li><li>对于`"FIRST_FULL_THEN_INCREMENTAL"`导出模式，您可以选择`"DAILY"`、`"EVERY_3_HOURS"`、`"EVERY_6_HOURS"`、`"EVERY_8_HOURS"`、`"EVERY_12_HOURS"`。</li></ul> |
| `triggerType` | 仅适用于&#x200B;*批次目标*。 仅当在`"DAILY_FULL_EXPORT"`选择器中选择`frequency`模式时，才需要此字段。 <br>必填。<br> <ul><li>选择`"AFTER_SEGMENT_EVAL"`以使激活作业在每日Experience Platform批处理分段作业完成后立即运行。 这可确保在激活作业运行时，将最新的配置文件导出到您的目标。</li><li>选择`"SCHEDULED"`以使激活作业在固定时间运行。 这可确保每天在同一时间导出Experience Platform用户档案数据，但您导出的用户档案可能不是最新的，具体取决于批量分段作业是否在激活作业开始之前完成。 当选择此选项时，还必须添加`startTime`以指示每日导出应在UTC时段的哪个时间发生。</li></ul> |
| `endDate` | 仅适用于&#x200B;*批次目标*。 只有在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中将受众添加到数据流时，才需要使用此字段。 选择<br>和`"exportMode":"DAILY_FULL_EXPORT"`时，`"frequency":"ONCE"`不适用。 <br>设置受众成员停止导出到目标的日期。 |
| `startTime` | 仅适用于&#x200B;*批次目标*。 只有在批量文件导出目标(如Amazon S3、SFTP或Azure Blob)中将受众添加到数据流时，才需要使用此字段。 <br>必填。 选择应生成包含受众成员的文件并将其导出到目标的时间。 |

**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 从数据流中删除受众 {#remove-segment}

要从现有目标数据流中删除受众，请提供要移除的受众的流ID、版本和索引选择器，同时对[!DNL Flow Service] API执行PATCH请求。 索引从`0`开始。 例如，下面的示例请求从数据流中删除第一和第二受众。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求从现有目标数据流中删除两个受众。

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
   "path":"/transformations/0/params/segmentSelectors/selectors/0",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/1",
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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 要从数据流中删除受众，请使用`remove`操作。 |
| `path` | 根据受众选择器的索引，指定应从目标数据流中删除哪些现有受众。 要检索数据流中受众的顺序，请对`/flows`端点执行GET调用并检查`transformations.segmentSelectors`属性。 要删除数据流中的第一个受众，请使用`"path":"/transformations/0/params/segmentSelectors/selectors/0"`。 |


**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 更新数据流中受众的组件 {#update-segment}

您可以更新现有目标数据流中受众的组件。 例如，可以更改导出频率或编辑文件名模板。 为此，请提供要更新的受众的流ID、版本和索引选择器，同时对[!DNL Flow Service] API执行PATCH请求。 索引从`0`开始。 例如，下面的请求会更新数据流中的第九个受众。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

在现有目标数据流中更新受众时，您应该首先执行GET操作，以检索要更新的受众的详细信息。 然后，在有效负荷中提供所有受众信息，而不仅仅是要更新的字段。 在以下示例中，自定义文本会添加到文件名模板的末尾，导出计划频率会从6小时更新为12小时。

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

有关有效负载中属性的描述，请参阅[将受众添加到数据流](#add-segment)部分。


**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

有关可在数据流中更新的受众组件的更多示例，请参阅以下示例。

## 在受众评估后将受众的导出模式从计划的更新为的 {#update-export-mode}

+++ 单击以查看示例，其中受众导出从每天在指定时间激活更新为在Experience Platform批量分段作业完成后每天激活。

每天的16:00 UTC导出受众。

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

每日批量分段作业完成后，每天都会导出受众。

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

## 更新文件名模板以在文件名中包含其他字段 {#update-filename-template}

+++ 单击以查看文件名模板的更新示例，该模板在文件名中包含其他字段

导出的文件包含目标名称和Experience Platform受众ID

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

导出的文件包含目标名称、Experience Platform受众ID、Experience Platform生成文件的日期和时间，以及在文件末尾附加的自定义文本。


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

要向目标数据流添加配置文件属性，请在提供流ID、版本和要添加的配置文件属性的同时，对[!DNL Flow Service] API执行PATCH请求。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求将新的配置文件属性添加到现有目标数据流。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 若要向数据流添加配置文件属性，请使用`add`操作。 |
| `path` | 定义要更新的流部分。 将配置文件属性添加到数据流时，请使用示例中指定的路径。 |
| `value.path` | 要添加到数据流的配置文件属性的值。 |

**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 从数据流中删除配置文件属性 {#remove-profile-attribute}

要从现有目标数据流中删除配置文件属性，请在提供流ID、版本以及要删除的配置文件属性的索引选择器的同时，对[!DNL Flow Service] API执行PATCH请求。 索引从`0`开始。 例如，下面的示例请求从数据流中删除第五个配置文件属性。


**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求从现有目标数据流中删除配置文件属性。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 要从数据流中删除受众，请使用`remove`操作。 |
| `path` | 根据受众选择器的索引，指定应从目标数据流中删除的现有配置文件属性。 要检索数据流中配置文件属性的顺序，请对`/flows`端点执行GET调用并检查`transformations.profileSelectors`属性。 要删除数据流中的第一个受众，请使用`"path":"transformations/0/params/segmentSelectors/selectors/0/"`。 |


**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience Platform API错误消息原则。 有关解释错误响应的详细信息，请参阅Experience Platform疑难解答指南中的[API状态代码](/help/landing/troubleshooting.md#api-status-codes)和[请求标头错误](/help/landing/troubleshooting.md#request-header-errors)。

## 后续步骤 {#next-steps}

通过学习本教程，您已了解如何更新目标数据流的各种组件，例如使用[!DNL Flow Service] API添加或删除受众或配置文件属性。 有关目标的详细信息，请参阅[目标概述](../home.md)。
