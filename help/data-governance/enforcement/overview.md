---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 原則執行概觀
description: 瞭解如何在Adobe Experience Platform上執行資料使用原則。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 原則執行概觀

一次 [資料使用標籤](../labels/overview.md) 已套用且 [資料使用原則](../policies/overview.md) 已定義，您可以強制執行這些原則，以防止構成原則違規的資料作業。

>[!NOTE]
>
>本檔案著重於資料使用原則的實作。 如需有關存取控制原則的資訊，請參閱以下指南： [基於屬性的存取控制](../../access-control/abac/overview.md).

在Adobe Experience Platform上執行原則的方法有兩種：自動執行和API型執行。

## 自動強制執行

Experience Platform會利用資料譜系、資料分類和原則管理功能，自動評估並處理原則違規。 請參閱以下文章的概觀： [自動原則執行](./auto-enforcement.md) 以取得詳細資訊。

## API型強制執行

此 [!DNL Policy Service] API提供端點，可讓您根據資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何原則違規。 接著，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當地強制資料控管原則相容。

請參閱教學課程，位置如下： [API型強制執行](./api-enforcement.md) 瞭解如何使用API評估政策的步驟。
