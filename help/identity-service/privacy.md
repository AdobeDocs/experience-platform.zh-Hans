---
keywords: Experience Platform；首頁；熱門主題
title: Identity Service中的隱私權請求處理
description: Adobe Experience Platform Privacy Service會處理客戶存取、選擇退出銷售或刪除其個人資料的請求，如多項隱私權法規所規定。 本文介紹與Identity Service隱私權請求處理相關的重要概念。
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# 隱私權請求處理於 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 處理客戶存取、選擇退出銷售或刪除其個人資料的請求，這些請求由隱私權法規(例如一般資料保護規範(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。

本檔案說明與處理隱私權請求相關的重要概念。 [!DNL Identity Service] 在Adobe Experience Platform中。

>[!NOTE]
>
>本指南僅涵蓋如何向Experience Platform中的Identity資料存放區提出隱私權請求。 如果您也計畫針對Platform Data Lake或提出隱私權請求 [!DNL Real-Time Customer Profile]，請參閱以下內容的相關指南： [資料湖中的隱私權請求處理](../catalog/privacy.md) 及指南： [設定檔的隱私權請求處理](../profile/privacy.md) 除了本教學課程外。
>
>如需針對其他Adobe Experience Cloud應用程式提出隱私權請求的步驟，請參閱 [Privacy Service檔案](../privacy-service/experience-cloud-apps.md).

## 快速入门

建議您實際瞭解下列事項 [!DNL Experience Platform] 閱讀本指南之前的服務：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。
* [[!DNL Real-Time Customer Profile]](home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系統和裝置橋接客戶身分資料。 [!DNL Identity Service] 使用 **身分名稱空間** 將身分值與其來源系統建立關聯，以提供身分值的前後關聯。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

Identity Service維護全域定義（標準）和使用者定義（自訂）的身分名稱空間存放區。 標準名稱空間適用於所有組織（例如「Email」和「ECID」），而您的組織也可以建立自訂名稱空間以滿足其特定需求。

如需中識別名稱空間的詳細資訊 [!DNL Experience Platform]，請參閱 [身分名稱空間總覽](../identity-service/namespaces.md).

## 提交請求 {#submit}

以下各節概述如何針對以下專案提出隱私權請求： [!DNL Identity Service] 使用 [!DNL Privacy Service] API或UI。 在閱讀這些章節之前，強烈建議您先檢閱 [PRIVACY SERVICEAPI](../privacy-service/api/getting-started.md) 或 [PRIVACY SERVICEUI](../privacy-service/ui/overview.md) 有關如何提交隱私權工作的完整步驟的檔案，包括如何正確格式化請求裝載中的使用者資料。

### 使用 API

在API中建立工作請求時，在中提供的任何ID `userIDs` 必須使用特定 `namespace` 和 `type`. 有效的 [身分名稱空間](#namespaces) 識別者 [!DNL Identity Service] 必須提供 `namespace` 值，而 `type` 必須是 `standard` 或 `unregistered` （分別針對標準與自訂名稱空間）。

此外， `include` 請求承載的陣列必須包含請求所針對的不同資料存放區的產品值。 向提出請求時 [!DNL Identity]，陣列必須包含值 `Identity`.

以下請求會根據GDPR為中的單一客戶資料建立新的隱私權工作。 [!DNL Identity] 商店。 在以下位置為客戶提供兩個身分值： `userIDs` 陣列；一個使用標準 `Email` 身分名稱空間，以及使用 `ECID` 名稱空間，也包含 [!DNL Identity] (`Identity`)中 `include` 陣列：

>[!TIP]
>
>使用API刪除自訂名稱空間時，您必須指定身分符號作為名稱空間，而不是顯示名稱。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### 使用UI

>[!TIP]
>
>使用UI刪除自訂名稱空間時，您必須指定身分符號作為名稱空間，而不是顯示名稱。 此外，您無法刪除非生產沙箱的UI中的自訂名稱空間。

在UI中建立工作請求時，請務必選取 **[!UICONTROL 身分]** 在 **[!UICONTROL 產品]** 以便處理儲存在中的資料作業 [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## 正在處理刪除請求

時間 [!DNL Experience Platform] 接收來自的刪除請求 [!DNL Privacy Service]， [!DNL Platform] 傳送確認至 [!DNL Privacy Service] 已收到請求，且受影響的資料已標示為刪除。 個人身分的刪除是根據提供的名稱空間和/或ID值。 此外，刪除也會針對與指定組織相關聯的所有沙箱進行。

根據您是否同時包含即時客戶個人檔案(`ProfileService`)和資料湖(`aepDataLake`)以產品身分作為Identity Service隱私權請求中的產品(`identity`)，則與身分相關的不同資料集會在不同的時間從系統中移除：

| 包含的產品 | 效果 |
| --- | --- |
| `identity` 僅限 | 當Platform傳送確認已收到刪除請求時，會立即刪除與提供的身分相關聯的身分圖表。 從該身分圖表建構的設定檔仍會保留，但不會更新為擷取新資料，因為身分關聯現在已移除。 與設定檔相關聯的資料也會保留在資料湖中。 |
| `identity` 和 `ProfileService` | 一旦Platform傳送確認已收到刪除請求，就會立即刪除身分圖表及其關聯的設定檔。 與設定檔相關聯的資料會保留在資料湖中。 |
| `identity` 和 `aepDataLake` | 當Platform傳送確認已收到刪除請求時，會立即刪除與提供的身分相關聯的身分圖表。 從該身分圖表建構的設定檔仍會保留，但不會更新為擷取新資料，因為身分關聯現在已移除。<br><br>當Data Lake產品回應收到請求且目前正在處理時，與設定檔相關聯的資料會軟刪除，因此任何人都無法存取 [!DNL Platform] 服務。 工作完成後，資料會從資料湖中完全移除。 |
| `identity`, `ProfileService`, 和 `aepDataLake` | 一旦Platform傳送確認已收到刪除請求，就會立即刪除身分圖表及其關聯的設定檔。<br><br>當Data Lake產品回應收到請求且目前正在處理時，與設定檔相關聯的資料會軟刪除，因此任何人都無法存取 [!DNL Platform] 服務。 工作完成後，資料會從資料湖中完全移除。 |

請參閱 [[!DNL Privacy Service] 檔案](../privacy-service/home.md#monitor) 以取得追蹤工作狀態的詳細資訊。

## 后续步骤

閱讀本檔案後，您將瞭解中處理隱私權請求相關的重要概念。 [!DNL Identity Service]. 有關處理其他人的隱私權請求的資訊 [!DNL Experience Cloud] 應用程式，請參閱以下檔案： [[!DNL Privacy Service] and [!DNL Experience Cloud] 應用計畫](../privacy-service/experience-cloud-apps.md).
