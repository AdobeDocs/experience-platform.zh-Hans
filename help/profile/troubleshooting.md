---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 即時客戶個人檔案疑難排解指南
type: Documentation
description: 本檔案提供即時客戶設定檔相關常見問題的解答，以及使用Adobe Experience Platform處理設定檔資料時常見錯誤的疑難排解指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 即時客戶個人檔案疑難排解指南

本檔案提供有關即時客戶個人檔案的常見問題解答，以及常見錯誤的疑難排解指南。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

替換為 [!DNL Real-Time Customer Profile]，您可以透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 這可讓行銷人員跨多個管道為客戶推動協調、一致且相關的體驗。

## 常见问题解答

以下是有關Real-Time Customer Profile常見問題的回答清單。

### Real-time Customer Profile可接受哪些型別的資料？

設定檔接受兩者 **記錄** 和 **時間序列** 資料，前提是有問題的資料至少包含一個身分值，可讓資料與不重複個人建立關聯。

和所有Platform服務一樣，Profile要求其資料在語義上結構化為體驗資料模型(XDM)結構描述。 反過來，此結構描述必須有 **主要身分** 已定義並已啟用，以便在設定檔中使用。

如果您不熟悉XDM，請從 [XDM概觀](../xdm/home.md) 以深入瞭解。 接下來，請參閱XDM使用指南，以瞭解操作步驟 [設定身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 和 [為設定檔啟用結構描述](../xdm/tutorials/create-schema-ui.md#profile).

### 設定檔資料會儲存在何處？

Real-Time Customer Profile會維護其本身的資料存放區（稱為「設定檔存放區」），與包含其他已擷取Platform資料的Data Lake分開。

### 如果我已經將資料內嵌至Platform，可以在設定檔存放區中使用嗎？

如果資料已內嵌至非設定檔資料集，您必須將該資料重新內嵌至啟用設定檔的資料集，才能使其在設定檔存放區中使用。 可以為設定檔啟用現有資料集，但是在該設定之前擷取的任何資料仍將不會顯示在設定檔存放區中。

如果您想要將先前擷取的資料新增至設定檔存放區，請遵循 [資料集設定教學課程](./tutorials/dataset-configuration.md) 建立新資料集或轉換現有資料集以啟用設定檔，然後將所需資料重新內嵌至該資料集。

### 如何檢視我內嵌的設定檔資料？

檢視設定檔資料的方法有很多種，視您使用的是API還是UI而定。

#### 使用 API

如果您知道要存取之設定檔實體的ID，則可以使用 `/entities` （設定檔存取）設定檔API中的端點以查詢這些實體。 請參閱以下小節： [實體](./api/entities.md) 詳細資訊，請參閱開發人員指南。

您也可以使用Adobe Experience Platform Segmentation Service API來存取符合區段會籍資格的客戶的個人設定檔。 請參閱 [Segmentation Service概述](../segmentation/home.md) 以取得詳細資訊。

#### 使用UI

在Experience PlatformUI中， **[!UICONTROL 瀏覽]** 索引標籤中的 **[!UICONTROL 設定檔]** 工作區可讓您檢視設定檔總數，並按其身分值搜尋個別設定檔。 請參閱 [設定檔使用手冊](./ui/user-guide.md) 以取得詳細資訊。

您也可以在「 」下檢視區段清單 **[!UICONTROL 瀏覽]** 索引標籤中的 **[!UICONTROL 區段]** 工作區。 選取區段後，會顯示符合該區段資格的設定檔範例。 然後，您可以選取任何列出的設定檔來檢視其詳細資訊。 請參閱 [區段UI總覽](../segmentation/ui/overview.md) 以取得詳細資訊。

## 错误代码

以下是您在使用Real-Time Customer Profile API時可能會遇到的錯誤訊息清單。 如果您遇到的錯誤未在此處列出，您可能會在一般中找到 [平台疑難排解指南](../landing/troubleshooting.md) 而非。

### 無法查詢所提供路徑的計算屬性的結構描述

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

建立新的計算屬性時，當系統找不到要求裝載中提供的結構描述時，就會發生此錯誤。 確定您已在裝載的中提供正確的租使用者ID `path` 屬性，而且其值 `schema.name` 是有效的結構描述名稱。

如果您不知道租使用者ID，可以依照以下檔案中的步驟擷取它： [Schema Registry開發人員指南](../xdm/api/getting-started.md).

### 指定的結構描述或definedOn已存在同名函式

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

建立新的計算屬性時，如果提供的是 `name` 屬性已用於 `schema.name`. 在重試之前，以唯一名稱取代值。

### 運算式的傳回結構描述與XDM結構描述中運算屬性的結構描述不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

建立新的計算屬性時，如果提供的是 `name` 屬性已用於 `schema.name`. 在重試之前，以唯一名稱取代值。

### 無效的刪除請求（設定檔系統工作）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

為刪除系統作業提供無效的裝載時，會發生此錯誤。 確保您在有效負載的底下提供有效的資料集或批次ID `dataSetID` 或 `batchID` 屬性。 請參閱以下小節： [建立刪除請求](./api/profile-system-jobs.md#create-a-delete-request) 詳細資訊，請參閱個人資料開發人員指南。

### 找不到設定檔資料集的批次

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

當嘗試建立設定檔資料的刪除請求時找不到有效的批次時，就會發生此錯誤。 在重試之前，請檢查您已為啟用設定檔的資料集輸入正確的ID。

### 尚未建立投影目的地

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

此錯誤發生於 `destinationId` 提供於 `POST /config/projections` 請求無效。 在重試之前，請仔細檢查您是否已提供有效的目的地ID。 若要建立新目的地，請依照以下說明的步驟： [設定檔開發人員指南](./api/edge-projections.md#create-a-destination).

### 不支援的媒體型別

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

傳送具有無效Content-Type標頭的POST或PUT請求時，會發生此錯誤。 仔細檢查您是否為使用的端點提供有效的Content-Type值。

大部分的設定檔端點都接受「application/json」做為其Content-Type標頭，但有下列例外：

| 端點 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json； version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json； version=1 |
