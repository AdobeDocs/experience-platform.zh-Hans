---
keywords: Experience Platform；开发人员指南；Data Science Workspace；热门主题；实时机器学习；节点引用；
solution: Experience Platform
title: 管理实时机器学习笔记本
description: 以下指南概述了在Adobe Experience Platform JupyterLab中构建实时机器学习应用程序所需的步骤。
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# 管理实时机器学习笔记本(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习功能。 此功能位于Alpha中，且仍在测试中。 本文档可能会更改。

以下指南概述了构建实时机器学习应用程序所需的步骤。 使用提供的Adobe **[!UICONTROL 实时ML]** Python笔记本模板，本指南涵盖培训模型、创建DSL、将DSL发布到Edge以及对请求打分。 在您实施实时机器学习模型的过程中，您应该根据数据集的需求修改模板。

## 创建实时机器学习笔记本

在Adobe Experience Platform UI中，选择 **[!UICONTROL 笔记本]** 从 **数据科学**. 接下来，选择 **[!UICONTROL JupyterLab]** 并允许一些时间加载环境。

![打开JupyterLab](../images/rtml/open-jupyterlab.png)

的 [!DNL JupyterLab] 出现启动器。 向下滚动到 *实时机器学习* ，然后选择 **[!UICONTROL 实时ML]** 笔记本。 此时会打开一个模板，其中包含带有示例数据集的示例笔记本单元格。

![空python](../images/rtml/authoring-notebook.png)

## 导入和发现节点

首先，为模型导入所有必需的包。 确保已导入您计划用于节点创作的任何包。

>[!NOTE]
>
>您的导入列表可能会因您希望创建的模型而异。 随着新节点的添加，此列表将会发生更改。 请参阅 [节点参考指南](./node-reference.md) 以获取可用节点的完整列表。

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

以下代码单元格打印可用节点列表。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![注释列表](../images/rtml/node-list.png)

## 实时机器学习模型的训练

使用下列选项之一，您将编写 [!DNL Python] 读取、预处理和分析数据的代码。 接下来，您需要培训自己的ML模型，将其序列化为ONNX格式，然后将其上传到实时机器学习模型存储。

