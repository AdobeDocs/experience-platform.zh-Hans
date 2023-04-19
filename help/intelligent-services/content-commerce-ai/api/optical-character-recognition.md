---
keywords: OCR；文本存在；光学字符识别
solution: Experience Platform
title: 文本存在与光学字符识别
description: 在内容标记API中，文本存在/光学字符识别(OCR)服务可指示给定图像中是否存在文本。 如果存在文本，则OCR可返回该文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# 文本存在与光学字符识别

文本存在/光学字符识别(OCR)服务在给定图像时，可以指示图像中是否存在文本。 如果存在文本，则OCR可返回该文本。

本文档中显示的示例请求使用了下图：

![示例图像](../images/sample_image.png)

**API格式**

```http
POST /services/v2/predict
```

**请求**

以下请求根据有效载荷中提供的输入图像检查文本是否存在。 有关所示输入参数的更多信息，请参阅有效负载示例下表。

使用内联图像执行：

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**响应**

成功响应会返回在 `tags` 列表。 如果特定图像中没有文本， `is_text_present` 表示0和 `tags` 为空列表。

[结果0，结果1, ...]:每个输入文档的响应列表。 每个结果都有一个带键的dict :

1. request_element_id:对应于此响应的输入文件的索引，对于请求文档列表中的第一个图像为0，对于下一个图像为1，依此类推。
2. 标记：词典列表中，每个词典有两个键：文本，该文本是从图像中识别出的单词，以及相关性，该文本计算为与全图像相比，所提取文本的边界框的面积的分数。 0.01将翻译成至少占图像1%的文本。
3. is_text_present:0或1，具体取决于图像中是否存在文本。 如果标记为0，则列表为空。

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**请求**

以下请求根据有效载荷中提供的输入图像检查文本是否存在。 有关所示输入参数的更多信息，请参阅有效负载示例下表。

通过URL执行：

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `documents` | JSON元素列表，列表中每个项目表示一个图像。 作为此列表的一部分传递的任何参数都会覆盖在列表外部为相应列表元素指定的全局参数。 | 是 |
| `sensei:multipart_field_name` | field_name，从中读取输入文件路径。 | 是 |
| `repo:path` | 预签名的图像资产URL。 | 是 |
| `sensei:repoType` | &quot;HTTP&quot;（对于presigned-url）。 | 否 |
| `dc:format` | 输入图像的编码格式。 图像编码仅允许使用jpeg、jpg、png和tiff等图像格式。 dc:format与允许的格式匹配。 | 否 |
| `correct_with_dictionary` | 是否用英语词典来更正单词？ 如果未打开此设置，则可能会识别非英语单词。 默认值为True:打开。) 请注意，打开字典时，不必总是得到一个英文单词。 我们会尝试更正它，但如果它无法在一定的编辑距离内完成，我们会返回原始单词。 | 否 |
| `filter_with_dictionary` | 是否过滤词语以仅包含来自英语词典的词语？ 如果启用此设置，则返回的词语将始终属于包含47万个词的大型英语。 | 否 |
| `min_probability` | 可识别词语的最小概率是多少？ 服务仅返回从图像中提取的概率大于min_probability的词。 默认值为0.2。 | 否 |
| `min_relevance` | 可识别词语的最低相关性是多少？ 服务仅返回从图像中提取的与min_relevace有较大相关性的词语。 默认值设置为0.01。与全图相比，相关性计算为提取文本边界框的面积比。 0.01将翻译成至少占图像1%的文本。 | 否 |

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字符串 | - | - | - | 需要从中提取文本的图像的预签名URL。 |
| `sensei:repoType` | 字符串 | - | - | HTTPS | 存储图像的存储库类型。 |
| `sensei:multipart_field_name` | 字符串 | - | - | - | 在将图像作为多部分参数传递时，请使用此参数，而不是使用预签名的url。 |
| `dc:format` | 字符串 | 是 | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | 在处理之前，将针对允许的输入编码类型检查图像编码。 |