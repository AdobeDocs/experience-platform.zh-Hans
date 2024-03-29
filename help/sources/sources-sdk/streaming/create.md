---
title: 使用流服务API为Streaming SDK创建新的连接规范
description: 以下文档提供了有关如何使用Flow Service API创建连接规范以及通过自助式源集成新源的步骤。
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta 版
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# 使用创建新的连接规范 [!DNL Flow Service] API

>[!NOTE]
>
>自助源流SDK处于测试阶段。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

连接规范表示源的结构。 它包含有关源身份验证要求的信息，定义如何探索和检查源数据，并提供有关给定源属性的信息。 此 `/connectionSpecs` 中的端点 [!DNL Flow Service] API允许您以编程方式管理组织内的连接规范。

以下文档提供了有关如何使用创建连接规范的步骤 [!DNL Flow Service] API并通过自助源(Streaming SDK)集成新源。

## 快速入门

在继续之前，请查看 [快速入门指南](./getting-started.md) 有关相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 收集工件

要使用自助源创建新的流源，您必须首先协调Adobe、请求专用Git存储库，并与Adobe提供有关源的标签、描述、类别和图标的详细信息保持一致。

提供后，您必须构建私有Git存储库，如下所示：

* 源
   * {your_source}
      * 工件
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 工件（文件名） | 描述 | 示例 |
| --- | --- | --- |
| {your_source} | 源的名称。 此文件夹应包含与您的源相关的所有工件，位于您的专用Git存储库中。 | `medallia` |
| {your_source}-category.txt | 源所属的类别，格式为文本文件。 **注意**：如果您认为您的信息源不符合以上任何类别，请联系您的Adobe代表进行讨论。 | `medallia-category.txt` 在文件中，请指定源的类别，如： `streaming`. |
| {your_source}-description.txt | 源的简要说明。 | [!DNL Medallia] 是营销自动化源，可用于将 [!DNL Medallia] 要Experience Platform的数据。 |
| {your_source}-icon.svg | 用于在Experience Platform源目录中表示您的源的图像。 此图标必须是SVG文件。 |
| {your_source}-label.txt | 应显示在Experience Platform源目录中的源名称。 | 梅达利亚 |
| {your_source}-connectionSpec.json | 包含源连接规范的JSON文件。 最初不需要此文件，因为您将在完成本指南时填充连接规范。 | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>在连接规范的测试期间，您可以使用 `text` 在连接规范中。

将必要的文件添加到专用Git存储库后，您必须创建一个拉取请求(PR)以供Adobe审查。 您的PR获得批准并合并后，将为您提供一个可用于连接规范的ID，以引用源的标签、描述和图标。

接下来，按照下面列出的步骤配置您的连接规范。 有关可添加到源的不同功能（如高级计划、自定义架构或不同分页类型）的其他指导，请查看以下方面的指南： [配置源规范](../config/sourcespec.md).

## 复制连接规范模板

收集完所需的工件后，将下面的连接规范模板复制并粘贴到您选择的文本编辑器中，然后更新括号中的属性 `{}` ，其中包含与您的特定来源相关的信息。

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## 创建连接规范 {#create}

获得连接规范模板后，您现在可以通过填写与源对应的相应值来开始创作新的连接规范。

连接规范可以分为两个不同的部分：源规范和浏览规范。

有关连接规范各部分的更多信息，请参阅以下文档：

* [配置源规范](../config/sourcespec.md)
* [配置浏览规范](../config/explorespec.md)

更新您的规范信息后，您可以通过向以下POST请求提交新的连接规范： `/connectionSpecs` 的端点 [!DNL Flow Service] API。

**API格式**

```http
POST /connectionSpecs
```

**请求**

以下请求是流源的完全编写的连接规范示例：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**响应**

成功的响应会返回新创建的连接规范，包括其唯一的 `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
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
    }
  ]
}
```

## 后续步骤

现在您已经创建了新的连接规范，则必须将其对应的连接规范ID添加到现有流规范中。 请参阅上的教程 [更新流规范](./update-flow-specs.md) 以了解更多信息。

要修改您创建的连接规范，请参阅上的教程 [更新连接规范](./update-connection-specs.md).