- [在JupyterLab笔记本中培训您自己的型号](#training-your-own-model)
- [将您自己经过预先培训的ONNX型号上传到JupyterLab笔记本](#pre-trained-model-upload)

### 培训您自己的模型 {#training-your-own-model}

首先加载培训数据。

>[!NOTE]
>
>在 **实时ML** 模板， [车险CSV数据集](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) 从 [!DNL Github].

![加载培训数据](../images/rtml/load_training.png)

如果要在Adobe Experience Platform中使用数据集，请取消对下面单元格的注释。 接下来，您需要将 `DATASET_ID` 值。

![rtml数据集](../images/rtml/rtml-dataset.png)

访问 [!DNL JupyterLab] 笔记本，选择 **数据** 的左侧导航 [!DNL JupyterLab]. 的 **[!UICONTROL 数据集]** 和 **[!UICONTROL 模式]** 目录。 选择 **[!UICONTROL 数据集]** 并右键单击，然后选择 **[!UICONTROL 在笔记本中浏览数据]** 选项。 可执行代码条目出现在笔记本的底部。 这个细胞里 `dataset_id`.

![数据集访问](../images/rtml/access-dataset.png)

完成后，右键单击并删除您在笔记本底部生成的单元格。

### 培训属性

使用提供的模板，修改 `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 准备模型

使用 **[!UICONTROL 实时ML]** 模板，则需要分析、预处理、训练和评估ML模型。 这可以通过应用数据转换和构建培训管道来完成。

**数据转换**

的 **[!UICONTROL 实时ML]** 模板 **数据转换** 单元格需要进行修改才能与您自己的数据集配合使用。 通常，这包括重命名列、数据汇总和数据准备/功能工程。

>[!NOTE]
>
>出于可读性目的，以下示例已使用 `[ ... ]`. 请查看并展开 *实时ML* 完整代码单元格的模板数据转换部分。

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

运行提供的单元格以查看示例结果。 从 `carinsurancedataset.csv` 数据集会返回您定义的修改。

![数据转换示例](../images/rtml/table-return.png)

**培训管道**

接下来，您需要创建培训管道。 这将类似于任何其他培训管道文件，但需要转换并生成ONNX文件。

使用上一单元格中定义的数据转换，修改模板。 下面突出显示的代码用于在功能管道中生成ONNX文件。 请查看 *实时ML* 完整管道代码单元格的模板。

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

### 生成并上传ONNX模型

完成成功的培训运行后，需要生成ONNX模型，并将培训的模型上传到实时机器学习模型存储。 运行以下单元格后，ONNX型号会与所有其他笔记本一起显示在左边栏中。

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>更改 `model_path` 字符串值(`model.onnx`)以更改模型的名称。

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>以下单元格不可编辑或删除，并且要求您的实时机器学习应用程序正常工作。

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ONNX模型](../images/rtml/onnx-model-rail.png)

### 上传您自己预先培训的ONNX模型 {#pre-trained-model-upload}

使用位于 [!DNL JupyterLab] 笔记本，将您预先培训过的ONNX型号上传到 [!DNL Data Science Workspace] 笔记本环境。

![上传图标](../images/rtml/upload.png)

接下来，更改 `model_path` 字符串值(位于 *实时ML* 笔记本以匹配ONNX型号名称。 完成后，运行 *设置模型路径* 然后运行 *将模型上传到RTML模型存储* 单元格。 成功时，响应中会返回模型位置和模型ID。

![上传自己的模型](../images/rtml/upload-own-model.png)

## 域特定语言(DSL)创建

本节概述了如何创建DSL。 您将创作节点，其中包含任何数据预处理以及ONNX节点。 接下来，使用节点和边缘创建DSL图。 边缘使用基于元组的格式(node_1、node_2)连接节点。 图表不应具有循环。

>[!IMPORTANT]
>
>必须使用ONNX节点。 如果没有ONNX节点，应用程序将失败。

### 节点创作

>[!NOTE]
>
> 您可能会根据所使用的数据类型有多个节点。 以下示例仅概述了 *实时ML* 模板。 请查看 *实时ML* 模板 *节点创作* 部分。

下面的Pantics节点使用 `"import": "map"` 要将方法名称作为字符串导入参数中，然后将参数作为映射函数输入。 以下示例使用 `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. 映射到适当位置后，您可以选择设置 `inplace` as `True` 或 `False`. 已设置 `inplace` as `True` 或 `False` 根据是否要就地应用转换。 默认情况下 `"inplace": False` 创建新列。 将在后续版本中设置支持提供新列名称。 最后一行 `cols` 可以是单列名称或列列表。 指定要应用转换的列。 在本例中 `leasing` 指定。 有关可用节点及其使用方法的更多信息，请访问 [节点参考指南](./node-reference.md).

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

创建节点后，下一步是将节点链在一起以创建一个图。

首先，通过构建数组来列出图形中所包含的所有节点。

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

接下来，将节点与边连接起来。 每个元组都是 [!DNL Edge] 连接。

>[!TIP]
>
> 由于节点之间是相互线性依赖的（每个节点取决于前一个节点的输出），因此您可以使用简单的Python列表理解创建链接。 如果节点依赖于多个输入，请添加您自己的连接。

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

连接节点后，构建图。 以下单元格是必填的，无法编辑或删除。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

完成后， `edge` 返回的对象包含每个节点以及映射到这些节点的参数。

![边缘返回](../images/rtml/edge-return.png)

## 发布到Edge（中心）

>[!NOTE]
>
>实时机器学习功能临时部署到Adobe Experience Platform中心并由其管理。 有关更多详细信息，请访问 [实时机器学习架构](./home.md#architecture).

现在，您已创建DSL图表，接下来可以将图表部署到 [!DNL Edge].

>[!IMPORTANT]
>
>不发布到 [!DNL Edge] 通常，这会使负载过重 [!DNL Edge] 节点。 不建议多次发布同一模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### 更新DSL并重新发布到Edge（可选）

如果您不需要更新DSL，则可以跳到 [评分](#scoring).

>[!NOTE]
>
>仅当您希望更新已发布到Edge的现有DSL时，才需要以下单元格。

您的模型可能会继续开发。 与其创建全新服务，不如使用新模式更新现有服务。 您可以定义要更新的节点，为其分配新ID，然后将新DSL重新上传到 [!DNL Edge].

在以下示例中，节点0已更新为一个新ID。

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![更新的节点](../images/rtml/updated-node.png)

更新节点ID后，您可以将更新的DSL重新发布到边缘。

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

将返回更新的DSL。

![更新了DSL](../images/rtml/updated-dsl.png)

## 评分 {#scoring}

发布到 [!DNL Edge]，则评分由客户的POST请求完成。 通常，这可以从需要ML分数的客户端应用程序中完成。 您也可以从Postman执行此操作。 的 **[!UICONTROL 实时ML]** 模板使用EdgeUtils来演示此过程。

>[!NOTE]
>
>在开始评分之前，需要较短的处理时间。

```python
# Wait for the app to come up
import time
time.sleep(20)
```

使用与培训中使用的相同模式，生成样本评分数据。 此数据用于生成评分数据帧，然后转换为评分词典。 请查看 *实时ML* 模板。

![评分数据](../images/rtml/generate-score-data.png)

### 对边缘端点进行分数

在 *实时ML* 根据您的 [!DNL Edge] 服务。

![与边缘对比得分](../images/rtml/scoring-edge.png)

评分完成后， [!DNL Edge] 从 [!DNL Edge] 的次数。

## 从 [!DNL Edge]

要在 [!DNL Edge]，运行以下代码单元格。 无法编辑或删除此单元格。

```python
services = edge_utils.list_deployed_services()
print(services)
```

返回的响应是已部署服务的数组。

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

## 从中删除已部署的应用程序或服务ID [!DNL Edge] （可选）

>[!CAUTION]
>
>此单元格用于删除已部署的边缘应用程序。 除非需要删除已部署的 [!DNL Edge] 应用程序。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 后续步骤

按照上述教程，您已成功培训ONNX模型并将其上传到实时机器学习模型存储。 此外，您还对实时机器学习模型进行了评分并进行了部署。 如果您想进一步了解可用于模型创作的节点，请访问 [节点参考指南](./node-reference.md).
