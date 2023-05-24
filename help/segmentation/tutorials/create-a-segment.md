---
keywords: Experience Platform；首頁；熱門主題；區段；區段；建立區段；分段；建立區段；分段服務；
solution: Experience Platform
title: 使用區段服務API建立區段
type: Tutorial
description: 按照本教學課程瞭解如何使用Adobe Experience Platform Segmentation Service API開發、測試、預覽和儲存區段定義。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---

# 使用區段服務API建立區段

本檔案提供開發、測試、預覽和儲存區段定義的教學課程，使用 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

有關如何使用使用者介面建立區段的資訊，請參閱 [區段產生器指南](../ui/overview.md).

## 快速入门

本教學課程需要深入瞭解各種 [!DNL Adobe Experience Platform] 建立受眾區段所涉及的服務。 在開始本教學課程之前，請檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從即時客戶個人檔案資料建立受眾區段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。 為了充分利用「分段」，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).

以下小節提供您需瞭解的其他資訊，才能成功對 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type： application/json

## 開發區段定義

區段的第一個步驟是定義區段，以稱為區段定義的建構來表示。 區段定義是一個物件，可封裝寫入的查詢 [!DNL Profile Query Language] (PQL)。 此物件也稱為PQL述詞。 PQL述詞會根據與您提供至的任何記錄或時間序列資料相關的條件，定義區段的規則 [!DNL Real-Time Customer Profile]. 請參閱 [PQL指南](../pql/overview.md) 有關寫入PQL查詢的詳細資訊。

您可以透過向以下專案發出POST請求，以建立新的區段定義： `/segment/definitions` 中的端點 [!DNL Segmentation] API。 下列範例概述如何格式化定義請求，包括成功定義區段所需的資訊。

如需如何定義區段的詳細說明，請參閱 [區段定義開發人員指南](../api/segment-definitions.md#create).

## 估计和预览受众 {#estimate-and-preview-an-audience}

當您開發區段定義時，可以使用中的預估和預覽工具 [!DNL Real-Time Customer Profile] 檢視摘要層級資訊，以協助確保您隔離預期的對象。 預估可提供區段定義的統計資訊，例如預計對象人數和信賴區間。 預覽提供符合區段定義之設定檔的編頁清單，可讓您比較結果與預期。

透過估計和預覽對象，您可以測試和最佳化PQL述詞，直到產生理想的結果，然後可以在更新的區段定義中使用它們。

要預覽或取得區段的預估值，有兩個必要步驟：

1. [建立預覽工作](#create-a-preview-job)
2. [檢視預估或預覽](#view-an-estimate-or-preview) 使用預覽作業的ID

### 如何產生預估值

資料範例可用來評估區段及估計合格設定檔的數量。 每天早上（上午12點至凌晨2點之間，亦即UTC時間上午7點至上午9點）新資料都會載入記憶體，而所有分段查詢都會使用當天的範例資料來估算。 因此，新增的任何新欄位或收集的其他資料都將反映在第二天的估計值中。

樣本大小取決於設定檔存放區中的實體總數。 這些範例大小如下表所示：

| 設定檔存放區中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 少於100萬 | 完整資料集 |
| 1到2000萬 | 100萬 |
| 超過2,000萬 | 佔總數的5% |

預估通常會在10-15秒內執行，從粗略的估計開始，並隨著閱讀更多記錄而調整。

### 建立預覽工作

您可以透過向以下專案發出POST請求來建立新的預覽作業： `/preview` 端點。

有關建立預覽工作的詳細指示，請參閱 [預覽和估計端點指南](../api/previews-and-estimates.md#create-preview).

### 檢視預估或預覽

預估和預覽程式會以非同步方式執行，因為不同的查詢可能需要不同的時間長度才能完成。 啟動查詢後，您可以使用API呼叫來擷取(GET)目前的估計狀態，或在其進行時預覽。

使用 [!DNL Segmentation Service] API，您可以透過預覽作業的ID來查詢其目前狀態。 如果狀態為「RESULT_READY」，則可以檢視結果。 若要查詢預覽工作的目前狀態，請閱讀以下章節： [擷取預覽作業區段](../api/previews-and-estimates.md#get-preview) 在預覽和預估端點指南中。 若要查詢預估工作的目前狀態，請閱讀以下章節： [擷取預估工作](../api/previews-and-estimates.md#get-estimate) 在預覽和預估端點指南中。


## 后续步骤

開發、測試並儲存區段定義後，您就可以使用建立區段工作來建立受眾。 [!DNL Segmentation Service] API。 請參閱教學課程，位置如下： [評估及存取區段結果](./evaluate-a-segment.md) 以取得如何完成此作業的詳細步驟。
