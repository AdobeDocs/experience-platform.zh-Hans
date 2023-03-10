---
keywords: Experience Platform；快速入门；content ai；commerce ai；内容标记；颜色标记；颜色提取；
solution: Experience Platform
title: 内容标记API中的颜色标记
description: 当给定图像时，颜色标记服务可以计算像素颜色的直方图，并按主颜色将它们排序为分段。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 颜色标记

当给定图像时，颜色标记服务可以计算像素颜色的直方图，并按主颜色将它们排序成存储桶。 图像像素中的颜色被分成40种代表颜色光谱的主要颜色。 然后在这40种颜色中计算颜色值的直方图。 该服务有两种变体：

**颜色标记（完整图像）**

此方法提取整个图像的颜色直方图。

**颜色标记（使用蒙版）**

该方法使用基于深度学习的前台提取器来识别前台对象。 模型基于电子商务图像目录进行训练。 一旦提取了前景对象，就如前文所述在主要颜色上计算直方图。

在本文档中显示的示例中使用了以下图像：

![测试图像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v2/predict
```

**请求**

以下示例请求使用全图像方法进行颜色标记。

以下请求基于在有效负荷中提供的输入参数从图像提取颜色。 有关显示的输入参数的更多信息，请参阅示例有效负载下表。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
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
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `application-id` | 您创建的应用程序的ID。 | 是 |
| `documents` | JSON元素列表，列表中的每一项代表一个文档。 | 是 |
| `top_n` | 要返回的结果数（不能为负整数）。 使用值 `0` 以返回所有结果。 当与结合使用时 `threshold`，则返回的结果数是设置的任一限制中的较小值。 此属性的默认值为 `0`. | 否 |
| `min_coverage` | 覆盖阈值，超过该阈值需要返回结果。 排除参数可返回所有结果。 | 否 |
| `resize_image` | 指示是否调整输入图像的大小。 默认情况下，在执行颜色标记之前，图像大小将调整为320*320像素。 出于调试目的，我们也可以通过将它设置为False来允许代码在完整映像上运行。 | 否 |
| `enable_mask` | 启用/禁用蒙版中的颜色标记。 | 否 |

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字符串 | - | - | - | 要从中提取关键短语的文档的预签名URL。 |
| `sensei:repoType` | 字符串 | - | - | HTTPS | 存储图像的存储库的类型。 |
| `sensei:multipart_field_name` | 字符串 | - | - | - | 在将图像文件作为多部分参数传递时，请使用此方法，而不是使用预签名URL。 |
| `dc:format` | 字符串 | 是 | - | &quot;image/jpg&quot;， <br> &quot;image/jpeg&quot;， <br>&quot;image/png&quot;， <br>&quot;image/tiff&quot; | 在处理之前，将根据允许的输入编码类型检查图像编码。 |

**响应**

成功的响应将返回提取颜色的详细信息。 每种颜色表示为 `feature_value` 键，包含以下信息：

- 颜色名称
- 此颜色相对于图像显示的百分比
- 颜色的RGB

在下面的第一个示例对象中， `feature_value` 之 `Mud_Green,0.069,102,72,95` 泥绿是图像的6.9%，其RGB值为102,72,95。

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
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
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
