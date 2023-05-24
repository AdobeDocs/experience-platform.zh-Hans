---
keywords: Experience Platform；開發人員指南；Data Science Workspace；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 管理Real-time Machine Learning筆記本
description: 以下指南概述在Adobe Experience Platform JupyterLab中建置Real-time Machine Learning應用程式所需的步驟。
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# 管理Real-time Machine Learning筆記本(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未開放所有使用者使用。 此功能目前處於Alpha測試階段，仍在測試中。 此檔案可能會有變動。

下列指南會概述建置Real-time Machine Learning應用程式所需的步驟。 使用提供的Adobe **[!UICONTROL 即時ML]** Python筆記型電腦範本，本指南涵蓋訓練模型、建立DSL、將DSL發佈至Edge，以及評分請求。 當您逐步實作即時機器學習模型時，預計您會修改範本以符合資料集的需求。

## 建立Real-time Machine Learning筆記本

在Adobe Experience Platform UI中，選取 **[!UICONTROL Notebooks]** 從內部 **資料科學**. 接下來，選取 **[!UICONTROL JupyterLab]** 並留出一些時間來載入環境。

![開啟JupyterLab](../images/rtml/open-jupyterlab.png)

此 [!DNL JupyterLab] 啟動器隨即出現。 向下捲動至 *即時機器學習* 並選取 **[!UICONTROL 即時ML]** notebook。 範本隨即開啟，其中包含範例筆記本儲存格和範例資料集。

![空白python](../images/rtml/authoring-notebook.png)

## 匯入和探索節點

首先，匯入模型的所有必要套件。 請確定已匯入您計畫用於節點編寫的任何套件。

>[!NOTE]
>
>您的匯入清單可能會因您想要建立的模型而異。 此清單將隨著時間新增新節點而變更。 請參閱 [節點參考指南](./node-reference.md) 以取得可用節點的完整清單。

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

下列程式碼儲存格會列印可用節點清單。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![附註清單](../images/rtml/node-list.png)

## 訓練Real-time Machine Learning模型

您即將使用下列其中一個選項，撰寫 [!DNL Python] 讀取、預處理和分析資料的程式碼。 接下來，您需要訓練自己的ML模型、將其序列化為ONNX格式，然後將其上傳到Real-time Machine Learning模型存放區。

