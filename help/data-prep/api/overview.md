---
keywords: Experience Platform；資料準備；資料準備api；疑難排解； API
title: 資料準備API總覽
description: 「資料準備API」可讓您以程式設計方式建立對應集和函式，讓您在來源和目的地結構描述之間轉換資料。
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Mapping Service API指南

「資料準備」可讓資料工程師對應、轉換和驗證與Experience Data Model (XDM)之間的資料。 「資料準備」在資料擷取程式（包括CSV擷取工作流程）中顯示為「對應」步驟。

對應服務API，也稱為資料準備API，包含下列多個端點。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

## 函数

對應集函式可讓您在來源和目的地結構描述之間轉換資料。 您可以使用 `/languages/el` 端點來驗證運算式，並取得所有可用對應集函式和操作的清單。

如需如何使用對應集函式的詳細資訊，請參閱 [函式端點指南](./functions.md).

## 對應集

對應集可用來定義來源結構描述中的資料如何對應到目的地結構描述。 您可以使用 `/mappingSets` 資料準備API中的端點，以程式設計方式擷取、建立、更新和驗證對應集。

如需如何使用對應集的詳細資訊，請參閱 [對應集端點指南](./mapping-set.md).

## 后续步骤

若要開始使用對應服務API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後選取其中一個端點指南，以瞭解如何使用特定端點。
