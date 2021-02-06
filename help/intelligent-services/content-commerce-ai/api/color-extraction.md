---
keywords: Experience Platform；入门；内容ai；商务ai；内容和商务ai；颜色提取；颜色提取
solution: Experience Platform, Intelligent Services
title: 内容和商务AI API中的颜色提取
topic: Developer guide
description: 当给定图像时，颜色提取服务可以计算像素颜色的直方图，并按主色将其排序为桶。
translation-type: tm+mt
source-git-commit: d10c00694b0a3b2a9da693bd59615b533cfae468
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---


# 颜色提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是测试版。文档可能会更改。

当给定图像时，颜色提取服务可以计算像素颜色的直方图，并按主色将其排序为桶。 图像像素中的颜色被嵌入到代表色谱的40种主要颜色中。 然后在这40种颜色中计算颜色值的直方图。 该服务有两个变体：

**颜色提取（完整图像）**

此方法提取整个图像上的颜色直方图。

**颜色提取（带蒙版）**

该方法采用基于深度学习的前景提取器来识别前景中的物体。 该模型在电子商务图像目录上进行培训。 一旦提取前景对象，就像之前描述的那样在主色上计算直方图。

本文档中显示的示例使用了以下图像：

![测试图像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下示例请求使用全图像方法进行颜色提取。

以下请求基于在有效负荷中提供的输入参数从图像提取颜色。 有关显示的输入参数的详细信息，请参阅示例有效负荷下表。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 使用对象。请在发出请求之前，检查您是否有正确的`analyzer_id`。 对于颜色提取服务，`analyzer_id` ID为：
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
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
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| 属性 | 描述 | 强制 |
| --- | --- | --- |
| `analyzer_id` | 您的请求部署在下面的[!DNL Sensei]服务ID。 此ID确定使用哪个[!DNL Sensei Content Frameworks]。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 已创建应用程序的ID。 | 是 |
| `data` | 包含JSON对象的数组。 数组中的每个对象都表示一个图像。 作为此数组的一部分传递的任何参数都将覆盖在`data`数组外指定的全局参数。 下表中概述的任何其余属性都可从`data`中覆盖。 | 是 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 要由颜色提取服务分析的内容。 在图像是请求主体一部分的事件下，使用curl命令中的`-F file=@<filename>`传递图像，将此参数保留为空字符串。 <br> 如果图像是S3上的文件，请传递已签名的url。当内容是请求主体的一部分时，列表数据元素应仅具有一个对象。 如果传递了多个对象，则只处理第一个对象。 | 是 |
| `content-type` | 用于指示输入是请求主体的一部分还是S3存储段的已签名URL。 此属性的默认值为`inline`。 | 否 |
| `encoding` | 输入图像的文件格式。 目前只能处理JPEG和PNG图像。 此属性的默认值为`jpeg`。 | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值`0`返回所有结果。 此属性的默认值为`0`。 | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用值`0`返回所有结果。 与`threshold`结合使用时，返回的结果数是任一限制集的较小者。 此属性的默认值为`0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 | 否 |
| `historic-metadata` | 可传递元数据的数组。 | 否 |

**响应**

成功的响应会返回提取颜色的详细信息。 每种颜色都由`feature_value`键表示，它包含以下信息：

- 颜色名称
- 此颜色相对于图像的显示百分比
- 颜色的RGB值

在下面的第一个示例对象中，`White,0.59,251,251,243`的`feature_value`表示找到的颜色为白色，在图像的59%中为白色，RGB值为251,251,243。

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| 属性 | 描述 |
| --- | --- |
| `content_id` | 在您的POST请求中上传的图像的名称。 |
| `feature_value` | 其对象包含具有相同属性名称的键的数组。 这些键包含一个字符串，它表示颜色名称、此颜色相对于在`content_id`中发送的图像的百分比以及颜色的RGB值。 |
