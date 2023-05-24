---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 邊緣投影API端點
type: Documentation
description: Adobe Experience Platform可讓您透過隨時提供正確的資料，並隨著變更持續更新，即時跨多個管道為您的客戶推動協調、一致和個人化的體驗。 這是透過使用Edges來完成的，這是一種地理上放置的伺服器，可儲存資料並讓應用程式能夠輕鬆存取。
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# 邊緣投影設定和目的地端點

為了即時跨多個管道為您的客戶推動協調、一致和個人化的體驗，需要隨時提供正確的資料，並隨著變更持續更新。 Adobe Experience Platform透過使用所謂的edge功能，實現資料的即時存取。 Edge是地理位置上放置的伺服器，可儲存資料並讓應用程式輕鬆存取資料。 例如，Adobe Target和Adobe Campaign等Adobe應用程式會使用Edge來即時提供個人化客戶體驗。 資料會透過投影路由至邊緣，投影目的地定義資料將傳送至的邊緣，投影組態定義可在邊緣上使用的特定資訊。 本指南提供詳細的使用說明 [!DNL Real-Time Customer Profile] 適用於邊緣預測的API，包括目的地和設定。

## 快速入门

本指南中使用的API端點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

>[!NOTE]
>
>包含裝載(POST、PUT、PATCH)的要求需要 `Content-Type` 標頭。 超過一個 `Content-Type` 用於本檔案。 請特別留意呼叫範例中的標題，以確保您使用正確的標頭 `Content-Type` 每個請求的。

## 投影目的地

您可以指定資料傳送的位置，將投影繞線至一或多個邊。 所建立的每個投影目的地都有一個唯一的ID，然後會用來建立投影組態。

### 列出所有目的地

您可以透過向以下網站發出GET請求，列出已為貴組織建立的邊緣目的地： `/config/destinations` 端點。

**API格式**