- [在JupyterLab筆記型電腦中訓練您自己的模型](#training-your-own-model)
- [將您自己預先訓練好的ONNX模型上傳至JupyterLab Notebooks](#pre-trained-model-upload)

### 訓練您自己的模型 {#training-your-own-model}

從載入您的訓練資料開始。

>[!NOTE]
>
>在 **即時ML** 範本， [汽車保險CSV資料集](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) 已擷取自 [!DNL Github].

![載入訓練資料](../images/rtml/load_training.png)

如果您想要使用Adobe Experience Platform中的資料集，請取消註解下方的儲存格。 接下來，您需要取代 `DATASET_ID` 具有適當的值。

![rtml資料集](../images/rtml/rtml-dataset.png)

若要存取中的資料集 [!DNL JupyterLab] 記事本，選取 **資料** 索引標籤中位於左側導覽列中的 [!DNL JupyterLab]. 此 **[!UICONTROL 資料集]** 和 **[!UICONTROL 結構描述]** 目錄出現。 選取 **[!UICONTROL 資料集]** 並按一下滑鼠右鍵，然後選取 **[!UICONTROL 探索筆記本中的資料]** 從下拉式選單中選取您要使用的選項。 筆記本底部會出現一個可執行程式碼專案。 此儲存格具有 `dataset_id`.

![資料集存取權](../images/rtml/access-dataset.png)

完成後，按一下滑鼠右鍵並刪除您在筆記本底部產生的儲存格。

### 訓練屬性

使用提供的範本，修改內的任何訓練屬性 `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 準備您的模型

使用 **[!UICONTROL 即時ML]** 範本，您需要分析、預先處理、訓練及評估您的ML模型。 這是透過套用資料轉換和建立培訓管道來完成的。

**資料轉換**

此 **[!UICONTROL 即時ML]** 範本 **資料轉換** 需要修改儲存格，才能使用您自己的資料集。 這通常涉及重新命名欄、資料彙總和資料準備/功能工程。

>[!NOTE]
>
>為了方便閱讀，以下範例已使用以下進行壓縮 `[ ... ]`. 請檢視並展開 *即時ML* 完整程式碼儲存格的範本資料轉換區段。

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

執行提供的儲存格以檢視範例結果。 從傳回的輸出表格 `carinsurancedataset.csv` 資料集會傳回您定義的修改。

![資料轉換範例](../images/rtml/table-return.png)

**訓練管道**

接下來，您需要建立培訓管道。 除了您需要轉換和產生ONNX檔案外，這看起來將與任何其他培訓管道檔案類似。

使用先前儲存格中定義的資料轉換，修改範本。 以下醒目提示的程式碼用於在功能管道中產生ONNX檔案。 請檢視 *即時ML* 完整管道程式碼儲存格的範本。

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

完成培訓管道並透過資料轉換修改資料後，請使用以下儲存格執行培訓。

```python
model = train(config_properties, df_final)
```

### 產生和上傳ONNX模型

當您完成成功的訓練回合後，您需要產生ONNX模型並將經過訓練的模型上傳到Real-time Machine Learning模型存放區。 執行以下儲存格後，您的ONNX模型會出現在左側邊欄中，與您的所有其他Notebook並列。

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>變更 `model_path` 字串值(`model.onnx`)，以變更模型的名稱。

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>下列儲存格不可編輯或刪除，且您的Real-time Machine Learning應用程式需要此儲存格才能運作。

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ONNX模型](../images/rtml/onnx-model-rail.png)

### 上傳您自己預先訓練的ONNX模型 {#pre-trained-model-upload}

使用位於以下位置的上傳按鈕： [!DNL JupyterLab] 筆記型電腦，將預先訓練好的ONNX模型上傳至 [!DNL Data Science Workspace] 筆記型電腦環境。

![上傳圖示](../images/rtml/upload.png)

接下來，變更 `model_path` 中的字串值 *即時ML* 記事本以符合您的ONNX型號名稱。 完成後，請執行 *設定模型路徑* 儲存格，然後執行 *上傳您的模型至RTML模型存放區* 儲存格。 成功時，您的模型位置和模型ID都會在回應中傳回。

![上傳自己的模型](../images/rtml/upload-own-model.png)

## 網域特定語言(DSL)建立

本節概述如何建立DSL。 您即將編寫節點，其中包含資料的任何前置處理以及ONNX節點。 接下來，會使用節點和邊來建立DSL圖形。 邊會使用元組格式(node_1、node_2)連線節點。 圖表不應有週期。

>[!IMPORTANT]
>
>必須使用ONNX節點。 如果沒有ONNX節點，應用程式將會失敗。

### 節點製作

>[!NOTE]
>
> 根據使用的資料型別，您可能會有多個節點。 以下範例僅概述 *即時ML* 範本。 請檢視 *即時ML* 範本 *節點製作* 區段來代表完整的程式碼儲存格。

以下的Pandas節點使用 `"import": "map"` 將方法名稱匯入為引數中的字串，接著將引數輸入為對應函式。 以下範例使用來達成此目的 `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. 完成地圖設定後，您就可以選擇設定 `inplace` 作為 `True` 或 `False`. 設定 `inplace` 作為 `True` 或 `False` 根據您是否要套用轉換。 依預設 `"inplace": False` 建立新欄。 提供新欄名稱的支援已設定為在後續版本中新增。 最後一行 `cols` 可以是單一欄名稱或欄清單。 指定要套用轉換的欄。 在此範例中 `leasing` 已指定。 如需可用節點及其使用方式的詳細資訊，請造訪 [節點參考指南](./node-reference.md).

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

### 建立DSL圖表

建立節點後，下一步是將節點鏈結在一起以建立圖形。

首先，請建立陣列，列出圖表中的所有節點。

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

接下來，用邊緣連線節點。 每個元組都是 [!DNL Edge] 連線。

>[!TIP]
>
> 由於節點彼此線性相依（每個節點都取決於前一個節點的輸出），因此您可以使用簡單的Python清單理解來建立連結。 如果節點依賴多個輸入，請新增您自己的連線。

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

連線節點後，請建立圖表。 下方的儲存格為必要儲存格，無法編輯或刪除。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

完成後， `edge` 傳回物件，其中包含每個節點以及與節點對應的引數。

![邊緣傳回](../images/rtml/edge-return.png)

## 發佈至邊緣（中樞）

>[!NOTE]
>
>即時機器學習暫時部署至Adobe Experience Platform中心並由其管理。 如需其他詳細資訊，請瀏覽以下連結的概觀區段： [Real-time Machine Learning架構](./home.md#architecture).

現在您已建立DSL圖表，您可以將圖表部署至 [!DNL Edge].

>[!IMPORTANT]
>
>不要發佈至 [!DNL Edge] 這通常會導致 [!DNL Edge] 節點。 不建議多次發佈相同的模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### 更新DSL並重新發佈至Edge （可選）

如果您不需要更新DSL，可以跳至 [評分](#scoring).

>[!NOTE]
>
>只有當您想要更新已發佈至Edge的現有DSL時，才需要下列儲存格。

您的模型可能會繼續開發。 您可以使用新模型更新現有服務，而不必建立全新的服務。 您可以定義要更新的節點、指派新ID，然後將新DSL重新上傳至 [!DNL Edge].

在以下範例中，節點0會以新ID更新。

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![已更新節點](../images/rtml/updated-node.png)

更新節點ID後，您可以將更新後的DSL重新發佈至Edge。

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

您會傳回更新後的DSL。

![已更新DSL](../images/rtml/updated-dsl.png)

## 評分 {#scoring}

發佈至後 [!DNL Edge]，評分是透過使用者端的POST要求完成。 通常可從需要ML分數的使用者端應用程式執行此操作。 您也可以從Postman執行此操作。 此 **[!UICONTROL 即時ML]** 範本使用EdgeUtils來示範此程式。

>[!NOTE]
>
>評分開始前需要很短的處理時間。

```python
# Wait for the app to come up
import time
time.sleep(20)
```

使用訓練中使用的相同結構描述，會產生樣本評分資料。 此資料用於建立評分資料流，然後轉換為評分字典。 請檢視 *即時ML* 完整程式碼儲存格的範本。

![評分資料](../images/rtml/generate-score-data.png)

### 對邊緣端點計分

使用下列儲存格於 *即時ML* 要針對您的評分的範本 [!DNL Edge] 服務。

![對邊緣計分](../images/rtml/scoring-edge.png)

評分完成後， [!DNL Edge] URL、承載和已評分的輸出 [!DNL Edge] 會傳回。

## 從列出您部署的應用程式 [!DNL Edge]

若要在上產生目前部署的應用程式清單 [!DNL Edge]，請執行以下程式碼儲存格。 無法編輯或刪除此儲存格。

```python
services = edge_utils.list_deployed_services()
print(services)
```

傳回的回應是您部署的服務陣列。

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

## 從刪除已部署的應用程式或服務ID [!DNL Edge] （選擇性）

>[!CAUTION]
>
>此儲存格用於刪除已部署的Edge應用程式。 除非您需要刪除已部署的儲存格，否則請勿使用下列儲存格 [!DNL Edge] 應用程式。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 后续步骤

按照上述教學課程，您已成功訓練ONNX模型並上傳到Real-time Machine Learning模型商店。 此外，您已為即時機器學習模型評分並部署。 如果您想進一步瞭解模型製作可用的節點，請造訪 [節點參考指南](./node-reference.md).
