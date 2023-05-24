---
keywords: Experience Platform；首頁；熱門主題；流程服務；API；API；刪除；刪除目的地資料流程
solution: Experience Platform
title: 使用流程服務API刪除目的地資料流
type: Tutorial
description: 瞭解如何使用資料流服務API刪除批次和串流目的地的資料流。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# 使用流程服務API刪除目的地資料流

您可以使用來刪除包含錯誤或已過時的資料流 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教學課程涵蓋使用將資料流刪除至批次和串流目的地的步驟。 [!DNL Flow Service].

## 快速入门 {#get-started}

本教學課程要求您具備有效的流量ID。 如果您沒有有效的流量ID，請從「 」中選擇您選擇的目的地 [目的地目錄](../catalog/overview.md) 並依照下列步驟進行 [連線到目的地](../ui/connect-destination.md) 和 [啟用資料](../ui/activation-overview.md) 在嘗試本教學課程之前。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [目的地](../home.md)： [!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，才能使用成功刪除資料流 [!DNL Flow Service] API。

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值 {#gather-values-for-required-headers}

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 標頭未指定，請求解析於 `prod` 沙箱。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 刪除目的地資料流 {#delete-destination-dataflow}

DELETE有了現有的資料流ID，您可以透過對 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 您要刪除之目的地資料流的值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態202 （無內容）和空白內文。 您可以嘗試對資料流進行查詢(GET)請求以確認刪除。 API將傳回HTTP 404 （找不到）錯誤，這表示資料流已刪除。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) （位於Platform疑難排解指南中），以取得有關解釋錯誤回應的詳細資訊。

## 后续步骤 {#next-steps}

依照本教學課程，您已成功使用 [!DNL Flow Service] 用於刪除現有資料流到目的地的API。

如需如何使用使用者介面執行這些操作的步驟，請參閱以下教學課程： [在UI中刪除資料流](../ui/delete-destinations.md).

您現在可以繼續並 [刪除目的地帳戶](/help/destinations/api/delete-destination-account.md) 使用 [!DNL Flow Service] API。
