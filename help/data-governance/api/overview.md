---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 原則服務API指南
description: 原則服務API可讓開發人員管理Experience Platform中的資料使用標籤和原則。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。 它在以下方面發揮著關鍵作用 [!DNL Experience Platform] 在不同的層級，包括編目、資料譜系、資料使用標籤、資料使用原則，以及控制行銷動作的資料使用。

此 [!DNL Policy Service] API提供數個端點，可讓您以程式設計方式管理資料使用標籤和原則，並評估違反原則的行銷動作。 這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

若要檢視所有可用的端點和CRUD作業，請造訪 [[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## 标签

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，讓您靈活選擇控管資料的方式。 最佳實務建議在資料內嵌至後立即加上標籤 [!DNL Experience Platform]，或在資料可用於以下專案時立即啟用： [!DNL Platform]. 您可以使用建立、檢視、編輯和刪除標籤 `/labels` 端點。 若要瞭解如何使用此端點，請造訪 [標籤端點指南](./labels.md).

## 行銷動作

在資料控管架構中，行銷動作（也稱為行銷使用案例）是 [!DNL Experience Platform] 資料消費者可能會採取某些措施，而您的組織想要針對這些措施限制資料使用。 如需有關使用行銷動作的詳細資訊，請參閱 [行銷動作端點指南](./marketing-actions.md).

## 支持

資料控管原則是描述允許或限制您對內資料執行何種行銷動作的規則 [!DNL Experience Platform].

>[!NOTE]
>
>資料控管原則與存取控制原則不應混淆，存取控制原則會決定組織中特定Platform使用者可存取的特定資料屬性。 請參閱指南： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得詳細資訊。

資料治理原則的定義如下：

1. 特定行銷動作
1. 限制動作執行的資料使用標籤

若要瞭解如何在API中管理原則，請參閱 [原則端點指南](./policies.md)

## 评估

將資料使用標籤套用至 [!DNL Platform] 資料集和資料使用原則已針對這些標籤定義了行銷動作，資料控管功能可讓您強制執行這些原則並防止構成原則違規的資料作業。

此 [!DNL Policy Service] API提供端點，可讓您根據資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何原則違規。 接著，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當地強制資料使用原則相容。 請參閱 [評估端點指南](./evaluation.md) 以取得詳細資訊。

## 后续步骤

若要開始使用進行呼叫 [!DNL Policy Service] API，請閱讀 [快速入門手冊](./getting-started.md) 然後選取其中一個端點指南，以瞭解如何使用特定端點。 若要使用標籤和原則，請使用 [!DNL Experience Platform] UI，請參閱 [標籤使用手冊](../labels/user-guide.md) 和 [原則使用手冊](../policies/user-guide.md)（分別）。
