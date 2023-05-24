---
keywords: Experience Platform；JupyterLab；配方；筆記本；資料科學工作區；熱門主題；建立配方
solution: Experience Platform
title: 使用JupyterLab Notebooks建立模型
type: Tutorial
description: 本教學課程將逐步引導您完成使用JupyterLab Notebooks配方產生器範本建立配方所需的步驟。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# 使用JupyterLab Notebooks建立模型

本教學課程將逐步引導您完成使用JupyterLab Notebooks配方產生器範本建立模型的必要步驟。

## 引入的概念：

- **配方：** 配方是模型規格的Adobe術語，是代表特定機器學習、AI演演算法或演演算法組合、處理邏輯以及建立和執行已訓練模型所需設定的頂層容器。
- **型號：** 模型是機器學習方法的執行個體，會使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。
- **培訓：** 訓練是從標籤資料中學習模式和深入分析的程式。
- **評分：** 評分是使用經過訓練的模型，從資料產生深入分析的程式。

## 下載必要的資產 {#assets}

在繼續本教學課程之前，您必須建立必要的結構描述和資料集。 造訪的教學課程 [建立Luma傾向模型結構描述和資料集](../models-recipes/create-luma-data.md) 以下載必要資產和設定必要條件。

## 開始使用 [!DNL JupyterLab] 筆記型電腦環境

