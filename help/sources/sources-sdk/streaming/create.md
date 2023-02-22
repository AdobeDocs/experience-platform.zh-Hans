---
title: 使用流服务API为流式SDK创建新的连接规范
description: 以下文档提供了如何使用流服务API创建连接规范并通过自助源集成新源的步骤。
hide: true
hidefromtoc: true
source-git-commit: 6b78ed695bca5912c9af4371a8423fdcd7471bde
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

连接规范表示源的结构。 它包含有关源的身份验证要求的信息，定义如何探索和检查源数据，并提供有关给定源的属性的信息。 的 `/connectionSpecs` 的端点 [!DNL Flow Service] API允许您以编程方式管理组织内的连接规范。

以下文档提供了如何使用 [!DNL Flow Service] API，并通过自助源（流SDK）集成新源。

## 快速入门

在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 收集工件

要使用自助源创建新的流源，您必须先与Adobe协调，请求专用Git存储库，并与Adobe保持一致，以了解与源的标签、描述、类别和图标相关的详细信息。

提供后，您必须按如下方式构建专用Git存储库：

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
| {your_source} | 源的名称。 此文件夹应当包含与您的专用Git存储库中的源相关的所有工件。 | `medallia` |
| {your_source}-category.txt | 源所属的类别，格式为文本文件。 **注意**:如果您认为来源不适合上述任何类别，请联系您的Adobe代表进行讨论。 | `medallia-category.txt` 在文件中，请指定源的类别，如： `streaming`. |
| {your_source}-description.txt | 您的来源的简要描述。 | [!DNL Medallia] 是营销自动化源，您可以 [!DNL Medallia] Experience Platform。 |
| {your_source}-icon.svg | 在Experience Platform源目录中用于表示源的图像。 此图标必须是SVG文件。 |
| {your_source}-label.txt | 源应显示在Experience Platform源目录中的名称。 | 梅达利亚 |
| {your_source}-connectionSpec.json | 包含源连接规范的JSON文件。 最初不需要此文件，因为在您完成本指南时，您将填充连接规范。 | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>在连接规范的测试期间，您可以使用 `text` 在连接规范中。

将必要的文件添加到专用Git存储库后，必须创建拉取请求(PR)以供Adobe查看。 当您的PR获得批准和合并后，您将获得一个ID，可用于连接规范以引用源的标签、描述和图标。

接下来，按照下面列出的步骤配置连接规范。 有关可添加到源的不同功能（如高级计划、自定义模式或不同分页类型）的其他指导，请参阅 [配置源规范](../config/sourcespec.md).

## 复制连接规范模板

收集所需工件后，将下面的连接规范模板复制并粘贴到所选的文本编辑器中，然后更新方括号中的属性 `{}` 包含与您的特定来源相关的信息。

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

有关连接规范各节的详细信息，请参阅以下文档：

* [配置源规范](../config/sourcespec.md)
* [配置浏览规范](../config/explorespec.md)

更新规范信息后，您可以通过向 `/connectionSpecs` 的端点 [!DNL Flow Service] API。

**API格式**

```http
POST /connectionSpecs
```

**请求**

以下请求是流源完全创作的连接规范的一个示例：

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

成功的响应会返回新创建的连接规范，包括其唯一 `id`.

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

现在，您已创建了新的连接规范，必须将其相应的连接规范ID添加到现有的流规范中。 请参阅 [更新流程规范](./update-flow-specs.md) 以了解更多信息。

要修改您创建的连接规范，请参阅 [更新连接规范](./update-connection-specs.md).
