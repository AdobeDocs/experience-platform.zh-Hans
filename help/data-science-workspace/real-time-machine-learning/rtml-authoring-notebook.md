---
keywords: Experience Platform；开发人员指南；数据科学工作区；热门主题；实时机器学习；节点参考；
solution: Experience Platform
title: 管理实时机器学习笔记本
topic-legacy: Training and scoring a ML model
description: 以下指南概述了在Adobe Experience Platform JupyterLab中构建实时机器学习应用程序所需的步骤。
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# 管理实时机器学习笔记本(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习。 此功能位于alpha中，仍在测试中。 此文档可能会更改。

以下指南概述了构建实时机器学习应用程序所需的步骤。 使用提供的&#x200B;**[!UICONTROL Real-time ML]** Python笔记本模板Adobe，本指南涵盖培训模型、创建DSL、将DSL发布到Edge并对请求打分。 在您实施实时机器学习模型的过程中，您需要修改模板以满足数据集的需求。

## 创建实时机器学习笔记本

在Adobe Experience Platform UI中，从&#x200B;**数据科学**&#x200B;中选择&#x200B;**[!UICONTROL Notebooks]**。 接下来，选择&#x200B;**[!UICONTROL JupyterLab]**，并为加载环境留出一些时间。

![打开JupyterLab](../images/rtml/open-jupyterlab.png)

出现[!DNL JupyterLab]启动器。 向下滚动至&#x200B;*Real-Time Machine Learning*&#x200B;并选择&#x200B;**[!UICONTROL Real-time ML]**&#x200B;笔记本。 此时会打开一个模板，其中包含带有示例数据集的示例笔记本单元格。

![blank python](../images/rtml/authoring-notebook.png)

## 导入和发现节点

开始，方法是为模型导入所有所需的包。 确保您计划用于节点创作的任何包都已导入。

>[!NOTE]
>
>您对导入的列表可能因您希望创建的模型而有所不同。 随着新节点的添加，此列表将随时间而改变。 有关可用节点的完整列表，请参阅[节点参考指南](./node-reference.md)。

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

![列表备注](../images/rtml/node-list.png)

## 实时机器学习模型的训练

使用以下选项之一，您即将编写[!DNL Python]代码以读取、预处理和分析数据。 接下来，您需要培训自己的ML模型，将其序列化为ONNX格式，然后将其上传到Real-time Machine Learning模型存储。

