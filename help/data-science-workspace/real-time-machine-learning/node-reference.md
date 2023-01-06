---
keywords: Experience Platform；开发人员指南；Data Science Workspace；热门主题；实时机器学习；节点引用；
solution: Experience Platform
title: 实时机器学习节点参考
description: 节点是形成图的基本单位。 每个节点都执行特定任务，并且可以使用链接将它们链接在一起，以形成表示ML管道的图形。 节点执行的任务表示对输入数据的操作，如数据或模式的转换或机器学习推理。 节点将转换或推断的值输出到下一个节点。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 实时机器学习节点引用(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习功能。 此功能位于Alpha中，且仍在测试中。 本文档可能会更改。

节点是形成图的基本单位。 每个节点都执行特定任务，并且可以使用链接将它们链接在一起，以形成表示ML管道的图形。 节点执行的任务表示对输入数据的操作，如数据或模式的转换或机器学习推理。 节点将转换或推断的值输出到下一个节点。

以下指南概述了用于实时机器学习的受支持节点库。

## 了解要在ML管道中使用的节点

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

标准节点构建在开源数据科学库（如Pantics和ScikitLearn）之上。

### ModelUpload

ModelUpload节点是一个内部Adobe节点，它采用model_path，并将模型从本地模型路径上传到实时机器学习Blob存储。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXode是一个内部Adobe节点，它采用模型ID来提取预先训练好的ONNX模型，并使用它对传入数据进行评分。

>[!TIP]
>
>以您希望将数据发送到ONNX模型进行评分的相同顺序指定列。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊猫 {#pandas}

以下Pantics节点允许您导入任何 `pd.DataFrame` 方法或任何普通熊猫的顶级功能。 要进一步了解Pantics的方法，请访问 [Pantics方法文档](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). 有关顶级功能的更多信息，请访问 [Pantics API一般功能参考指南](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

以下节点使用 `"import": "map"` 要将方法名称作为字符串导入参数中，然后将参数作为映射函数输入。 以下示例使用 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. 映射到适当位置后，您可以选择设置 `inplace` as `True` 或 `False`. 已设置 `inplace` as `True` 或 `False` 根据是否要就地应用转换。 默认情况下 `"inplace": False` 创建新列。 将在后续版本中设置支持提供新列名称。 最后一行 `cols` 可以是单列名称或列列表。 指定要应用转换的列。 在本例中 `device` 指定。

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
| 功能 | 输入模型特征（字符串列表）。 <br> 例如： `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Target列名称（字符串）。 |
| 模式 | 培训/测试（字符串）。 |
| model_path | 以onnx格式在本地保存模型的路径。 |
| params.model | 模型的绝对导入路径（字符串），例如： `sklearn.linear_model.LogisticRegression`. |
| params.model_params | 模型超参数，请参阅 [sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 文档以了解更多信息。 |
| node_instance.process(data_message_from_previous_node) | 方法 `process()` 从前一个节点获取数据消息并应用转换。 这取决于当前使用的节点。 |

### 拆分

使用以下节点将数据帧拆分为多个类型，并通过 `train_size` 或 `test_size`. 这会返回具有多索引的数据帧。 您可以使用以下示例访问培训和测试数据帧， `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 后续步骤

下一步是创建用于对实时机器学习模型进行评分的节点。 有关更多信息，请访问 [实时机器学习笔记本用户指南](./rtml-authoring-notebook.md).
