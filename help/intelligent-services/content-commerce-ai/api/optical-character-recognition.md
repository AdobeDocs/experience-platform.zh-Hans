---
keywords: OCR；文本存在；光学字符识别
solution: Experience Platform
title: 文本存在与光学字符识别
topic-legacy: Developer guide
description: 在内容和商务AI API中，文本存在/光学字符识别(OCR)服务可以指示给定图像中是否存在文本。 如果存在文本，则OCR可返回该文本。
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# 文本存在与光学字符识别

>[!NOTE]
>
>Content and Commerce AI是测试版。 文档可能会发生更改。

文本存在/光学字符识别(OCR)服务在给定图像时，可以指示图像中是否存在文本。 如果存在文本，则OCR可返回该文本。

本文档中显示的示例请求使用了下图：

![测试图像](../images/shef.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求根据有效载荷中提供的输入图像检查文本是否存在。 有关所示输入参数的更多信息，请参阅有效负载示例下表。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 中，将使用。 请检查您是否拥有 `analyzer_id` 之前。 请联系内容和商务AI测试版团队，以接收您的 `analyzer_id` 为此服务。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
    "parameters": {
      "application-id": "1234",
      "content-type": "inline",
      "encoding": "jpeg",
      "threshold": "0",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "0987",
        "content": "inline-image",
        "content-type": "inline",
        "encoding": "jpeg",
        "threshold": "0",
        "top-N": "0",
        "historic-metadata": [],
        "custom": {}
        }]
      }
    }]
  }'
```

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `analyzer_id` | 的 [!DNL Sensei] 请求部署在下的服务ID。 此ID确定 [!DNL Sensei Content Frameworks] 中，将使用。 对于自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，该对象在数组中的每个对象表示传递的一个图像。 作为此数组的一部分传递的任何参数都会覆盖在 `data` 数组。 下表中列出的任何其余属性都可以从中覆盖 `data`. | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求正文的一部分还是S3存储段的带符号的url。 此属性的默认值为 `inline`. | 否 |
| `encoding` | 输入图像的文件格式。 当前只能处理JPEG和PNG图像。 此属性的默认值为 `jpeg`. | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值 `0` 返回所有结果。 此属性的默认值为 `0`. | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用值 `0` 返回所有结果。 与 `threshold`，则返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`. | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 内容可以是原始图像（“内联”内容类型）。 <br> 如果内容是S3(“s3-bucket”content-type)上的文件，请传递带签名的URL。 | 是 |

**响应**

成功响应会返回在 `feature_value` 数组。 文本将从左到右读取并返回。 这意味着如果检测到“I loveAdobe”，则有效负载会在单独的对象中返回“I”、“love”和“Adobe”。 在对象中，您被赋予 `feature_name` 包含单词和 `feature_value` 包含该文本的置信度量度。

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
