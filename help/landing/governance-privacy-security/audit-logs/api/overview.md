---
title: 稽核查詢API指南
description: 稽核查詢是RESTful API，可讓開發人員檢視誰在Adobe Experience Platform中執行了哪些動作。
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---

# [!DNL Audit Query] API指南

此 [!DNL Audit Query] API提供端點，可讓您以程式設計方式擷取和監控各種Adobe Experience Platform功能的事件資料。 端點概述如下。 請造訪 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

若要檢視所有可用的端點和CRUD作業，請造訪 [[!DNL Audit Query] API swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## 事件

稽核事件提供對Platform中使用者動作的深入分析，包括動作型別、日期和時間、執行動作之使用者的電子郵件ID，以及與Adobe Experience Platform各種功能的動作型別相關的其他屬性。 若要瞭解如何使用API擷取量度，請參閱 [事件端點指南](./events.md).

## 导出

稽核匯出可讓您指定要在裝載中擷取的事件，以擷取事件資料。 若要瞭解如何使用API擷取量度，請參閱 [匯出端點指南](./export.md).
