---
keywords: Experience Platform；首頁；熱門主題；資料準備；資料準備；串流；更新插入；串流更新插入
title: 使用「資料準備」將部分資料列更新傳送至設定檔服務
description: 本檔案提供如何使用「資料準備」將部分列更新傳送至「設定檔服務」的資訊。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---

# 傳送部分列更新至 [!DNL Profile Service] 使用 [!DNL Data Prep]

串流更新插入 [!DNL Data Prep] 可讓您將部分列更新傳送至 [!DNL Profile Service] 同時使用單一API請求建立和建立新的身分連結。

透過串流更新插入，您可以保留資料格式，同時將該資料轉譯為 [!DNL Profile Service] 在內嵌期間PATCH請求。 根據您提供的輸入， [!DNL Data Prep] 可讓您傳送單一API裝載，並將資料轉譯為兩者 [!DNL Profile Service] PATCH和 [!DNL Identity Service] 建立請求。

本檔案提供如何在中串流更新插入的資訊 [!DNL Data Prep].

## 快速入门

此概觀需要深入瞭解下列Adobe Experience Platform元件：

* [[!DNL Data Prep]](./home.md)： [!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
* [即時客戶個人檔案](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [來源](../sources/home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。

## 在中使用串流更新插入 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>下列來源支援使用串流更新插入：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 串流更新插入高階工作流程

串流更新插入 [!DNL Data Prep] 其運作方式如下：

* 您必須先建立和啟用資料集 [!DNL Profile] 消耗。 請參閱指南： [啟用資料集 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 以取得詳細資訊；
* 如果新身分必須連結，則您也必須建立其他資料集 **使用相同結構描述** 作為您的 [!DNL Profile] 資料集；
* 準備好資料集後，您必須建立資料流，將傳入的請求對應至 [!DNL Profile] 資料集；
* 接下來，您必須更新傳入請求以包含必要的標頭。 這些標頭會定義：
   * 需要執行的資料操作 [!DNL Profile]： `create`， `merge`、和 `delete`；
   * 要透過執行的選擇性身分操作 [!DNL Identity Service]： `create`.

### 設定身分資料集

如果新身分必須連結，則您必須在傳入裝載中建立並傳遞其他資料集。 建立身分資料集時，您必須確保符合下列要求：

* 身分資料集必須有關聯的結構描述為 [!DNL Profile] 資料集。 結構描述的不匹配可能導致不一致的系統行為；
* 不過，您必須確保身分資料集與 [!DNL Profile] 資料集。 如果資料集相同，則會覆寫資料而非更新；
* 雖然初始資料集必須啟用 [!DNL Profile]，身分資料集 **不應該** 已啟用： [!DNL Profile]. 否則，也會覆寫資料，而非更新。

#### 與身分資料集相關聯的結構描述中的必填欄位 {#identity-dataset-required-fileds}

如果您的結構描述包含必填欄位，則必須隱藏資料集的驗證才能啟用 [!DNL Identity Service] 以僅接收身分。 您可以套用 `disabled` 值至 `acp_validationContext` 引數。 請參閱下列範例：

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>如果與身分資料集關聯的結構描述沒有任何必填欄位，則不需要進行任何其他設定。

## 傳入的裝載結構

以下顯示建立新身分連結之傳入裝載結構的範例。

### 具有身分設定的裝載

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| 参数 | 描述 |
| --- | --- |
| `flowId` | 用於識別資料流的唯一ID。 此資料流ID應該對應至使用建立的來源連線 [!DNL Amazon Kinesis]， [!DNL Azure Event Hubs]，或 [!DNL HTTP API]. 此資料流也應具有 [!DNL Profile] — 啟用的資料集作為目標資料集。 **注意**：的ID [!DNL Profile]-enabled目標資料集也會用作 `datasetId` 引數。 |
| `imsOrgId` | 與您的組織相對應的ID。 |
| `datasetId` | 的ID [!DNL Profile] — 啟用資料流的目標資料集。 **注意**：此ID與 [!DNL Profile] — 已在資料流中找到啟用的目標資料集ID。 |
| `operations` | 此引數概述以下動作： [!DNL Data Prep] 將根據傳入的請求來進行。 |
| `operations.data` | 定義必須在中執行的動作 [!DNL Profile Service]. |
| `operations.identity` | 透過以下方式定義資料上允許的操作 [!DNL Identity Service]. |
| `operations.identityDatasetId` | （選用）只有在必須連結新身分時才需要身分資料集的ID。 |

#### 支援的作業

下列作業受到支援 [!DNL Profile Service]：

| 操作 | 描述 |
| --- | --- | 
| `create` | 預設操作。 這會為產生XDM實體建立方法 [!DNL Profile Service]. |
| `merge` | 這會為以下專案產生XDM實體更新方法： [!DNL Profile Service]. |
| `delete` | 這會為以下專案產生XDM實體刪除方法： [!DNL Profile Service] 並從下列位置永久移除資料： [!DNL Profile Store]. |

下列作業受到支援 [!DNL Identity Service]：

| 操作 | 描述 |
| --- | --- |
| `create` | 此引數唯一允許的作業。 若 `create` 傳遞為的值 `operations.identity`，則 [!DNL Data Prep] 產生XDM實體建立請求 [!DNL Identity Service]. 如果身分已存在，則會忽略身分。 **注意：** 若 `operations.identity` 設為 `create`，然後 `identityDatasetId` 也必須指定。 XDM實體建立訊息是由內部產生 [!DNL Data Prep] 將為此資料集id產生元件。 |

### 沒有身分設定的裝載

如果不需要連結新身分，您可以省略 `identity` 和 `identityDatasetId` 操作中的引數。 如此一來，資料只會傳送至 [!DNL Profile Service] 並略過 [!DNL Identity Service]. 如需範例，請參閱以下裝載：

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## 動態傳遞主要身分

若要進行XDM更新，結構描述必須啟用 [!DNL Profile] 和包含主要身分。 您可以透過兩種方式指定XDM結構描述的主要身分：

* 在XDM結構描述中指定靜態欄位作為主要身分；
* 透過XDM結構描述中的身分對應欄位群組，將其中一個身分欄位指定為主要身分。

### 指定靜態欄位做為XDM結構描述中的主要身分欄位

在以下範例中， `state`， `homePhone.number` 和其他屬性會以其各自的指定值更新插入 [!DNL Profile] 具有主要身分識別 `sampleEmail@gmail.com`. 然後，串流會產生XDM實體更新訊息 [!DNL Data Prep] 元件。 [!DNL Profile Service] 然後確認XDM更新訊息以更新插入設定檔記錄。

>[!NOTE]
>
>在此範例中，身分將不會連結在一起，因為沒有定義身分的操作。

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### 透過XDM結構描述中的身分對應欄位群組，將其中一個身分欄位指定為主要身分

在此範例中，標題包含 `operations` 屬性和 `identity` 和 `identityDatasetId` 屬性。 如此可讓資料與 [!DNL Profile Service] 以及要傳遞至的身分 [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## 已知限制和主要考量事項

以下概述使用串流更新插入時應考量的已知限制清單 [!DNL Data Prep]：

* 只有在傳送部分列更新至時，才應使用串流更新插入方法 [!DNL Profile Service]. 部分列更新為 **not** 由資料湖使用。
* 串流更新插入方法不支援更新、取代和移除身分。 如果新的身分不存在，則會建立這些身分。 因此， `identity` 操作必須一律設定為建立。 如果身分已經存在，則作業為無操作。
* 串流更新插入方法目前不支援 [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) 和 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## 后续步骤

閱讀本檔案後，您現在應該瞭解如何在中串流更新插入 [!DNL Data Prep] 將部分資料列更新傳送至 [!DNL Profile Service] 資料，同時使用單一API請求建立和連結身分識別。 如需其他專案的詳細資訊 [!DNL Data Prep] 功能，請閱讀 [[!DNL Data Prep] 概觀](./home.md). 若要瞭解如何在 [!DNL Data Prep] API，請閱讀 [[!DNL Data Prep] 開發人員指南](./api/overview.md).
