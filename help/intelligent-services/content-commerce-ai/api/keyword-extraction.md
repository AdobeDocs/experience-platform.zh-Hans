---
keywords: Experience Platform；入门；内容ai；商务ai；内容和商务ai；关键字提取；关键字提取
solution: Experience Platform, Intelligent Services
title: 内容和商务AI API中的关键字提取
topic-legacy: Developer guide
description: 当给定文本文档时，关键字提取服务会自动提取最能描述文档主题的关键字或关键词组。 为了提取关键字，使用命名实体识别(NER)和无监督关键字提取算法的组合。
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 3%

---

# 关键字提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是贝塔。文档可能会更改。

当给定文本文档时，关键字提取服务会自动提取最能描述文档主题的关键字或关键词组。 为了提取关键字，使用命名实体识别(NER)和无监督关键字提取算法的组合。

下表列出了由[!DNL Content and Commerce AI]识别的命名实体：

| 实体名称 | 描述 |
| --- | --- |
| PERSON | 人，包括虚构。 |
| NORP | 民族或宗教或政治团体。 |
| GPE | 国家、城市和州。 |
| LOC | 非全球普惠地点、山脉、水体。 |
| FAC | 建筑物、机场、高速公路、桥梁等 |
| 组织 | 公司、机构、机构等 |
| 产品 | 物品、车辆、食品等 （不是服务。） |
| 事件 | 有名的飓风、战斗、战争、运动事件等 |
| WORK_OF_ART | 书名、歌曲等 |
| 法律 | 被命名为法律的文档。 |
| 语言 | 任何指定语言。 |

>[!NOTE]
>
>如果您计划处理PDF，请跳到此文档中[PDF关键字提取](#pdf-extraction)的说明。 此外，还将在以后发布对docx、ppt、amd xml等其他文件类型的支持。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求基于在有效负荷中提供的输入参数从文档提取关键字。

输入文件的简化JSON:

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

有关所示输入参数的详细信息，请参阅示例有效负荷下表。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 使用的。在发出请求之前，请检查您是否有正确的`analyzer_id`。 对于关键字提取服务，`analyzer_id` ID为：
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

| 属性 | 描述 | 必填 |
| --- | --- | --- |
| `analyzer_id` | 您的请求部署到的[!DNL Sensei]服务ID。 此ID决定使用哪个[!DNL Sensei Content Frameworks]。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，数组中的每个对象都表示一个文档。 作为此数组的一部分传递的任何参数都将覆盖在`data`数组外部指定的全局参数。 下表中列出的所有其余属性都可从`data`中覆盖。 | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求主体的一部分还是S3存储段的已签名URL。 此属性的默认值为`inline`。 | 是 |
| `encoding` | 输入文本的编码格式。 这可以是`utf-8`或`utf-16`。 此属性的默认值为`utf-8`。 | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值`0`返回所有结果。 此属性的默认值为`0`。 | 否 |
| `top-N` | 要返回的结果数（不能为负整数）。 使用值`0`返回所有结果。 与`threshold`一起使用时，返回的结果数是任一限制集中的较小者。 此属性的默认值为`0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 有关自定义参数的详细信息，请参见[附录](#appendix)。 | 否 |
| `content-id` | 在响应中返回的数据元素的唯一ID。 如果未传递，则分配一个自动生成的ID。 | 否 |
| `content` | 关键字提取服务使用的内容。 内容可以是原始文本（“内联”内容类型）。 <br> 如果内容是S3(&#39;s3-bucket&#39; content-type)上的文件，请传递已签名的url。当内容是请求主体的一部分时，列表数据元素应仅包含一个对象。 如果传递了多个对象，则只处理第一个对象。 | 是 |

**响应**

成功的响应返回一个JSON对象，其中包含在`response`数组中提取的关键字。

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

## PDF关键字提取{#pdf-extraction}

关键字提取服务支持PDF，但您需要对PDF文件使用新的AnalyzerID，并将文档类型更改为PDF。 有关更多信息，请参阅以下示例。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求基于有效负荷中提供的输入参数从PDF文档提取关键字。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 使用的。在发出请求之前，请检查您是否有正确的`analyzer_id`。 对于PDF关键字提取,`analyzer_id` ID为：
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

| 属性 | 描述 | 必填 |
| --- | --- | --- |
| `analyzer_id` | 您的请求部署到的[!DNL Sensei]服务ID。 此ID决定使用哪个[!DNL Sensei Content Frameworks]。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，数组中的每个对象都表示一个文档。 作为此数组的一部分传递的任何参数都将覆盖在`data`数组外部指定的全局参数。 下表中列出的所有其余属性都可从`data`中覆盖。 | 是 |
| `language` | 输入语言。 默认值为`en`（英语）。 | 否 |
| `content-type` | 用于指示输入内容类型。 此值应设置为`file`。 | 是 |
| `encoding` | 输入的编码格式。 此值应设置为`pdf`。 以后将支持更多编码类型。 | 是 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值`0`返回所有结果。 此属性的默认值为`0`。 | 否 |
| `top-N` | 要返回的结果数（不能为负整数）。 使用值`0`返回所有结果。 与`threshold`一起使用时，返回的结果数是任一限制集中的较小者。 此属性的默认值为`0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 有关自定义参数的详细信息，请参见[附录](#appendix)。 | 否 |
| `content-id` | 在响应中返回的数据元素的唯一ID。 如果未传递，则分配一个自动生成的ID。 | 否 |
| `content` | 此值应设置为`file`。 | 是 |

**响应**

成功的响应返回一个JSON对象，其中包含在`response`数组中提取的关键字。

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

有关使用PDF提取的更多信息和示例，其中包含有关如何设置、部署和与AEM云服务集成的说明。 访问[CCAI PDF提取工作库github存储库](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract)。

## 附录 {#appendix}

下表包含可从`custom`中使用的可用参数。

| 名称 | 描述 | 必填 |
| --- | --- | --- |
| `min-n` | 关键字中所需的最少字数。 | 否 |
| `entity-types` | 要返回的实体类型。 请参阅此文档开头的命名实体识别表。 | 否 |
