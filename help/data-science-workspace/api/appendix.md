---
keywords: Experience Platform；开发人员指南；端点；数据科学Workspace；热门主题；
solution: Experience Platform
title: Sensei机器学习API指南附录
description: 以下部分提供Sensei机器学习API各种功能的参考信息。
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning] API指南附录

以下部分提供[!DNL Sensei Machine Learning] API各种功能的参考信息。

## 用于资源检索的查询参数 {#query}

[!DNL Sensei Machine Learning] API为检索资产的查询参数提供支持。 下表描述了可用的查询参数及其用法：

| 查询参数 | 描述 | 默认值 |
| --------------- | ----------- | ------- |
| `start` | 指示分页的开始索引。 | `start=0` |
| `limit` | 指示要返回的最大结果数。 | `limit=25` |
| `orderby` | 指示用于按优先级排序的属性。 在属性名称前添加一个破折号(**-**)以按降序排序，否则结果将按升序排序。 | `orderby=created` |
| `property` | 指示对象必须满足才能返回的比较表达式。 | `property=deleted==false` |

>[!NOTE]
>
>组合多个查询参数时，必须用&amp;符号(**&amp;**)分隔。

## Python CPU和GPU配置 {#cpu-gpu-config}

Python引擎能够在CPU或GPU之间进行选择，用于训练或评分，并在[MLInstance](./mlinstances.md)上定义为任务规范(`tasks.specification`)。

以下是一个示例配置，它指定使用CPU进行训练，使用GPU进行评分：

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
>`cpus`和`gpus`的值不表示CPU或GPU的数量，而是表示物理计算机的数量。 这些值许可为`"1"`，否则将引发异常。

## PySpark和Spark资源配置 {#resource-config}

Spark引擎能够修改计算资源以进行训练和评分。 下表介绍了这些资源：

| 资源 | 描述 | 类型 |
| -------- | ----------- | ---- |
| driveremory | 驱动程序的内存(MB) | int |
| driverCores | 驱动程序使用的内核数 | int |
| executorMemory | 执行器的内存(MB) | int |
| executorCores | 执行器使用的内核数 | int |
| numExecuters | 执行者数量 | int |

可在[MLInstance](./mlinstances.md)上将资源指定为(A)单独的训练或评分参数，或(B)在附加规范对象(`specification`)中。 例如，以下资源配置对于训练和评分都是相同的：

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
