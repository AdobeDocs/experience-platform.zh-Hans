---
keywords: Experience Platform；開發人員指南；Data Science Workspace；熱門主題；即時機器學習；
solution: Experience Platform
title: Real-time Machine Learning快速入門
description: 以下檔案概述在Adobe Experience Platform中建立Real-time Machine Learning模型所需的步驟。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Real-time Machine Learning (Alpha)快速入門

>[!IMPORTANT]
>
>即時機器學習尚未開放所有使用者使用。 此功能目前處於Alpha測試階段，仍在測試中。 此檔案可能會有變動。

若要使用即時機器學習，您必須具備已布建Adobe Experience Platform的組織的存取權，並且 [!DNL Data Science Workspace]. 此外，您還需要完整資料集，才能用於訓練和評分。

即時機器學習指南需要實際瞭解Python 3， [Jupyter Notebooks](../jupyterlab/overview.md)、資料科學和機器學習。

**主要條款：**

- **DSL：** 網域特定語言。
- **Edge：** Real-time Machine Learning評分服務可在距離您啟動和應用程式較近的邊緣叢集上執行。
- **集線器：** 目前的Alpha在Adobe Experience Platform Hub上執行Real-time Machine Learning評分服務，而Experience Edge Network正在開發中。
- **節點：** 節點是形成圖形的基本單位。 每個節點會執行特定工作，而且它們可以使用連結連結連結在一起，以形成代表ML管道的圖形。 節點所執行的任務代表對輸入資料的操作，例如資料或結構描述的轉換，或機器學習推斷。 節點會將轉換或推斷的值輸出到下一個節點。

## Adobe Experience Platform中的資料集

若要開始使用Real-time Machine Learning，您必須擁有資料集的存取權。 您可以選擇使用外部資料集並將其上傳至 [!DNL JupyterLab] 環境或在Platform中建立新資料集（如果尚未這麼做的話）。

>[!NOTE]
>
>如果您已有資料集要使用，可以跳至 [後續步驟](#next-steps).

### 使用外部資料集

若要進一步瞭解如何使用外部資料集，例如將資料上傳至 [!DNL JupyterLab] 環境，請造訪本教學課程： [使用筆記型電腦分析資料](../jupyterlab/analyze-your-data.md#external-data).

### 建立新的資料集

若要建立新資料集以用於Real-time Machine Learning，您的資料集需要資料結構描述。 接下來，您需要使用您建立的結構描述擷取資料。 使用下列教學課程來建立和填入資料集 [!DNL Platform]：

- [在API中建立並填入資料集](../../catalog/datasets/create.md)
- [在UI中建立並填入資料集](../../ingestion/tutorials/ingest-batch-data.md)

## 后续步骤 {#next-steps}

當您準備好資料以進行即時機器學習後，請依照以下步驟開始 [Real-time Machine Learning筆記本使用手冊](./rtml-authoring-notebook.md) 瞭解如何建立ONNX模型並上傳到Real-time Machine Learning模型存放區。
