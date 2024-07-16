---
keywords: 视觉相似度；视觉相似度；ccai api
solution: Experience Platform
title: 内容和Commerce AI API中的视觉相似度
description: 视觉相似性服务在给定图像时，自动从目录中找到视觉上相似的图像。
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# 视觉相似度

>[!NOTE]
>
>[!DNL Content and Commerce AI]处于Beta版。 文档可能会发生更改。

视觉相似性服务在给定图像时，自动从目录中找到视觉上相似的图像。

在本文档显示的示例请求中使用了以下图像：

![测试映像](../images/Query_Image.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求根据有效负荷中提供的输入参数，从目录中检索视觉上相似的图像。 有关显示的输入参数的更多信息，请参阅示例有效负载下方的表。

>[!CAUTION]
>
>`analyzer_id`确定使用哪个[!DNL Sensei Content Framework]。 在提出请求之前，请检查您是否拥有适当的`analyzer_id`。 请联系内容和Commerce AI测试版团队，接收您关于此服务的`analyzer_id`。

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
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
      }
    ]
}'
```

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `analyzer_id` | 您的请求部署所在的[!DNL Sensei]服务ID。 此ID确定使用了[!DNL Sensei Content Frameworks]中的哪一个。 对于自定义服务，请联系内容和Commerce AI团队以设置自定义ID。 | 是 |
| `application-id` | 您创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，该数组中的每个对象都表示一个图像。 作为此数组的一部分传递的任何参数都将覆盖`data`数组外部指定的全局参数。 此表格中下面列出的任何剩余属性都可以从`data`中覆盖。 | 是 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递此ID，则会分配自动生成的ID。 | 否 |
| `content` | 视觉相似度服务分析内容。 如果图像是请求正文的一部分，请在curl命令中使用`-F file=@<filename>`传递图像，并将此参数保留为空字符串。 <br>如果图像是S3上的文件，请传递已签名的URL。 当内容是请求正文的一部分时，数据元素列表应仅有一个对象。 如果传递了多个对象，则仅处理第一个对象。 | 是 |
| `content-type` | 用于指示输入是请求正文的一部分还是S3存储桶的已签名URL。 此属性的默认值为`inline`。 | 否 |
| `encoding` | 输入图像的文件格式。 当前只能处理JPEG和PNG图像。 此属性的默认值为`jpeg`。 | 否 |
| `threshold` | 分数阈值（0到1），超过该阈值需要返回结果。 使用值`0`返回所有结果。 此属性的默认值为`0`。 | 否 |
| `top-N` | 要返回的结果数（不能为负整数）。 使用值`0`返回所有结果。 当与`threshold`一起使用时，返回的结果数是设置的任一限制中的较小值。 此属性的默认值为`0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 | 否 |
| `historic-metadata` | 可传递元数据的数组。 | 否 |

**响应**

成功的响应返回一个`response`数组，该数组包含在目录中找到的所有视觉上相似的图像的`feature_value`和`feature_name`。

以下示例响应中返回了视觉上相似的图像，如下所示：

![相似图像](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
