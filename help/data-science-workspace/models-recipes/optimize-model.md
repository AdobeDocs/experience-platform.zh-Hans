---
keywords: Experience Platform；最佳化；模型；資料科學工作區；熱門主題；模型深入分析
solution: Experience Platform
title: 使用模型深入分析架構最佳化模型
type: Tutorial
description: 模型深入分析架構為資料科學家提供資料科學工作區中的工具，以便根據實驗針對最佳機器學習模型做出快速且明智的選擇。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 使用「模型分析」架構最佳化模型

模型深入分析框架為資料科學家提供以下工具： [!DNL Data Science Workspace] 根據實驗，快速且明智地選擇最佳機器學習模型。 此架構將提高機器學習工作流程的速度和有效性，並改善資料科學家的易用性。 為每個機器學習演演算法型別提供預設範本，以協助進行模型調整，藉此完成模型調整。 最終結果可讓資料科學家和公民資料科學家為其最終客戶做出更好的模型最佳化決策。

## 什麼是量度？

實作和訓練模型後，資料科學家的下一步工作是找出模型的執行效能。 系統會使用各種量度來瞭解模型與其他量度相較之下的效能。 部分使用的量度範例包括：
- 分類準確度
- 曲線下的區域
- 混淆矩陣
- 分類報告

## 設定配方代碼

目前，模型深入分析架構支援下列執行階段：
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

配方範常式式碼可在以下網址找到： [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) 存放庫位於 `recipes`. 在本教學課程中，將會參考此存放庫中的特定檔案。

### Scala {#scala}

有兩種方式可將量度帶入配方。 一種是使用SDK提供的預設評估量度，另一種是撰寫自訂評估量度。

#### Scala的預設評估量度

預設評估作為分類演演算法的一部分進行計算。 以下是目前已實作的評估器的一些預設值：

| 評估器類別 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

您可以在的配方中定義評估器 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 中的檔案 `recipe` 資料夾。 啟用「 」的範常式式碼 `DefaultBinaryClassificationEvaluator` 如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

啟用評估器類別後，系統會依預設在訓練期間計算多個量度。 您可以將下列行新增至以明確宣告預設量度 `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定義量度，預設量度將會啟用。

可以透過變更的值來啟用特定量度 `evaluation.metrics.com`. 在以下範例中，已啟用F分數量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出每個類別的預設量度。 使用者也可以使用 `evaluation.metric` 欄，以啟用特定量度。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` |  — 精確度 <br>-Recall <br> — 混淆矩陣 <br>-F分數 <br> — 精確度 <br> — 接收者操作特性 <br> — 接收器操作特性下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` |  — 精確度 <br>-Recall <br> — 混淆矩陣 <br>-F分數 <br> — 精確度 <br> — 接收者操作特性 <br> — 接收器操作特性下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` |  — 平均平均精確度(MAP) <br> — 標準化折現累積收益 <br> — 平均倒數排名 <br> — 量度K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自訂評估量度

