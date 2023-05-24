---
keywords: Experience Platform；luma網路資料；資料科學工作區；熱門主題；配方；示範資料；示範網路資料；luma資料
solution: Experience Platform
title: 建立Luma網頁結構描述和資料集
type: Tutorial
description: 本教學課程提供Luma示範傾向模型所需的先決條件和資產。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 建立Luma傾向模型結構描述和資料集

本教學課程提供您所有其他課程所需的先決條件和資產 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教學課程。 完成後，您和您的組織將可以使用以下結構描述和資料集。

**架构:**

- Luma Web資料結構
- 傾向模型評分結果結構描述

**数据集:**

- Luma網路資料集
- 傾向模型訓練資料集
- 傾向模型評分資料集
- 傾向模型評分結果資料集

## 下載資產 {#assets}

以下教學課程使用自訂Luma購買傾向模型。 繼續之前， [下載必要資產](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip資料夾。 此資料夾包含：

- 購買傾向模型筆記本
- 用於將資料擷取至訓練和評分資料集（Luma網頁資料的子集）的筆記本
- 包含730,000名Luma使用者之網頁資料的示範JSON檔案
- 選購的Python 3 EDA （探索性資料分析）筆記型電腦，可協助您瞭解網路資料和模型。

>[!NOTE]
>
> 您可以將自己的結構描述和資料用於任何教學課程。 但是，除非提供適當的設定檔和需求檔案，否則資產中提供的示範模型無法運作。 此示範傾向模型旨在搭配Luma網頁資料使用。

### 建立Luma Web資料結構描述並擷取資料

為了建立模型，您必須在Platform中有一個資料集，可用來訓練和評分您的模型。 下列影片教學課程來自 [資料科學工作區課程](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) 逐步引導您建立Luma結構描述，並擷取購買傾向模型使用的資料。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 建立訓練、評分和評分結果資料集

若要執行配方產生器筆記本或使用API來訓練和評分模型，您需要指定用於訓練/評分的資料集和結構描述。 以下影片教學課程會逐步引導您設定訓練、評分和評分結果資料集，以及Luma購買傾向模型中使用的評分結果結構描述。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 后续步骤

依照本教學課程，您已成功建立Luma傾向模型所需的結構描述和資料集。 您現在已準備好繼續下一教學課程，並使用建立模型 [配方產生器筆記本](../jupyterlab/create-a-model.md) 教學課程。

此外，您也可以使用提供的Exploration Data Analysis (EDA)筆記本來探索資料。 此筆記本可用來協助瞭解Luma資料中的模式、檢查資料是否健全以及總結預測性傾向模型的相關資料。 若要進一步瞭解探索資料分析，請造訪 [EDA檔案](../jupyterlab/eda-notebook.md).
