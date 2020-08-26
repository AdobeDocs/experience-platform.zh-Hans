---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: 颜色提取
topic: Developer guide
description: 给定文本提取时，关键字文档服务会自动提取最能描述文档主题的关键字或关键字短语。 为了提取关键字，使用命名实体识别(NER)和无监督关键字提取算法的组合。
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---


# 关键字提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是测试版。 文档可能会更改。

给定文本提取时，关键字文档服务会自动提取最能描述文档主题的关键字或关键字短语。 为了提取关键字，使用命名实体识别(NER)和无监督关键字提取算法的组合。

**无监督关键字提取**

对于非监督关键字提取 [，使用[!DNL](http://yake.inesctec.pt/) YAKE]。 [!DNL YAKE] 是一种快速、准确的无监督自动关键字提取方法，用于从文档中选择最重要的关键字。 然后，对关 [!DNL YAKE] 键字提取进行过滤，以仅选择名词短语。

**命名实体识别**

对于命名实体 [识别，使用[!DNL spaCy](https://spacy.io/)]的OntoNotes模型。 该模型指定上下文特定的令牌矢量、语音部分(POS)标签、依赖性分析和命名实体。 OntoNotes模型是核心模型之 [!DNL spaCy] 一。 有关OntoNotes模型的更多信息，请参 [阅](https://spacy.io/models/en)。

下表列出了被识 [!DNL Content and Commerce AI] 别的命名实体：

| 实体名称 | 描述 |
| --- | --- |
| 人 | 人，包括虚构。 |
| NORP | 国籍或宗教或政治团体。 |
| GPE | 国家、城市和州。 |
| LOC | 非全球普惠地点、山脉、水体。 |
| FAC | 建筑物、机场、公路、桥梁等 |
| 组织 | 公司、机构、机构等。 |
| 产品 | 物品、车辆、食品等 （非服务。） |
| 事件 | 指定飓风、战斗、战争、运动事件等 |
| WORK_OF_ART | 书名、歌曲等 |
| 法律 | 被命名的文档成为法律。 |
| 语言 | 任何已命名语言。 |

结果与 [!DNL OntoNotes] 关键字结合， [!DNL YAKE]然后根据其重要性按排序返回。

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

有关显示的输入参数的详细信息，请参阅示例有效负荷下表。

>[!CAUTION]
>
>`analyzer_id` 确定使 [!DNL Sensei Content Framework] 用哪个。 请在提出请求前检查 `analyzer_id` 您是否有适当的。 对于关键字提取服 `analyzer_id` 务，ID为：
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

| 属性 | 描述 | 强制 |
| --- | --- | --- |
| `analyzer_id` | 您 [!DNL Sensei] 的请求所部署的服务ID。 此ID决定使用哪 [!DNL Sensei Content Frameworks] 个ID。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 包含JSON对象的数组，数组中的每个对象都表示文档。 作为此数组的一部分传递的任何参数都将覆盖在数组外部指定的全局 `data` 参数。 此表中概述的任何其余属性都可以从中覆盖 `data`。 | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求主体的一部分还是S3存储段的已签名URL。 此属性的默认值为 `inline`。 | 是 |
| `encoding` | 输入文本的编码格式。 这可以是 `utf-8` 或 `utf-16`。 此属性的默认值为 `utf-8`。 | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用该值 `0` 返回所有结果。 此属性的默认值为 `0`。 | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用该值 `0` 返回所有结果。 与一起使用时， `threshold`返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 有关自定 [义参数](#appendix) ，请参阅附录。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配自动生成的ID。 | 否 |
| `content` | 关键字提取服务使用的内容。 内容可以是原始文本（“内联”内容类型）。 <br> 如果内容是S3(&#39;s3-bucket&#39; content-type)上的文件，请传递已签名的url。 当内容是请求主体的一部分时，列表数据元素应仅具有一个对象。 如果传递了多个对象，则只处理第一个对象。 | 是 |

**响应**

成功的响应会返回一个JSON对象，该对象包含数组中提取的关 `response` 键字。

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

## 附录 {#appendix}

下表包含可从中使用的可用参数 `custom`。

| 名称 | 描述 | 强制 |
| --- | --- | --- |
| `min-n` | 关键字中所需的最小单词数。 | 否 |
| `entity-types` | 要返回的实体类型。 请参阅此文档开头的命名实体识别表。 | 否 |