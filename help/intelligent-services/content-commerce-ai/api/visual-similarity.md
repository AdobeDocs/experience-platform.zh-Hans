---
keywords: Visual similarity;visual similarity;ccai api
solution: Experience Platform, Intelligent Services
title: 视觉相似性
topic: Developer guide
description: 当给定图像时，视觉相似性服务会自动从目录中找到视觉相似的图像。
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---


# 视觉相似性

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是测试版。 文档可能会更改。

当给定图像时，视觉相似性服务会自动从目录中找到视觉相似的图像。

此文档中显示的示例请求使用了以下图像：

![测试图像](../images/Query_Image.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求基于有效负荷中提供的输入参数从目录检索视觉上相似的图像。 有关显示的输入参数的详细信息，请参阅示例有效负荷下表。

>[!CAUTION]
>
>`analyzer_id` 确定使 [!DNL Sensei Content Framework] 用哪个。 请在提出请求前检查 `analyzer_id` 您是否有适当的。 请与内容和商务AI测试版团队联系，以接 `analyzer_id` 收您的此服务。

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

| 属性 | 描述 | 强制 |
| --- | --- | --- |
| `analyzer_id` | 您 [!DNL Sensei] 的请求所部署的服务ID。 此ID决定使用哪 [!DNL Sensei Content Frameworks] 个ID。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 已创建应用程序的ID。 | 是 |
| `data` | 包含JSON对象的数组，数组中的每个对象都表示一个图像。 作为此数组的一部分传递的任何参数都将覆盖在数组外部指定的全局 `data` 参数。 此表中概述的任何其余属性都可以从中覆盖 `data`。 | 是 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 视觉相似性服务要分析的内容。 在图像是请求主体一部分的事件中， `-F file=@<filename>` 在curl命令中使用以传递图像，将此参数保留为空字符串。 <br> 如果图像是S3上的文件，请传递已签名的url。 当内容是请求主体的一部分时，列表数据元素应仅具有一个对象。 如果传递了多个对象，则只处理第一个对象。 | 是 |
| `content-type` | 用于指示输入是请求主体的一部分还是S3存储段的已签名URL。 此属性的默认值为 `inline`。 | 否 |
| `encoding` | 输入图像的文件格式。 目前只能处理JPEG和PNG图像。 此属性的默认值为 `jpeg`。 | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用该值 `0` 返回所有结果。 此属性的默认值为 `0`。 | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用该值 `0` 返回所有结果。 与一起使用时， `threshold`返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 | 否 |
| `historic-metadata` | 可传递元数据的数组。 | 否 |

**响应**

成功的响应会返回 `response` 一个数组，该数组 `feature_value` 包含 `feature_name` 目录中找到的每个视觉上相似的图像。

以下示例响应中返回了以下视觉效果相似的图像：

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

