---
title: 使用流服务API更新流SDK的流规范
description: 以下文档提供了有关如何使用适用于自助源的流服务API (Streaming SDK)检索和更新流规范的步骤。
exl-id: cc9dab7a-08fa-4c6c-bbac-cb658a6376fb
badge: Beta 版
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API更新流规范

>[!NOTE]
>
>自助源流SDK处于测试阶段。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

生成新的连接规范ID后，必须将此ID添加到流规范中，才能创建数据流。

流程规范包含定义流程的信息，包括它支持的源连接ID和目标连接ID、需要应用于数据的转换规范以及生成流程所需的计划参数。 您可以使用`/flowSpecs`端点编辑流规范。

以下文档提供了有关如何使用[!DNL Flow Service] API for Self-Serve Sources (Streaming SDK)检索和更新流规范的步骤。

## 快速入门

在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 查找流规范 {#lookup}

使用`generic-streaming`模板创建的源都使用`GenericStreamingAEP`流规范。 通过向`/flowSpecs/`端点发出GET请求并提供`e77fde5a-22a8-11ed-861d-0242ac120002`的`flowSpec.id`，可以检索此流规范。

**API格式**

```http
GET /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**请求**

以下请求检索`e77fde5a-22a8-11ed-861d-0242ac120002`流规范。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

成功的响应将返回查询流程规范的详细信息。

```json
{
  "items": [
    {
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
            }
          }
        }
      },
      "transformationSpecs": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

## 更新流规范 {#update}

您可以通过PUT操作更新流规格的字段。 通过PUT请求更新流规范时，正文必须包括在POST请求中创建新流规范时所需的所有字段。

>[!IMPORTANT]
>
>为新的源创建连接规范时，必须将其规范ID添加到与源对应的流规范的`sourceConnectionSpecIds`数组中。 这可确保现有流规范支持新源，从而允许您使用新源完成数据流创建过程。

**API格式**

```http
PUT /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**请求**

以下请求更新`e77fde5a-22a8-11ed-861d-0242ac120002`的流规范以包含连接规范ID `bdb5b792-451b-42de-acf8-15f3195821de`。

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
          "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "bdb5b792-451b-42de-acf8-15f3195821de"
      ],
      "targetConnectionSpecIds": [
          "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
          "name": "OptionSpec",
          "spec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object",
              "properties": {
                  "errorDiagnosticsEnabled": {
                      "title": "Error diagnostics.",
                      "description": "Flag to enable detailed and sample error diagnostics summary.",
                      "type": "boolean",
                      "default": false
                  },
                  "partialIngestionPercent": {
                      "title": "Partial ingestion threshold.",
                      "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                      "type": "number",
                      "exclusiveMinimum": 0
                  },
                  "inletUrl": {
                      "title": "Inlet Url.",
                      "description": "Inlet Url which defines the streaming endpoint.",
                      "type": "string"
                  }
              }
          }
      },
      "transformationSpecs": [
          {
              "name": "Mapping",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "defines various params required for different mapping from source to target",
                  "properties": {
                      "mappingId": {
                          "type": "string"
                      },
                      "mappingVersion": {
                          "type": "string"
                      }
                  }
              }
          }
      ],
      "attributes": {
          "isSourceFlow": true,
          "flacValidationSupported": true,
          "frequency": "streaming",
          "uiAttributes": {
              "apiFeatures": {
                  "updateSupported": true,
                  "flowRunsSupported": true
              }
          }
      },
      "permissionsInfo": {
          "view": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "read"
                  ]
              }
          ],
          "manage": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "write"
                  ]
              }
          ]
      }
  }'
```

**响应**

成功的响应返回查询的流规范的详细信息，包括其更新的`sourceConnectionSpecIds`列表。

```json
{
    "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "GenericStreamingAEP",
    "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
    "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
            }
          }
        }
      },
      "transformationSpecs": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

## 后续步骤

在将新的连接规范添加到适当的流量规范后，您现在可以继续测试和提交新源。 有关详细信息，请参阅有关[测试和提交新源](./submit.md)的指南。
