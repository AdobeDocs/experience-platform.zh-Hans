---
keywords: Experience Platform；开发人员指南；数据科学工作区；热门主题；实时机器学习；节点参考；
solution: Experience Platform
title: 实时机器学习节点参考
topic-legacy: Nodes reference
description: 节点是图形的基本单位。 每个节点都执行特定任务，它们可以通过链接链接链接在一起，形成表示ML管线的图形。 由节点执行的任务表示对输入数据的操作，例如数据或模式的转换，或机器学习推理。 节点将变换或推断的值输出到下一个节点。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 实时机器学习节点参考(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习。 此功能位于alpha中，仍在测试中。 此文档可能会更改。

节点是图形的基本单位。 每个节点都执行特定任务，它们可以通过链接链接链接在一起，形成表示ML管线的图形。 由节点执行的任务表示对输入数据的操作，例如数据或模式的转换，或机器学习推理。 节点将变换或推断的值输出到下一个节点。

以下指南概述了实时机器学习支持的节点库。

## 发现要在ML管道中使用的节点

将以下代码复制到[!DNL Python]笔记本中，以视图所有可用节点。

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

标准节点建立在开放源数据科学库的基础上，如Pactis和ScikitLearn。

### ModelUpload

ModelUpload节点是一个内部Adobe节点，它采用model_path并将模型从本地模型路径上载到实时机器学习Blob存储。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXode是一个内部Adobe节点，它使用模型ID来拉取预训练的ONNX模型，并使用它对传入数据进行评分。

>[!TIP]
>
>以您希望将数据发送到ONNX模型以得分的相同顺序指定列。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊猫{#pandas}

下面的Pactis节点允许你导入任何`pd.DataFrame`方法或任何普通的Appotis顶级函数。 要了解关于Apnotics方法的更多信息，请访问[Appotics方法文档](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)。 有关顶级函数的详细信息，请访问[Apactis API参考指南，了解一般函数](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)。

以下节点使用`"import": "map"`将方法名称作为字符串导入参数中，然后将参数作为映射函数输入。 以下示例使用`{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`执行此操作。 映射到位后，您可以选择将`inplace`设置为`True`或`False`。 根据是否要应用转换，将`inplace`设置为`True`或`False`。 默认情况下，`"inplace": False`会创建新列。 为提供新列名称提供支持的设置将添加到后续发行版中。 最后一行`cols`可以是单列名称或列列表。 指定要应用转换的列。 在此示例中，指定了`device`。

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

ScikitLearn节点允许您导入任何ScikitLearn ML模型或缩放器。 有关示例中使用的任何值的详细信息，请使用下表：

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| 值 | 描述 |
| --- | --- |
| 功能 | 将特征输入到模型(字符串列表)。 <br> 例如： `browser`,  `device`, `login_page`  `product_page`,  `search_page` |
| 标签 | 目标列名称（字符串）。 |
| 模式 | 培训/测试（字符串）。 |
| model_path | 以onnx格式本地保存模型的路径。 |
| params.model | 模型（字符串）的绝对导入路径，例如：`sklearn.linear_model.LogisticRegression`。 |
| params.model_params | 模型超参数，有关详细信息，请参阅[sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)文档。 |
| node_instance.process(data_message_from_previous_node) | 方法`process()`从上一个节点获取DataMsg并应用转换。 这取决于当前使用的节点。 |

### Split

使用以下节点将数据帧拆分为多个列并通过传递`train_size`或`test_size`进行测试。 这将返回具有多索引的数据帧。 您可以使用以下示例`msg5.data.xs(“train”)`访问培训和测试数据帧。

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 后续步骤

下一步是创建节点，以便对实时机器学习模型进行评分。 有关详细信息，请访问[实时机器学习笔记本用户指南](./rtml-authoring-notebook.md)。
