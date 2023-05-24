---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；
solution: Experience Platform
title: Sensei Machine Learning API指南附錄
description: 以下小節提供Sensei Machine Learning API各種功能的參考資訊。
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API指南附錄

以下各節提供各種功能的參考資訊 [!DNL Sensei Machine Learning] API。

## 用於資產擷取的查詢引數 {#query}

此 [!DNL Sensei Machine Learning] API支援擷取資產的查詢引數。 下表說明可用的查詢引數及其用途：

| 查询参数 | 描述 | 默认值 |
| --------------- | ----------- | ------- |
| `start` | 表示分頁的起始索引。 | `start=0` |
| `limit` | 表示要傳回的結果數目上限。 | `limit=25` |
| `orderby` | 指示要用於依優先順序排序的屬性。 包含破折號(**-**)，然後依遞減順序排序，否則結果會依遞增順序排序。 | `orderby=created` |
| `property` | 表示物件必須滿足才能傳回的比較運算式。 | `property=deleted==false` |

>[!NOTE]
>
>合併多個查詢引數時，必須以&amp;符號(**和**)。

## Python CPU和GPU設定 {#cpu-gpu-config}

Python引擎能夠選擇CPU或GPU，用於訓練或評分目的，並定義於 [MLInstance](./mlinstances.md) 作為任務規格(`tasks.specification`)。

以下是指定使用CPU進行訓練，並使用GPU進行評分的設定範例：

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>的值 `cpus` 和 `gpus` 並不表示CPU或GPU的數量，而是表示實體機器的數量。 這些值是可允許的 `"1"` 否則和會擲回例外狀況。

## PySpark和Spark資源設定 {#resource-config}

Spark引擎能夠修改運算資源，以用於訓練和評分目的。 下表說明這些資源：

| 资源 | 描述 | 类型 |
| -------- | ----------- | ---- |
| driverMemory | 驅動程式的記憶體(MB) | int |
| driverCores | 驅動程式使用的核心數目 | int |
| executorMemory | 執行器的記憶體(MB) | int |
| executorCores | 執行程式使用的核心數目 | int |
| numExecutors | 執行者數量 | int |

資源可在 [MLInstance](./mlinstances.md) 作為(A)個別訓練或評分引數，或(B)其他規格物件內(`specification`)。 例如，下列資源設定對於訓練和評分都是相同的：

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
