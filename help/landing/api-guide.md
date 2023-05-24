---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience Platform API快速入門
description: Adobe Experience Platform提供的API服務彼此緊密連結。 本指南包含可用服務、CRUD作業所需標頭、錯誤訊息、Postman集合和範例API呼叫的相關資訊。
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Adobe Experience Platform API快速入門

Adobe Experience Platform是以「API優先」的理念開發。 使用Platform API，您可以利用程式設計方式針對資料執行基本CRUD （建立、讀取、更新、刪除）操作，例如設定計算屬性、存取資料/實體、匯出資料、刪除不需要的資料或批次等。

每個Experience Platform服務的API都共用相同的驗證標題集，並對其CRUD操作使用類似的語法。 下列指南概述開始使用Platform API的必要步驟。

## 驗證和標頭

為了成功呼叫Platform端點，您必須完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### 沙箱標頭

Experience Platform中的所有資源都與特定的虛擬沙箱隔離。 對Platform API的請求需要標頭，該標頭會指定將在哪個沙箱中執行操作：

- `x-sandbox-name: {SANDBOX_NAME}`

如需Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../sandboxes/home.md).

### Content-type標題

要求內文中具有裝載的所有要求(例如POST、PUT和PATCH呼叫)必須包含 `Content-Type` 標頭。 接受的值是每個API端點專屬的值。 若為特定 `Content-Type` 端點需要值，其值將顯示在提供的範例API請求中。 [適用於個別平台服務的API指南](#api-guides).

## Experience PlatformAPI基礎知識

Adobe Experience Platform API運用了幾項重要的基礎技術和語法，以便有效管理Platform資源。

若要進一步瞭解Platform使用的基礎API技術，包括範例JSON結構描述物件，請造訪 [Experience PlatformAPI基礎知識](api-fundamentals.md) 指南。

## Experience Platform API的Postman集合

Postman是API開發的共同作業平台，可讓您使用預設變數設定環境、共用API集合、簡化CRUD請求等。 大部分的Platform API服務都有Postman集合，可用來協助進行API呼叫。

若要進一步瞭解Postman，包括如何設定環境、可用集合清單以及如何匯入集合，請造訪 [Platform Postman檔案](postman.md).

## 讀取範例API呼叫 {#sample-api}

請求格式會因使用的平台API而異。 瞭解如何建構API呼叫的最佳方式，是遵循您使用的特定平台服務的檔案中提供的範例。

的相關檔案： [!DNL Experience Platform] 以兩種不同的方式顯示API呼叫範例。 首先，呼叫會顯示在其 **API格式**，此範本表示法僅會顯示使用的操作(GET、POST、PUT、PATCH、DELETE)和端點(例如 `/global/classes`)。 有些範本也會顯示變數的位置，以說明呼叫的建構方式，例如 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

然後，這些呼叫會顯示為cURL命令 **請求**，包括成功與API互動所需的必要標題和完整「基本路徑」。 基底路徑應預先附加到所有端點。 例如，上述的 `/global/classes` 端點變成 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. 在整個檔案中，您都會看到API格式/請求模式，當您對Platform API發出自己的呼叫時，應使用範例請求中顯示的完整路徑。

### 範例API請求

以下範例API請求會示範您將在檔案中遇到的格式。

**API格式**

API格式會顯示使用的操作(GET)和端點。 變數會以大括弧表示(在此情況下， `{CONTAINER_ID}`)。

```http
GET /{CONTAINER_ID}/classes
```

**请求**

在此範例請求中，來自API格式的變數在請求路徑中被指定實際值。 此外，所有必要的標頭都會顯示為範例標頭值或變數，其中應包含敏感資訊（例如安全性權杖和存取ID）。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應會根據已傳送的請求，說明在成功呼叫API後您會收到的內容。 回應偶爾會截斷空格，這表示您可能會看到範例中顯示的更多資訊或其他資訊。

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## 错误消息

此 [平台疑難排解指南](troubleshooting.md#errors-and-troubleshooting) 提供您使用任何Experience Platform服務時可能遇到的錯誤清單。

如需個別平台服務的疑難排解指南，請參閱 [服務疑難排解目錄](troubleshooting.md#service-troubleshooting-directory).

如需Platform API中特定端點的詳細資訊，包括必要的標題和請求內文，請參閱 [平台API指南](#api-guides).

## 平台API指南 {#api-guides}

| API指南 | 描述 |
| --- | --- |
| [[!DNL Access Control] API指南](.././access-control/api/getting-started.md) | 此 [!DNL Access Control] API端點可以擷取使用者在指定沙箱內的指定資源上有效的目前原則。 所有其他存取控制功能是透過 [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [批次擷取API指南](.././ingestion/batch-ingestion/api-overview.md) | Adobe Experience Platform [!DNL Data Ingestion] API可讓您將資料以批次檔案的形式擷取到Platform。 所擷取的資料可以是CRM系統中平面檔案（例如Parquet檔案）的設定檔資料，或是符合Schema Registry (XDM)中已知結構的資料。 |
| [[!DNL Catalog Service] API指南](.././catalog/api/getting-started.md) | 此 [!DNL Catalog Service] API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 這包括資料位置、處理階段、處理期間發生的錯誤以及資料報表。 |
| [[!DNL Data Access] API指南](.././data-access/api.md) | 此 [!DNL Data Access] API可讓開發人員擷取Experience Platform內擷取資料集的資訊。 這包括存取和下載資料集檔案、擷取標頭資訊、列出失敗和成功的批次，以及下載預覽CSV / Parquet檔案。 |
| [[!DNL Dataset Service] API指南](.././data-governance/labels/dataset-api.md) | 資料集服務API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。 |
| [[!DNL Identity Service] API指南](.././identity-service/api/getting-started.md) | 此 [!DNL Identity Service] API可讓開發人員使用Adobe Experience Platform中的身分圖表，管理跨裝置、跨頻道及幾乎即時的客戶身分識別。 |
| [[!DNL Observability Insights] API指南](.././observability/api/overview.md) | [!DNL Observability Insights] 是RESTful API，可讓開發人員在Adobe Experience Platform中公開關鍵可觀察性量度。 這些量度可提供Platform使用狀況統計資料、Platform服務的健康情況檢查、歷史趨勢，以及各種Platform功能的績效指標的深入分析。 |
| [[!DNL Policy Service] API指南](.././data-governance/api/overview.md) <br> （資料控管） | 此 [!DNL Policy Service] API可讓您建立和管理資料使用標籤和原則，以決定可以對包含特定資料使用標籤的資料採取哪些行銷動作。 若要將標籤套用至資料集和欄位，請參閱 [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) 指南 |
| [[!DNL Privacy Service] API指南](.././privacy-service/api/getting-started.md) | 此 [!DNL Privacy Service] API可讓開發人員建立和管理客戶請求，以存取或刪除他們在Experience Cloud應用程式中的個人資料，以符合法律隱私權法規。 |
| [[!DNL Query Service] API指南](.././query-service/api/getting-started.md) | 此 [!DNL Query Service] API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 |
| [[!DNL Real-Time Customer Profile] API指南](.././profile/api/overview.md) | 即時客戶設定檔API可讓開發人員探索和使用設定檔資料，包括檢視設定檔、建立和更新合併原則、匯出或取樣設定檔資料，以及刪除不再需要或錯誤新增的設定檔資料。 |
| [Sandbox API指南](.././sandboxes/api/getting-started.md) | 沙箱API可讓開發人員以程式設計方式管理Adobe Experience Platform中的獨立虛擬沙箱環境。 |
| [[!DNL Schema Registry] API指南](.././xdm/api/overview.md) <br> (XDM) | 此 [!DNL Schema Registry] API可讓開發人員以程式設計方式管理Adobe Experience Platform中的所有結構描述和相關的Experience Data Model (XDM)資源。 |
| [[!DNL Segmentation Service] API指南](.././segmentation/api/overview.md) | 此 [!DNL Segmentation Service] API可讓開發人員以程式設計方式管理Adobe Experience Platform中的細分作業。 這包括建立區段，以及從您的即時客戶設定檔資料產生對象。 |
| [[!DNL Sensei Machine Learning] API指南](.././data-science-workspace/api/getting-started.md) <br> （資料科學工作區） | 此 [!DNL Sensei Machine Learning] API為資料科學家提供了一種機制，可組織和管理機器學習(ML)服務，從演演算法上線、實驗到服務部署。 |

如需每個服務特定端點和可用操作的詳細資訊，請參閱 [API參考檔案](https://www.adobe.com/go/platform-api-reference-en) 在Adobe I/O上。

## 后续步骤

本檔案會介紹必要的標頭、可用的指南，並提供API呼叫的範例。 現在您已擁有在Adobe Experience Platform上進行API呼叫所需的標頭值，請從中選擇您要探索的API端點 [平台API指南表格](#api-guides).

如需常見問題的解答，請參閱 [平台疑難排解指南](troubleshooting.md).

若要設定Postman環境並探索可用的Postman集合，請參閱 [Platform Postman指南](postman.md).
