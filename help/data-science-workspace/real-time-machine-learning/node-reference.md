---
keywords: Experience Platform；开发人员指南；Data Science Workspace；热门主题；实时机器学习；节点引用；
solution: Experience Platform
title: 实时机器学习节点参考
description: 节点是形成图形的基本单元。 每个节点执行特定的任务，并且它们可以使用链接链接链接在一起，以形成一个表示ML管道的图形。 节点执行的任务表示对输入数据的操作，例如数据或架构的转换或机器学习推断。 节点将转换值或推断值输出到下一个节点。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 实时机器学习节点引用(Alpha)

>[!IMPORTANT]
>
>实时机器学习尚未对所有用户可用。 此功能处于Alpha阶段，并且仍在测试中。 此文档可能会发生更改。

节点是形成图形的基本单元。 每个节点执行特定的任务，并且它们可以使用链接链接链接在一起，以形成一个表示ML管道的图形。 节点执行的任务表示对输入数据的操作，例如数据或架构的转换或机器学习推断。 节点将转换值或推断值输出到下一个节点。

以下指南概述了实时机器学习支持的节点库。

## 发现要在ML管道中使用的节点

将以下代码复制到 [!DNL Python] 笔记本以查看所有可用节点。

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**示例响应**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## 标准节点

标准节点基于开源数据科学库（如Pandas和ScikitLearn）构建。

### ModelUpload

ModelUpload节点是一个内部Adobe节点，它采用model_path并将模型从本地模型路径上载到实时机器学习blob存储。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode是一个内部Adobe节点，它获取模型ID以提取预训练的ONNX模型，并使用它来对传入数据进行评分。

>[!TIP]
>
>以您希望数据发送到ONNX模型评分的顺序指定列。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊猫 {#pandas}

以下Pandas节点允许您导入任何 `pd.DataFrame` 方法或任何常规的大熊猫顶级函数。 要了解有关Pandas方法的更多信息，请访问 [Pandas方法文档](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). 欲了解关于顶级功能的更多信息，请访问 [用于一般函数的Pandas API参考指南](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

以下节点使用 `"import": "map"` 将方法名称作为字符串导入到参数中，然后将参数作为映射函数输入。 下面的示例通过使用 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. 设置好地图后，您可以选择设置 `inplace` 作为 `True` 或 `False`. 设置 `inplace` 作为 `True` 或 `False` 基于是否想要就地应用转换。 默认情况下 `"inplace": False` 创建新列。 对提供新列名称的支持设置为在后续版本中添加。 最后一行 `cols` 可以是单个列名或列列表。 指定要应用转换的列。 在此示例中 `device` 已指定。

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

ScikitLearn节点允许您导入任何ScikitLearn ML模型或缩放器。 有关示例中使用的任何值的详细信息，请参阅下表：

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| 值 | 描述 |
| --- | --- |
| 功能 | 将功能输入到模型（字符串列表）。 <br> 例如： `browser`， `device`， `login_page`， `product_page`， `search_page` |
| label | 目标列名称（字符串）。 |
| 模式 | 训练/测试（字符串）。 |
| model_path | 以Onx格式本地存储模型的路径。 |
| params.model | 模型的绝对导入路径（字符串），例如： `sklearn.linear_model.LogisticRegression`. |
| params.model_params | 模型超参数，请参见 [sklearn API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 文档，以了解更多信息。 |
| node_instance.process(data_message_from_previous_node) | 方法 `process()` 从上一个节点获取DataMsg并应用转换。 这取决于当前使用的节点。 |

### 拆分

使用以下节点，通过测试将数据流拆分为训练集和测试集 `train_size` 或 `test_size`. 这会返回一个具有多索引的数据流。 您可以使用以下示例访问训练数据和测试数据流： `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 后续步骤

下一步是创建用于评分实时机器学习模型的节点。 欲知更多信息，请访问 [实时机器学习笔记本用户指南](./rtml-authoring-notebook.md).
