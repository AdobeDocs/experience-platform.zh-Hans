---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；資料存取api；讀取python；寫入python
solution: Experience Platform
title: 在Data Science Workspace中使用Python存取資料
type: Tutorial
description: 以下檔案包含如何在Python中存取資料以用於資料科學工作區的範例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 在資料科學工作區中使用Python存取資料

以下檔案包含如何使用Python存取資料以用於資料科學工作區的範例。 如需使用JupyterLab筆記型電腦存取資料的詳細資訊，請造訪 [JupyterLab Notebooks資料存取](../jupyterlab/access-notebook-data.md) 說明檔案。

## 讀取資料集

設定環境變數並完成安裝後，現在可將您的資料集讀入pandas dataframe。

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 從資料集中選取欄

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 取得分割資訊：

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT子句

DISTINCT子句可讓您擷取列/欄層級的所有相異值，從回應中移除所有重複值。

使用 `distinct()` 函式如下所示：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

您可以在Python中使用某些運運算元，協助篩選資料集。

>[!NOTE]
>
>用於篩選的函式區分大小寫。

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

以下提供使用這些篩選函式的範例：

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY子句

ORDER BY子句允許接收的結果以特定順序（升序或降序）依指定資料行排序。 這是透過使用 `sort()` 函式。

使用 `sort()` 函式如下所示：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句可讓您限制從資料集接收的記錄數。

使用 `limit()` 函式如下所示：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句可讓您從頭開始略過資料列，以開始從後面傳回資料列。 在搭配LIMIT的情況下，這可用於在區塊中疊代列。

使用 `offset()` 函式如下所示：

```python
df = dataset_reader.offset(100).read()
```

## 寫入資料集

若要寫入資料集，您必須為資料集提供pandas資料流。

### 正在寫入熊貓資料流

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## 使用者空間目錄（檢查點）

若要讓工作執行時間更長，您可能需要儲存中繼步驟。 在類似的情況下，您可以讀取和寫入使用者空間。

>[!NOTE]
>
>資料的路徑為 **not** 已儲存。 您需要儲存其個別資料的對應路徑。

### 寫入使用者空間

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 從使用者空間讀取

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## 后续步骤

Adobe Experience Platform Data Science Workspace提供使用上述程式碼範例來讀取和寫入資料的配方範例。 如果您想進一步瞭解如何使用Python存取您的資料，請檢視 [資料科學工作區Python GitHub存放庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
