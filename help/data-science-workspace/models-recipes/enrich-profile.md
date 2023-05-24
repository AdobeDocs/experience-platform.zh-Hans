---
keywords: Experience Platform；機器學習模型；Data Science Workspace；即時客戶設定檔；熱門主題；機器學習深入分析
solution: Experience Platform
title: 透過機器學習深入分析豐富即時客戶個人檔案
type: Tutorial
description: 本檔案提供如何透過機器學習深入分析來擴充即時客戶設定檔的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 擴充 [!DNL Real-Time Customer Profile] 使用機器學習深入分析

Adobe Experience Platform [!DNL Data Science Workspace] 提供建立、評估及利用機器學習模型的工具和資源，以產生資料預測和見解。 將機器學習深入分析擷取至 [!DNL Profile]-enabled資料集，相同的資料也會擷取為 [!DNL Profile] 接著可使用下列方式分段的記錄： [!DNL Adobe Experience Platform Segmentation Service].

本檔案提供可讓您擴充的教學課程連結 [!DNL Real-Time Customer Profile] 搭配您的機器學習深入分析。

## 快速入门

若要完成下列教學課程，您必須實際瞭解擷取 [!DNL Profile] 資料並建立區段。 在開始本教學課程之前，請檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供每位個別客戶的完整、統一呈現。
- [[!DNL Identity Service]](../../identity-service/home.md)：啟用 [!DNL Real-Time Customer Profile] 透過橋接擷取到Platform中的不同資料來源的身分。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。

除了上述檔案之外，強烈建議您也檢閱下列有關結構描述和結構描述編輯器的指南：

- [結構描述組合基本概念](../../xdm/schema/composition.md)：說明XDM結構描述、建置區塊、構成要使用的結構描述的原則和最佳實務 [!DNL Experience Platform].
- [結構描述編輯器教學課程](../../xdm/tutorials/create-schema-ui.md)：提供在中使用結構編輯器建立結構描述的詳細指示 [!DNL Experience Platform].

## 建立和設定輸出結構描述和資料集 {#create-an-output-schema-and-dataset}

邁向充實的第一步 [!DNL Real-Time Customer Profile] 透過評分分析，您可以瞭解資料所定義的真實世界物件（例如個人）。 瞭解您的資料後，您就可以描述和設計結構來增加意義，就像設計關聯式資料庫一樣。

構成結構描述從指派類別開始。 類別會定義結構描述將包含之資料（記錄或時間序列）的行為方面。 若要開始建立自己的結構描述，請依照以下教學課程中的步驟操作： [使用結構編輯器建立結構](../../xdm/tutorials/create-schema-ui.md). 請注意，在您可以啟用資料集之前， [!DNL Profile]，您需要設定資料集的結構描述，讓其具有主要身分欄位，然後啟用的結構描述 [!DNL Profile]. 當資料被擷取到 [!DNL Profile]-enabled資料集，相同的資料也會擷取為 [!DNL Profile] 記錄。

如果您偏好使用來撰寫結構 [!DNL Schema Registry] API請改為從讀取 [[!DNL Schema Registry] 開發人員指南](../../xdm/api/getting-started.md) 在嘗試進行教學課程之前： [使用API建立結構描述](../../xdm/tutorials/create-schema-api.md).

準備好結構描述和資料集後，您可以使用適當的模型執行評分回合，產生評分資料並內嵌到資料集中。

## 使用建立區段 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

在您產生並內嵌您的評分資料深入分析至 [!DNL Profile]-enabled資料集，您可以使用以下專案建立動態區段： [!DNL Segment Builder].

此 [!DNL Segment Builder] 提供豐富的工作區，讓您與互動 [!DNL Profile] 資料元素。 工作區提供直覺式控制項來建置和編輯規則，例如用來表示資料屬性的拖放圖磚。 請遵循 [[!DNL Segment Builder] 使用手冊](../../segmentation/ui/segment-builder.md) 若要瞭解：

- 使用屬性、事件和現有對象的組合作為建置區塊來建立區段定義。
- 使用規則產生器畫布和容器來控制區段規則的執行順序。
- 檢視潛在對象的預估值，讓您視需要調整區段定義。
- 啟用已排程區段的所有區段定義。
- 為串流細分啟用指定的區段定義。

## 后续步骤 {#next-steps}

若要進一步瞭解區段和 [!DNL Segment Builder]，閱讀 [Segmentation Service概述](../../segmentation/home.md).

若要深入瞭解 [!DNL Real-Time Customer Profile]，閱讀 [即時客戶個人檔案總覽](../../profile/home.md)
