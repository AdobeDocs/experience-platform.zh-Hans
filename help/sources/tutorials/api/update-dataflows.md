---
title: 使用流服务API更新数据流
description: 了解如何使用流服务API创建数据流，包括其名称、描述和计划。
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 292fb89d457a86ee9f63cebd461abf1f2ecb9662
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

# 使用流服务API更新数据流

本教程介绍了使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新数据流的步骤，包括其基本信息、计划和映射集。

>[!TIP]
>
>源连接和目标连接应映射到单个数据流。 您不应单独更新源连接和目标连接，因为所做更改将不会反映在其相应数据流中。 如果您的用例需要更新源连接和目标连接，则必须创建一对新源连接和目标连接，以及新的数据流。

## 快速入门

本教程要求您拥有有效的流ID。 如果您没有有效的流ID，请从[源概述](../../home.md)中选择您选择的连接器，并按照尝试本教程之前概述的步骤操作。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

## 查找数据流详细信息

更新数据流的第一步是使用流ID检索数据流详细信息。 通过向`/flows`端点发出GET请求，可查看现有数据流的当前详细信息。

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要检索的数据流的唯一`id`值。 |

**请求**

以下请求将检索有关您的流ID的更新信息。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回数据流的当前详细信息，包括其版本、时间表和唯一标识符(`id`)。

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## 更新数据流

要更新数据流的运行计划、名称和描述，请对[!DNL Flow Service] API执行PATCH请求，同时提供您的流ID、版本以及要使用的新计划。

>[!IMPORTANT]
>
>* 发出PATCH请求时需要使用`If-Match`标头。 此标头的值是您要更新的连接的唯一版本。 每次成功更新数据流时，etag值都会更新。
>
>* 如果初始计划的`startTime`已经发生，则无法更新数据流的`startTime`。 此限制同时适用于已启用和已禁用的数据流。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求将更新您的流运行计划以及数据流的名称和描述。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "Database Dataflow Feb2021"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "Database dataflow for testing update API"
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

## 更新映射

您可以通过向[!DNL Flow Service] API发出PATCH请求并为`mappingId`和`mappingVersion`提供更新的值来更新现有数据流的映射集。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求更新数据流的映射集。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
  -d '[
      {
          "op": "replace",
          "path": "/transformations/0",
          "value": {
              "name": "Mapping",
              "params": {
                  "mappingId": "c5f22f04e09f44498e528901546a83b1",
                  "mappingVersion": 2
              }
          }
      }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 在此示例中，正在更新`transformations`。 |
| `value.name` | 要更新的属性的名称。 |
| `value.params.mappingId` | 用于更新数据流映射集的新映射ID。 |
| `value.params.mappingVersion` | 与更新的映射ID关联的新映射版本。 |

**响应**

成功的响应将返回您的流ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供流ID来验证更新。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API更新了数据流的基本信息、计划和映射集。 有关使用源连接器的更多信息，请参阅[源概述](../../home.md)。
