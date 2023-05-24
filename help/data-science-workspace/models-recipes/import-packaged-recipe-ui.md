---
keywords: Experience Platform；匯入封裝的配方；Data Science Workspace；熱門主題；配方；ui；建立引擎
solution: Experience Platform
title: 在資料科學工作區UI中匯入封裝的配方
type: Tutorial
description: 本教學課程深入分析如何使用提供的零售範例設定和匯入封裝配方。 在本教學課程結束時，您已準備好在Adobe Experience Platform資料科學工作區中建立、訓練和評估模型。
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# 在資料科學工作區UI中匯入封裝的配方

本教學課程深入分析如何使用提供的零售範例設定和匯入封裝配方。 在本教學課程結束時，您已準備好在Adobe Experience Platform中建立、訓練及評估模型 [!DNL Data Science Workspace].

## 先决条件

本教學課程需要以Docker影像URL形式的封裝方法。 請參閱教學課程，瞭解如何 [將來源檔案封裝到配方中](./package-source-files-recipe.md) 以取得詳細資訊。

## UI工作流程

將封裝的配方匯入 [!DNL Data Science Workspace] 需要特定的配方設定，編譯成單一JavaScript物件標籤法(JSON)檔案，這種配方設定的編譯稱為設定檔案。 具有特定組態的封裝配方稱為配方例項。 一個配方可用於建立許多配方例項 [!DNL Data Science Workspace].

