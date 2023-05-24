---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service疑難排解指南
description: 本檔案提供有關Privacy Service常見問題的解答，以及API中常見錯誤的資訊。
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# [!DNL Privacy Service] 疑難排解指南

Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，以協助公司管理客戶資料隱私權請求。 替換為 [!DNL Privacy Service]，您可以提交存取和刪除私人或個人客戶資料的請求，促進自動遵守組織和法律隱私權法規。

本檔案提供以下專案的常見問題解答： [!DNL Privacy Service]以及API中常見錯誤的資訊。

## 在API中提出隱私權請求時，使用者與使用者ID之間有何差異？ {#user-ids}

為了在API中建立新的隱私權工作，請求的JSON裝載必須包含 `users` 陣列，列出隱私權請求適用的每個使用者的特定資訊。 中的每一個專案 `users` array是代表特定使用者的物件，由其 `key` 值。

反過來，每個使用者物件(或 `key`)包含自己的 `userIDs` 陣列。 此陣列會列出特定的ID值 **針對該特定使用者**.

考量下列範例 `users` 陣列：

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

陣列包含兩個物件，代表各自識別的使用者 `key` 值(「DavidSmith」和「user12345」)。 「DavidSmith」只有一個列出的ID （他們的電子郵件地址），而「user12345」有兩個的（他們的電子郵件地址和ECID）。

如需有關提供使用者身分資訊的詳細資訊，請參閱以下指南： [隱私權請求的身分資料](identity-data.md).


## 我可以使用 [!DNL Privacy Service] 以清除不小心傳送到的資料 [!DNL Platform]？

Adobe不支援使用 [!DNL Privacy Service] 用於清除意外提交給產品的資料。 [!DNL Privacy Service] 旨在協助您履行資料主體（或消費者）存取或刪除請求的義務。 不支援或不允許將Privacy Service用於資料清理或維護的任何其他用途。

隱私權請求常有時效性，而且是根據適用的隱私權法律完成。 提交非資料主體/消費者存取或刪除請求的請求會影響所有 [!DNL Privacy Service] 客戶及以下功能 [!DNL Privacy Service] 以支援適當的法律時間表。 現已設定每日硬性上傳限制，以防止服務被濫用。

請聯絡您的Adobe客戶團隊，以協調並提供移除任何PII或資料問題的幫助。

## 如何取得隱私權請求或工作狀態的相關資訊？

您可以使用來擷取特定工作的詳細資訊 [!DNL Privacy Service] API或使用者介面。

### 使用 API

若要使用擷取特定工作的狀態 [!DNL Privacy Service] API，向根提出請求(`GET /`)端點，使用請求路徑中作業的ID。 如需詳細資訊，請參閱以下章節： [檢查工作狀態](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

所有作用中的工作請求都會列在 **[!UICONTROL 工作請求]** 上的Widget [!DNL Privacy Service] UI儀表板。 每個工作請求的狀態都會顯示在 **[!UICONTROL 狀態]** 欄。 如需在UI中檢視工作請求的詳細資訊，請參閱 [Privacy Service使用手冊](ui/user-guide.md).

## 如何下載已完成的隱私權工作的結果？

此 [!DNL Privacy Service] API和使用者介面都提供以ZIP格式下載已完成作業結果的方法。

### 使用 API

向根提出請求(`GET /`)端點(在 [!DNL Privacy Service] API，使用您要在請求路徑中下載其結果的工作的ID。 如果工作的狀態為完成，則API將包含 `downloadURL` 屬性。 此屬性包含一個URL，您可以將其貼到瀏覽器的位址列來下載ZIP檔案。

如需詳細資訊，請參閱以下章節： [依作業ID查詢作業](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

於 [!DNL Privacy Service] UI控制面板，找出您要從下載的工作 **工作請求** Widget. 選取工作的ID以開啟「工作詳細資訊」頁面。 從此處選取 **下載** 右上角下載ZIP檔案。 請參閱 [Privacy Service使用手冊](ui/user-guide.md) 以取得更詳細的步驟。

## 常见错误消息

下表概述中的幾個常見錯誤 [!DNL Privacy Service]，並提供說明，以協助解決各自的問題。

| 错误消息 | 描述 |
| --- | --- |
| 找不到使用者識別碼。 | 找不到請求中提供的部分使用者ID，已略過。 確保您在請求裝載中使用正確的名稱空間和ID值。 檢視檔案： [提供身分資料](./identity-data.md) 以取得更詳細的說明。 |
| 無效的名稱空間 | 為使用者ID提供的身分名稱空間無效。 請參閱以下小節： [標準身分名稱空間](./api/appendix.md#standard-namespaces) 在 [!DNL Privacy Service] API指南附錄，以取得接受的名稱空間清單。 如果您使用自訂名稱空間，請務必設定ID的 `type` 屬性重新命名為「custom」。 |
| 部分完成 | 工作已成功完成，但部分資料不適用於特定請求，已略過。 |
| 資料不是要求的格式。 | 指定應用程式的一個或多個資料值格式不正確。 如需詳細資訊，請檢視工作詳細資料。 |
| 尚未布建IMS組織。 | 當您的組織尚未布建時，就會出現此訊息 [!DNL Privacy Service]. 如需詳細資訊，請聯絡管理員。 |
| 需要存取權和許可權。 | 需要存取權和許可權才能使用 [!DNL Privacy Service]. 請聯絡您的管理員以取得存取權。 |
| 上傳和封存存取資料時發生問題。 | 發生此錯誤時，請重新上傳存取資料，然後重試。 |
| 工作負載超過目前的檔案速率限制。 | 發生此錯誤時，請降低提交率並重試。 |
