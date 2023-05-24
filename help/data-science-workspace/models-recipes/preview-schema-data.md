---
keywords: Experience Platform；預覽結構描述資料；Data Science Workspace；熱門主題
solution: Experience Platform
title: 預覽零售銷售結構描述和資料集
type: Tutorial
description: 以下檔案概述在Adobe Experience Platform上預覽結構描述和資料集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 預覽零售銷售結構描述和資料集

成功完成bootstrap指令碼後， [零售銷售結構描述和資料集](./create-retails-sales-dataset.md) 教學課程。 輸出結構描述和資料集可以在以下位置檢視： [!DNL Experience Platform]. 若要檢視結構描述和資料集，請遵循下列步驟：

選取 **[!UICONTROL 結構描述]** 索引標籤的位置，並尋找由啟動程式指令碼建立的輸入結構描述。 結構描述的名稱將對應至中定義的名稱 `config.yaml` 上一步驟中的。 按一下結構描述，即可檢視結構描述詳細資訊及其組成。

![](../images/models-recipes/access-data/schema.PNG)

選取 **[!UICONTROL 資料集]** 索引標籤放置在左側導覽中，並開啟透過選取資料集名稱而建立的輸入資料集。 資料集的名稱與中的定義相對應 `config.yaml` 上一步驟中的。

![](../images/models-recipes/access-data/dataset.PNG)

選取 **[!UICONTROL 預覽資料集]** 位於右上方，以預覽資料集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 后续步骤

您現在已成功將零售業範例資料擷取至 [!DNL Experience Platform] 使用提供的啟動程式指令碼。

若要繼續使用擷取的資料：
- [使用Jupyter Notebooks分析您的資料](../jupyterlab/analyze-your-data.md)
   - 在中使用Jupyter Notebooks [!DNL Data Science Workspace] 存取、探索、視覺化及瞭解您的資料。
- [將來源檔案封裝到配方中](./package-source-files-recipe.md)
   - 按照本教學課程瞭解如何將您自己的模型帶入 [!DNL Data Science Workspace] 將來源檔案封裝在可匯入的「配方」檔案中。
