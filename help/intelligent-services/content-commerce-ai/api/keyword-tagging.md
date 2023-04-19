---
keywords: Experience Platform；入门；内容；内容标记ai；关键字标记；关键字标记
solution: Experience Platform
title: 内容标记API中的关键字标记
description: 在提供文本文档时，关键字标记服务会自动提取最能描述文档主题的关键字或关键短语。 为了提取关键字，使用命名实体识别(NER)和无监督关键字标记算法的组合。
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: 7c8c1d69f4c4e0a1374603d541b634ac7f64ab38
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---

# 关键词标记

在给定文本文档时，关键字标记服务会自动提取最能描述文档主题的关键字或关键短语。 为了提取关键字，使用命名实体识别(NER)和无监督关键字标记算法的组合。

下表列出了 [!DNL Content Tagging] 能识别：

| 实体名称 | 描述 |
| --- | --- |
| 人员 | 人，包括虚构的人。 |
| GPE | 国家、城市和州。 |
| LOC | 非GPE地点、山脉和水体。 |
| FAC | 建筑物、机场、公路、桥梁等 |
| 组织 | 公司、代理、机构等 |
| 产品 | 物品、车辆、食品等 （非服务。） |
| 事件 | 有名的飓风、战斗、战争、体育活动等。 |
| WORK_OF_ART | 书籍、歌曲等的标题。 |
| 法律 | 成为法律的已命名文件。 |
| 语言 | 任何命名语言。 |

**API格式**

```http
POST /services/v2/predict
```

**请求**

以下请求基于在有效载荷中提供的输入参数从文档中提取关键字。

有关所示输入参数的更多信息，请参阅有效负载示例下表。

