---
keywords: Experience Platform；首頁；熱門主題；日期範圍
solution: Experience Platform
title: Observability Insights API快速入門
description: 「可觀察性深入分析API」可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案會介紹您在嘗試呼叫Observability Insights API之前需要瞭解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 開始使用 [!DNL Observability Insights] API

此 [!DNL Observability Insights] api可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案會介紹您在嘗試呼叫「 」之前需要瞭解的核心概念。 [!DNL Observability Insights] API。

## 讀取範例API呼叫

此 [!DNL Observability Insights] API檔案提供範例API呼叫，示範如何格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱中如何讀取範例API呼叫的區段 [Experience Platform疑難排解指南](../../landing/troubleshooting.md).

## 必要的標頭

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱。 如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

若要開始使用進行呼叫 [!DNL Observability Insights] API，繼續前往 [量度端點指南](./metrics.md).