匯入套裝程式配方的工作流程包含下列步驟：
- [設定配方](#configure)
- [匯入Docker型配方 — Python](#python)
- [匯入以Docker為基礎的配方 — R](#r)
- [匯入Docker型配方 — PySpark](#pyspark)
- [以Docker為基礎的匯入配方 — Scala](#scala)

### 設定配方 {#configure}

中的每個配方執行個體 [!DNL Data Science Workspace] 隨附一組設定，可量身打造適合特定使用案例的配方執行個體。 設定檔案會定義使用此配方執行個體建立之模型的預設訓練和評分行為。

>[!NOTE]
>
>設定檔案會因配方和大小寫而異。

底下是設定檔範例，其中顯示零售方式預設的訓練和評分行為。

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| 引數索引鍵 | 类型 | 描述 |
| ----- | ----- | ----- |
| `learning_rate` | 数值 | 漸層乘法的純量。 |
| `n_estimators` | 数值 | 隨機樹系分類器的樹系中的樹數目。 |
| `max_depth` | 数值 | 隨機森林分類器中樹狀結構的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 以逗號分隔的輸入結構描述屬性清單。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 逗號分隔的輸出結構描述屬性清單。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 決定輸入和輸出特徵是否可修改 |
| `tenantId` | 字符串 | 此ID可確保您建立的資源能正確建立名稱空間，並包含在您的組織內。 [請依照這裡的步驟操作](../../xdm/api/getting-started.md#know-your-tenant_id) 以尋找您的租使用者ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用於訓練模型的輸入結構描述。 在UI中匯入時，請將此欄留空；使用API匯入時，請以培訓SchemaID取代。 |
| `evaluation.labelColumn` | 字符串 | 評估視覺效果的欄標籤。 |
| `evaluation.metrics` | 字符串 | 用於評估模型的評估量度清單（以逗號分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用於對模型評分的輸出結構描述。 在UI中匯入時，請將此欄留空；使用API匯入時，請以評分SchemaID取代。 |

在本教學課程中，您可以將零售配方的預設設定檔保留在 [!DNL Data Science Workspace] 參考其運作方式。

### 匯入以Docker為基礎的配方 —  [!DNL Python] {#python}

從導覽和選取開始 **[!UICONTROL 工作流程]** 位於左側的 [!DNL Platform] UI。 接下來，選取 **匯入配方** 並選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **匯入配方** 工作流程隨即顯示。 輸入配方的名稱與摘要，然後選取 **[!UICONTROL 下一個]** 右上角。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將來源檔案封裝到配方中](./package-source-files-recipe.md) 教學課程，在使用Python來源檔案建立零售銷售方式結束時，提供了Docker URL。

一旦您登入 **選取來源** 頁面，貼上與使用建立的封裝配方相對應的Docker URL [!DNL Python] 中的來源檔案 **[!UICONTROL 來源URL]** 欄位。 接下來，透過拖放或使用檔案系統匯入提供的組態檔案 **瀏覽器**. 提供的設定檔案可在以下網址找到： `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. 選取 **[!UICONTROL Python]** 在 **執行階段** 下拉式清單和 **[!UICONTROL 分類]** 在 **型別** 下拉式清單。 填寫完所有內容後，選取 **[!UICONTROL 下一個]** 前往右上角 **管理結構描述**.

>[!NOTE]
>
> 型別支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果您的模型不屬於這些型別之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接著，選取區段下方的零售銷售輸入和輸出結構 **管理結構描述**，這些範本是使用 [建立零售業銷售結構描述和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 **功能管理** 區段中，在結構描述檢視器中選取租使用者識別以展開零售銷售輸入結構描述。 反白所需的特徵並選取 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右側 **[!UICONTROL 欄位屬性]** 視窗。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 作為  **[!UICONTROL 目標功能]** 和其他所有專案為 **[!UICONTROL 輸入功能]**. 選取 **[!UICONTROL 下一個]** 以檢閱您新設定的配方。

視需要檢閱配方、新增、修改或移除設定。 選取 **[!UICONTROL 完成]** 以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續前往 [後續步驟](#next-steps) 以瞭解如何在中建立模型 [!DNL Data Science Workspace] 使用新建立的零售銷售配方。

### 匯入以Docker為基礎的配方 — R {#r}

從導覽和選取開始 **[!UICONTROL 工作流程]** 位於左側的 [!DNL Platform] UI。 接下來，選取 **匯入配方** 並選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **匯入配方** 工作流程隨即顯示。 輸入配方的名稱與摘要，然後選取 **[!UICONTROL 下一個]** 右上角。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將來源檔案封裝到配方中](./package-source-files-recipe.md) 教學課程中，在使用R來源檔案建立零售銷售配方結束時，提供了Docker URL。

一旦您登入 **選取來源** 頁面，貼上與使用R來源檔案建置的封裝配方相對應的Docker URL **[!UICONTROL 來源URL]** 欄位。 接下來，透過拖放或使用檔案系統匯入提供的組態檔案 **瀏覽器**. 提供的設定檔案可在以下網址找到： `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 選取 **[!UICONTROL R]** 在 **執行階段** 下拉式清單和 **[!UICONTROL 分類]** 在 **型別** 下拉式清單。 填寫完所有內容後，選取 **[!UICONTROL 下一個]** 前往右上角 **管理結構描述**.

>[!NOTE]
>
> *型別* 支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果您的模型不屬於這些型別之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接著，選取區段下方的零售銷售輸入和輸出結構 **管理結構描述**，這些範本是使用 [建立零售業銷售結構描述和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 *功能管理* 區段中，在結構描述檢視器中選取租使用者識別以展開零售銷售輸入結構描述。 反白所需的特徵並選取 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右側 **[!UICONTROL 欄位屬性]** 視窗。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 作為  **[!UICONTROL 目標功能]** 和其他所有專案為 **[!UICONTROL 輸入功能]**. 選取 **[!UICONTROL 下一個]** 以檢閱您的新已設定配方。

視需要檢閱配方、新增、修改或移除設定。 選取 **完成** 以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續前往 [後續步驟](#next-steps) 以瞭解如何在中建立模型 [!DNL Data Science Workspace] 使用新建立的零售銷售配方。

### 匯入Docker型配方 — PySpark {#pyspark}

從導覽和選取開始 **[!UICONTROL 工作流程]** 位於左側的 [!DNL Platform] UI。 接下來，選取 **匯入配方** 並選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **匯入配方** 工作流程隨即顯示。 輸入配方的名稱與摘要，然後選取 **[!UICONTROL 下一個]** 前往右上角以繼續。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將來源檔案封裝到配方中](./package-source-files-recipe.md) 教學課程，在使用PySpark來源檔案建置零售方式結束時提供了Docker URL。

一旦您登入 **選取來源** 頁面，將對應到使用PySpark來源檔案建立的封裝配方的Docker URL貼到 **[!UICONTROL 來源URL]** 欄位。 接下來，透過拖放或使用檔案系統匯入提供的組態檔案 **瀏覽器**. 提供的設定檔案可在以下網址找到： `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. 選取 **[!UICONTROL PySpark]** 在 **執行階段** 下拉式清單。 選取PySpark執行階段後，預設成品會自動填入 **[!UICONTROL Docker]**. 接下來，選取 **[!UICONTROL 分類]** 在 **型別** 下拉式清單。 填寫完所有內容後，選取 **[!UICONTROL 下一個]** 前往右上角 **管理結構描述**.

>[!NOTE]
>
> *型別* 支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果您的模型不屬於這些型別之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下來，使用「 」選取「零售銷售」輸入和輸出結構描述。 **管理結構描述** 選擇器中，使用中提供的啟動程式指令碼建立方案 [建立零售業銷售結構描述和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![管理結構描述](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 區段中，在結構描述檢視器中選取租使用者識別以展開零售銷售輸入結構描述。 反白所需的特徵並選取 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右側 **[!UICONTROL 欄位屬性]** 視窗。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 作為  **[!UICONTROL 目標功能]** 和其他所有專案為 **[!UICONTROL 輸入功能]**. 選取 **[!UICONTROL 下一個]** 以檢閱您新設定的配方。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

視需要檢閱配方、新增、修改或移除設定。 選取 **[!UICONTROL 完成]** 以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續前往 [後續步驟](#next-steps) 以瞭解如何在中建立模型 [!DNL Data Science Workspace] 使用新建立的零售銷售配方。

### 以Docker為基礎的匯入配方 — Scala {#scala}

從導覽和選取開始 **[!UICONTROL 工作流程]** 位於左側的 [!DNL Platform] UI。 接下來，選取 **匯入配方** 並選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **匯入配方** 工作流程隨即顯示。 輸入配方的名稱與摘要，然後選取 **[!UICONTROL 下一個]** 前往右上角以繼續。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將來源檔案封裝到配方中](./package-source-files-recipe.md) 教學課程，在使用Scala ([!DNL Spark])來源檔案。

一旦您登入 **選取來源** 頁面，在來源URL欄位中貼上與使用Scala來源檔案建置的封裝配方對應的Docker URL。 接下來，拖放或使用檔案系統「瀏覽器」來匯入提供的組態檔案。 提供的設定檔案可在以下網址找到： `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 選取 **[!UICONTROL Spark]** 在 **執行階段** 下拉式清單。 一旦 [!DNL Spark] 執行階段已選取，預設成品會自動填入 **[!UICONTROL Docker]**. 接下來，選取 **[!UICONTROL 回歸]** 從 **型別** 下拉式清單。 填寫完所有內容後，選取 **[!UICONTROL 下一個]** 前往右上角 **管理結構描述**.

>[!NOTE]
>
> 型別支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果您的模型不屬於這些型別之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下來，使用「 」選取「零售銷售」輸入和輸出結構描述。 **管理結構描述** 選擇器中，使用中提供的啟動程式指令碼建立方案 [建立零售業銷售結構描述和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![管理結構描述](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 區段中，在結構描述檢視器中選取租使用者識別以展開零售銷售輸入結構描述。 反白所需的特徵並選取 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右側 **[!UICONTROL 欄位屬性]** 視窗。 在本教學課程中，請設定&quot;[!UICONTROL weeklySales]」作為  **[!UICONTROL 目標功能]** 和其他所有專案為 **[!UICONTROL 輸入功能]**. 選取 **[!UICONTROL 下一個]** 以檢閱您新設定的配方。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

視需要檢閱配方、新增、修改或移除設定。 選取 **[!UICONTROL 完成]** 以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續前往 [後續步驟](#next-steps) 以瞭解如何在中建立模型 [!DNL Data Science Workspace] 使用新建立的零售銷售配方。

## 后续步骤 {#next-steps}

本教學課程深入分析如何設定配方並將其匯入 [!DNL Data Science Workspace]. 您現在可以使用新建立的配方來建立、訓練及評估模型。

- [在UI中訓練及評估模型](./train-evaluate-model-ui.md)
- [使用API訓練及評估模型](./train-evaluate-model-api.md)
