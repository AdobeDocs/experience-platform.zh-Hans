---
keywords: Experience Platform；开发人员指南；Data Science Workspace；热门主题；实时机器学习；节点引用；
solution: Experience Platform
title: 管理Real-time Machine Learning笔记本
description: 以下指南概述了在Adobe Experience Platform JupyterLab中构建实时机器学习应用程序所需的步骤。
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# 管理Real-time Machine Learning笔记本(Alpha)

>[!IMPORTANT]
>
>实时机器学习尚未对所有用户可用。 此功能处于Alpha阶段，并且仍在测试中。 此文档可能会发生更改。

以下指南概述了构建实时机器学习应用程序所需的步骤。 使用提供的Adobe **[!UICONTROL 实时ML]** Python笔记本模板，本指南涵盖培训模型、创建DSL、将DSL发布到Edge以及对请求进行评分。 在实施实时机器学习模型过程中，您应修改模板以符合数据集的需求。

## 创建实时机器学习笔记本

在Adobe Experience Platform UI中，选择 **[!UICONTROL Notebooks]** 从内部 **数据科学**. 接下来，选择 **[!UICONTROL JupyterLab]** 并留出一些时间来加载环境。

![打开JupyterLab](../images/rtml/open-jupyterlab.png)

此 [!DNL JupyterLab] 出现启动器。 向下滚动到 *实时机器学习* 并选择 **[!UICONTROL 实时ML]** 笔记本。 此时将打开一个模板，其中包含具有示例数据集的示例笔记本单元格。

![空白蟒](../images/rtml/authoring-notebook.png)

## 导入和发现节点

首先，导入模型所需的所有资源包。 确保已导入您计划用于节点创作的任何资源包。

>[!NOTE]
>
>导入列表可能会因您希望创建的模型而异。 此列表将随着时间推移添加新节点而更改。 请参阅 [节点参考指南](./node-reference.md) 以获取可用节点的完整列表。

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

以下代码单元格打印可用节点的列表。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![注释列表](../images/rtml/node-list.png)

## 训练实时机器学习模型

使用以下选项之一，您将 [!DNL Python] 用于读取、预处理和分析数据的代码。 接下来，您需要培训自己的ML模型，将其序列化为ONNX格式，然后将其上传到Real-time Machine Learning模型库。