此 [示例pdf](../pdf-files/simple-text.pdf) 文件在本文档中显示的示例中使用。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "test",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-ner:Service-1e9081c865214d1e8bace51dd918b5c0"
      },
      "sensei:inputs": {
        "documents": [
          {
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "application/pdf"
          }
        ]
      },
      "sensei:params": {
        "application-id": "1234",
        "min_key_phrase_length": 1,
        "max_key_phrase_length": 3,
        "top_n": 5,
        "last_semantic_unit_type": "concept"
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@simple-text.pdf'
```

**输入参数**

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `top_n` | 要返回的结果数。 0，返回所有结果。 与阈值结合使用时，返回的结果数将小于任一限制。 | 否 |
| `min_relevance` | 必须返回结果的分数阈值。 排除参数以返回所有结果。 | 否 |
| `min_key_phrase_length` | 关键短语中所需的最少词数。 | 否 |
| `max_key_phrase_length` | 关键短语中所需的最大词数。 | 否 |
| `last_semantic_unit_type` | 在分层响应中仅返回到给定级别的语义单元。 &quot;key_phrase&quot;仅返回关键短语，&quot;linked_entity&quot;仅返回关键短语及其相应的链接实体，而&quot;concept&quot;则返回关键短语、链接实体和概念。 | 否 |
| `entity_types` | 要作为关键短语返回的实体类型。 | 否 |

**文档对象**

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字符串 | - | - | - | 要从中提取关键短语的文档的预签名URL。 |
| `sensei:repoType` | 字符串 | - | - | HTTPS | 存储文档的存储库类型。 |
| `sensei:multipart_field_name` | 字符串 | - | - | - | 在将文档作为多部分参数传递时，请使用此参数，而不是使用预签名的url。 |
| `dc:format` | 字符串 | 是 | - | &quot;text/plain&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml.presentation&quot; | 在处理文档之前，将针对允许的输入编码类型检查文档编码。 |

**响应**

成功响应会返回一个JSON对象，该对象包含 `response` 数组。

```json
{
  [
  {
    "key_phrases": [
      {
        "name": "Canada",
        "type": "GPE",
        "relevance": 0.9525035277863068,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Canada",
          "id": "b27a82e6-e963-45de-add8-dc4f3f0dd399",
          "confidence": 1.0,
          "relevance": 0.9706433035237365,
          "concepts": [
            {
              "name": "Commonwealth realm",
              "relationship": "instance_of",
              "id": "f5354ab6-ad25-406a-b289-9209db0db8ea",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "sovereign state",
              "relationship": "instance_of",
              "id": "10c24191-beef-43cc-a823-c170f217fe12",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "dominion of the British Empire",
              "relationship": "instance_of",
              "id": "4ffabaee-e6ab-422d-b121-145dcdbcf427",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "country",
              "relationship": "instance_of",
              "id": "6e8f43cb-7e64-41fc-93b4-119adfe87926",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "North America",
              "relationship": "part_of",
              "id": "0f4b1f78-9681-414a-91c6-576ed643941a",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            }
          ]
        }
      },
      {
        "name": "Sherlock Homles",
        "type": "ENTITY_UNKNOWN_TYPE",
        "relevance": 0.9516463011782174,
        "confidence": 1.0,
        "linked_entity": null
      },
      {
        "name": "Albert Einstein",
        "type": "PERSON",
        "relevance": 0.95080732382989,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Albert Einstein",
          "id": "0fdb37f6-f575-4b4d-91e9-fbff57eae0ab",
          "confidence": 1.0,
          "relevance": 0.9695742180192723,
          "concepts": [
            {
              "name": "pedagogue",
              "relationship": "occupation",
              "id": "1439eb14-2988-43cc-865d-ad5a60d3ea62",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher of science",
              "relationship": "occupation",
              "id": "eefb9bbf-e617-4434-abb2-56b5853abd3a",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "university teacher",
              "relationship": "occupation",
              "id": "bb2c4745-4116-46ef-a122-c28c2f902026",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "science writer",
              "relationship": "occupation",
              "id": "5084431d-9073-45cb-be82-4a6898becd5b",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "non-fiction writer",
              "relationship": "occupation",
              "id": "57cc1f7b-5391-458b-9303-ec35b3ba01a4",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "patent examiner",
              "relationship": "occupation",
              "id": "d3f10fc5-ca81-4049-8c48-3d935552d9e7",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher",
              "relationship": "occupation",
              "id": "04d3cd32-68ad-4b71-9231-bdf3acfb09b2",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "scientist",
              "relationship": "occupation",
              "id": "dc8c068b-aa75-4ece-acd7-06fa304964fb",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "physicist",
              "relationship": "occupation",
              "id": "56ac942c-12a2-42c1-b10c-d1394a7971af",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "teacher",
              "relationship": "occupation",
              "id": "c70301bd-bcf4-47ab-b958-b983f0b0a6bd",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "human",
              "relationship": "instance_of",
              "id": "ead8a1d7-f901-44e6-b80f-63ebbbca4ffe",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "professor",
              "relationship": "occupation",
              "id": "c6d691f2-1e26-49fd-8481-58cb2d64d3e9",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "mathematician",
              "relationship": "occupation",
              "id": "23bf46db-a69a-4546-b18a-690a41144caa",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physics",
              "relationship": "field_of_work",
              "id": "d6c03027-4efd-49d6-a7e5-ac4994c9143e",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physicist",
              "relationship": "occupation",
              "id": "eedb6531-c2bf-4d05-af92-6f21751bc894",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "inventor",
              "relationship": "occupation",
              "id": "7baf322e-5913-4e2a-997a-90a039b0ff5c",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "writer",
              "relationship": "occupation",
              "id": "4c4c287c-0d83-4da3-b8c7-26df5adc9b33",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            }
          ]
        }
      },
      {
        "name": "Toronto",
        "type": "GPE",
        "relevance": 0.9370046727951885,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Toronto",
          "id": "762db630-b272-4828-b1af-e7c65334e1d3",
          "confidence": 1.0,
          "relevance": 0.9608202651283239,
          "concepts": [
            {
              "name": "provincial or territorial capital city in Canada",
              "relationship": "instance_of",
              "id": "d7447629-e940-43b1-a726-4ac3f675410c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city",
              "relationship": "instance_of",
              "id": "d9d95c34-a2ce-4098-bd9d-3616b85620a8",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "big city",
              "relationship": "instance_of",
              "id": "68275742-3451-40af-8f5a-84211953a438",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "single-tier municipality",
              "relationship": "instance_of",
              "id": "a0f67ef3-52bb-44d9-bc52-9059d37c6d0c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city with millions of inhabitants",
              "relationship": "instance_of",
              "id": "b08def76-4b71-4545-9efb-f4858aaf253d",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            }
          ]
        }
      },
      {
        "name": "vacation",
        "type": "KEY_PHRASE",
        "relevance": 0.933964522339908,
        "confidence": 1.0,
        "linked_entity": null
      }
    ],
    "detected_languages": [
      {
        "language": "en",
        "confidence": 0.9999951616458576
      }
    ],
    "word_count": 183
  }
]   
}
```
