---
keywords: Experience Platform；JupyterLab；笔记本；数据科学Workspace；热门主题；%数据集；交互模式；批处理模式；Spark sdk；python sdk；访问数据；笔记本数据访问
solution: Experience Platform
title: Jupyterlab Notebooks中的数据访问
description: 本指南重点介绍如何使用Jupyter Notebooks(内置于数据科学Workspace中)访问您的数据。
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '3274'
ht-degree: 3%

---

# [!DNL Jupyterlab]笔记本中的数据访问

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

每个受支持的内核都提供了内置功能，允许您从笔记本内的数据集读取Experience Platform数据。 目前，Adobe Experience Platform Data Science Workspace中的JupyterLab支持[!DNL Python]、R、PySpark和Scala的笔记本。 但是，对分页数据的支持仅限于[!DNL Python]和R笔记本。 本指南重点介绍如何使用JupyterLab笔记本访问您的数据。

## 快速入门

在阅读本指南之前，请查看[[!DNL JupyterLab] 用户指南](./overview.md)，以详细了解[!DNL JupyterLab]及其在数据科学Workspace中的角色。

## 笔记本数据限制 {#notebook-data-limits}

>[!IMPORTANT]
>
>对于PySpark和Scala笔记本，如果收到错误，原因为“远程RPC客户端已取消关联”。 这通常意味着驱动程序或执行器的内存不足。 尝试切换到[“批处理”模式](#mode)以解决此错误。

以下信息定义了可读取的最大数据量、使用了什么类型的数据以及读取数据的估计时间范围。

对于[!DNL Python]和R，使用配置为40GB RAM的笔记本服务器进行基准测试。 对于PySpark和Scala，配置为64GB RAM、8核、2个DBU且最多4个工作线程的数据库群集用于下面列出的基准。

使用的ExperienceEvent架构数据大小不一，从1,000行(1K)到十亿(1B)行。 请注意，对于PySpark和[!DNL Spark]量度，XDM数据使用了10天的日期范围。

使用[!DNL Query Service]创建表作为选择(CTAS)预处理了临时架构数据。 这些数据也各不相同，从1,000行（1,000行）到最多10亿（1,000行）不等。

### 何时使用批处理模式与交互模式 {#mode}

读取包含PySpark和Scala笔记本的数据集时，您可以选择使用交互模式或批处理模式来读取数据集。 交互模式用于快速结果，而批处理模式用于大型数据集。

- 对于PySpark和Scala笔记本，在读取500万行或更多数据时应使用批处理模式。 有关每种模式效率的更多信息，请参阅下面的[PySpark](#pyspark-data-limits)或[Scala](#scala-data-limits)数据限制表。

### [!DNL Python]笔记本数据限制

**XDM ExperienceEvent架构：**&#x200B;您最多可以在22分钟内读取200万行（磁盘上约6.1 GB的数据）的XDM数据。 添加其他行可能会导致错误。

| 行数 | 1K | 10K | 100K | 100万 | 200万 |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁盘大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（以秒为单位） | 20.3 | 86.8 | 63 | 659 | 1315 |

**临时架构：**&#x200B;您应该能够在14分钟内读取非XDM （临时）数据的最多500万行（磁盘上约5.6 GB的数据）。 添加其他行可能会导致错误。

| 行数 | 1K | 10K | 100K | 100万 | 200万 | 3M | 5分钟 |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁盘大小（以MB为单位） | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（以秒为单位） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R笔记本数据限制

**XDM ExperienceEvent架构：**&#x200B;您在13分钟内最多可读取100万行XDM数据（磁盘上的3GB数据）。

| 行数 | 1K | 10K | 100K | 100万 |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁盘大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R内核（秒） | 14.03 | 69.6 | 86.8 | 775 |

**临时架构：**&#x200B;您最多可以在10分钟内读取300万行临时数据（磁盘上为293MB数据）。

| 行数 | 1K | 10K | 100K | 100万 | 200万 | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁盘大小（以MB为单位） | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark （[!DNL Python]内核）笔记本数据限制： {#pyspark-data-limits}

**XDM ExperienceEvent架构：**&#x200B;在交互模式下，您应该能够在大约20分钟内读取最多500万行（磁盘上约13.42GB的数据）的XDM数据。 交互模式最多仅支持500万行。 如果要读取更大的数据集，建议切换到批处理模式。 在批处理模式中，您最多可以在14小时内读取5亿行（磁盘上大约1.31TB的数据）的XDM数据。

| 行数 | 1K | 10K | 100K | 100万 | 200万 | 3M | 5分钟 | 10分钟 | 50分钟 | 1亿 | 5亿 |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁盘大小 | 2.93兆字节 | 4.38兆字节 | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31太字节 |
| SDK（交互模式） | 33秒 | 32.4秒 | 55.1秒 | 253.5秒 | 489.2秒 | 729.6秒 | 1206.8秒 | - | - | - | - |
| SDK（批处理模式） | 815.8秒 | 492.8秒 | 379.1秒 | 637.4秒 | 624.5秒 | 869.2秒 | 1104.1秒 | 1786年代 | 5387.2秒 | 10624.6秒 | 50547秒 |

**临时架构：**&#x200B;在交互模式下，您应该可以在3分钟内读取非XDM数据的最多500万行（磁盘上约5.36GB的数据）。 在批处理模式下，您最多可以在18分钟内读取非XDM数据的10亿行（磁盘上大约1.05TB的数据）。

| 行数 | 1K | 10K | 100K | 100万 | 200万 | 3M | 5分钟 | 10分钟 | 50分钟 | 1亿 | 5亿 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁盘大小 | 1.12兆字节 | 11.24兆字节 | 109.48兆字节 | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05太字节 |
| SDK交互模式（以秒为单位） | 28.2秒 | 18.6秒 | 20.8秒 | 20.9秒 | 23.8秒 | 21.7秒 | 24.7秒 | - | - | - | - | - |
| SDK批处理模式（以秒为单位） | 428.8秒 | 578.8秒 | 641.4秒 | 538.5秒 | 630.9秒 | 467.3秒 | 411秒 | 675秒 | 702秒 | 719.2秒 | 1022.1秒 | 1122.3秒 |

### [!DNL Spark] （Scala内核）笔记本数据限制： {#scala-data-limits}

**XDM ExperienceEvent架构：**&#x200B;在交互模式下，您应该能够在大约18分钟内读取最多500万行（磁盘上约13.42GB的数据）的XDM数据。 交互模式最多仅支持500万行。 如果要读取更大的数据集，建议切换到批处理模式。 在批处理模式中，您最多可以在14小时内读取5亿行（磁盘上大约1.31TB的数据）的XDM数据。

| 行数 | 1K | 10K | 100K | 100万 | 200万 | 3M | 5分钟 | 10分钟 | 50分钟 | 1亿 | 5亿 |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁盘大小 | 2.93兆字节 | 4.38兆字节 | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31太字节 |
| SDK交互模式（以秒为单位） | 37.9秒 | 22.7秒 | 45.6秒 | 231.7秒 | 444.7秒 | 66秒 | 1100秒 | - | - | - | - |
| SDK批处理模式（以秒为单位） | 374.4秒 | 398.5秒 | 527秒 | 487.9秒 | 588.9秒 | 829秒 | 939.1秒 | 1441秒 | 5473.2秒 | 10118.8 | 49207.6 |

**临时架构：**&#x200B;在交互模式下，您应该能够在3分钟内读取最多500万行（磁盘上约5.36GB的数据）的非XDM数据。 在批处理模式下，您最多可以在16分钟内读取非XDM数据的10亿行（磁盘上大约1.05TB的数据）。

| 行数 | 1K | 10K | 100K | 100万 | 200万 | 3M | 5分钟 | 10分钟 | 50分钟 | 1亿 | 5亿 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁盘大小 | 1.12兆字节 | 11.24兆字节 | 109.48兆字节 | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05太字节 |
| SDK交互模式（以秒为单位） | 35.7秒 | 31秒 | 19.5秒 | 25.3秒 | 23秒 | 33.2秒 | 25.5秒 | - | - | - | - | - |
| SDK批处理模式（以秒为单位） | 448.8秒 | 459.7秒 | 519秒 | 475.8秒 | 599.9秒 | 347.6秒 | 407.8秒 | 397秒 | 518.8秒 | 487.9秒 | 760.2秒 | 975.4秒 |

## Python笔记本 {#python-notebook}

[!DNL Python]笔记本允许您在访问数据集时分页数据。 下面演示了使用分页和不使用分页读取数据的示例代码。 有关可用入门Python笔记本的更多信息，请访问JupyterLab用户指南中的[[!DNL JupyterLab] 启动器](./overview.md#launcher)部分。

以下Python文档概述了以下概念：

- [从数据集中读取](#python-read-dataset)
- [写入数据集](#write-python)
- [查询数据](#query-data-python)
- [筛选ExperienceEvent数据](#python-filter)

### 从Python中的数据集读取 {#python-read-dataset}

**没有分页：**

执行以下代码将读取整个数据集。 如果执行成功，则数据将保存为变量`df`引用的熊猫数据流。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**分页：**

执行以下代码将从指定的数据集中读取数据。 通过分别通过函数`limit()`和`offset()`限制和偏移数据来实现分页。 限制数据是指要读取的最大数据点数，而偏移是指在读取数据之前要跳过的数据点数。 如果读取操作执行成功，则数据将保存为变量`df`引用的Pandas数据流。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 写入Python中的数据集 {#write-python}

要写入JupyterLab笔记本中的数据集，请在JupyterLab的左侧导航中选择“数据”图标选项卡（下面高亮显示）。 出现&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从要使用的数据集上的下拉菜单中选择&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;选项。 笔记本底部会显示一个可执行代码条目。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;生成包含选定数据集的写入单元格。
- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;生成具有选定数据集的读取单元格。
- 使用&#x200B;**[!UICONTROL Query Data in Notebook]**&#x200B;生成包含选定数据集的基本查询单元格。

或者，您可以复制并粘贴以下代码单元格。 同时替换`{DATASET_ID}`和`{PANDA_DATAFRAME}`。

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 在[!DNL Query Service]中使用[!DNL Python]查询数据 {#query-data-python}

[!DNL JupyterLab]上的[!DNL Experience Platform]允许您使用[!DNL Python]笔记本中的SQL通过[Adobe Experience Platform查询服务](https://www.adobe.com/go/query-service-home-en)访问数据。 通过[!DNL Query Service]访问数据对于处理大型数据集很有用，因为其运行时间较长。 请注意，使用[!DNL Query Service]查询数据的处理时间限制为10分钟。

在[!DNL Query Service]中使用[!DNL JupyterLab]之前，请确保您对[[!DNL Query Service] SQL语法](https://www.adobe.com/go/query-service-sql-syntax-en)有一定的了解。

使用[!DNL Query Service]查询数据需要您提供目标数据集的名称。 您可以使用&#x200B;**[!UICONTROL Data explorer]**&#x200B;查找所需的数据集来生成必要的代码单元格。 右键单击数据集列表，然后单击&#x200B;**[!UICONTROL Query Data in Notebook]**&#x200B;以在笔记本中生成两个代码单元格。 下面将更详细地概述这两个单元格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

为了在[!DNL Query Service]中利用[!DNL JupyterLab]，您必须首先在正在处理的[!DNL Python]笔记本和[!DNL Query Service]之间创建连接。 这可以通过执行第一个生成的单元格来实现。

```python
qs_connect()
```

在第二个生成的单元格中，必须在SQL查询之前定义第一行。 默认情况下，生成的单元格定义了一个可选变量(`df0`)，该变量将查询结果保存为Pandas数据流。 <br> `-c QS_CONNECTION`参数是必需的，它告知内核对[!DNL Query Service]执行SQL查询。 有关其他参数的列表，请参阅[附录](#optional-sql-flags-for-query-service)。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

通过使用字符串格式语法并将变量括在大括号(`{}`)中，可以直接在SQL查询中引用Python变量，如以下示例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 筛选[!DNL ExperienceEvent]数据 {#python-filter}

要访问和筛选[!DNL ExperienceEvent]笔记本中的[!DNL Python]数据集，您必须提供数据集(`{DATASET_ID}`)的ID以及使用逻辑运算符定义特定时间范围的筛选规则。 定义时间范围后，将忽略任何指定的分页，并会考虑整个数据集。

筛选运算符列表如下所述：

- `eq()`：等于
- `gt()`：大于
- `ge()`：大于或等于
- `lt()`：小于
- `le()`：小于或等于
- `And()`：逻辑AND运算符
- `Or()`：逻辑或运算符

以下单元格筛选[!DNL ExperienceEvent]数据集，以使其包含在2019年1月1日至2019年12月31日终了期间专门存在的数据。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R笔记本 {#r-notebooks}

R笔记本允许您在访问数据集时分页数据。 下面演示了使用分页和不使用分页读取数据的示例代码。 有关可用入门R笔记本的更多信息，请访问JupyterLab用户指南中的[[!DNL JupyterLab] 启动器](./overview.md#launcher)部分。

以下R文档概述了以下概念：

- [从数据集中读取](#r-read-dataset)
- [写入数据集](#write-r)
- [筛选ExperienceEvent数据](#r-filter)

### 从R中的数据集读取 {#r-read-dataset}

**没有分页：**

执行以下代码将读取整个数据集。 如果执行成功，则数据将保存为变量`df0`引用的熊猫数据流。

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

执行以下代码将从指定的数据集中读取数据。 通过分别通过函数`limit()`和`offset()`限制和偏移数据来实现分页。 限制数据是指要读取的最大数据点数，而偏移是指在读取数据之前要跳过的数据点数。 如果读取操作执行成功，则数据将保存为变量`df0`引用的Pandas数据流。

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

### 写入R中的数据集 {#write-r}

要写入JupyterLab笔记本中的数据集，请在JupyterLab的左侧导航中选择“数据”图标选项卡（下面高亮显示）。 出现&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从要使用的数据集上的下拉菜单中选择&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;选项。 笔记本底部会显示一个可执行代码条目。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;生成包含选定数据集的写入单元格。
- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;生成具有选定数据集的读取单元格。

或者，您可以复制并粘贴以下代码单元格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 筛选[!DNL ExperienceEvent]数据 {#r-filter}

要访问和筛选R笔记本中的[!DNL ExperienceEvent]数据集，您必须提供数据集(`{DATASET_ID}`)的ID以及使用逻辑运算符定义特定时间范围的筛选规则。 定义时间范围后，将忽略任何指定的分页，并会考虑整个数据集。

筛选运算符列表如下所述：

- `eq()`：等于
- `gt()`：大于
- `ge()`：大于或等于
- `lt()`：小于
- `le()`：小于或等于
- `And()`：逻辑AND运算符
- `Or()`：逻辑或运算符

以下单元格筛选[!DNL ExperienceEvent]数据集，以使其包含在2019年1月1日至2019年12月31日终了期间专门存在的数据。

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

## PySpark 3笔记本 {#pyspark-notebook}

以下PySpark文档概述了以下概念：

- [初始化sparkSession](#spark-initialize)
- [读取和写入数据](#magic)
- [创建本地数据流](#pyspark-create-dataframe)
- [筛选ExperienceEvent数据](#pyspark-filter-experienceevent)

### 初始化sparkSession {#spark-initialize}

所有[!DNL Spark] 2.4笔记本都要求您使用以下样板代码初始化会话。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%dataset对PySpark 3笔记本进行读取和写入 {#magic}

随着[!DNL Spark] 2.4的引入，提供了`%dataset`自定义魔术以用于PySpark 3 ([!DNL Spark] 2.4)笔记本。 有关IPython内核中可用的魔术命令的更多详细信息，请访问[IPython魔术文档](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。


**用法**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**描述**

用于从[!DNL Data Science Workspace]笔记本（[!DNL PySpark] 3内核）读取或写入数据集的自定义[!DNL Python]魔术命令。

| 名称 | 描述 | 必需 |
| --- | --- | --- |
| `{action}` | 要对数据集执行的操作的类型。 有两个操作可用“读取”或“写入”。 | 是 |
| `--datasetId {id}` | 用于提供要读取或写入的数据集的ID。 | 是 |
| `--dataFrame {df}` | 熊猫的数据流。 <ul><li> 当操作为“读取”时，{df}是变量，其中数据集读取操作的结果可用（例如数据流）。 </li><li> 当操作为“写入”时，此数据流{df}将写入数据集。 </li></ul> | 是 |
| `--mode` | 更改数据读取方式的其他参数。 允许的参数为“batch”和“interactive”。 默认情况下，该模式设置为“批处理”。<br>建议您“交互”模式以在较小的数据集上提高查询性能。 | 是 |

>[!TIP]
>
>查看[笔记本数据限制](#notebook-data-limits)部分中的PySpark表，以确定`mode`是否应设置为`interactive`或`batch`。

**示例**

- **阅读示例**： `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **编写示例**： `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 在写入数据之前使用`df.cache()`缓存数据可以大大提高笔记本性能。 如果您收到以下任何错误，这将很有帮助：
> 
> - 由于暂存失败，作业已中止……只能压缩每个分区中具有相同元素数的RDD。
> - 远程RPC客户端已取消关联和其他内存错误。
> - 读取和写入数据集时性能不佳。
> 
> 有关详细信息，请参阅[疑难解答指南](../troubleshooting-guide.md)。

您可以使用以下方法在JupyterLab buy中自动生成上述示例：

选择JupyterLab左侧导航栏中的数据图标选项卡（突出显示如下）。 出现&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从要使用的数据集上的下拉菜单中选择&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;选项。 笔记本底部会显示一个可执行代码条目。

- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;生成读取单元格。
- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;生成写单元格。

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### 创建本地数据流 {#pyspark-create-dataframe}

要使用PySpark 3创建本地数据流，请使用SQL查询。 例如：

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
>您还可以指定可选种子样本，如withReplacement布尔值、双分数或长种子。

### 筛选[!DNL ExperienceEvent]数据 {#pyspark-filter-experienceevent}

访问和筛选PySpark笔记本中的[!DNL ExperienceEvent]数据集需要您提供数据集标识(`{DATASET_ID}`)、组织的IMS标识以及定义特定时间范围的筛选规则。 通过使用函数`spark.sql()`定义过滤时间范围，其中函数参数是SQL查询字符串。

以下单元格将[!DNL ExperienceEvent]数据集筛选为2019年1月1日至2019年12月31日终了期间专门存在的数据。

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Scala笔记本 {#scala-notebook}

以下文档包含有关以下概念的示例：

- [初始化sparkSession](#scala-initialize)
- [读取数据集](#read-scala-dataset)
- [写入数据集](#scala-write-dataset)
- [创建本地数据流](#scala-create-dataframe)
- [筛选ExperienceEvent数据](#scala-experienceevent)

### 初始化SparkSession {#scala-initialize}

所有Scala笔记本都要求您使用以下样板代码初始化会话：

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 读取数据集 {#read-scala-dataset}

在Scala中，您可以导入`clientContext`以获取和返回Experience Platform值，这样就无需定义变量，如`var userToken`。 在下面的Scala示例中，`clientContext`用于获取和返回读取数据集所需的所有值。

>[!IMPORTANT]
>
> 在写入数据之前使用`df.cache()`缓存数据可以大大提高笔记本性能。 如果您收到以下任何错误，这将很有帮助：
> 
> - 由于暂存失败，作业已中止……只能压缩每个分区中具有相同元素数的RDD。
> - 远程RPC客户端已取消关联和其他内存错误。
> - 读取和写入数据集时性能不佳。
> 
> 有关详细信息，请参阅[疑难解答指南](../troubleshooting-guide.md)。

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
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一个变量，表示用于读取和写入数据的Pandas数据流。 |
| user-token | 使用`clientContext.getUserToken()`自动获取的用户令牌。 |
| service-token | 使用`clientContext.getServiceToken()`自动获取的服务令牌。 |
| ims-org | 使用`clientContext.getOrgId()`自动获取的组织ID。 |
| api-key | 使用`clientContext.getApiKey()`自动获取的API密钥。 |

>[!TIP]
>
>查看[笔记本数据限制](#notebook-data-limits)部分中的Scala表以确定`mode`是否应设置为`interactive`或`batch`。

可以使用以下方法在JupyterLab buy中自动生成上述示例：

选择JupyterLab左侧导航栏中的数据图标选项卡（突出显示如下）。 出现&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从要使用的数据集上的下拉菜单中选择&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;选项。 笔记本底部会显示一个可执行代码条目。

与

- 使用&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;生成读取单元格。
- 使用&#x200B;**[!UICONTROL Write Data in Notebook]**&#x200B;生成写单元格。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 写入数据集 {#scala-write-dataset}

在Scala中，您可以导入`clientContext`以获取和返回Experience Platform值，这样就无需定义变量，如`var userToken`。 在下面的Scala示例中，`clientContext`用于定义和返回写入数据集所需的所有值。

>[!IMPORTANT]
>
> 在写入数据之前使用`df.cache()`缓存数据可以大大提高笔记本性能。 如果您收到以下任何错误，这将很有帮助：
> 
> - 由于暂存失败，作业已中止……只能压缩每个分区中具有相同元素数的RDD。
> - 远程RPC客户端已取消关联和其他内存错误。
> - 读取和写入数据集时性能不佳。
> 
> 有关详细信息，请参阅[疑难解答指南](../troubleshooting-guide.md)。

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
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一个变量，表示用于读取和写入数据的Pandas数据流。 |
| user-token | 使用`clientContext.getUserToken()`自动获取的用户令牌。 |
| service-token | 使用`clientContext.getServiceToken()`自动获取的服务令牌。 |
| ims-org | 使用`clientContext.getOrgId()`自动获取的组织ID。 |
| api-key | 使用`clientContext.getApiKey()`自动获取的API密钥。 |

>[!TIP]
>
>查看[笔记本数据限制](#notebook-data-limits)部分中的Scala表以确定`mode`是否应设置为`interactive`或`batch`。

### 创建本地数据流 {#scala-create-dataframe}

要使用Scala创建本地数据流，需要SQL查询。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 筛选[!DNL ExperienceEvent]数据 {#scala-experienceevent}

访问和筛选Scala笔记本中的[!DNL ExperienceEvent]数据集需要您提供数据集标识(`{DATASET_ID}`)、组织的IMS标识以及定义特定时间范围的筛选规则。 使用函数`spark.sql()`定义筛选时间范围，其中函数参数是SQL查询字符串。

以下单元格将[!DNL ExperienceEvent]数据集筛选为2019年1月1日至2019年12月31日终了期间专门存在的数据。

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

本文档介绍了使用JupyterLab笔记本访问数据集的一般准则。 有关查询数据集的更深入示例，请访问JupyterLab notebooks中的[查询服务](./query-service.md)文档。 有关如何浏览和可视化数据集的更多信息，请访问[使用笔记本分析数据](./analyze-your-data.md)上的文档。

## [!DNL Query Service]的可选SQL标记 {#optional-sql-flags-for-query-service}

此表概述了可用于[!DNL Query Service]的可选SQL标记。

| **标志** | **描述** |
| --- | --- |
| `-h`、`--help` | 显示帮助消息并退出。 |
| `-n`、`--notify` | 用于通知查询结果的切换选项。 |
| `-a`、`--async` | 使用此标记可异步执行查询，并可在查询执行时释放内核。 将查询结果分配给变量时，请务必谨慎，因为如果查询不完整，变量可能会未定义。 |
| `-d`、`--display` | 使用此标志可防止显示结果。 |
