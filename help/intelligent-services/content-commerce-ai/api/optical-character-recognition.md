---
keywords: OCR；文本存在；光学字符识别
solution: Experience Platform
title: 文本存在和光学字符识别
description: 在内容标记API中，文本存在/光学字符识别(OCR)服务可以指示文本是否在给定的图像中存在。 如果文本存在，则OCR可以返回文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# 文本存在和光学字符识别

文本存在/光学字符识别(OCR)服务在给定图像时，可以指示图像中是否存在文本。 如果文本存在，则OCR可以返回文本。

以下图像已用于本文档中所示的示例请求：

![示例图像](../images/sample_image.png)

**API格式**

```http
POST /services/v2/predict
```

**请求**

以下请求根据有效负载中提供的输入图像检查文本是否存在。 有关显示的输入参数的更多信息，请参阅示例有效负载下表。

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

成功的响应会返回在中检测到的文本 `tags` 请求中传递的每个图像的列表。 如果某个图像中没有文本， `is_text_present` 为0且 `tags` 是一个空列表。

[result0， result1， ...]：每个输入文档的响应列表。 每个结果都是一个带键的指令：

1. request_element_id：此响应的输入文件对应的索引，0表示请求文档列表中的第一个图像，1表示下一个图像，依此类推。
2. 标记：词典列表，每个词典有两个键：文本（从图像识别的单词）和相关性（计算为提取文本边界框区域相对于完整图像的分数）。 0.01将翻译为至少占图像1%的文本。
3. is_text_present： 0或1，具体取决于图像中存在文本。 如果标记为0，则列表为空。

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
          "relevance": 0.05604639115920341
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**请求**

以下请求根据有效负载中提供的输入图像检查文本是否存在。 有关显示的输入参数的更多信息，请参阅示例有效负载下表。

使用URL执行：

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
| `documents` | JSON元素列表，列表中的每一项代表一个图像。 作为此列表的一部分传递的任何参数，都会覆盖在列表外部为相应列表元素指定的全局参数。 | 是 |
| `sensei:multipart_field_name` | 从中读取输入文件路径的field_name。 | 是 |
| `repo:path` | 指向图像资源的预签名URL。 | 是 |
| `sensei:repoType` | &quot;HTTP&quot;（表示预签名的url）。 | 否 |
| `dc:format` | 输入图像的编码格式。 图像编码仅允许使用图像格式，如jpeg、jpg、png和tiff。 dc：format与允许的格式匹配。 | 否 |
| `correct_with_dictionary` | 要不要用英语字典来更正这些字词？ 如果未打开此功能，则可能会识别出非英语单词。 默认值为True：打开。) 请注意，打开词典时，没有必要总是得到一个英文单词。 我们尝试更正它，但是如果在一定编辑距离内无法更正它，我们返回原始单词。 | 否 |
| `filter_with_dictionary` | 是否过滤单词以仅包含英语词典中的单词？ 如果启用此项，则返回的单词将始终属于大型英语，包含47万个单词。 | 否 |
| `min_probability` | 被识别单词的最小概率是多少？ 服务只返回从图像中提取的概率大于min_probability的单词。 缺省值设置为0.2。 | 否 |
| `min_relevance` | 对于已识别的单词，最小相关性是什么？ 服务只返回从图像中提取并且相关性大于min_relevance的单词。 缺省值设置为0.01。相关性计算为提取的文本边界框区域与完整图像相比所占区域的分数。 0.01将翻译为至少占图像1%的文本。 | 否 |

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字符串 | - | - | - | 需要从中提取文本的图像预签名URL。 |
| `sensei:repoType` | 字符串 | - | - | HTTPS | 存储图像的存储库的类型。 |
| `sensei:multipart_field_name` | 字符串 | - | - | - | 将图像作为多部分参数传递时，请使用此方法，而不是使用预签名URL。 |
| `dc:format` | 字符串 | 是 | - | &quot;image/jpg&quot;， <br>&quot;image/jpeg&quot;， <br>&quot;image/png&quot;， <br>&quot;image/tiff&quot; | 在处理之前，将根据允许的输入编码类型检查图像编码。 |