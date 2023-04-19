---
keywords: Experience Platform；入门；内容；内容标记；颜色标记；颜色提取；
solution: Experience Platform
title: 内容标记API中的颜色标记
description: 当给定图像时，“颜色标记”服务可以计算像素颜色的直方图，并按主色对它们进行分段排序。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# 颜色标记

当给定图像时，颜色标记服务可以计算像素颜色的直方图，并按主色对它们进行分段。 图像像素中的颜色被分段为40种主要颜色，它们代表颜色谱。 然后，在这40种颜色中计算颜色值的直方图。 该服务有两个变体：

**颜色标记（完整图像）**

此方法可提取整个图像的颜色直方图。

**颜色标记（带有蒙版）**

该方法采用基于深度学习的前景提取器来识别前景中的对象。 一旦提取了前景对象，就在前景区域和背景区域以及整个图像的主导颜色上计算直方图。

**色调提取**

除了上述变体之外，您还可以配置服务以检索以下各项的色调直方图：

- 整体图像（使用完整图像变体时）
- 整体图像以及前景和背景区域（当将变体与蒙版结合使用时）

本文档所示的示例使用了下图：

![测试图像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v2/predict
```

**请求 — 完整图像变体**

以下示例请求使用全图像方法进行颜色标记，并根据有效载荷中提供的输入参数从图像中提取颜色。 有关所示输入参数的更多信息，请参阅有效负载示例下表。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**响应 — 完整图像变体**

成功的响应会返回提取颜色的详细信息。 每种颜色由 `feature_value` 键，其中包含以下信息：

- 颜色名称
- 此颜色相对于图像显示的百分比
- 颜色的RGB值

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`表示找到的颜色为白色，在图像的58.34%中找到，其平均RGB值为254、254、243。

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

请注意，此处的结果在“整体”图像区域中提取了颜色。

**请求 — 掩盖的图像变体**

以下示例请求使用掩码方法进行颜色标记。 可通过将 `enable_mask` 参数 `true` 中。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>[!NOTE]
>
>此外， `retrieve_tone` 参数也设置为 `true` 中。 这使我们能够在图像的整体、前景和背景区域中检索暖色调、中性色调和冷色调上的色调分布直方图。

**响应 — 掩盖的图像变体**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

除了整个图像中的颜色之外，您现在还可以看到前景区域和背景区域的颜色。 由于已为上述每个区域启用了色调检索，因此您还可以检索色调的直方图。

**输入参数**

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| `documents` | 数组(Document-Object) | 是 | - | 请参阅下文 | JSON元素列表，列表中每个项目表示一个文档。 |
| `top_n` | 数字 | 否 | 0 | 非负整数 | 要返回的结果数。 0，返回所有结果。 与阈值结合使用时，返回的结果数将少于任一限制。 |
| `min_coverage` | 数字 | 否 | 0.05 | 实数 | 需要返回结果的覆盖范围阈值。 Exclude（排除）参数以返回所有结果。 |
| `resize_image` | 数字 | 否 | True | True/False | 是否调整输入图像的大小。 默认情况下，在执行颜色提取之前，会先将图像大小调整为320*320像素。 出于调试目的，我们还可以允许代码在完整图像上运行，方法是将其设置为 `False`. |
| `enable_mask` | 数字 | 否 | False | True/False | 启用/禁用颜色提取 |
| `retrieve_tone` | 数字 | 否 | False | True/False | 启用/禁用音调提取 |

**文档对象**

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字符串 | - | - | - | 文档的预签名URL。 |
| `sensei:repoType` | 字符串 | - | - | HTTPS | 存储图像的存储库类型。 |
| `sensei:multipart_field_name` | 字符串 | - | - | - | 在将图像文件作为多部分参数传递时，请使用此参数，而不是使用预签名的URL。 |
| `dc:format` | 字符串 | 是 | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | 在处理之前，将针对允许的输入编码类型检查图像编码。 |