---
keywords: Experience Platform;JupyterLab；笔记本；数据科学工作区；热门主题；%dataset；交互模式；批处理模式；Spark sdk;python sdk；访问数据；笔记本数据访问
solution: Experience Platform
title: Jupyterlab笔记本中的数据访问
topic-legacy: Developer Guide
description: 本指南重点介绍如何使用Jupyter Notebooks，它是在Data Science Workspace中构建的，用于访问您的数据。
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 9%

---

# [!DNL Jupyterlab]笔记本中的数据访问

每个支持的内核都提供内置功能，允许您从笔记本内的数据集中读取平台数据。 目前，Adobe Experience Platform Data Science Workspace中的JupyterLab支持[!DNL Python]、R、PySpark和Scala的笔记本电脑。 但是，对分页数据的支持仅限于[!DNL Python]和R笔记本。 本指南重点介绍如何使用JupyterLab笔记本访问您的数据。

## 入门指南

在阅读本指南之前，请阅读[[!DNL JupyterLab] 用户指南](./overview.md)，了解[!DNL JupyterLab]的高级介绍及其在数据科学工作区中的作用。

## 笔记本数据限制{#notebook-data-limits}

>[!IMPORTANT]
>
>对于PySpark和Scala笔记本，如果您收到错误，原因是“远程RPC客户端不关联”。 这通常意味着驱动程序或执行器内存不足。 尝试切换到[&quot;batch&quot; mode](#mode)以解决此错误。

以下信息定义可读取的最大数据量、使用的数据类型以及读取数据所花费的估计时间范围。

对于[!DNL Python]和R，使用配置为40GB RAM的笔记本服务器作为基准。 对于PySpark和Scala，以64GB RAM、8个核心、2个DBU（最多4个工作线程）配置的数据库群集用于以下概述的基准测试。

使用的ExperienceEvent模式数据在大小上各不相同，从1000(1K)行开始，最多可达10亿(1B)行。 请注意，对于PySpark和[!DNL Spark]量度，XDM数据使用10天的日期范围。

使用[!DNL Query Service] Create Table as Select(CTAS)预处理临时模式数据。 此数据也从1000(1K)行开始，大小变化，行数范围高达10亿(1B)行。

### 何时使用批处理模式与交互模式{#mode}

在使用PySpark和Scala笔记本读取数据集时，您可以选择使用交互模式或批处理模式来读取数据集。 交互式是为了获得快速结果，而批处理模式是为了大数据集。

- 对于PySpark和Scala笔记本，在读取500万行或更多数据时应使用批处理模式。 有关每种模式效率的详细信息，请参阅以下[ PySpark](#pyspark-data-limits)或[ Scala](#scala-data-limits)数据限制表。

### [!DNL Python] 笔记本数据限制

**XDM ExperienceEvent模式:** 您应该能够在不到22分钟内读取XDM数据的最大200万行（磁盘上约6.1 GB数据）。添加其他行可能会导致错误。

| 行数 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁盘大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（以秒为单位） | 20.3 | 86.8 | 63 | 659 | 1315 |

**临时模式:** 在14分钟内，您最多可以读取非XDM（临时）数据的500万行（磁盘上约5.6 GB数据）。添加其他行可能会导致错误。

| 行数 | 1K | 1万 | 10万 | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁盘大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（以秒为单位） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R笔记本数据限制

**XDM体验事件模式** ：在13分钟内，您最多可以读取100万行XDM数据（磁盘上有3GB数据）。

| 行数 | 1K | 1万 | 10万 | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁盘大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R内核（秒） | 14.03 | 69.6 | 86.8 | 775 |

**临时模式:** 您应该能够在约10分钟内读取最多300万行的临时数据（磁盘上有293MB数据）。

| 行数 | 1K | 1万 | 10万 | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁盘大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark（[!DNL Python]内核）笔记本数据限制：{#pyspark-data-limits}

**XDM体验事件模式:** 在交互模式下，您应能够在约20分钟内读取XDM数据的最多500万行（磁盘上约有13.42GB数据）。交互式模式仅支持多达500万行。 如果您希望读取较大的数据集，建议您切换到批处理模式。 在批处理模式下，您应该能够在约14小时内读取XDM数据的最多5亿行（磁盘上约有1.31TB数据）。

| 行数 | 1K | 1万 | 10万 | 1M | 2M | 3M | 5M | 10M | 50M | 1亿 | 5亿 |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁盘大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1.31太字节 |
| SDK（交互模式） | 33秒 | 32.4秒 | 55.1秒 | 253.5秒 | 489.2秒 | 729.6秒 | 1206.8秒 | - | - | - | - |
| SDK（批处理模式） | 815.8秒 | 492.8秒 | 379.1秒 | 637.4秒 | 624.5秒 | 869.2秒 | 1104.1秒 | 1786年代 | 5387.2秒 | 10624.6s | 50547s |

**临时模式：在** 交互模式下，您最多可以在3分钟内读取500万行（磁盘上约5.36GB数据）的非XDM数据。在“批处理”模式下，您应该能够在约18分钟内读取最多10亿行（磁盘上的数据约为1.05TB）的非XDM数据。

| 行数 | 1K | 1万 | 10万 | 1M | 2M | 3M | 5M | 10M | 50M | 1亿 | 5亿 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁盘大小 | 1.12MB | 11.24兆字节 | 109.48兆字节 | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1.05太字节 |
| SDK交互模式（以秒为单位） | 28.2秒 | 18.6秒 | 20.8秒 | 20.9秒 | 23.8秒 | 21.7秒 | 24.7秒 | - | - | - | - | - |
| SDK批处理模式（以秒为单位） | 428.8秒 | 578.8秒 | 641.4秒 | 538.5秒 | 630.9秒 | 467.3秒 | 411 | 675年代 | 702s | 719.2秒 | 1022.1秒 | 1122.3秒 |

### [!DNL Spark] （Scala内核）笔记本数据限制：  {#scala-data-limits}

**XDM体验事件模式:** 在交互模式下，您应能够在约18分钟内读取XDM数据的最多500万行（磁盘上约有13.42GB数据）。交互式模式仅支持多达500万行。 如果您希望读取较大的数据集，建议您切换到批处理模式。 在批处理模式下，您应该能够在约14小时内读取XDM数据的最多5亿行（磁盘上约有1.31TB数据）。

| 行数 | 1K | 1万 | 10万 | 1M | 2M | 3M | 5M | 10M | 50M | 1亿 | 5亿 |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁盘大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB | 5.39 GB | 8.09 GB | 13.42 GB | 26.82 GB | 134.24 GB | 268.39 GB | 1.31太字节 |
| SDK交互模式（以秒为单位） | 37.9秒 | 22.7秒 | 45.6秒 | 231.7秒 | 444.7秒 | 660.6秒 | 1100年代 | - | - | - | - |
| SDK批处理模式（以秒为单位） | 374.4秒 | 398.5秒 | 527年代 | 487.9秒 | 588.9秒 | 829年代 | 939.1秒 | 1441年代 | 5473.2秒 | 10118.8 | 49207.6 |

**临时模式：在** 交互模式下，您最多可以在3分钟内读取500万行（磁盘上约5.36GB数据）的非XDM数据。在批处理模式下，您应该能够在约16分钟内读取最多10亿行非XDM数据（磁盘上的数据约为1.05TB）。

| 行数 | 1K | 1万 | 10万 | 1M | 2M | 3M | 5M | 10M | 50M | 1亿 | 5亿 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁盘大小 | 1.12MB | 11.24兆字节 | 109.48兆字节 | 2.69 GB | 2.14 GB | 3.21 GB | 5.36 GB | 10.71 GB | 53.58 GB | 107.52 GB | 535.88 GB | 1.05太字节 |
| SDK交互模式（以秒为单位） | 35.7秒 | 31秒 | 19.5秒 | 25.3秒 | 23秒 | 33.2秒 | 25.5秒 | - | - | - | - | - |
| SDK批处理模式（以秒为单位） | 448.8秒 | 459.7秒 | 519年代 | 475.8秒 | 599.9秒 | 347.6秒 | 407.8秒 | 397年代 | 518.8秒 | 487.9秒 | 760.2秒 | 975.4秒 |

## Python笔记本{#python-notebook}

[!DNL Python] 笔记本电脑允许您在访问数据集时对数据进行分页。下面演示了有无分页读取数据的示例代码。 有关可用的启动Python笔记本的详细信息，请访问JupyterLab用户指南中的[[!DNL JupyterLab] Launcher](./overview.md#launcher)部分。

下面的Python文档概述了以下概念：

- [从数据集读取](#python-read-dataset)
- [写入数据集](#write-python)
- [查询数据](#query-data-python)
- [过滤ExperienceEvent数据](#python-filter)

### 从Python {#python-read-dataset}中的数据集读取

**无分页：**

执行以下代码将读取整个数据集。 如果执行成功，则数据将保存为变量`df`引用的Pactis数据帧。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**分页：**

执行以下代码将从指定的数据集中读取数据。 通过分别通过函数`limit()`和`offset()`限制和偏移数据来实现分页。 限制数据是指要读取的数据点的最大数，而偏移是指在读取数据之前要跳过的数据点的数量。 如果读取操作成功执行，则数据将保存为变量`df`引用的Pactis数据帧。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 在Python {#write-python}中写入数据集

要在JupyterLab笔记本中写入数据集，请在JupyterLab的左侧导航中选择“数据”图标选项卡（在下面突出显示）。 将显示&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从您要使用的数据集的下拉菜单中选择&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;选项。 可执行代码条目显示在笔记本的底部。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;为所选数据集生成一个写单元格。
- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;为所选数据集生成读取单元格。
- 使用&#x200B;**[!UICONTROL Query Data in Notebook]**&#x200B;为所选查询集生成基本数据单元格。

或者，您也可以复制并粘贴以下代码单元格。 同时替换`{DATASET_ID}`和`{PANDA_DATAFRAME}`。

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 在[!DNL Python] {#query-data-python}中使用[!DNL Query Service]的查询数据

[!DNL JupyterLab] on允 [!DNL Platform] 许您在笔记本中使 [!DNL Python] 用SQL通过Adobe Experience Platform  [查询 Service访问数据](https://www.adobe.com/go/query-service-home-en)。通过[!DNL Query Service]访问数据对于处理大数据集非常有用，因为它的运行时间很长。 请注意，使用[!DNL Query Service]查询数据的处理时间限制为十分钟。

在[!DNL JupyterLab]中使用[!DNL Query Service]之前，请确保您对[[!DNL Query Service]  SQL语法](https://www.adobe.com/go/query-service-sql-syntax-en)有正确的了解。

使用[!DNL Query Service]查询目标时，需要提供数据集的名称。 您可以使用&#x200B;**[!UICONTROL Data explorer]**&#x200B;查找所需的数据集，从而生成必要的代码单元格。 右键单击数据集列表，然后单击&#x200B;**[!UICONTROL Query Data in Notebook]**&#x200B;在笔记本中生成两个代码单元格。 下面将详细介绍这两个单元格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

要在[!DNL JupyterLab]中使用[!DNL Query Service]，必须首先在工作[!DNL Python]笔记本和[!DNL Query Service]之间创建连接。 这可以通过执行第一生成的单元来实现。

```python
qs_connect()
```

在第二个生成的单元格中，必须在SQL查询之前定义第一行。 默认情况下，生成的单元格定义一个可选变量(`df0`)，该变量将查询结果保存为Pactis数据帧。 <br>该参 `-c QS_CONNECTION` 数是必需的，它告诉内核执行SQL查询 [!DNL Query Service]。有关其他参数的列表，请参见[附录](#optional-sql-flags-for-query-service)。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python变量可以在SQL查询中直接引用，方法是使用字符串格式的语法并将变量包装在大括号(`{}`)中，如下例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 筛选[!DNL ExperienceEvent]数据{#python-filter}

要访问和筛选[!DNL Python]笔记本中的[!DNL ExperienceEvent]数据集，必须提供数据集(`{DATASET_ID}`)的ID以及使用逻辑运算符定义特定时间范围的筛选器规则。 定义时间范围时，将忽略任何指定的分页，并考虑整个数据集。

过滤操作符的列表说明如下：

- `eq()`: 等于
- `gt()`: 大于
- `ge()`: 大于或等于
- `lt()`: 小于
- `le()`: 小于或等于
- `And()`:逻辑AND运算符
- `Or()`:逻辑OR运算符

以下单元格将[!DNL ExperienceEvent]数据集过滤器为2019年1月1日至2019年12月31日之间仅存的数据。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R笔记本{#r-notebooks}

R笔记本允许您在访问数据集时对数据进行分页。 下面演示了有无分页读取数据的示例代码。 有关可用启动R笔记本的详细信息，请访问JupyterLab用户指南中的[[!DNL JupyterLab]  Launcher](./overview.md#launcher)部分。

以下R文档概述了以下概念：

- [从数据集读取](#r-read-dataset)
- [写入数据集](#write-r)
- [过滤ExperienceEvent数据](#r-filter)

### 从R {#r-read-dataset}中的数据集读取

**无分页：**

执行以下代码将读取整个数据集。 如果执行成功，则数据将保存为变量`df0`引用的Pactis数据帧。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**分页：**

执行以下代码将从指定的数据集中读取数据。 通过分别通过函数`limit()`和`offset()`限制和偏移数据来实现分页。 限制数据是指要读取的数据点的最大数，而偏移是指在读取数据之前要跳过的数据点的数量。 如果读取操作成功执行，则数据将保存为变量`df0`引用的Pactis数据帧。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### 写入R {#write-r}中的数据集

要在JupyterLab笔记本中写入数据集，请在JupyterLab的左侧导航中选择“数据”图标选项卡（在下面突出显示）。 将显示&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从您要使用的数据集的下拉菜单中选择&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;选项。 可执行代码条目显示在笔记本的底部。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;为所选数据集生成一个写单元格。
- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;为所选数据集生成读取单元格。

或者，您也可以复制并粘贴以下代码单元格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 筛选[!DNL ExperienceEvent]数据{#r-filter}

要访问和筛选R笔记本中的[!DNL ExperienceEvent]数据集，必须提供数据集(`{DATASET_ID}`)的ID以及使用逻辑运算符定义特定时间范围的筛选器规则。 定义时间范围时，将忽略任何指定的分页，并考虑整个数据集。

过滤操作符的列表说明如下：

- `eq()`: 等于
- `gt()`: 大于
- `ge()`: 大于或等于
- `lt()`: 小于
- `le()`: 小于或等于
- `And()`:逻辑AND运算符
- `Or()`:逻辑OR运算符

以下单元格将[!DNL ExperienceEvent]数据集过滤器为2019年1月1日至2019年12月31日之间仅存的数据。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3笔记本{#pyspark-notebook}

以下PySpark文档概述了以下概念：

- [初始化SparkSession](#spark-initialize)
- [读写数据](#magic)
- [创建本地数据帧](#pyspark-create-dataframe)
- [过滤ExperienceEvent数据](#pyspark-filter-experienceevent)

### 正在初始化SparkSession {#spark-initialize}

所有[!DNL Spark] 2.4笔记本都要求使用以下样板代码初始化会话。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%dataset读写PySpark 3笔记本{#magic}

随着[!DNL Spark] 2.4的推出，`%dataset`自定义幻灯可用于PySpark 3([!DNL Spark] 2.4)笔记本。 有关IPython内核中可用的magic命令的详细信息，请访问[IPython magic文档](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。


**用法**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**描述**

用于从[!DNL PySpark]笔记本（[!DNL Python] 3内核）读取或写入数据集的自定义[!DNL Data Science Workspace]魔术命令。

| 名称 | 描述 | 必需 |
| --- | --- | --- |
| `{action}` | 要对数据集执行的操作类型。 有两种操作可用：“read”或“write”。 | 是 |
| `--datasetId {id}` | 用于提供要读或写的数据集的ID。 | 是 |
| `--dataFrame {df}` | 熊猫数据框。 <ul><li> 当操作为&quot;read&quot;时， {df}是数据集读取操作结果可用的变量。 </li><li> 当操作为&quot;write&quot;时，此数据帧{df}将写入数据集。 </li></ul> | 是 |
| `--mode` | 更改数据读取方式的其他参数。 允许的参数为“batch”和“interactive”。 默认情况下，该模式设置为“交互”。 建议在读取大量数据时使用“批处理”模式。 | 否 |

>[!TIP]
>
>查看[笔记本数据限制](#notebook-data-limits)部分中的PySpark表，以确定应将`mode`设置为`interactive`还是`batch`。

**示例**

- **阅读示例**:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **编写示例**:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

您可以使用以下方法在JupyterLab购买中自动生成上述示例：

在JupyterLab的左侧导航中选择“数据”图标选项卡（在下面突出显示）。 将显示&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从您要使用的数据集的下拉菜单中选择&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;选项。 可执行代码条目显示在笔记本的底部。

- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;生成读取单元格。
- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;生成写单元格。

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### 创建本地数据帧{#pyspark-create-dataframe}

要使用PySpark 3创建本地数据帧，请使用SQL查询。 例如：

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>您还可以指定可选种子样本，如布尔值withReplacement、多次分数或长种子。

### 筛选[!DNL ExperienceEvent]数据{#pyspark-filter-experienceevent}

访问和筛选PySpark笔记本中的[!DNL ExperienceEvent]数据集需要您提供数据集标识(`{DATASET_ID}`)、组织的IMS标识以及定义特定时间范围的筛选器规则。 使用函数`spark.sql()`定义过滤时间范围，其中函数参数是SQL查询字符串。

以下单元格将[!DNL ExperienceEvent]数据集过滤为2019年1月1日至2019年12月31日之间仅存的数据。

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Scala笔记本电脑{#scala-notebook}

以下文档包含以下概念的示例：

- [初始化SparkSession](#scala-initialize)
- [读取数据集](#read-scala-dataset)
- [写入数据集](#scala-write-dataset)
- [创建本地数据帧](#scala-create-dataframe)
- [过滤ExperienceEvent数据](#scala-experienceevent)

### 初始化SparkSession {#scala-initialize}

所有Scala笔记本都要求使用以下样板代码初始化会话：

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 读取数据集{#read-scala-dataset}

在Scala中，您可以导入`clientContext`以获取并返回平台值，这样就无需定义`var userToken`等变量。 在下面的Scala示例中，`clientContext`用于获取并返回读取数据集所需的所有值。

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一个变量，表示用于读取和写入数据的Pactys数据帧。 |
| 用户令牌 | 使用`clientContext.getUserToken()`自动获取的用户令牌。 |
| 服务令牌 | 使用`clientContext.getServiceToken()`自动获取的服务令牌。 |
| ims-org | 使用`clientContext.getOrgId()`自动获取的IMS组织ID。 |
| api-key | 使用`clientContext.getApiKey()`自动获取的API密钥。 |

>[!TIP]
>
>查看[笔记本数据限制](#notebook-data-limits)部分中的Scala表，以确定应将`mode`设置为`interactive`还是`batch`。

您可以使用以下方法在JupyterLab购买中自动生成上述示例：

在JupyterLab的左侧导航中选择“数据”图标选项卡（在下面突出显示）。 将显示&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从您要使用的数据集的下拉菜单中选择&#x200B;**[!UICONTROL Explore Data in Notebook]**选项。 可执行代码条目显示在笔记本的底部。
和
- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;生成读取单元格。
- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;生成写单元格。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 写入数据集{#scala-write-dataset}

在Scala中，您可以导入`clientContext`以获取并返回平台值，这样就无需定义`var userToken`等变量。 在下面的Scala示例中，`clientContext`用于定义并返回写入数据集所需的所有值。

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一个变量，表示用于读取和写入数据的Pactys数据帧。 |
| 用户令牌 | 使用`clientContext.getUserToken()`自动获取的用户令牌。 |
| 服务令牌 | 使用`clientContext.getServiceToken()`自动获取的服务令牌。 |
| ims-org | 使用`clientContext.getOrgId()`自动获取的IMS组织ID。 |
| api-key | 使用`clientContext.getApiKey()`自动获取的API密钥。 |

>[!TIP]
>
>查看[笔记本数据限制](#notebook-data-limits)部分中的Scala表，以确定应将`mode`设置为`interactive`还是`batch`。

### 创建本地数据帧{#scala-create-dataframe}

要使用Scala创建本地数据帧，需要SQL查询。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 筛选[!DNL ExperienceEvent]数据{#scala-experienceevent}

访问和筛选Scala笔记本中的[!DNL ExperienceEvent]数据集需要您提供数据集标识(`{DATASET_ID}`)、组织的IMS标识以及定义特定时间范围的筛选器规则。 过滤时间范围是使用函数`spark.sql()`定义的，其中函数参数是SQL查询字符串。

以下单元格将[!DNL ExperienceEvent]数据集过滤为2019年1月1日至2019年12月31日之间仅存的数据。

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## 后续步骤

本文档涵盖了使用JupyterLab笔记本访问数据集的一般准则。 有关查询数据集的详细示例，请访问JupyterLab笔记本](./query-service.md)文档中的[查询服务。 有关如何浏览和可视化数据集的详细信息，请访问[上的文档，使用笔记本](./analyze-your-data.md)分析数据。

## [!DNL Query Service] {#optional-sql-flags-for-query-service}的可选SQL标志

此表概述了可用于[!DNL Query Service]的可选SQL标志。

| **标志** | **描述** |
| --- | --- |
| `-h`、`--help` | 显示帮助消息并退出。 |
| `-n`、`--notify` | 切换用于通知查询结果的选项。 |
| `-a`、`--async` | 使用此标志可异步执行查询，并可在查询执行时释放内核。 将查询结果分配给变量时要小心，因为如果查询不完整，则可能未定义该结果。 |
| `-d`、`--display` | 使用此标志可阻止显示结果。 |
