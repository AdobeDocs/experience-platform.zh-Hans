---
keywords: Experience Platform；开发人员指南；SDK；数据访问SDK；数据科学工作区；热门主题
solution: Experience Platform
title: 使用Adobe Experience Platform Platform SDK进行模型创作
topic-legacy: SDK authoring
description: 本教程向您提供有关在Python和R中将data_access_sdk_python转换为新的Python平台_sdk的信息。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# 使用Adobe Experience Platform [!DNL Platform] SDK进行模型创作

本教程向您提供了有关将`data_access_sdk_python`转换为Python和R中的新Python `platform_sdk`的信息。本教程提供有关以下操作的信息：

- [构建身份验证](#build-authentication)
- [数据的基本读取](#basic-reading-of-data)
- [基本数据写入](#basic-writing-of-data)

## 构建身份验证{#build-authentication}

对[!DNL Adobe Experience Platform]进行调用需要身份验证，由API密钥、IMS组织ID、用户令牌和服务令牌组成。

### Python

如果您使用Jupyter Notebook，请使用下面的代码构建`client_context`:

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

如果您使用Jupyter Notebook，请使用下面的代码构建`client_context`:

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

## 数据{#basic-reading-of-data}的基本读取

使用新的[!DNL Platform] SDK，最大读取大小为32 GB，最大读取时间为10分钟。

如果您的读取时间过长，您可以尝试使用以下筛选选项之一：

- [按偏移和限制筛选数据](#filter-by-offset-and-limit)
- [按日期筛选数据](#filter-by-date)
- [按列筛选数据](#filter-by-selected-columns)
- [获取排序结果](#get-sorted-results)

>[!NOTE]
>
>IMS组织设置在`client_context`中。

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

## 按偏移和限制{#filter-by-offset-and-limit}过滤

由于不再支持按批ID过滤，因此要对数据进行范围读取，您需要使用`offset`和`limit`。

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

## 按日期{#filter-by-date}筛选

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

新的[!DNL Platform] SDK支持以下操作：

| 操作 | 函数 |
| --------- | -------- |
| 等于 (`=`) | `eq()` |
| 大于 (`>`) | `gt()` |
| 大于或等于 (`>=`) | `ge()` |
| 小于 (`<`) | `lt()` |
| 小于或等于 (`<=`) | `le()` |
| 和(`&`) | `And()` |
| 或 (`|`) | `Or()` |

## 按选定列{#filter-by-selected-columns}过滤

要进一步优化数据阅读，您还可以按列名进行筛选。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 获取排序结果{#get-sorted-results}

收到的结果可以按目标数据集的指定列及其顺序(asc/desc)分别排序。

在下面的示例中，数据帧按“column-a”首先以升序顺序排序。 对“column-a”具有相同值的行随后按“column-b”以降序排序。

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 数据{#basic-writing-of-data}的基本写入

>[!NOTE]
>
>IMS组织设置在`client_context`中。

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

配置`platform_sdk`数据加载器后，数据将进行准备，然后被拆分到`train`和`val`数据集。 要了解数据准备和功能工程，请访问使用[!DNL JupyterLab]笔记本创建菜谱的教程中[数据准备和功能工程](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering)部分。
