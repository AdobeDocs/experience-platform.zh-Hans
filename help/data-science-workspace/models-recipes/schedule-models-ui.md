---
keywords: Experience Platform；排程模型；資料科學工作區；熱門主題；排程評分；排程訓練
solution: Experience Platform
title: 在Data Science Workspace UI中排程模型
type: Tutorial
description: Adobe Experience Platform Data Science Workspace可讓您在機器學習服務上設定已排程的評分和訓練執行。 自動化訓練和評分程式，可隨時掌握資料中的模式，協助維持及改善服務的效率。
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 在Data Science Workspace UI中排程模型

Adobe Experience Platform [!DNL Data Science Workspace] 可讓您在機器學習服務上設定排程的評分和訓練回合。 自動化訓練和評分程式，可隨時掌握資料中的模式，協助維持及改善服務的效率。

本教學課程會透過逐步說明在現有服務上設定訓練和評分排程的步驟。 [!UICONTROL 服務庫]. 它分為下列主要區段：

- [設定排程評分](#configure-scheduled-scoring)
- [設定排程訓練](#configure-scheduled-training)

## 快速入门

若要完成本教學課程，您必須擁有 [!DNL Experience Platform]. 如果您無權存取中的組織 [!DNL Experience Platform]，請在繼續之前聯絡您的系統管理員。

本教學課程需要現有服務。 如果您沒有可使用的可存取服務，您可以遵循的教學課程建立一個服務 [將模型發佈為服務](./publish-model-service-ui.md).

## 設定排程評分 {#configure-scheduled-scoring}

模型評分可以設定為排程基礎上的自動化程式。 建立服務後，您可以依照以下步驟設定並套用評分排程：

在Adobe Experience Platform中，選取 **[!UICONTROL 服務]** 標籤以存取 **[!DNL Service Gallery]**. 尋找您要排程評分執行的服務，然後選取 **[!UICONTROL 開啟]** 以檢視其 **[!UICONTROL 概觀]** 頁面。

![](../images/models-recipes/schedule/select_service.png)

「總覽」頁面會顯示服務的評分資訊。 選取 **[!UICONTROL 更新排程]** 設定評分排程的連結。

![](../images/models-recipes/schedule/update_scoring.png)

設定評分排程的頻率、開始日期、結束日期、輸入資料集和輸出資料集。 在您滿意設定後，請選取 **[!UICONTROL 建立]** 更新服務的評分排程。

![](../images/models-recipes/schedule/set_scoring_schedule.png)

您更新的評分排程會顯示在服務的 **[!UICONTROL 概觀]** 頁面。

![](../images/models-recipes/schedule/scoring_set.png)

## 設定排程訓練 {#configure-scheduled-training}

在服務上設定排程的訓練執行，可確保機器學習模型更新為最新的資料模式。 每當排程的訓練回合完成時，就會使用產生的訓練模型來支援服務，直到下一次排程的訓練回合為止。

建立服務後，您可以依照下列步驟設定並套用訓練排程：

在Adobe Experience Platform中，選取 **[!UICONTROL 服務]** 標籤以存取 **[!UICONTROL 服務庫]**. 尋找您想要排程訓練執行的服務，然後選取 **[!UICONTROL 開啟]** 以檢視其 **[!UICONTROL 概觀]** 頁面。

![](../images/models-recipes/schedule/select_service.png)

「總覽」頁面會顯示服務的訓練資訊。 選取 **[!UICONTROL 更新排程]** 設定訓練排程的連結。

![](../images/models-recipes/schedule/update_training.png)

設定用於訓練排程的頻率、開始日期、結束日期和輸入資料集。 在您滿意設定後，請選取 **[!UICONTROL 建立]** 更新服務的訓練排程。

![](../images/models-recipes/schedule/set_training_schedule.png)

您更新的訓練排程會顯示在服務的 **[!UICONTROL 概觀]** 頁面。

![](../images/models-recipes/schedule/training_set.png)

## 后续步骤

依照本教學課程所述，您已成功排程服務的自動化訓練和評分回合，並完成 [!DNL Data Science Workspace] 教學課程UI工作流程。 如果您尚未這麼做，請考慮 [重新啟動教學課程](./create-retails-sales-dataset.md) 並遵循API工作流程來建立、訓練、評分和發佈模型。
