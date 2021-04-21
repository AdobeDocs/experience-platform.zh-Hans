---
keywords: Experience Platform；主页；热门主题；数据访问；python sdk；数据访问api；读python;write python
solution: Experience Platform
title: 在数据科学工作区中使用Python访问数据
topic-legacy: tutorial
type: Tutorial
description: 以下文档包含有关如何在Python中访问数据以在数据科学工作区中使用的示例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 在数据科学工作区中使用Python访问数据

以下文档包含有关如何使用Python访问数据以在数据科学工作区中使用的示例。 有关使用JupyterLab笔记本访问数据的信息，请访问[JupyterLab笔记本数据访问](../jupyterlab/access-notebook-data.md)文档。

## 读取数据集

在设置环境变量并完成安装后，您的数据集现在可以读入pactis数据框。

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 数据集中的SELECT列

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 获取分区信息：

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT子句

DISTINCT子句允许您在行/列级别提取所有不同值，从响应中删除所有重复值。

下面可以看到使用`distinct()`函数的示例：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

您可以在Python中使用某些运算符来帮助筛选数据集。

>[!NOTE]
>
>用于筛选的函数区分大小写。

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

使用这些过滤函数的示例如下所示：

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY子句

ORDER BY子句允许按指定列按特定顺序（升序或降序）对接收结果进行排序。 这是使用`sort()`函数完成的。

下面可以看到使用`sort()`函数的示例：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允许您限制从数据集接收的记录数。

下面可以看到使用`limit()`函数的示例：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允许您从开头跳到从后一点返回行的开始。 与LIMIT结合使用时，可以对块中的行进行迭代。

下面可以看到使用`offset()`函数的示例：

```python
df = dataset_reader.offset(100).read()
```

## 写入数据集

要写入数据集，您需要向数据集提供熊猫数据框。

### 编写熊猫数据框

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Userspace目录（检查点）

对于运行时间较长的作业，您可能需要存储中间步骤。 在这种情况下，您可以读写用户空间。

>[!NOTE]
>
>数据的路径被存储在&#x200B;**中。**&#x200B;您需要存储其相应数据的相应路径。

### 写入用户空间

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 从用户空间读取

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## 后续步骤

Adobe Experience Platform Data Science Workspace提供了一个菜谱示例，它使用上述代码示例来读取和写入数据。 如果您想了解有关如何使用Python访问数据的更多信息，请查阅[数据科学工作区Python GitHub存储库](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)。
