---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api
solution: Experience Platform
title: 安全Python数据访问SDK
topic: tutorial
type: Tutorial
description: Secure Python Data Access SDK是一个软件开发工具包，它支持读取和写入来自Adobe Experience Platform的数据集。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---


# 安全 [!DNL Python][!DNL Data Access] SDK

Secure SDK [!DNL Python] 是一 [!DNL Data Access] 个软件开发工具包，它支持读取和写入来自Adobe Experience Platform的数据集。

## 入门指南

您必须已完成身份 [验证](../../tutorials/authentication.md) 教程，才能访问这些值以调用安全 [!DNL Python][!DNL Data Access] SDK:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 使用 [!DNL Python] SDK需要操作将在以下位置进行的沙箱的名称和ID:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 环境设置

默认情况下，服务端点设置为集成环境端点。 因此，要指向生产，请将以下环境变量设置为以下值：

| Variable | 端点 |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

此外，您的凭据也可以添加为环境变量。

| Variable | 值 |
| -------- | ----- |
| `ORG_ID` | 你的 `{IMS_ORG}` 身份。 |
| `SERVICE_API_KEY` | 您的 `{API_KEY}` 价值。 |
| `USER_TOKEN` | 您的 `{ACCESS_TOKEN}` 价值。 |
| `SERVICE_TOKEN` | 您 `{SERVICE_TOKEN}`的，您可能需要对服务之间的后渠道请求授权。 |
| `SANDBOX_ID` | 沙 `{SANDBOX_ID}` 箱的值。 |
| `SANDBOX_NAME` | 沙 `{SANDBOX_NAME}` 箱的值。 |

## 安装

所有包装在建筑后 `./dist` 输出。

### 车轮

```python
python3 setup.py bdist_wheel --universal
```

从项目目录，将轮载到您的 [!DNL Python] 3环境。

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### 鸡蛋文件

```python
python3 setup.py bdist_egg
```

## 读取数据集

设置环境变量并完成安装后，数据集现在可以读入熊猫数据框。

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### 数据集中的SELECT列

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 获取分区信息：

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT子句

DISTINCT子句允许您在行／列级别提取所有不同值，从响应中删除所有重复值。

使用函数的示 `distinct()` 例如下所示：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

SDK [!DNL Python] 支持某些操作符以帮助过滤数据集。

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

ORDER BY子句允许按指定列按特定顺序（升序或降序）对接收结果进行排序。 在SDK [!DNL Python] 中，这是使用函数完 `sort()` 成的。

使用函数的示 `sort()` 例如下所示：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允许用户限制从数据集接收的记录数。

使用函数的示 `limit()` 例如下所示：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允许用户从开始跳过行，从后一点开始返回行。 与LIMIT结合使用，可用于对块中的行进行迭代。

使用函数的示 `offset()` 例如下所示：

```python
df = dataset_reader.offset(100).read()
```

## 编写数据集

SDK支 [!DNL Python] 持编写数据集。 用户需要提供需要写入数据集的熊猫数据框。

### 编写熊猫数据框

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Userspace目录（检查点）

对于运行时间较长的作业，用户可能需要存储中间步骤。 在这种情况下， [!DNL Python] SDK为用户提供了读写用户空间的能力。

>[!NOTE]
>
>数据路径不 **由** SDK存储。 用户需要存储到其相应数据的相应路径。

### 写入用户空间

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 从用户空间读取

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
