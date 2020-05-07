---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: 为实时机器学习模型打分
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# 为实时机器学习模型打分

>[!IMPORTANT]
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

本教程向您展示如何使用实时机器学习节点对传入数据进行预处理并根据您的ONNX模型对其进行评分。

>[!IMPORTANT]
> - 节点中使用的函数无法序列化。 例如，在熊猫节点中使用的λ函数。
> - 手动完成边缘部署后有60秒的睡眠时间。 这可以转换为EdgeUtils的score_edge方法。


>[!NOTE]
>为了对用于实时机器学习的模型进行评分，您需要完成上一个教程，该教程 [将培训实时机器学习的模型](./training-ml-model.md)

## 创建新笔记本

在Adobe Experience Platform UI中，从数 **[!UICONTROL 据科]** 学中选择 *笔记本*。 接下来， **[!UICONTROL 选择Jupyter]** Lab，并允许一段时间加载环境。

![打开JupyterLab](../images/rtml/open-jupyterlab.png)

开始，从 **JupyterLab启动器中选** 择空白的Python 3笔记本。

![空白python](../images/rtml/python-blank.png)

## 导入和发现节点

开始，方法是为模型导入所有必需的包。 确保您计划用于节点创作的任何包均已导入。

>[!NOTE]
>您的导入列表可能会因您创建的模型而有所不同。

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

要查看可用节点的列表，请在笔记本中复制并粘贴以下示例。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

收到的响应是节点列表。

![列表附注](../images/rtml/node-list.png)

## 用于边缘评分的节点创作

接下来，您需要定义并创作边缘评分节点。 将示例 `model_id` 中的代码替换为您在上一个教程中完成培训时收到的模 [型ID](./training-ml-model.md)。 本例使用Pactys节点导入pd.DataDrame方法或通用的pactys顶级函数。 映射函数被导入并用于创建两个节点。 有关可用节点以及如何使用这些节点的详细信息，请访问节 [点参考指南](./node-reference.md)。

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## 构建图形DSL

创建节点后，下一步是将节点链在一起以创建图。

开始，方法是列出作为图形一部分的所有节点。

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

然后，将节点与边连接。 每个元组都是边连接。

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

连接节点后，构建图形。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## 发布到边缘

现在，您已创建了一个图，可以将图部署到边缘。

>[!IMPORTANT]
>不要经常向边缘发布，这会使边缘节点过载。 建议不要多次发布同一模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## 边缘客户端

发布到边缘后，评分由客户端的POST请求完成。 通常，这可以从需要ML分数的客户端应用程序中完成。 您也可以从邮递员处进行。 此处，EdgeUtils用于演示该过程。

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

评分完成后，将返回边缘URL、有效负荷和来自边缘的已评分输出。

![评分完成](../images/rtml/scoring-complete.png)

## 从边缘删除已部署的应用程序（可选）

>!![CAUTION]
此单元格用于删除已部署的边缘应用程序。 除非需要删除已部署的边缘应用程序，否则不要使用以下单元格。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 后续步骤

按照上面的教程，您已成功地对实时机器学习模型进行评分和部署。 如果要进一步了解可用于模型创作的节点，请访问节 [点参考指南](./node-reference.md)。