擴充介面以提供自訂評估器 `MLEvaluator.scala` 在您的 `Evaluator.scala` 檔案。 在範例中 [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 檔案，我們定義自訂 `split()` 和 `evaluate()` 函式。 我們的 `split()` 函式會以8:2的比率隨機分割資料，而 `evaluate()` 函式會定義並傳回3個量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>對於 `MLMetric` 類別，請勿使用 `"measures"` 的 `valueType` 建立新時 `MLMetric` 否則量度不會填入自訂評估量度表格中。
>  
> 執行此動作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是這個： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


一旦在配方中定義之後，下一步就是要在配方中啟用它。 這可在以下位置完成： [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 專案中的檔案 `resources` 資料夾。 此處 `evaluation.class` 設為 `Evaluator` 類別定義於 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在 [!DNL Data Science Workspace]，使用者將可檢視實驗頁面中「評估量度」索引標籤中的深入分析。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前，尚無下列專案的預設評估量度 [!DNL Python] 或 [!DNL Tensorflow]. 因此，若要取得的評估量度 [!DNL Python] 或 [!DNL Tensorflow]，您需要建立自訂評估量度。 這可透過實作 `Evaluator` 類別。

#### 自訂評估量度 [!DNL Python]

對於自訂評估量度，需要為評估器實作兩種主要方法： `split()` 和 `evaluate()`.

對象 [!DNL Python]，這些方法的定義如下： [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 的 `Evaluator` 類別。 請遵循 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 連結以取得以下專案的範例： `Evaluator`.

在中建立評估量度 [!DNL Python] 需要使用者實作 `evaluate()` 和 `split()` 方法。

此 `evaluate()` 方法會傳回量度物件，該物件包含量度物件的陣列，其屬性為 `name`， `value`、和 `valueType`.

目的 `split()` 方法是輸入資料，並輸出訓練和測試資料集。 在我們的範例中， `split()` 方法輸入資料時使用 `DataSetReader` SDK，接著移除不相關的欄，以清除資料。 從那裡，其他功能是從資料中的現有原始功能建立的。

此 `split()` 方法應傳回訓練和測試資料流，然後由 `pipeline()` 訓練和測試ML模型的方法。

#### Tensorflow的自訂評估量度

對象 [!DNL Tensorflow]，類似於 [!DNL Python]，方法 `evaluate()` 和 `split()` 在 `Evaluator` 類別需要實作。 對象 `evaluate()`，則傳回量度的時間 `split()` 傳回訓練集和測試資料集。

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

截至目前，R沒有預設的評估量度。因此，若要取得R的評估量度，您需要定義 `applicationEvaluator` 類別作為配方的一部分。

#### R的自訂評估量度

的主要用途 `applicationEvaluator` 是傳回包含量度索引鍵值配對的JSON物件。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 可作為範例。 在此範例中， `applicationEvaluator` 分為三個常見的區段：
- 載入資料
- 資料準備/功能工程
- 擷取已儲存的模型並評估

資料會先從來源載入至資料集，如中所定義 [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). 從那裡，資料經過清理和工程處理，以符合機器學習模型。 最後，此模型可用我們的資料集進行預測，並根據預測值和實際值計算量度。 在這種情況下，MAPE、MAE和RMSE定義並傳回 `metrics` 物件。

## 使用預先建立的量度和視覺效果圖表

此 [!DNL Sensei Model Insights Framework] 將支援每個機器學習演演算法型別的預設範本。 下表顯示常見的高階機器學習演演算法類別以及對應的評估量度和視覺效果。

| ml演演算法型別 | 評估量度 | 可视化图表 |
| --- | --- | --- |
| 回歸 | - RMSE<br>- MAPI<br>- MASE<br>- AME | 預測值與實際值的覆蓋曲線 |
| 二進位分類 |  — 混淆矩陣<br> — 精確召回<br> — 準確度<br>- F分數（特別指F1、F2）<br>- AUC<br>- ROC | ROC曲線和混淆矩陣 |
| 多類別分類 |  — 混淆矩陣 <br> — 針對每個類別： <br> — 精確召回率 <br>- F分數（尤其是F1、F2） | ROC曲線和混淆矩陣 |
| 叢集（包含基本事實） | - NMI （標準化相互資訊分數）、AMI （調整相互資訊分數）<br>- RI （蘭特指數）、ARI （調整後蘭特指數）<br> — 同質性分數、完整度分數和V量值<br>- FMI （Fowlkes-Mallows指數）<br> — 純度<br>- Jaccard索引 | 顯示叢集和質心的叢集圖，其相對叢集大小反映落在叢集內的資料點 |
| 叢集（不含地面真實值） |  — 慣性<br> — 剪影係數<br>- CHI (Calinski-Harabaz index)<br>- DBI （Davies-Bouldin索引）<br>- Dunn索引 | 顯示叢集和質心的叢集圖，其相對叢集大小反映落在叢集內的資料點 |
| 推荐 |  — 平均平均精確度(MAP) <br> — 標準化折現累積收益 <br> — 平均倒數排名 <br> — 量度K | 待定 |
| TensorFlow使用案例 | 張量流量模型分析(TFMA) | 深度比較神經網路模型比較/視覺效果 |
| 其他/錯誤擷取機制 | 模型作者定義的自訂量度邏輯（以及對應的評估圖表）。 範本不符時的正常錯誤處理 | 包含評估量度的索引鍵值配對的表格 |
