---
title: 驗證編輯器檢視
description: 本指南詳細說明Adobe Experience Platform Assurance中驗證編輯器檢視的相關資訊。
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# 驗證編輯器檢視

驗證編輯器可讓您快速輕鬆地管理JavaScript函式，以驗證Adobe Experience Platform保證工作階段中的事件。 每個函式都會在保證工作階段中接收事件。 您可以撰寫函式來驗證使用者端設定、事件條件、測試和使用案例。

## 開始使用驗證編輯器

晚於 [設定Assurance](../tutorials/implement-assurance.md)，位於 **[!UICONTROL 首頁]** 檢視，選取 **[!UICONTROL 驗證編輯器]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 撰寫驗證函式

此功能可讓您建立、編輯或刪除Adobe Experience Platform保證工作階段的驗證功能。

1. 選取 **[!UICONTROL 建立新驗證]**.
2. 輸入 **名稱** 以識別驗證，然後提供 **類別** 和 **說明**.
3. 編輯編輯器中的程式碼以驗證保證工作階段的事件。

完成功能測試後，選取 **[!UICONTROL 發佈]** 以儲存驗證。

### 事件定義

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 事件的通用唯一識別碼。 |
| `timestamp` | 数值 | 將事件傳送至Assurance時來自使用者端的時間戳記。 |
| `eventNumber` | 数值 | 用於排序事件的傳送時間。 當事件具有相同的時間戳記時，此金鑰很有用。 |
| `vendor` | 字符串 | 反向網域名稱格式的廠商識別字串（例如com.adobe.assurance）。 |
| `type` | 字符串 | 用於表示事件型別。 |
| `payload` | 对象 | 定義事件的資料，並包含唯一和常見屬性。 一些常見屬性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`. |
| `annotations` | 陣列 | 註釋物件的陣列。 |

### 附註定義

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 註解的通用唯一識別碼。 |
| `type` | 字符串 | 用來表示註解的型別，通常是外掛程式的名稱（例如analytics）。 |
| `payload` | 对象 | 定義應補充事件的資料。 對於Adobe Analytics，這是包含處理後點選資料的位置。 |

### 驗證結果

驗證函式應傳回包含以下內容的物件：

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `message` | 字符串 | 要在摘要結果中顯示的驗證訊息。 |
| `events` | 陣列 | 要報告為已比對或未比對的事件uuid陣列。 |
| `links` | 陣列 | 陣列 `ValidationResultLink` 物件以參考檔案和其他資源 `{( type: 'doc'|'product', url: String )}` |
| `result` | 字符串 | 這是驗證結果，而且應該是列舉字串之一：「相符」、「不相符」、「未知」 |

## 檢視驗證結果

函式的結果會顯示在程式碼編輯器下方的結果區段中。 如果驗證結果為 `unknown` 或 `not matched` 和 `events` 陣列有一或多個 `uuids`時，事件會在時間軸中以下列顏色反白顯示：

* 綠色 — 相符
* 橙色 — 未知
* 紅色 — 不相符

![Timeling-Validation-Highlights-Screen-shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 故障排除

您可以新增 `console.log()` ，以將專案列印至開發人員主控台。 或者，您可以使用結果物件的message屬性來偵錯傳送至結果面板的訊息。

如果JavaScript程式碼編輯器中發生錯誤，則會顯示錯誤狀態及原因。

若要進一步瞭解驗證，請造訪 [Adobe Experience Platform保證驗證](https://github.com/adobe/griffon-validation-plugins) GitHub。 您會在這裡找到Adobe擁有的驗證範例。 請參閱 [Wiki](https://github.com/adobe/griffon-validation-plugins/wiki) 以取得更詳細的驗證說明。