```http
GET /config/destinations
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應包括 `projectionDestinations` 陣列，每個目的地的詳細資料顯示為陣列中的個別物件。 如果尚未設定任何投影，則 `projectionDestinations` 陣列傳回空白。

>[!NOTE]
>
>此回應已縮短，空間不足，只顯示兩個目的地。

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| 属性 | 描述 |
|---|---|
| `_links.self.href` | 在最上層，會比對用於發出GET請求的路徑。 在每個個別目的地物件中，此路徑可用於GET要求中，以直接查詢特定目的地的詳細資訊。 |
| `id` | 在每個目的地物件內， `"id"` 顯示唯讀、系統產生的目的地唯一ID。 此ID用於參考特定目的地以及建立投影設定時。 |

如需個別目的地屬性的詳細資訊，請參閱以下章節： [建立目的地](#create-a-destination) 後續步驟。

### 建立目的地 {#create-a-destination}

如果您需要的目的地尚不存在，您可以透過向以下專案發出POST要求，以建立新的投影目的地： `/config/destinations` 端點。

**API格式**

```http
POST /config/destinations
```

**请求**

以下請求會建立新的邊緣目的地。

>[!NOTE]
>
>建立目的地的POST請求需要特定 `Content-Type` 標題，如下所示。 使用不正確的 `Content-Type` 標題會導致HTTP狀態415 （不支援的媒體型別）錯誤。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| 属性 | 描述 |
|---|---|
| `type` **（必要）** | 要建立的目的地型別。 唯一接受的值「EDGE」會建立邊緣目的地。 |
| `dataCenters` **（必要）** | 字串陣列，列出要繞線投影的邊緣。 可能包含下列一或多個值：「OR1」 — 美國西部、「VA5」 — 美國東部、「NLD1」 — 歐洲、中東與非洲地區。 |
| `ttl` **（必要）** | 指定投影到期日。 接受的值範圍： 600到604800。 預設值： 3600。 |
| `replicationPolicy` **（必要）** | 定義從中樞到邊緣的資料復寫行為。  支援的值：主動、反應。 預設值： REACTIVE。 |

**响应**

成功回應會傳回新建立邊緣目的地的詳細資訊，包括唯讀、系統產生的唯一ID (`id`)。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| 属性 | 描述 |
|---|---|
| `self.href` | 此路徑用於直接查詢(GET)目的地，也可用於更新(PUT)或刪除(DELETE)目的地。 |
| `id` | 目的地唯讀、系統產生的唯一ID。 此ID用於直接參照目的地以及在建立投影組態時。 |
| `version` | 此唯讀值會顯示目的地的目前版本。 更新目的地時，版本編號會自動增加。 |

### 檢視目的地

如果您知道投影目的地的唯一ID，則可以執行查詢請求來檢視其詳細資訊。 這可透過向以下網站發出GET請求來完成： `/config/destinations` 端點並在要求路徑中包含目的地ID。

**API格式**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 您要檢視之投影目的地的唯一ID。 |

**请求**

以下請求會執行查詢(GET)，以檢視請求路徑中提供ID的目的地。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應物件會顯示投影目的地的詳細資訊。 此 `id` 屬性應符合請求中提供的投影目的地ID。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### 更新目的地

您可以透過向以下專案發出PUT請求來更新現有目的地： `/config/destinations` 端點，並包含要在請求路徑中更新的目的地ID。 此操作基本上是重寫目的地，因此，請求內文中提供的屬性必須與建立新目的地時提供的屬性相同。

>[!CAUTION]
>
>對更新請求的API回應是立即的，但投影的變更會以非同步方式套用。 換句話說，更新目的地的定義與套用定義之間會存在時間差異。

**API格式**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 您要更新的投影目的地的唯一ID。 |

**请求**

以下請求會更新現有目的地，以包含第二個位置(`dataCenters`)。

>[!IMPORTANT]
>
>PUT請求需要特定 `Content-Type` 標題，如下所示。 使用不正確的 `Content-Type` 標題會導致HTTP狀態415 （不支援的媒體型別）錯誤。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| 属性 | 描述 |
|---|---|
| `currentVersion` | 現有目的地的目前版本。 的值 `version` 執行目的地的查詢請求時的屬性。 |

**响应**

回應包含目標的更新詳細資料，包括其ID和新的 `version` 目的地的。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### 刪除目的地

如果您的組織不再需要投影目的地，您可以透過向以下連結發出DELETE要求來刪除它： `/config/destinations` 端點，並在請求路徑中包含您要刪除之目的地的ID。

>[!CAUTION]
>
>刪除請求的API會立即回應，但邊緣資料的實際變更為非同步進行。 換言之，輪廓資料將會從所有邊緣( `dataCenters` 在投影目的地中指定)，但程式需要時間才能完成。

**API格式**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 参数 | 描述 |
|---|---|
| `{DESTINATION_ID}` | 您要刪除之投影目的地的唯一ID。 |


**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

刪除要求會傳回HTTP狀態204 （無內容）和空白的回應內文。 您可以依目的地ID來執行目的地的查詢請求，以確認刪除成功。 查詢應傳回HTTP狀態404 （找不到）。

## 投影組態

投影設定提供有關每個邊緣上應可使用哪些資料的資訊。 而不是投影完整 [!DNL Experience Data Model] (XDM)結構描述到邊緣時，投影僅提供結構描述中的特定資料或欄位。 您的組織可以為每個XDM結構描述定義多個投影設定。

### 列出所有投影組態

您可以透過向以下網站發出GET請求，列出已為貴組織建立的所有投影配置： `/config/projections` 端點。 您也可以將選用引數新增至請求路徑，以存取特定結構的投影設定，或依名稱查詢個別的投影。

**API格式**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 参数 | 描述 |
|---|---|
| `{SCHEMA_NAME}` | 與您要存取的投影組態相關聯的結構描述類別名稱。 |
| `{PROJECTION_NAME}` | 您要存取的投影組態名稱。 |

>[!NOTE]
>
>`schemaName` 使用時需要使用 `name` 引數，因為投影組態名稱只有在結構描述類別的內容中是唯一的。

**请求**

以下請求列出所有與相關的投影組態 [!DNL Experience Data Model] 結構描述類別， [!DNL XDM Individual Profile]. 如需有關XDM及其在以下專案中所扮演角色的詳細資訊： [!DNL Platform]，請先閱讀 [XDM系統總覽](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回根目錄中的投影設定清單 `_embedded` 屬性，包含在 `projectionConfigs` 陣列。 如果您的組織尚未建立投影組態，則 `projectionConfigs` 陣列將是空的。

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### 建立投影組態

您可以建立(POST)新的投影組態，指定在邊緣上可以使用哪些XDM欄位。

**API格式**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 参数 | 描述 |
|---|---|
| `{SCHEMA_NAME}` | 與您要存取的投影組態相關聯的結構描述類別名稱。 |

**请求**

>[!NOTE]
>
>建立設定的POST請求需要特定 `Content-Type` 標題，如下所示。 使用不正確的 `Content-Type` 標題會導致HTTP狀態415 （不支援的媒體型別）錯誤。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| 属性 | 描述 |
|---|---|
| `selector` | 字串，其中包含要復寫至邊緣之綱要內的屬性清單。 有關使用選取器的最佳實務，請參閱 [選取器](#selectors) 區段。 |
| `name` | 新投影組態的描述性名稱。 |
| `destinationId` | 資料將投影到的邊緣目的地的識別碼。 |

**响应**

成功的回應會傳回新建立的投影組態的詳細資訊。

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## 選取器 {#selectors}

選擇器是以逗號分隔的XDM欄位名稱清單。 在投影組態中，選取器會指定要包含在投影中的屬性。 的格式 `selector` 引數值大體上以XPath語法為基礎。 支援的語法概述如下，並提供其他範例以供參考。

### 支援的語法

* 使用逗號選取多個欄位。 请勿使用空格。
* 使用點標籤法來選取巢狀欄位。
   * 例如，若要選取名為的欄位 `field` 巢狀內嵌於名為的欄位中 `foo`，使用選取器 `foo.field`.
* 當包含包含子欄位的欄位時，所有子欄位預設也會投影。 不過，您可以使用括弧來篩選傳回的子欄位 `"( )"`.
   * 例如， `addresses(type,city.country)` 針對每項，僅傳回地址型別和地址城市所在的國家/地區 `addresses` 陣列元素。
   * 上述範例等同於 `addresses.type,addresses.city.country`.

>[!NOTE]
>
>參考子欄位時，同時支援點標籤法和括弧標籤法。 不過，使用點標籤法是最佳做法，因為點標籤法更簡潔，且能更有效說明欄位階層。

* 選取器中的每個欄位都是相對於回應的根目錄指定的。
   * 如果資料是資源的集合，則投影將包含資源陣列。
   * 如果資料是單一資源，則投影將包含與該資源相關的欄位。
   * 如果您選取的欄位是（或是）陣列的一部分，則投影將包括陣列中所有元素的選定部分。

### 選取器引數的範例

下列範例顯示範例 `selector` 引數，後面接著引數所代表的結構化值。

**person.lastName**

傳回 `lastName` 的子欄位 `person` 物件。

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**地址**

傳回 `addresses` 陣列，包含每個元素中的所有欄位，但不包含其他欄位。

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName，地址**

傳回 `person.lastName` 欄位和中的所有元素 `addresses` 陣列。

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**addresses.city**

只傳回地址陣列中所有元素的city欄位。

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>每當傳回巢狀欄位時，投影都會包含封閉的父物件。 父欄位不包含任何其他子欄位，除非也明確選取它們。

**地址（型別，城市）**

只傳回 `type` 和 `city` 中每個元素的欄位 `addresses` 陣列。 每個子欄位中包含的所有其他子欄位 `addresses` 元素會被篩選掉。

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## 后续步骤

本指南向您說明設定預測和目的地所涉及的步驟，包括如何正確格式化 `selector` 引數。 您現在可以建立專屬於貴組織需求的新投影目的地和設定。
