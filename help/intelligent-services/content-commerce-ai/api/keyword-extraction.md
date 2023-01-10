---
keywords: Experience Platform；快速入门；内容ai；商务ai；内容和商务ai；关键词提取；关键词提取
solution: Experience Platform
title: 内容和商务AI API中的关键词提取
description: 在给定文本文档时，关键词提取服务会自动提取最能描述文档主题的关键词或关键词。 为了提取关键词，使用命名实体识别(NER)和无监督关键词提取算法的组合。
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 3%

---

# 关键词提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是测试版。 文档可能会发生更改。

在给定文本文档时，关键词提取服务会自动提取最能描述文档主题的关键词或关键词。 为了提取关键词，使用命名实体识别(NER)和无监督关键词提取算法的组合。

识别的命名实体 [!DNL Content and Commerce AI] 下表列出：

| 实体名称 | 描述 |
| --- | --- |
| 人员 | 人，包括虚构的。 |
| NORP | 民族或宗教或政治团体。 |
| GPE | 国家、城市和州。 |
| LOC | 非泛太平洋区域、山脉、水体。 |
| FAC | 建筑物、机场、公路、桥梁等 |
| 组织 | 公司、代理、机构等 |
| 产品 | 物品、车辆、食品等 （非服务。） |
| 事件 | 有名的飓风、战斗、战争、体育活动等。 |
| WORK_OF_ART | 书籍、歌曲等的标题。 |
| 法律 | 成为法律的已命名文件。 |
| 语言 | 任何命名语言。 |

>[!NOTE]
>
>如果您计划处理PDF，请跳到 [PDF关键词提取](#pdf-extraction) 在本文档中。 此外，还将设置对其他文件类型（如docx、ppt、amd xml）的支持，以在以后的日期发布。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求基于在有效载荷中提供的输入参数从文档中提取关键字。

简化的输入文件JSON:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

有关所示输入参数的更多信息，请参阅有效负载示例下表。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 中，将使用。 请检查您是否拥有 `analyzer_id` 之前。 对于关键词提取服务， `analyzer_id` ID是：
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `analyzer_id` | 的 [!DNL Sensei] 请求部署在下的服务ID。 此ID确定 [!DNL Sensei Content Frameworks] 中，将使用。 对于自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，该对象在数组中的每个对象都表示一个文档。 作为此数组的一部分传递的任何参数都会覆盖在 `data` 数组。 下表中列出的任何其余属性都可以从中覆盖 `data`. | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求正文的一部分还是S3存储段的带符号的url。 此属性的默认值为 `inline`. | 是 |
| `encoding` | 输入文本的编码格式。 这可以是 `utf-8` 或 `utf-16`. 此属性的默认值为 `utf-8`. | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值 `0` 返回所有结果。 此属性的默认值为 `0`. | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用值 `0` 返回所有结果。 与 `threshold`，则返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`. | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 请参阅 [附录](#appendix) 以了解有关自定义参数的更多信息。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 关键词提取服务使用的内容。 内容可以是原始文本（“内联”content-type）。 <br> 如果内容是S3(“s3-bucket”content-type)上的文件，请传递已签名的URL。 当内容是request-body的一部分时，数据元素列表应该只有一个对象。 如果传递了多个对象，则仅处理第一个对象。 | 是 |

**响应**

成功响应会返回一个JSON对象，该对象包含 `response` 数组。

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## PDF关键词提取 {#pdf-extraction}

关键词提取服务支持PDF，但是，您需要使用新的AnalyzerID来PDF文件，并将文档类型更改为PDF。 有关更多信息，请参阅以下示例。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求基于在有效负载中提供的输入参数从PDF文档中提取关键字。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 中，将使用。 请检查您是否拥有 `analyzer_id` 之前。 对于PDF关键词提取， `analyzer_id` ID是：
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `analyzer_id` | 的 [!DNL Sensei] 请求部署在下的服务ID。 此ID确定 [!DNL Sensei Content Frameworks] 中，将使用。 对于自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，该对象在数组中的每个对象都表示一个文档。 作为此数组的一部分传递的任何参数都会覆盖在 `data` 数组。 下表中列出的任何其余属性都可以从中覆盖 `data`. | 是 |
| `language` | 输入语言。 默认值为 `en` （英语）。 | 否 |
| `content-type` | 用于指示输入内容类型。 此值应设置为 `file`. | 是 |
| `encoding` | 输入的编码格式。 此值应设置为 `pdf`. 以后将支持更多编码类型。 | 是 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值 `0` 返回所有结果。 此属性的默认值为 `0`. | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用值 `0` 返回所有结果。 与 `threshold`，则返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`. | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 请参阅 [附录](#appendix) 以了解有关自定义参数的更多信息。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 此值应设置为 `file`. | 是 |

**响应**

成功响应会返回一个JSON对象，该对象包含 `response` 数组。

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

有关使用PDF提取的更多信息和示例，其中包含有关如何设置、部署和与AEM云服务集成的说明。 访问 [CCAIPDF提取工作程序github存储库](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## 附录 {#appendix}

下表包含可从内部使用的可用参数 `custom`.

| 名称 | 描述 | 必需 |
| --- | --- | --- |
| `min-n` | 关键词中所需的最少词数。 | 否 |
| `entity-types` | 要返回的实体类型。 请参阅本文档开头的命名实体识别表。 | 否 |
