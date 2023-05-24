---
keywords: Experience Platform；開發人員指南；Data Science Workspace；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 即時機器學習節點參考
description: 節點是形成圖形的基本單位。 每個節點會執行特定工作，而且它們可以使用連結連結連結在一起，以形成代表ML管道的圖形。 節點所執行的任務代表對輸入資料的操作，例如資料或結構描述的轉換，或機器學習推斷。 節點會將轉換或推斷的值輸出到下一個節點。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 即時機器學習節點參考(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未開放所有使用者使用。 此功能目前處於Alpha測試階段，仍在測試中。 此檔案可能會有變動。

節點是形成圖形的基本單位。 每個節點會執行特定工作，而且它們可以使用連結連結連結在一起，以形成代表ML管道的圖形。 節點所執行的任務代表對輸入資料的操作，例如資料或結構描述的轉換，或機器學習推斷。 節點會將轉換或推斷的值輸出到下一個節點。

下列指南會概述即時機器學習支援的節點程式庫。

## 探索節點以用於ML管道

將下列程式碼複製到 [!DNL Python] notebook以檢視所有可供使用的節點。

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**範例回應**

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

## 標準節點

標準節點是以開放原始碼資料科學資料庫（例如Pandas和ScikitLearn）為基礎。

### ModelUpload

ModelUpload節點是內部Adobe節點，會採用model_path並將模型從本機模型路徑上傳到Real-time Machine Learning blob存放區。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode是內部Adobe節點，會擷取模型ID以提取預先訓練的ONNX模型，並使用其對傳入資料評分。

>[!TIP]
>
>以您希望將資料傳送至ONNX模型評分的相同順序指定欄。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊貓 {#pandas}

下列「熊貓」節點可讓您匯入 `pd.DataFrame` 方法或任何一般熊貓頂層功能。 若要進一步瞭解Pandas方法，請造訪 [Pandas方法檔案](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). 如需頂層功能的詳細資訊，請瀏覽 [Pandas API一般功能參考指南](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

以下節點使用 `"import": "map"` 將方法名稱匯入為引數中的字串，接著將引數輸入為對應函式。 以下範例使用來達成此目的 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. 完成地圖設定後，您就可以選擇設定 `inplace` 作為 `True` 或 `False`. 設定 `inplace` 作為 `True` 或 `False` 根據您是否要套用轉換。 依預設 `"inplace": False` 建立新欄。 提供新欄名稱的支援已設定為在後續版本中新增。 最後一行 `cols` 可以是單一欄名稱或欄清單。 指定要套用轉換的欄。 在此範例中 `device` 已指定。

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

ScikitLearn節點可讓您匯入任何ScikitLearn ML模型或縮放器。 使用下表取得範例中所使用任何值的詳細資訊：

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
| 功能 | 輸入模型功能（字串清單）。 <br> 例如： `browser`， `device`， `login_page`， `product_page`， `search_page` |
| label | 目標欄名稱（字串）。 |
| 模式 | 訓練/測試（字串）。 |
| model_path | 以Onx格式在本機儲存模型的路徑。 |
| params.model | 模型的絕對匯入路徑（字串），例如： `sklearn.linear_model.LogisticRegression`. |
| params.model_params | 模型超引數，請參閱 [sklearn API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 說明檔案以取得詳細資訊。 |
| node_instance.process(data_message_from_previous_node) | 方法 `process()` 會從上一個節點取得DataMsg並套用轉換。 這取決於目前使用的節點。 |

### 拆分

使用以下節點，將資料流分割為訓練並透過傳遞進行測試 `train_size` 或 `test_size`. 這會傳回具有多個索引的資料流。 您可以使用以下範例來存取訓練與測試資料流： `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 后续步骤

下一步是建立節點，以用於對Real-time Machine Learning模型進行評分。 如需詳細資訊，請瀏覽 [Real-time Machine Learning筆記本使用手冊](./rtml-authoring-notebook.md).
