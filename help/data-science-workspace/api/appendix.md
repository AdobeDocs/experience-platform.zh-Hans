---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 附录
topic: Developer guide
translation-type: tm+mt
source-git-commit: 2940f69d193ff8a4ec6ad4a58813b5426201ef45

---


# 附录

以下各节提供了有关Sensei机器学习API的各种功能的参考信息。

## 查询资产检索参数 {#query}

Sensei Machine Learning API支持检索资源时查询参数。 下表介绍了可用的查询参数及其用法：

| 查询参数 | 描述 | 默认值 |
| --------------- | ----------- | ------- |
| `start` | 指示分页的起始索引。 | `start=0` |
| `limit` | 指示要返回的最大结果数。 | `limit=25` |
| `orderby` | 指示按优先级顺序进行排序的属性。 在属性名称前加&#x200B;**入虚线(-**)以按降序排序，否则，结果将按升序排序。 | `orderby=created` |
| `property` | 指示对象要返回必须满足的比较表达式。 | `property=deleted==false` |

>[!NOTE] 组合多个查询参数时，必须用&amp;符分隔(**&amp;**)。

## Python CPU和GPU配置 {#cpu-gpu-config}

Python Engine能够为其培训或评分目的在CPU或GPU之间进行选择，并在 [MLI实例中定义为任务规范](./mlinstances.md) (`tasks.specification`)。

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

>[!NOTE] 和的值 `cpus` 不表 `gpus` 示CPU或GPU的数量，而是表示物理计算机的数量。 这些值是可能的， `"1"` 否则将引发异常。

## PySpark和Spark资源配置 {#resource-config}

Spark Engine能够修改计算资源以用于培训和评分。 下表介绍了这些资源：

| 资源 | 描述 | 类型 |
| -------- | ----------- | ---- |
| driverMemory | 驱动程序的内存(MB) | int |
| driverCores | 驱动程序使用的内核数 | int |
| executorMemory | 执行器存储器（以兆字节为单位） | int |
| executorCores | 执行器使用的核数 | int |
| numExecutors | 执行者人数 | int |

可以在 [MLI实例上将资源指定为](./mlinstances.md) (A)单个培训或评分参数，或(B)其他规范对象(`specification`)中的资源。 例如，以下资源配置对于培训和评分都相同：

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