- [在JupyterLab笔记本中训练您自己的模型](#training-your-own-model)
- [将您自己预先训练好的ONNX模型上传到JupyterLab Notebooks](#pre-trained-model-upload)

### 培训您自己的模型 {#training-your-own-model}

首先加载您的培训数据。

>[!NOTE]
>
>在 **实时ML** 模板， [汽车保险CSV数据集](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) 是从以下位置抓取的 [!DNL Github].

![加载训练数据](../images/rtml/load_training.png)

如果要从Adobe Experience Platform中使用数据集，请取消注释下面的单元格。 接下来，您需要替换 `DATASET_ID` 具有相应的值。

![rtml数据集](../images/rtml/rtml-dataset.png)

要在中访问数据集，请执行以下操作 [!DNL JupyterLab] 笔记本，选择 **数据** 选项卡的左侧导航 [!DNL JupyterLab]. 此 **[!UICONTROL 数据集]** 和 **[!UICONTROL 架构]** 目录出现。 选择 **[!UICONTROL 数据集]** 并右键单击，然后选择 **[!UICONTROL 浏览笔记本中的数据]** 选项。 笔记本底部会显示一个可执行代码条目。 这间手机有你的 `dataset_id`.

![数据集访问](../images/rtml/access-dataset.png)

完成后，右键单击并删除您在笔记本底部生成的单元格。

### 培训属性

使用提供的模板，修改中的任何培训属性 `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 准备模型

使用 **[!UICONTROL 实时ML]** 模板，您需要分析、预处理、训练和评估ML模型。 这是通过应用数据转换和构建培训管道来完成的。

**数据转换**

此 **[!UICONTROL 实时ML]** 模板 **数据转换** 需要修改单元格才能使用您自己的数据集。 通常，这涉及重命名列、数据汇总和数据准备/功能工程。

>[!NOTE]
>
>以下示例已使用进行压缩以提高可读性 `[ ... ]`. 请查看并展开 *实时ML* 完整代码单元格的模板数据转换部分。

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

运行提供的单元格以查看示例结果。 输出表从 `carinsurancedataset.csv` 数据集返回您定义的修改。

![数据转换示例](../images/rtml/table-return.png)

**培训管道**

接下来，您需要创建培训管道。 除了需要转换和生成ONNX文件之外，这看起来将与任何其他培训管道文件类似。

使用上一个单元格中定义的数据转换，修改模板。 以下高亮显示的代码用于在功能管道中生成ONNX文件。 请查看 *实时ML* 完整管道代码单元格的模板。

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

完成培训管道并通过数据转换修改数据后，请使用以下单元格运行培训。

```python
model = train(config_properties, df_final)
```

### 生成和上传ONNX模型

成功完成训练运行后，您需要生成ONNX模型并将经过训练的模型上传到Real-time Machine Learning模型存储区。 运行以下单元格后，您的ONNX模型会出现在左边栏中所有其他笔记本旁边。

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>更改 `model_path` 字符串值(`model.onnx`)，以更改模型的名称。

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>以下单元格不可编辑或删除，并且是实时机器学习应用程序运行所必需的。

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ONNX模型](../images/rtml/onnx-model-rail.png)

### 上传您自己经过预先培训的ONNX模型 {#pre-trained-model-upload}

使用位于以下位置的上传按钮： [!DNL JupyterLab] 笔记本电脑，将预训练的ONNX模型上传到 [!DNL Data Science Workspace] 笔记本环境。

![上传图标](../images/rtml/upload.png)

接下来，更改 `model_path` 中的字符串值 *实时ML* 笔记本以匹配您的ONNX型号名称。 完成后，运行 *设置模型路径* 单元格，然后运行 *将模型上传到RTML模型库* 单元格。 成功后，响应中会返回模型位置和模型ID。

![上传自己的模型](../images/rtml/upload-own-model.png)

## 域特定语言(DSL)创建

本节概述了创建DSL。 您即将创作节点，其中包括数据的所有预处理以及ONNX节点。 接下来，使用节点和边创建DSL图。 边使用基于元组的格式(node_1、node_2)连接节点。 图表不应有周期。

>[!IMPORTANT]
>
>必须使用ONNX节点。 如果没有ONNX节点，应用程序将失败。

### 节点创作

>[!NOTE]
>
> 根据使用的数据类型，您可能会有多个节点。 以下示例仅概述了 *实时ML* 模板。 请查看 *实时ML* 模板 *节点创作* 完整代码单元格的部分。

下面的Pandas节点使用 `"import": "map"` 将方法名称作为字符串导入到参数中，然后将参数作为映射函数输入。 下面的示例通过使用 `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. 设置好地图后，您可以选择设置 `inplace` 作为 `True` 或 `False`. 设置 `inplace` 作为 `True` 或 `False` 基于是否想要就地应用转换。 默认情况下 `"inplace": False` 创建新列。 对提供新列名称的支持设置为在后续版本中添加。 最后一行 `cols` 可以是单个列名或列列表。 指定要应用转换的列。 在此示例中 `leasing` 已指定。 有关可用节点及其使用方式的更多信息，请访问 [节点参考指南](./node-reference.md).

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### 构建DSL图

创建节点后，下一步是将节点链在一起以创建图形。

首先，通过构建数组列出图表中的所有节点。

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

接下来，用边缘连接节点。 每个元组是一个 [!DNL Edge] 连接。

>[!TIP]
>
> 由于节点之间是线性依赖的（每个节点都取决于前一个节点的输出），因此您可以使用简单的Python列表理解来创建链接。 如果一个节点依赖于多个输入，请添加您自己的连接。

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

连接节点后，构建图形。 下面的单元格是必需的，无法编辑或删除。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

完成后， `edge` 返回包含每个节点以及映射到这些节点的参数的对象。

![边缘返回](../images/rtml/edge-return.png)

## 发布到边缘（中心）

>[!NOTE]
>
>实时机器学习暂时部署到Adobe Experience Platform中心并由其管理。 有关其他详细信息，请访问 [实时机器学习架构](./home.md#architecture).

现在，您已创建了一个DSL图形，您可以将图形部署到 [!DNL Edge].

>[!IMPORTANT]
>
>不发布到 [!DNL Edge] 通常，这会使 [!DNL Edge] 节点。 不建议多次发布同一模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### 更新DSL并重新发布到Edge（可选）

如果您不需要更新DSL，可以跳至 [评分](#scoring).

>[!NOTE]
>
>只有在要更新已发布到Edge的现有DSL时，才需要以下单元格。

您的模型可能会继续发展。 可以使用新模型更新现有服务，而不是创建全新的服务。 您可以定义要更新的节点，为其分配新的ID，然后将新的DSL重新上传到 [!DNL Edge].

在以下示例中，节点0使用新ID进行更新。

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![已更新节点](../images/rtml/updated-node.png)

更新节点ID后，您可以将更新后的DSL重新发布到边缘。

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

您将返回更新后的DSL。

![已更新DSL](../images/rtml/updated-dsl.png)

## 评分 {#scoring}

发布到后 [!DNL Edge]，评分由客户的POST请求完成。 通常，这可以从需要ML分数的客户端应用程序完成。 您也可以从Postman执行此操作。 此 **[!UICONTROL 实时ML]** 模板使用EdgeUtils演示此过程。

>[!NOTE]
>
>评分开始前需要很短的处理时间。

```python
# Wait for the app to come up
import time
time.sleep(20)
```

使用在训练中使用的相同架构，生成样本评分数据。 此数据用于构建评分数据流，然后转换为评分词典。 请查看 *实时ML* 完整代码单元格的模板。

![评分数据](../images/rtml/generate-score-data.png)

### 对边缘端点计分

使用以下单元格(在 *实时ML* 要根据您的 [!DNL Edge] 服务。

![对边缘打分](../images/rtml/scoring-edge.png)

评分完成后， [!DNL Edge] URL、有效负载和评分输出 [!DNL Edge] 会返回。

## 从列出您部署的应用程序 [!DNL Edge]

要在页面上生成当前部署的应用程序列表，请执行以下操作 [!DNL Edge]，运行以下代码单元格。 无法编辑或删除此单元格。

```python
services = edge_utils.list_deployed_services()
print(services)
```

返回的响应是您部署的一系列服务。

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## 从删除已部署的应用程序或服务ID [!DNL Edge] （可选）

>[!CAUTION]
>
>此单元格用于删除已部署的Edge应用程序。 除非需要删除已部署的，否则请不要使用以下单元格 [!DNL Edge] 应用程序。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 后续步骤

按照上面的教程，您已成功培训ONNX模型并将其上传到Real-time Machine Learning模型库。 此外，您还为实时机器学习模型评分并部署了该模型。 如果您想了解有关可用于模型创作的节点的更多信息，请访问 [节点参考指南](./node-reference.md).
