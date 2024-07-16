---
keywords: Experience Platform；主页；热门主题；数据访问；python sdk；数据访问api；读取python；写入python
solution: Experience Platform
title: 在数据科学Workspace中使用Python访问数据
type: Tutorial
description: 以下文档包含有关如何在Python中访问数据以用于数据科学Workspace的示例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 在数据科学Workspace中使用Python访问数据

以下文档包含有关如何使用Python访问数据以用于数据科学Workspace的示例。 有关使用JupyterLab笔记本访问数据的信息，请访问[JupyterLab笔记本数据访问](../jupyterlab/access-notebook-data.md)文档。

## 读取数据集

在设置环境变量并完成安装后，现在可以将您的数据集读入pandas数据流。

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 从数据集中选择列

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

DISTINCT子句允许您在行/列级别获取所有不同的值，从响应中删除所有重复值。

下面显示了使用`distinct()`函数的示例：

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

下面显示了使用这些筛选函数的示例：

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY子句

ORDER BY子句允许按指定列以特定顺序（升序或降序）对接收结果进行排序。 可使用`sort()`函数完成此操作。

下面显示了使用`sort()`函数的示例：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允许您限制从数据集接收的记录数。

下面显示了使用`limit()`函数的示例：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允许您从一开始就跳过行，以便从以后开始返回行。 在与LIMIT结合使用时，这可用于迭代块中的行。

下面显示了使用`offset()`函数的示例：

```python
df = dataset_reader.offset(100).read()
```

## 编写数据集

要写入数据集，您需要向数据集提供熊猫数据流。

### 正在编写熊猫数据流

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Userspace目录（检查点操作）

要获得运行时间较长的作业，可能需要存储中间步骤。 在这种情况下，您可以对用户空间进行读写操作。

>[!NOTE]
>
>数据的路径&#x200B;**未存储**。 您需要存储指向其各自数据的相应路径。

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

Adobe Experience Platform数据科学Workspace提供了一个方法示例，它使用上述代码示例来读取和写入数据。 如果您想了解有关如何使用Python访问您的数据的更多信息，请查看[数据科学Workspace Python GitHub存储库](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)。