從頭開始建立配方可以在中完成 [!DNL Data Science Workspace]. 若要開始，請導覽至 [Adobe Experience Platform](https://platform.adobe.com) 並選取 **[!UICONTROL Notebooks]** 索引標籤左側。 若要建立新的記事本，請從下列專案選取「配方產生器」範本： [!DNL JupyterLab Launcher].

此 [!UICONTROL 配方產生器] notebook可讓您在筆記本內執行訓練和評分回合。 這可讓您靈活地變更其 `train()` 和 `score()` 方法介乎執行訓練和評分資料的實驗。 一旦您對訓練和評分的輸出感到滿意，您就可以建立配方，並使用配方來模型化功能，進而將其發佈為模型。

>[!NOTE]
>
>此 [!UICONTROL 配方產生器] notebook支援使用所有檔案格式，但目前僅支援建立配方功能 [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

當您選取 [!UICONTROL 配方產生器] notebook從啟動器，會在新標籤中開啟。

在頂端的新筆記本標籤中，會載入一個包含三個額外動作的工具列 —  **[!UICONTROL 訓練]**， **[!UICONTROL 分數]**、和 **[!UICONTROL 建立配方]**. 這些圖示只會顯示在 [!UICONTROL 配方產生器] notebook。 提供了有關這些動作的詳細資訊 [在訓練和評分割槽段中](#training-and-scoring) 在記事本中建立您的配方後。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 開始使用 [!UICONTROL 配方產生器] notebook

在提供的資產資料夾中為Luma傾向模型 `propensity_model.ipynb`. 使用JupyterLab中的上傳筆記本選項，上傳提供的型號並開啟筆記本。

![上傳筆記本](../images/jupyterlab/create-recipe/upload_notebook.png)

本教學課程的其餘部分涵蓋傾向性模型筆記本中預先定義的下列檔案：

- [需求檔案](#requirements-file)
- [組態檔](#configuration-files)
- [訓練資料載入器](#training-data-loader)
- [評分資料載入器](#scoring-data-loader)
- [管道檔案](#pipeline-file)
- [評估器檔案](#evaluator-file)
- [資料儲存器檔案](#data-saver-file)

下列影片教學課程說明Luma傾向性模型筆記本：

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 需求檔案 {#requirements-file}

需求檔案用於宣告您要在模型中使用的其他程式庫。 如果有相依性，您可以指定版本編號。 若要尋找其他程式庫，請造訪 [anaconda.org](https://anaconda.org). 若要瞭解如何格式化需求檔案，請造訪 [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). 已使用的主要程式庫清單包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您新增的程式庫或特定版本可能與上述程式庫不相容。 此外，如果您選擇手動建立環境檔案， `name` 欄位不可覆寫。

Luma傾向性機型筆記型電腦不需要更新需求。

### 組態檔 {#configuration-files}

組態檔， `training.conf` 和 `scoring.conf`，用於指定您要用於訓練和評分以及新增超引數的資料集。 訓練和評分有不同的設定。

為了讓模型執行訓練，您必須提供 `trainingDataSetId`， `ACP_DSW_TRAINING_XDM_SCHEMA`、和 `tenantId`. 此外，若要評分，您必須提供 `scoringDataSetId`， `tenantId`、和 `scoringResultsDataSetId `.

若要尋找資料集和結構描述ID，請前往「資料」標籤 ![資料標籤](../images/jupyterlab/create-recipe/dataset-tab.png) （位於資料夾圖示下方）左側導覽列上的notebooks內。 需要提供三個不同的資料集ID。 此 `scoringResultsDataSetId` 用於儲存模型評分結果，且應為空白資料集。 這些資料集是先前在 [必要資產](#assets) 步驟。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

相同的資訊可在上找到 [Adobe Experience Platform](https://platform.adobe.com/) 在 **[結構描述](https://platform.adobe.com/schema)** 和 **[資料集](https://platform.adobe.com/dataset/overview)** 索引標籤。

完成之後，您的訓練和評分設定應該看起來類似下列熒幕擷圖：

![設定](../images/jupyterlab/create-recipe/config.png)

根據預設，當您訓練及評分資料時，系統會為您設定下列設定引數：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 瞭解訓練資料載入器 {#training-data-loader}

「培訓資料載入器」的用途是將用來建立機器學習模型的資料例項化。 通常，培訓資料載入器會完成兩項工作：

- 正在載入資料來源 [!DNL Platform]
- 資料準備和功能工程

以下兩個區段將過載資料和資料準備。

### 正在載入資料 {#loading-data}

此步驟使用 [熊貓資料流](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). 資料可從中的檔案載入 [!DNL Adobe Experience Platform] 使用 [!DNL Platform] SDK (`platform_sdk`)，或使用熊貓的外部來源 `read_csv()` 或 `read_json()` 函式。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部來源](#external-sources)

>[!NOTE]
>
>在配方產生器筆記本中，資料是透過 `platform_sdk` 資料載入器。

### [!DNL Platform] SDK {#platform-sdk}

有關使用的深入教學課程 `platform_sdk` 資料載入器，請造訪 [Platform SDK指南](../authoring/platform-sdk.md). 本教學課程提供有關建置驗證、基本讀取資料和基本寫入資料的資訊。

### 外部來源 {#external-sources}

本節說明如何將JSON或CSV檔案匯入熊貓物件。 熊貓資料庫的官方檔案可在以下網址找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是匯入CSV檔案的範例。 此 `data` 引數是CSV檔案的路徑。 此變數是從 `configProperties` 在 [上一節](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

您也可以從JSON檔案匯入。 此 `data` 引數是CSV檔案的路徑。 此變數是從 `configProperties` 在 [上一節](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

現在，您的資料位於資料流物件中，並可在中分析和操作 [下一節](#data-preparation-and-feature-engineering).

## 訓練資料載入器檔案

在此範例中，資料是使用Platform SDK載入。 您可以包含下列行，在頁面頂端匯入程式庫：

`from platform_sdk.dataset_reader import DatasetReader`

然後，您可以使用 `load()` 從擷取訓練資料集的方法 `trainingDataSetId` 如設定中所設定(`recipe.conf`)檔案。

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>如 [組態檔區段](#configuration-files)，當您使用從Experience Platform存取資料時，系統會為您設定以下設定引數 `client_context = get_client_context(config_properties)`：
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


現在您有了資料，就可以開始資料準備和功能工程了。

### 資料準備和功能工程 {#data-preparation-and-feature-engineering}

載入資料後，需要清除資料並做好資料準備。 在此範例中，模型的目標是預測客戶是否會訂購產品。 由於模型並未檢視特定產品，因此您不需要 `productListItems` 因此會捨棄該欄。 接著，會刪除只包含單一值或單一欄中兩個值的其他欄。 在訓練模型時，請務必僅保留有助於預測目標的有用資料。

![資料準備範例](../images/jupyterlab/create-recipe/data_prep.png)

刪除任何不必要的資料後，即可開始特徵工程。 用於此範例的示範資料不包含任何工作階段資訊。 通常情況下，您會想要取得特定客戶目前和過去工作階段的資料。 由於缺少工作階段資訊，此範例改為透過歷程分界模擬目前和過去的工作階段。

![歷程分界](../images/jupyterlab/create-recipe/journey_demarcation.png)

分界完成後，資料會加上標籤，並建立歷程。

![為資料加上標籤](../images/jupyterlab/create-recipe/label_data.png)

接著會建立特徵，並分成過去和現在。 然後，會捨棄任何不必要的欄，留下Luma客戶的過去和目前歷程。 這些歷程包含諸如客戶是否購買了一個專案以及他們購買之前所經歷的歷程等資訊。

![目前的最終訓練](../images/jupyterlab/create-recipe/final_journey.png)

## 評分資料載入器 {#scoring-data-loader}

載入資料以進行評分的程式與載入訓練資料類似。 仔細檢視程式碼，您可以看到除了 `scoringDataSetId` 在 `dataset_reader`. 這是因為訓練和評分會使用相同的Luma資料來源。

如果您想要使用不同的資料檔案進行訓練和評分，訓練和評分資料載入器會分開。 這可讓您執行其他預先處理，例如視需要將您的訓練資料對應至評分資料。

## 管道檔案 {#pipeline-file}

此 `pipeline.py` 檔案包含訓練和評分的邏輯。

訓練的目的是使用訓練資料集中的功能和標籤來建立模型。 選擇訓練模型後，您必須將x和y訓練資料集調整為適合模型，函式會傳回經過訓練的模型。

>[!NOTE]
> 
>功能是指機器學習模型用來預測標籤的輸入變數。

![def train](../images/jupyterlab/create-recipe/def_train.png)

此 `score()` 函式應包含評分演演算法並傳回測量以指出模型執行的成效。 此 `score()` 函式會使用評分資料集標籤和經過訓練的模型來產生一組預測功能。 然後，這些預測值與評分資料集中的實際功能進行比較。 在此範例中， `score()` 函式會使用訓練好的模型，使用評分資料集中的標籤來預測功能。 會傳回預測功能。

![定義分數](../images/jupyterlab/create-recipe/def_score.png)

## 評估器檔案 {#evaluator-file}

此 `evaluator.py` 檔案包含您希望如何評估訓練好的配方，以及如何分割訓練資料的邏輯。

### 分割資料集 {#split-the-dataset}

訓練的資料準備階段需要分割資料集，以用於訓練和測試。 此 `val` 在訓練模型後，會隱含使用資料來評估模型。 此程式與評分不同。

本區段顯示 `split()` 將資料載入筆記本的函式，接著移除資料集中不相關的欄，以清除資料。 從那裡，您可以執行特徵工程，即從資料中的現有原始特徵建立其他相關特徵的程式。

![Split函式](../images/jupyterlab/create-recipe/split.png)

### 評估訓練好的模型 {#evaluate-the-trained-model}

此 `evaluate()` 函式會在模型訓練後執行，並傳回量度以指出模型的執行成效。 此 `evaluate()` 函式會使用測試資料集標籤和經過訓練的模型來預測一組功能。 然後，這些預測值與測試資料集中的實際功能進行比較。 在此範例中，使用的量度包括 `precision`， `recall`， `f1`、和 `accuracy`. 請注意，函式會傳回 `metric` 包含評估量度陣列的物件。 這些量度用於評估訓練後模型的執行效果。

![評估](../images/jupyterlab/create-recipe/evaluate.png)

新增 `print(metric)` 可讓您檢視量度結果。

![量度結果](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 資料儲存器檔案 {#data-saver-file}

此 `datasaver.py` 檔案包含 `save()` 函式中，並用於在測試評分時儲存您的預測。 此 `save()` 函式會使用您的預測和使用 [!DNL Experience Platform Catalog] API，將資料寫入 `scoringResultsDataSetId` 您已指定 `scoring.conf` 檔案。 您可以

![資料儲存器](../images/jupyterlab/create-recipe/data_saver.png)

## 訓練和評分 {#training-and-scoring}

當您完成筆記本的變更並想要訓練配方時，您可以選取列頂端的關聯按鈕，以在儲存格中建立訓練回合。 選取按鈕後，訓練指令碼的指令和輸出記錄會顯示在記事本中(在 `evaluator.py` 儲存格)。 Conda會先安裝所有相依性，然後開始培訓。

請注意，在執行評分之前，您必須至少執行一次訓練。 選取 **[!UICONTROL 執行評分]** 按鈕將在訓練期間產生的已訓練模型上計分。 評分指令碼會顯示在 `datasaver.py`.

基於偵錯目的，如果您想要檢視隱藏的輸出，請新增 `debug` 到輸出儲存格的結尾，然後重新執行。

![訓練與分數](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 建立配方 {#create-recipe}

當您完成編輯配方並滿意訓練/評分輸出時，您可以透過選取「 」，從筆記本建立配方 **[!UICONTROL 建立配方]** 右上角。

![](../images/jupyterlab/create-recipe/create-recipe.png)

選取後 **[!UICONTROL 建立配方]**，系統會提示您輸入配方名稱。 此名稱代表實際配方建立日期 [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

一旦您選取 **[!UICONTROL 確定]**，配方建立程式隨即開始。 這可能需要一些時間，並且會顯示進度列來取代建立配方按鈕。 完成後，您可以選取 **[!UICONTROL 檢視配方]** 按鈕帶您前往 **[!UICONTROL 配方]** 標籤下的 **[!UICONTROL ML模型]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 請勿刪除任何檔案儲存格
> - 不要編輯 `%%writefile` 檔案儲存格頂端的行
> - 不要同時在不同筆記型電腦中建立配方


## 后续步骤 {#next-steps}

完成本教學課程後，您已瞭解如何在中建立機器學習模型 [!UICONTROL 配方產生器] notebook。 您也學習了如何運用筆記本來操作配方工作流程。

若要繼續學習如何使用中的資源 [!DNL Data Science Workspace]，請造訪 [!DNL Data Science Workspace] 配方和模型下拉式清單。