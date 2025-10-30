---
keywords: Experience Platform；开发人员指南；SDK；数据访问SDK；数据科学Workspace；热门主题
solution: Experience Platform
title: 使用Adobe Experience Platform SDK创作模型
description: 本教程向您提供有关在Python和R中将data_access_sdk_python转换为新Python platform_sdk的信息。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# 使用Adobe [!DNL Experience Platform] SDK创作模型

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

本教程为您提供有关在Python和R中将`data_access_sdk_python`转换为新Python `platform_sdk`的信息。本教程提供了有关以下操作的信息：

- [生成身份验证](#build-authentication)
- [数据基本读取](#basic-reading-of-data)
- [基本的数据写入](#basic-writing-of-data)

## 生成身份验证 {#build-authentication}

需要身份验证才能调用[!DNL Adobe Experience Platform]，它由API密钥、组织ID、用户令牌和服务令牌组成。

### Python

如果您使用的是Jupyter Notebook，请使用以下代码构建`client_context`：

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您没有使用Jupyter Notebook，或者您需要更改组织，请使用以下代码示例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用的是Jupyter Notebook，请使用以下代码构建`client_context`：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter Notebook或需要更改组织，请使用以下代码示例：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 数据基本读取 {#basic-reading-of-data}

使用新的[!DNL Experience Platform] SDK，最大读取大小为32 GB，最大读取时间为10分钟。

如果读取时间过长，可以尝试使用以下筛选选项之一：

- [按偏移和限制过滤数据](#filter-by-offset-and-limit)
- [按日期过滤数据](#filter-by-date)
- [按列过滤数据](#filter-by-selected-columns)
- [获取排序的结果](#get-sorted-results)

>[!NOTE]
>
>组织在`client_context`内设置。

### Python

要读取Python中的数据，请使用以下代码示例：

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

要读取R中的数据，请使用下面的代码示例：

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## 按偏移和限制筛选 {#filter-by-offset-and-limit}

由于不再支持按批次ID进行筛选，为了限定数据读取的范围，您需要使用`offset`和`limit`。

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

## 按日期筛选 {#filter-by-date}

日期过滤的粒度现在由时间戳定义，而不是按天设置。

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

新的[!DNL Experience Platform] SDK支持以下操作：

| 操作 | 函数 |
| --------- | -------- |
| 等于(`=`) | `eq()` |
| 大于(`>`) | `gt()` |
| 大于或等于(`>=`) | `ge()` |
| 小于(`<`) | `lt()` |
| 小于或等于(`<=`) | `le()` |
| 和(`&`) | `And()` |
| 或(&amp;amp；vert； ) | `Or()` |

## 按所选列筛选 {#filter-by-selected-columns}

为进一步优化数据读取，您还可以按列名进行筛选。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 获取排序的结果 {#get-sorted-results}

收到的结果可以分别按目标数据集的指定列和它们的顺序(asc/desc)排序。

在以下示例中，数据流首先按“column-a”升序排序。 随后，“column-a”的值相同的行将按“column-b”降序排序。

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 基本的数据写入 {#basic-writing-of-data}

>[!NOTE]
>
>组织在`client_context`内设置。

要使用Python和R编写数据，请使用以下示例之一：

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

配置`platform_sdk`数据加载器后，数据将进行准备，然后拆分到`train`和`val`数据集。 要了解有关数据准备和功能工程的信息，请访问使用[笔记本创建方法的教程中有关](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering)数据准备和功能工程[!DNL JupyterLab]的部分。
