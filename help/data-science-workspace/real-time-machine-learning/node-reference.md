---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: 实时机器学习节点参考指南
topic: Nodes reference
translation-type: tm+mt
source-git-commit: dc63ad0c0764355aed267eccd1bcc4965b04dba4
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# 实时机器学习节点参考指南(Alpha)

>[!IMPORTANT]
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

节点是图形形成的基本单位。 每个节点都执行特定任务，可以使用链接将它们链在一起，以形成表示ML管道的图。 由节点执行的任务表示对输入数据的操作，如数据的转换或模式，或机器学习推理。 节点将转换或推断的值输出到下一个节点。

以下指南概述了实时机器学习支持的节点库。

## 发现要在ML管道中使用的节点

将以下代码复制到Python笔记本中，以视图所有可用节点。

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

标准节点建立在开放源码数据科学库的基础上，如Pactys和ScikitLearn。

### 模型上传

ModelUpload节点是一个内部Adobe节点，它采用model_path并将模型从本地模型路径上传到实时机器学习Blob存储。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXode是一个内部Adobe节点，它使用模型ID拉取预先训练好的ONNX模型，并使用它对传入数据进行评分。

>[!TIP]
>按您希望将数据发送到ONNX模型以得分的相同顺序指定列。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊猫 {#pandas}

下面的熊猫节点可以导入任何方 `pd.DataFrame` 法或普通熊猫的顶级功能。 要了解更多关于熊猫方法的信息，请访 [问熊猫方法文件](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)。 有关顶级功能的更多信息，请访 [问Apcots API参考指南以了解一般功能](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)。

以下节点使 `"import": "map"` 用将方法名称作为字符串导入到参数中，然后将参数输入为映射函数。 以下示例通过使用实现 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`。 在将地图置于适当位置后，您可以选择将其 `inplace` 设置为 `True` 或 `False`。 设 `inplace` 置 `True` 为 `False` 还是基于是否要就地应用转换。 默认情 `"inplace": False` 况下，创建新列。 支持提供新列名称设置为在后续版本中添加。 最后一行 `cols` 可以是单列名称或列列表。 指定要应用转换的列。 在此示例中 `device` 指定。

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

通过ScikitLearn节点，可导入任何ScikitLearn ML模型或缩放器。 有关示例中使用的任何值的详细信息，请使用下表：

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
| 特征 | 输入模型的特征(字符串的列表)。 <br> 例如： `browser`, `device`, `login_page`, `product_page``search_page` |
| 标签 | 目标列名称（字符串）。 |
| 模式 | 培训／测试（字符串）。 |
| model_path | 以onnx格式本地保存模型的路径。 |
| params.model | 模型（字符串）的绝对导入路径，例如： `sklearn.linear_model.LogisticRegression`. |
| params.model_params | 模型超参数，请参 [阅sklearn API(map/dict)文档](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) ，以了解更多信息。 |
| node_instance.process(data_message_from_previous_node) | 该方法 `process()` 从前一个节点获取DataMsg并应用转换。 这取决于当前使用的节点。 |

### 拆分

使用以下节点将数据帧拆分为培训并通过或进行 `train_size` 测试 `test_size`。 这将返回具有多索引的数据帧。 您可以使用以下示例访问培训和测试数据帧 `msg5.data.xs(“train”)`。

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 后续步骤

下一步是创建用于对实时机器学习模型进行评分的节点。 有关详细信息，请 [访问实时机器学习笔记本用户指南](./rtml-authoring-notebook.md)。
