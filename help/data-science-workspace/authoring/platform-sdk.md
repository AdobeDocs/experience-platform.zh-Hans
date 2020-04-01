---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: 平台SDK指南
topic: SDK authoring
translation-type: tm+mt
source-git-commit: a68aa62c3c3cc3e42083d6b0a1d1003f4137840f

---


# 平台SDK指南

本教程提供了有关在Python和R `data_access_sdk_python` 中转换为新 `platform_sdk` 的Python的信息。本教程提供了有关以下操作的信息：

- [构建身份验证](#build-authentication)
- [数据的基本读取](#basic-reading-of-data)
- [基本的数据编写](#basic-writing-of-data)

## 构建身份验证

对Adobe Experience Platform进行调用需要身份验证，由API密钥、IMS组织ID、用户令牌和服务令牌组成。

### Python

如果您使用Jupyter Notebook，请使用以下代码构建 `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您没有使用Jupyter Notebook，或者您需要更改IMS组织，请使用以下代码示例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用Jupyter Notebook，请使用以下代码构建 `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您没有使用Jupyter Notebook，或者您需要更改IMS组织，请使用以下代码示例：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 数据的基本读取

使用新的Platform SDK，最大读取大小为32 GB，最大读取时间为10分钟。

如果您的阅读时间过长，您可以尝试使用以下筛选选项之一：

- [按偏移和限制筛选数据](#filter-by-offset-and-limit)
- [按日期筛选数据](#filter-by-date)
- [按列过滤数据](#filter-by-selected-columns)
- [获取排序结果](#get-sorted-results)

>[!NOTE] IMS组织在中设置 `client_context`。

### Python

要读取Python中的数据，请使用下面的代码示例：

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

要在R中读取数据，请使用下面的代码示例：

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## 按偏移和限制过滤

由于不再支持按批ID过滤，因此要对数据进行范围读取，您需要使用 `offset` 和 `limit`。

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## 按日期筛选

日期筛选的粒度现在由时间戳定义，而不是按日设置。

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

新的Platform SDK支持以下操作：

| 操作 | 函数 |
| --------- | -------- |
| 等于 (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| And (`&`) | `And()` |
| 或 (`|`) | `Or()` |

## 按选定列过滤

要进一步优化数据读取，您还可以按列名进行筛选。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 获取排序结果

接收的结果可以按目标数据集的指定列和其顺序(asc/desc)分别排序。

在以下示例中，数据帧按“column-a”第一个按升序排序。 对“column-a”具有相同值的行随后按“column-b”以降序排序。

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 基本的数据编写

>[!NOTE] IMS组织在中设置 `client_context`。

要在Python和R中写入数据，请使用以下示例之一：

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## 后续步骤

配置数据加载 `platform_sdk` 器后，数据将进行准备，然后被拆分到数据 `train` 集和数 `val` 据集。 要了解数据准备和功能工程，请访问JupyterLab笔记本 [创建菜谱教程中有关数据准备和功能工程的部分](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) 。