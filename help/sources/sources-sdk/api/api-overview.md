---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 自助來源（批次SDK） API指南
description: 本檔案提供建立新來源的程式概述，包括如何使用「流程服務API」擷取、寫入及提交新連線規格的步驟。
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 自助來源（批次SDK） API指南

本檔案概述建立新來源的過程，包括有關如何使用編寫並提交新連線規格的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] 用於收集並集中來自Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，可讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證協力廠商系統、設定擷取執行時間，以及管理資料擷取輸送量。

此 [!DNL Flow Service] API提供數個端點，可讓您以程式設計方式管理要透過自助式來源（批次SDK）整合之新來源的連線和流程規格。

## 建立新的連線規格

設定新來源的第一步是建立新的連線規格。

連線規格會傳回來源的聯結器屬性。 它們包括與建立基礎和來源連線相關的驗證規格，以及指派給特定來源的固定連線規格ID。 連線規格與租使用者和組織無關。 典型的連線規格包含指定來源的基本資訊，以及三個不同的區段： `authSpec`， `sourceSpec`、和 `exploreSpec`.

如需詳細指示，請參閱以下指南： [建立新的連線規格](./create.md). 如需用於連線規格的屬性和值的詳細資訊，包括設定驗證、來源和探索規格的詳細資訊，請參閱 [組態選項檔案](../config/config.md).

## 更新流程規格

成功建立連線規格後，您必須附加 `RestStorageToAEP` 流量規格，讓您的來源能夠建立資料流。

流程規格包含定義流程的資訊，包括它支援的來源和目標連線ID、需要套用至資料的轉換規格，以及產生流程所需的排程引數。

如需詳細指示，請參閱以下指南： [更新流程規格](./update-flow-specs.md).

## 更新您的連線規格

您可以向以下網址發出PUT要求，更新您的連線規格： [!DNL Flow Service] API。 請參閱指南： [更新您的連線規格](./update-connection-specs.md) 以取得詳細資訊。

## 提交您的來源

若要提交您的來源以整合至Experience Platform，您必須先完成整個 [!DNL Flow Service] 來源的API工作流程，以確保您的來源可成功運作。 如果您的來源成功執行，則可以繼續並聯絡您的Adobe代表以進行驗證和提升。 請參閱指南： [測試和提交您的來源](./submit.md) 以取得詳細資訊

## 后续步骤

若要開始使用 [!DNL Flow Service] API和透過自助來源（批次SDK）建立新來源，請參閱 [快速入門手冊](./getting-started.md) 然後選取其中一個端點指南，以瞭解如何使用特定端點。
