---
solution: Experience Platform
title: 使用Flow Service API編輯目的地連線
type: Tutorial
description: 瞭解如何使用流量服務API編輯目的地連線的各種元件。
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---

# 使用Flow Service API編輯目的地連線

本教學課程涵蓋編輯目的地連線各種元件的步驟。 瞭解如何使用，更新驗證認證、匯出位置等 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 本教學課程中說明的編輯操作目前僅透過「流量服務API」支援。

## 快速入门 {#get-started}

本教學課程需要您具備有效的資料流ID。 如果您沒有有效的資料流ID，請從「 」中選擇您選擇的目的地 [目的地目錄](../catalog/overview.md) 並依照下列步驟進行 [連線到目的地](../ui/connect-destination.md) 和 [啟用資料](../ui/activation-overview.md) 在嘗試本教學課程之前。

>[!NOTE]
>
> 條款 *流量* 和 *資料流* 在本教學課程中可互換使用。 在本教學課程的內容中，兩者皆有相同涵義。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [目的地](../home.md)： [!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。
* [沙箱](../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，以使用 [!DNL Flow Service] API。

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

### 收集必要標題的值 {#gather-values-for-required-headers}

若要對Platform API發出呼叫，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有資源，包括屬於下列專案的資源： [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 對Platform API的所有請求都需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 標頭未指定，請求解析於 `prod` 沙箱。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 查詢資料流詳細資料 {#look-up-dataflow-details}

編輯目的地連線的第一個步驟，是使用流量ID擷取資料流詳細資訊。 您可以透過向以下網站發出GET要求，檢視現有資料流的目前詳細資料： `/flows` 端點。

>[!TIP]
>
>您可以使用Experience PlatformUI來取得目的地所需的資料流ID。 前往 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**，選取所需的目的地資料流，然後在右側邊欄中尋找目的地ID。 目的地ID是您將在下一個步驟中作為流量ID使用的值。
>
> ![使用Experience PlatformUI取得目的地ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 您要擷取之目的地資料流的值。 |

**请求**

以下請求會擷取有關您的流量ID的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回資料流的目前詳細資料，包括其版本、唯一識別碼(`id`)，以及其他相關資訊。 與本教學課程最相關的是目標連線與基本連線ID，其於以下回應中醒目提示。 您將在下一節中使用這些ID來更新目的地連線的各種元件。

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## 編輯目標連線元件（儲存位置和其他元件） {#patch-target-connection}

目標連線的元件會依目的地而有所不同。 例如， [!DNL Amazon S3] 目的地，您可以更新檔案匯出的貯體和路徑。 對象 [!DNL Pinterest] 目的地，您可以更新 [!DNL Pinterest Advertiser ID] 和for [!DNL Google Customer Match] 您可以更新 [!DNL Pinterest Account ID].

PATCH若要更新目標連線的元件，請對 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，並提供您的目標連線ID、版本以及您要使用的新值。 請記住，您在上一步中檢查了到所需目的地的現有資料流時，已取得目標連線ID。

>[!IMPORTANT]
>
>此 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是要更新的目標連線的唯一版本。 每次成功更新資料流、目標連線等流程實體時，etag值都會隨之更新。
>
> GET若要取得etag值的最新版本，請對 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，其中 `{TARGET_CONNECTION_ID}` 是要更新的目標連線ID。

以下是一些更新不同目的地型別之目標連線規格中的引數的範例。 但更新任何目的地引數的一般規則如下：

取得連線的資料流ID >取得目標連線ID >使用所需引數的更新值PATCH目標連線。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下請求會更新 `bucketName` 和 `path` 引數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目的地連線。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的目標連線ID和更新的Etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google廣告管理員與Google廣告管理員360]

**请求**

以下請求會更新 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 或 [[!DNL Google Ad Manager 360] 目的地](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 連線以新增新的 [**[!UICONTROL 將區段ID附加至區段名稱]**](/help/release-notes/2023/april-2023.md#destinations) 欄位。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的目標連線ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**请求**

以下請求會更新 `advertiserId` 引數 [[!DNL Pinterest] 目的地連線](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的目標連線ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 編輯基本連線元件（驗證引數和其他元件） {#patch-base-connection}

基礎連線的元件會依目的地而有所不同。 例如， [!DNL Amazon S3] 目的地，您可以將存取金鑰和秘密金鑰更新為 [!DNL Amazon S3] 位置。

PATCH若要更新基本連線的元件，請對 `/connections` 端點，並提供您的基本連線ID、版本以及您想要使用的新值。

請記住，您在上一步中檢查了到您所要目的地的現有資料流時，已經取得基本連線ID。

>[!IMPORTANT]
>
>此 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是您要更新的基礎連線的唯一版本。 每次成功更新資料流、基本連線等流程實體時，etag值都會隨之更新。
>
> GET若要取得最新版Etag值，請對 `/connections/{BASE_CONNECTION_ID}` 端點，其中 `{BASE_CONNECTION_ID}` 是您要更新的基本連線ID。

以下是一些更新不同型別目的地之基本連線規格中引數的範例。 但更新任何目的地引數的一般規則如下：

取得連線的資料流ID >取得基本連線ID >使用所需引數的更新值PATCH基本連線。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下請求會更新 `accessId` 和 `secretKey` 引數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目的地連線。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的基本連線ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**请求**

以下請求會更新 [[!DNL Azure Blob] 目的地](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 連線以更新連線至Azure Blob執行個體所需的連線字串。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的基本連線ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) （位於Platform疑難排解指南中），以取得有關解釋錯誤回應的詳細資訊。

## 后续步骤 {#next-steps}

依照本教學課程，您已瞭解如何使用 [!DNL Flow Service] API。 如需目的地的詳細資訊，請參閱 [目的地概觀](../home.md).
