---
keywords: Experience Platform；快速入門；內容；內容標籤；色彩標籤；色彩擷取；
solution: Experience Platform
title: 內容標籤API中的顏色標籤
description: 指定影像時，「顏色標籤」服務可以計算畫素顏色的色階分佈圖，並依主色排序成貯體。
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# 顏色標籤

指定影像時，色彩標籤服務可以計算畫素顏色的色階分佈圖，並按主色排序成色桶。 影像畫素中的顏色會分成40種主要顏色，這些顏色代表色彩光譜。 然後計算這40種顏色中的顏色值色階分佈圖。 此服務有兩種變體：

**顏色標籤（完整影像）**

此方法會擷取整個影像的色階分佈圖。

**顏色標籤（使用遮色片）**

此方法會使用深度學習型前景擷取器來識別前景中的物件。 提取前景物件後，會針對前景和背景區域的主要顏色以及整個影像計算色階分佈圖。

**色調擷取**

除了上述的變體之外，您還可以設定服務來擷取色調長條圖：

- 整體影像（使用完整影像變體時）
- 整體影像、前景和背景區域（搭配遮色片使用變體時）

本檔案所示範例中使用了下列影像：

![測試影像](../images/QQAsset1.jpg)

**API格式**

```http
POST /services/v2/predict
```

**請求 — 完整影像變體**

以下範例要求使用完整影像方法進行色彩標籤，並根據承載中提供的輸入引數從影像擷取顏色。 請參閱裝載範例下表，以瞭解有關所示輸入引數的詳細資訊。

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

**回應 — 完整影像變體**

成功的回應會傳回所擷取顏色的詳細資料。 每種顏色由 `feature_value` 索引鍵，其中包含下列資訊：

- 顏色名稱
- 此顏色相對於影像出現的百分比
- 色彩的RGB值

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`表示找到的顏色是白色，佔影像的58.34%，平均RGB值為254、254、243。

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

請注意，這裡的結果已在「整體」影像區域上擷取顏色。

**請求 — 遮罩的影像變體**

下列範例要求使用遮罩方法來標籤顏色。 這可透過設定 `enable_mask` 引數至 `true` 在請求中。

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
>此外， `retrieve_tone` 引數也設為 `true` 在上述請求中。 這可讓我們在影像的整體、前景和背景區域中，擷取暖色、中性色和冷色的色調分佈色階分佈圖。

**回應 — 遮罩的影像變體**

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

除了來自整個影像的顏色外，您現在也可以看到來自前景和背景區域的顏色。 由於已針對上述每個區域啟用色調擷取，因此您也可以擷取色調的色階分佈圖。

**輸入引數**

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| `documents` | 陣列(Document-Object) | 是 | - | 請參閱下文 | JSON元素清單，清單中的每個專案代表一個檔案。 |
| `top_n` | 数字 | 否 | 0 | 非負整數 | 要傳回的結果數。 0，傳回所有結果。 當與臨界值搭配使用時，傳回的結果數將小於任一限制。 |
| `min_coverage` | 数字 | 否 | 0.05 | 實數 | 覆蓋範圍的臨界值，超過此值後需要傳回結果。 排除引數以傳回所有結果。 |
| `resize_image` | 数字 | 否 | True | 真/假 | 是否要調整輸入影像的大小。 依照預設，在執行色彩擷取之前，影像會調整為320*320畫素。 為了偵錯目的，我們也可以將設定為，讓程式碼在完整影像上執行 `False`. |
| `enable_mask` | 数字 | 否 | False | 真/假 | 啟用/停用色彩擷取 |
| `retrieve_tone` | 数字 | 否 | False | 真/假 | 啟用/停用色調提取 |

**檔案物件**

| 名称 | 数据类型 | 必需 | 默认 | 值 | 描述 |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | 字符串 | - | - | - | 檔案的預先簽署URL。 |
| `sensei:repoType` | 字符串 | - | - | HTTPS | 儲存影像的存放庫型別。 |
| `sensei:multipart_field_name` | 字符串 | - | - | - | 將影像檔案作為多部分引數傳遞時，請使用此選項，而不使用預先簽署的URL。 |
| `dc:format` | 字符串 | 是 | - | &quot;image/jpg&quot;，<br>&quot;image/jpeg&quot;，<br>&quot;image/png&quot;，<br>&quot;image/tiff&quot; | 影像編碼在處理前會根據允許的輸入編碼型別進行檢查。 |