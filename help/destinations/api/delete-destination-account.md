---
keywords: Experience Platform；首頁；熱門主題；流程服務；刪除目的地帳戶；刪除；API
solution: Experience Platform
title: 使用流程服務API刪除目的地帳戶
type: Tutorial
description: 瞭解如何使用流量服務API刪除目的地帳戶。
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 使用流程服務API刪除目的地帳戶

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

在啟用資料之前，您必須先設定目的地帳戶，以連線至目的地。 本教學課程涵蓋刪除不再需要的目的地帳戶的步驟，這些帳戶是使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>目前僅流程服務API支援刪除目的地帳戶。 無法使用Experience PlatformUI刪除目的地帳戶。

## 快速入门 {#get-started}

本教學課程要求您具備有效的連線ID。 連線ID代表與目的地的帳戶連線。 如果您沒有有效的連線ID，請從 [目的地目錄](../catalog/overview.md) 並依照下列步驟進行 [連線到目的地](../ui/connect-destination.md) 在嘗試本教學課程之前。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [目的地](../home.md)： [!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，才能使用成功刪除目的地帳戶 [!DNL Flow Service] API。

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

## 尋找要刪除的目的地帳戶的連線ID {#find-connection-id}

>[!NOTE]
>本教學課程使用 [飛艇目的地](../catalog/mobile-engagement/airship-attributes.md) 例如，但概述的步驟適用於下列任何步驟： [可用的目的地](../catalog/overview.md).

刪除目的地帳戶的第一步，是找出與您要刪除的目的地帳戶對應的連線ID。

在Experience PlatformUI中，瀏覽至 **[!UICONTROL 目的地]** > **[!UICONTROL 帳戶]** ，並選取您要刪除的帳戶，方法是在 **[!UICONTROL 目的地]** 欄。

![選取要刪除的目的地帳戶](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

接著，您可以從瀏覽器的URL擷取目的地帳戶的連線ID。

![從URL擷取連線ID](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## 刪除連線 {#delete-connection}

>[!IMPORTANT]
>
>在刪除目的地帳戶之前，您必須先刪除目的地帳戶的任何現有資料流。
>若要刪除現有資料流，請參閱以下頁面：
>* [使用Experience PlatformUI](../ui/delete-destinations.md) 刪除現有資料流；
>* [使用流程服務API](delete-destination-dataflow.md) 以刪除現有的資料流。


擁有連線ID並確保目的地帳戶不存在任何資料流後，請對執行DELETE請求 [!DNL Flow Service] API。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 唯一 `id` 要刪除之連線的值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。 您可以嘗試向連線查詢(GET)要求以確認刪除。 API將傳回HTTP 404 （找不到）錯誤，這表示已刪除目的地帳戶。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

依照本教學課程，您已成功使用 [!DNL Flow Service] 用於刪除現有目的地帳戶的API。 如需使用目的地的詳細資訊，請參閱 [目的地概觀](/help/destinations/home.md).