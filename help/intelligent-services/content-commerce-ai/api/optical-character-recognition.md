---
keywords: OCR;text presence;optical character recognition
solution: Experience Platform, Intelligent Services
title: 光学字符识别
topic: Developer guide
description: 给定图像时，文本存在／光学字符识别(OCR)服务可指示图像中是否存在文本。 如果存在文本，OCR可以返回文本
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 3%

---


# 文本存在与光学字符识别

>[!NOTE]
>
>Content and Commerce AI为测试版。 文档可能会更改。

给定图像时，文本存在／光学字符识别(OCR)服务可指示图像中是否存在文本。 如果存在文本，OCR可返回文本。

此文档中显示的示例请求使用了以下图像：

![测试图像](../images/shef.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求根据有效负荷中提供的输入图像检查文本是否存在。 有关显示的输入参数的详细信息，请参阅示例有效负荷下表。

>[!CAUTION]
>
>`analyzer_id` 确定使 [!DNL Sensei Content Framework] 用哪个。 请在提出请求前检查 `analyzer_id` 您是否有适当的。 请与内容和商务AI测试版团队联系，以接 `analyzer_id` 收您的此服务。

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

| 属性 | 描述 | 强制 |
| --- | --- | --- |
| `analyzer_id` | 您 [!DNL Sensei] 的请求所部署的服务ID。 此ID决定使用哪 [!DNL Sensei Content Frameworks] 个ID。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 包含JSON对象的数组，数组中的每个对象表示传递的一个图像。 作为此数组的一部分传递的任何参数都将覆盖在数组外部指定的全局 `data` 参数。 此表中概述的任何其余属性都可以从中覆盖 `data`。 | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求主体的一部分还是S3存储段的已签名URL。 此属性的默认值为 `inline`。 | 否 |
| `encoding` | 输入图像的文件格式。 目前只能处理JPEG和PNG图像。 此属性的默认值为 `jpeg`。 | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用该值 `0` 返回所有结果。 此属性的默认值为 `0`。 | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用该值 `0` 返回所有结果。 与一起使用时， `threshold`返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 内容可以是原始图像（“内联”内容类型）。 <br> 如果内容是S3(&#39;s3-bucket&#39; content-type)上的文件，请传递已签名的URL。 | 是 |

**响应**

成功的响应会返回在数组中检测到的 `feature_value` 文本。 文本将从左到右读取并返回。 这意味着，如果检测到“我喜欢Adobe”，则有效负荷在单独的对象中返回“I”、“love”和“Adobe”。 在对象中，您会得到一 `feature_name` 个包含该单词的词 `feature_value` 和一个包含该文本的置信度量的词。

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
