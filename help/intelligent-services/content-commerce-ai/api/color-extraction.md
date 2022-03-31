---
keywords: Experience Platform；快速入门；内容ai；商务ai；内容和商务ai；颜色提取；颜色提取
solution: Experience Platform
title: 内容和商务AI API中的颜色提取
topic-legacy: Developer guide
description: 当给定图像时，颜色提取服务可以计算像素颜色的直方图，并按主色对它们进行分段。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# 颜色提取

>[!NOTE]
>
>[!DNL Content and Commerce AI] 是测试版。 文档可能会发生更改。

当给定图像时，颜色提取服务可以计算像素颜色的直方图，并按主色对它们进行分段。 图像像素中的颜色被分段为40种主要颜色，它们代表颜色谱。 然后，在这40种颜色中计算颜色值的直方图。 该服务有两个变体：

**颜色提取（完整图像）**

此方法可提取整个图像的颜色直方图。

**颜色提取（带有蒙版）**

该方法采用基于深度学习的前景提取器对前景中的目标进行识别。 该模型在电子商务图像目录上进行培训。 一旦提取前景对象，就像先前描述的那样在主色上计算直方图。

本文档所示的示例使用了下图：

![测试图像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下示例请求使用全图像方法进行颜色提取。

以下请求基于有效载荷中提供的输入参数从图像中提取颜色。 有关所示输入参数的更多信息，请参阅有效负载示例下表。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 中，将使用。 请检查您是否拥有 `analyzer_id` 之前。 对于颜色提取服务， `analyzer_id` ID是：
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

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `analyzer_id` | 的 [!DNL Sensei] 请求部署在下的服务ID。 此ID确定 [!DNL Sensei Content Frameworks] 中，将使用。 对于自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 包含JSON对象的数组。 数组中的每个对象都表示一个图像。 作为此数组的一部分传递的任何参数都会覆盖在 `data` 数组。 下表中列出的任何其余属性都可以从中覆盖 `data`. | 是 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递，则会分配一个自动生成的ID。 | 否 |
| `content` | 颜色提取服务要分析的内容。 如果图像是请求正文的一部分，请使用 `-F file=@<filename>` 在用于传递图像的curl命令中，将此参数保留为空字符串。 <br> 如果图像是S3上的文件，请传递带签名的url。 当内容是请求正文的一部分时，数据元素列表应该只有一个对象。 如果传递了多个对象，则仅处理第一个对象。 | 是 |
| `content-type` | 用于指示输入是请求正文的一部分还是S3存储段的带符号的url。 此属性的默认值为 `inline`. | 否 |
| `encoding` | 输入图像的文件格式。 当前只能处理JPEG和PNG图像。 此属性的默认值为 `jpeg`. | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值 `0` 返回所有结果。 此属性的默认值为 `0`. | 否 |
| `top-N` | 要返回的结果数（不能是负整数）。 使用值 `0` 返回所有结果。 与 `threshold`，则返回的结果数是任一限制集中的较小者。 此属性的默认值为 `0`. | 否 |
| `custom` | 要传递的任何自定义参数。 | 否 |
| `historic-metadata` | 可以传递元数据的数组。 | 否 |

**响应**

成功的响应会返回提取颜色的详细信息。 每种颜色由 `feature_value` 键，其中包含以下信息：

- 颜色名称
- 此颜色相对于图像显示的百分比
- 颜色的RGB值

在下面的第一个示例对象中， `feature_value` of `White,0.59,251,251,243` 表示找到的颜色为白色，在图像的59%中找到白色，其RGB值为251,251,243。

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
| `feature_value` | 其对象包含具有相同属性名称的键的数组。 这些键包含一个表示颜色名称的字符串，此颜色相对于在 `content_id`、和颜色的RGB值。 |
