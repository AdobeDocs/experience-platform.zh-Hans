---
keywords: Experience Platform；开发人员指南；端点；数据科学工作区；热门主题；
solution: Experience Platform
title: Sensei机器学习API指南附录
topic-legacy: Developer guide
description: 以下部分提供了有关Sensei机器学习API的各种功能的参考信息。
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API指南附录

以下各节提供了[!DNL Sensei Machine Learning] API的各种功能的参考信息。

## 查询资产检索参数{#query}

[!DNL Sensei Machine Learning] API支持检索资产时的查询参数。 下表介绍了可用查询参数及其用法：

| 查询参数 | 描述 | 默认值 |
| --------------- | ----------- | ------- |
| `start` | 指示分页的起始索引。 | `start=0` |
| `limit` | 指示要返回的最大结果数。 | `limit=25` |
| `orderby` | 指示按优先级顺序进行排序的属性。 在属性名称前加入虚线(**-**)以按降序排序，否则结果按升序排序。 | `orderby=created` |
| `property` | 指示要返回对象必须满足的比较表达式。 | `property=deleted==false` |

>[!NOTE]
>
>组合多个查询参数时，必须用&amp;符号(**&amp;**)分隔。

## Python CPU和GPU配置{#cpu-gpu-config}

Python引擎能够在CPU或GPU之间进行选择以用于其培训或评分，并在[MLInstance](./mlinstances.md)上定义为任务规范(`tasks.specification`)。

以下是一个示例配置，它指定使用CPU进行培训，使用GPU进行评分：

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
>`cpus`和`gpus`的值不表示CPU或GPU的数量，而表示物理计算机的数量。 这些值可以`"1"`使用，否则将引发异常。

## PySpark和Spark资源配置{#resource-config}

Spark Engine能够修改计算资源，用于培训和评分。 下表介绍了这些资源：

| 资源 | 描述 | 类型 |
| -------- | ----------- | ---- |
| driverMemory | 驱动程序的内存(MB) | int |
| driverCores | 驱动程序使用的核数 | int |
| executorMemory | 执行器的存储器(MB) | int |
| executorCores | 执行器使用的核数 | int |
| numExecutors | 执行者数 | int |

可以在[MLInstance](./mlinstances.md)上指定资源，作为(A)单个培训或评分参数，或(B)其他规范对象(`specification`)中的资源。 例如，以下资源配置对于培训和评分都是相同的：

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
