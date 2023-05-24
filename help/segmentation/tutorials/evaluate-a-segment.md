---
keywords: Experience Platform；首頁；熱門主題；區段評估；區段服務；區段；區段；評估區段；存取區段結果；評估和存取區段；
solution: Experience Platform
title: 評估並存取區段結果
type: Tutorial
description: 按照本教學課程瞭解如何使用Adobe Experience Platform Segmentation Service API評估區段和存取區段結果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# 評估並存取區段結果

本檔案提供評估區段及使用存取區段結果的教學課程。 [[!DNL Segmentation API]](../api/getting-started.md).

## 快速入门

本教學課程需要深入瞭解各種 [!DNL Adobe Experience Platform] 建立受眾區段所涉及的服務。 在開始本教學課程之前，請檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從以下專案建立受眾區段： [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。 為了充分利用「分段」，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 必要的標頭

本教學課程也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] API。 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 以下專案的請求： [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有POST、PUT和PATCH請求都需要額外的標頭：

- Content-Type： application/json

## 評估區段 {#evaluate-a-segment}

開發、測試並儲存區段定義後，您就可以透過排定的評估或隨選評估來評估區段。

[已排程的評估](#scheduled-evaluation) （也稱為「已排程分段」）可讓您建立在特定時間執行匯出工作的週期性排程，而 [隨選評估](#on-demand-evaluation) 包括建立區段工作以立即建立對象。 各步驟概述如下。

如果您尚未完成 [使用分段API建立區段](./create-a-segment.md) 教學課程或建立區段定義，使用 [區段產生器](../ui/overview.md)，請在繼續本教學課程之前完成此操作。

## 已排程的評估 {#scheduled-evaluation}

透過已排程的評估，您的組織可以建立週期性排程，以自動執行匯出作業。

>[!NOTE]
>
>對於最多有五(5)個合併原則的沙箱，可啟用排程評估 [!DNL XDM Individual Profile]. 如果貴組織有五個以上的合併原則 [!DNL XDM Individual Profile] 在單一沙箱環境中，您將無法使用排程的評估。

### 建立排程

藉由向發出POST請求 `/config/schedules` 端點，您可以建立排程並包含應觸發排程的特定時間。

有關使用此端點的更多詳細資訊，請參閱 [排程端點指南](../api/schedules.md#create)

### 啟用排程

依預設，排程在建立時為非使用中，除非 `state` 屬性已設定為 `active` (POST)要求內文中的。 您可以啟用排程(設定 `state` 至 `active`)向發出PATCH要求 `/config/schedules` 端點並在路徑中包含排程的ID。

有關使用此端點的更多詳細資訊，請參閱 [排程端點指南](../api/schedules.md#update-state)

### 更新排程時間

您可以透過向以下發出PATCH請求來更新排程計時： `/config/schedules` 端點並在路徑中包含排程的ID。

有關使用此端點的更多詳細資訊，請參閱 [排程端點指南](../api/schedules.md#update-schedule)

## 隨選評估

隨選評估可讓您建立區段工作，以便在您需要時產生對象區段。 與已排程的評估不同，這僅在請求時發生，而且不會重複發生。

### 建立區段工作

區段作業為非同步程式，可依需求建立對象區段。 它會參考區段定義，以及控制如何進行的任何合併原則 [!DNL Real-Time Customer Profile] 合併您的設定檔片段中的重疊屬性。 當區段工作成功完成時，您可以收集關於區段的各種資訊，例如處理期間可能發生的任何錯誤以及您的對象的最終規模。 每次想要重新整理目前符合區段定義資格的對象時，都需要執行區段工作。

您可以透過向以下專案發出POST請求，以建立新的區段作業： `/segment/jobs` 中的端點 [!DNL Real-Time Customer Profile] API。

有關使用此端點的更多詳細資訊，請參閱 [區段作業端點指南](../api/segment-jobs.md#create)

### 查詢區段工作狀態

您可以使用 `id` 針對特定區段工作，執行查詢請求(GET)，以檢視工作的目前狀態。

有關使用此端點的更多詳細資訊，請參閱 [區段作業端點指南](../api/segment-jobs.md#get)

## 解讀區段結果

成功執行區段作業時， `segmentMembership` 會針對區段中包含的每個設定檔更新地圖。 `segmentMembership` 也會儲存任何擷取到的預先評估對象區段 [!DNL Platform]，允許與其他解決方案整合，例如 [!DNL Adobe Audience Manager].

以下範例說明 `segmentMembership` 屬性看起來像每個個別設定檔記錄：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `lastQualificationTime` | 進行區段會籍判斷提示以及設定檔進入或退出區段時的時間戳記。 |
| `status` | 目前請求中的區段參與狀態。 必須等於下列其中一個已知值： <ul><li>`realized`：實體符合區段的資格。</li><li>`exited`：實體正在退出區段。</li></ul> |

>[!NOTE]
>
>任何位於中的區段會籍 `exited` 超過30天的狀態，根據 `lastQualificationTime`，可能會刪除。

## 存取區段結果

區段工作的結果可透過以下兩種方式之一存取：您可以存取個別設定檔，或匯出整個對象至資料集。

以下各節會更詳細地概述這些選項。

## 查詢設定檔

如果您知道想要存取的特定設定檔，可以使用 [!DNL Real-Time Customer Profile] API。 存取個別設定檔的完整步驟可在以下網址取得： [使用設定檔API存取即時客戶設定檔資料](../../profile/api/entities.md) 教學課程。

## 匯出區段 {#export}

成功完成分段工作後( `status` 屬性為「SUCCEEDED」)，您可以將對象匯出至資料集，在其中存取對象並對其採取行動。

匯出對象時，需要執行下列步驟：

- [建立目標資料集](#create-a-target-dataset)  — 建立資料集以存放對象成員。
- [在資料集中產生受眾設定檔](#generate-profiles)  — 根據區段作業的結果，以XDM個別設定檔填入資料集。
- [監視匯出進度](#monitor-export-progress)  — 檢查匯出程式的目前進度。
- [讀取對象資料](#next-steps)  — 擷取代表您對象之成員的XDM個別設定檔。

### 建立目標資料集 {#create-dataset}

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所根據的結構描述(`schemaRef.id` （位於以下的API範例請求中）。 為了匯出區段，資料集必須以 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 聯合結構描述是系統產生的唯讀結構描述，其彙總共用相同類別的結構描述（在此例中為XDM個別設定檔類別）的欄位。 如需聯合檢視結構描述的詳細資訊，請參閱 [Schema Registry開發人員指南的Real-Time Customer Profile一節](../../xdm/api/getting-started.md).

建立必要資料集的方法有兩種：

- **使用API：** 本教學課程後續步驟會概述如何建立參照 [!DNL XDM Individual Profile Union Schema] 使用 [!DNL Catalog] API。
- **使用UI：** 若要使用 [!DNL Adobe Experience Platform] 使用者介面若要建立參考聯合結構的資料集，請依照以下步驟操作： [UI教學課程](../ui/overview.md) 然後返回本教學課程，繼續的步驟 [產生受眾設定檔](#generate-profiles).

如果您已有相容的資料集且知道其ID，您可以直接繼續進行以下步驟： [產生受眾設定檔](#generate-profiles).

**API格式**

```http
POST /dataSets
```

**请求**

以下請求會建立新資料集，在承載中提供設定引數。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 與資料集建立關聯的聯合檢視（結構描述）的ID。 |

**响应**

成功的回應會傳回陣列，其中包含新建立資料集的唯讀、系統產生的唯一ID。 需要正確設定的資料集ID才能成功匯出受眾成員。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 產生對象成員的設定檔 {#generate-profiles}

擁有聯合持續資料集後，您可以透過向以下專案發出POST請求，建立匯出工作以將對象成員持續存在資料集： `/export/jobs` 中的端點 [!DNL Real-Time Customer Profile] API並為您要匯出的區段提供資料集ID和區段資訊。

有關使用此端點的更多詳細資訊，請參閱 [匯出作業端點指南](../api/export-jobs.md#create)

### 監視匯出進度

匯出作業進行時，您可以透過向以下發出GET請求來監控其狀態： `/export/jobs` 端點，並包含 `id` 路徑中匯出作業的ID。 匯出作業於下列時間後完成： `status` 欄位會傳回「SUCCEEDED」值。

有關使用此端點的更多詳細資訊，請參閱 [匯出作業端點指南](../api/export-jobs.md#get)

## 后续步骤

匯出成功完成後，您的資料可在 [!DNL Data Lake] 在 [!DNL Experience Platform]. 然後，您可以使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 以使用存取資料 `batchId` 與匯出相關聯。 視區段的大小而定，資料可能以區塊為單位，批次可能包含數個檔案。

如需如何使用 [!DNL Data Access] 存取和下載批次檔案的API，請遵循 [資料存取教學課程](../../data-access/tutorials/dataset-data.md).

您也可以使用存取成功匯出的區段資料 [!DNL Adobe Experience Platform Query Service]. 使用UI或RESTful API， [!DNL Query Service] 可讓您對中的資料寫入、驗證及執行查詢 [!DNL Data Lake].

如需如何查詢受眾資料的詳細資訊，請參閱以下說明檔案： [[!DNL Query Service]](../../query-service/home.md).