- [在JupyterLab笔记本中培训您自己的型号](#training-your-own-model)
- [将您自己预先训练好的ONNX模型上传到JupyterLab笔记本](#pre-trained-model-upload)

### 培训您自己的型号{#training-your-own-model}

开始。

>[!NOTE]
>
>在&#x200B;**实时ML**&#x200B;模板中，从[!DNL Github]中捕获[汽车保险CSV数据集](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance)。

![加载培训数据](../images/rtml/load_training.png)

如果您希望从Adobe Experience Platform中使用数据集，请取消以下单元格的注释。 接下来，您需要用相应的值替换`DATASET_ID`。

![rtml数据集](../images/rtml/rtml-dataset.png)

要访问[!DNL JupyterLab]笔记本中的数据集，请在[!DNL JupyterLab]的左侧导航中选择&#x200B;**数据**&#x200B;选项卡。 将显示&#x200B;**[!UICONTROL Datasets]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目录。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;并右键单击，然后从您要使用的数据集的下拉菜单中选择&#x200B;**[!UICONTROL Explore Data in Notebook]**&#x200B;选项。 可执行代码条目显示在笔记本的底部。 此单元格包含您的`dataset_id`。

![数据集访问](../images/rtml/access-dataset.png)

完成后，右键单击并删除您在笔记本底部生成的单元格。

### 培训属性

使用提供的模板，修改`config_properties`中的任何培训属性。

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 准备模型

使用&#x200B;**[!UICONTROL Real-time ML]**&#x200B;模板，您需要分析、预处理、培训和评估ML模型。 通过应用数据转换和构建培训管道来完成此操作。

**数据转换**

需要修改&#x200B;**[!UICONTROL Real-time ML]**&#x200B;模板&#x200B;**数据转换**&#x200B;单元格，才能使用您自己的数据集。 通常，这涉及重命名列、数据汇总以及数据准备/功能工程。

>[!NOTE]
>
>以下示例已使用`[ ... ]`进行压缩以用于可读性。 请视图并展开完整代码单元格的&#x200B;*实时ML*&#x200B;模板数据转换部分。

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid' : 'ecid',
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

df1['city'] = df1.groupby('country')['city'].transform(lambda x : x.fillna(x.mode()))
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

运行提供的单元格以查看示例结果。 从`carinsurancedataset.csv`数据集返回的输出表返回您定义的修改。

![数据转换示例](../images/rtml/table-return.png)

**培训渠道**

然后，您需要创建培训管道。 除了需要转换和生成ONNX文件外，这看起来与任何其他培训管道文件相似。

使用在上一个单元格中定义的数据转换，修改模板。 下面突出显示的代码用于在功能管道中生成ONNX文件。 请视图&#x200B;*实时ML*&#x200B;模板，以获取完整的管道代码单元格。

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

完成成功的培训运行后，您需要生成一个ONNX模型并将培训的模型上传到Real-time Machine Learning模型存储。 运行以下单元格后，您的ONNX型号将与所有其他笔记本一起显示在左边栏中。

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>更改`model_path`字符串值(`model.onnx`)以更改模型的名称。

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>以下单元格不可编辑或删除，并且需要该单元格才能使用实时机器学习应用程序。

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

![ONNX模型](../images/rtml/onnx-model-rail.png)

### 上传您自己预先培训的ONNX模型{#pre-trained-model-upload}

使用位于[!DNL JupyterLab]笔记本中的上载按钮，将您预先培训的ONNX型号上载到[!DNL Data Science Workspace]笔记本环境。

![上载图标](../images/rtml/upload.png)

接下来，更改&#x200B;*实时ML*&#x200B;笔记本中的`model_path`字符串值以匹配您的ONNX型号名称。 完成后，运行&#x200B;*设置模型路径*&#x200B;单元格，然后运行&#x200B;*将模型上传到RTML模型存储*&#x200B;单元格。 成功时，您的模型位置和模型ID都会在响应中返回。

![上传自己的模型](../images/rtml/upload-own-model.png)

## 域特定语言(DSL)创建

本节概述创建DSL。 您即将创作包含任何数据预处理的节点，以及ONNX节点。 接下来，使用节点和边创建DSL图。 边缘使用基于元组的格式(node_1、node_2)连接节点。 图形不应具有循环。

>[!IMPORTANT]
>
>必须使用ONNX节点。 如果没有ONNX节点，应用程序将失败。

### 节点创作

>[!NOTE]
>
> 您可能会根据所使用的数据类型有多个节点。 下面的示例仅概述&#x200B;*实时ML*&#x200B;模板中的单个节点。 请视图完整代码单元格的&#x200B;*实时ML*&#x200B;模板&#x200B;*节点创作*&#x200B;部分。

下面的Pacnots节点使用`"import": "map"`将方法名称作为字符串导入参数中，然后输入参数作为映射函数。 以下示例使用`{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`执行此操作。 映射到位后，您可以选择将`inplace`设置为`True`或`False`。 根据是否要应用转换，将`inplace`设置为`True`或`False`。 默认情况下，`"inplace": False`会创建新列。 为提供新列名称提供支持的设置将添加到后续发行版中。 最后一行`cols`可以是单列名称或列列表。 指定要应用转换的列。 在此示例中，指定了`leasing`。 有关可用节点以及如何使用这些节点的详细信息，请访问[节点参考指南](./node-reference.md)。

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

开始，通过构建数组来列出图形的所有节点。

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

接下来，将节点与边连接。 每个元组都是[!DNL Edge]连接。

>[!TIP]
>
> 由于节点之间是线性相关的（每个节点都取决于前一个节点的输出），您可以使用简单的Python列表理解创建链接。 如果节点依赖多个输入，请添加您自己的连接。

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

连接节点后，构建图。 以下单元格为必填项，无法编辑或删除。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

完成后，将返回一个`edge`对象，其中包含每个节点以及映射到这些节点的参数。

![edge retur](../images/rtml/edge-return.png)

## 发布到边缘（集线器）

>[!NOTE]
>
>实时机器学习临时部署到Adobe Experience Platform Hub并由其管理。 有关其他详细信息，请访问[实时机器学习架构](./home.md#architecture)的概述部分。

现在您已创建了DSL图形，可以将图形部署到[!DNL Edge]。

>[!IMPORTANT]
>
>不要经常发布到[!DNL Edge]，这会使[!DNL Edge]节点过载。 建议不要多次发布同一模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### 更新DSL并重新发布到Edge（可选）

如果不需要更新DSL，可跳至[评分](#scoring)。

>[!NOTE]
>
>仅当您希望更新已发布到Edge的现有DSL时，才需要以下单元格。

您的模型可能会不断发展。 与其创建全新服务，不如使用新模型更新现有服务。 您可以定义要更新的节点，为其分配新ID，然后将新DSL重新上传到[!DNL Edge]。

在以下示例中，节点0会使用新ID进行更新。

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![更新的节点](../images/rtml/updated-node.png)

更新节点ID后，您可以将更新的DSL重新发布到Edge。

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

您将返回更新的DSL。

![更新的DSL](../images/rtml/updated-dsl.png)

## 评分{#scoring}

发布到[!DNL Edge]后，评分由客户端的POST请求完成。 通常，这可以从需要ML分数的客户端应用程序中完成。 您也可以从邮递员那里做。 **[!UICONTROL Real-time ML]**&#x200B;模板使用EdgeUtils演示此过程。

>[!NOTE]
>
>在对开始评分之前，需要少量处理时间。

```python
# Wait for the app to come up
import time
time.sleep(20)
```

使用与培训中使用的模式相同的内容，生成样本评分数据。 此数据用于构建一个评分数据帧，然后转换为评分词典。 请视图完整代码单元格的&#x200B;*实时ML*&#x200B;模板。

![评分数据](../images/rtml/generate-score-data.png)

### 对Edge端点进行分数

使用&#x200B;*实时ML*&#x200B;模板中的以下单元格对[!DNL Edge]服务进行评分。

![对边缘得分](../images/rtml/scoring-edge.png)

评分完成后，将返回[!DNL Edge]中的[!DNL Edge] URL、Payload和计分输出。

## 从[!DNL Edge]列表已部署的应用程序

要在[!DNL Edge]上生成当前部署的应用程序的列表，请运行以下代码单元格。 无法编辑或删除此单元格。

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

## 从[!DNL Edge]中删除已部署的应用程序或服务ID（可选）

>[!CAUTION]
>
>此单元格用于删除已部署的Edge应用程序。 除非需要删除已部署的[!DNL Edge]应用程序，否则不要使用以下单元格。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 后续步骤

通过上面的教程，您成功地培训了ONNX模型并将其上传到实时机器学习模型存储。 此外，您还对实时机器学习模型进行了评分和部署。 如果您想了解有关可用于模型创作的节点的更多信息，请访问[节点参考指南](./node-reference.md)。
