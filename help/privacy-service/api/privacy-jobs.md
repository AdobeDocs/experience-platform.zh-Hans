---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 隱私權工作API端點
description: 瞭解如何使用Privacy Service API管理Experience Cloud應用程式的隱私權工作。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 1%

---

# 隱私權工作端點

本文介紹如何使用API呼叫處理隱私權工作。 具體來說，它涵蓋了 `/job` 中的端點 [!DNL Privacy Service] API。 閱讀本指南前，請參閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

>[!NOTE]
>
>如果您嘗試管理客戶的同意或選擇退出請求，請參閱 [同意端點指南](./consent.md).

## 列出所有工作 {#list}

您可以透過向以下網站發出GET請求，檢視組織內所有可用隱私權工作的清單： `/jobs` 端點。

**API格式**

此請求格式使用 `regulation` 上的查詢引數 `/jobs` 端點，因此開頭為問號(`?`)，如下所示。 回應會分頁，讓您能夠使用其他查詢引數(`page` 和 `size`)以篩選回應。 您可以使用&amp;符號(`&`)。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 参数 | 描述 |
| --- | --- |
| `{REGULATION}` | 要查詢的規則型別。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱以下文章的概觀： [支援的法規](../regulations/overview.md) 以取得上述值所代表之隱私權法規的詳細資訊。 |
| `{PAGE}` | 要顯示的資料頁（使用0編號）。 默认值为 `0`。 |
| `{SIZE}` | 要在每個頁面上顯示的結果數量。 預設值為 `1` 最大值為 `100`. 超過上限會導致API傳回400程式碼錯誤。 |

{style="table-layout:auto"}

**请求**

下列請求會從頁面大小為50的第三個頁面開始，擷取組織內所有工作的分頁清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的回應會傳回工作清單，而每個工作都包含詳細資訊，例如 `jobId`. 在此範例中，回應會包含50個作業的清單，從結果的第三個頁面開始。

### 存取後續頁面

若要在分頁回應中擷取下一組結果，您必須對相同端點進行另一個API呼叫，同時增加 `page` 查詢引數，按1。

## 建立隱私權工作 {#create-job}

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利請求。 不支援或不允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行負載測試，因為這是僅限生產的環境，且會建立有效隱私權請求的不必要待處理專案。
>
>現已設定每日硬性上傳限制，以防止服務被濫用。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與其舉行會議，討論其行動並討論可接受的Privacy Service用途。

在建立新的工作請求之前，您必須先收集有關您要存取、刪除或選擇退出銷售的資料主體的識別資訊。 擁有所需資料後，您必須在向發出的POST請求的有效負載中提供該資料 `/jobs` 端點。

>[!NOTE]
>
>相容的Adobe Experience Cloud應用程式使用不同的值來識別資料主體。 請參閱指南： [Privacy Service和Experience Cloud應用程式](../experience-cloud-apps.md) 以取得應用程式所需識別碼的詳細資訊。 如需判斷要傳送至哪些ID的一般指引 [!DNL Privacy Service]，請參閱本檔案： [隱私權請求中的身分資料](../identity-data.md).

此 [!DNL Privacy Service] API支援兩種針對個人資料的工作請求：

* [存取和/或刪除](#access-delete)：存取（讀取）或刪除個人資料
* [選擇退出銷售](#opt-out)：將個人資料標籤為不出售。

>[!IMPORTANT]
>
>雖然存取和刪除請求可以合併為單一API呼叫，但選擇退出請求必須單獨提出。

### 建立存取/刪除工作 {#access-delete}

本節示範如何使用API提出存取/刪除工作請求。

**API格式**

```http
POST /jobs
```

**请求**

以下請求會建立新的作業請求，由承載中提供的屬性進行設定，如下所述。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 属性 | 描述 |
| --- | --- |
| `companyContexts` **（必要）** | 包含貴組織驗證資訊的陣列。 每個列出的識別碼都包含以下屬性： <ul><li>`namespace`：識別碼的名稱空間。</li><li>`value`：識別碼的值。</li></ul>它是 **必填** 其中一個識別碼使用 `imsOrgId` 作為其 `namespace`，及其他 `value` 包含貴組織的唯一ID。 <br/><br/>其他識別碼可以是產品特定的公司限定詞(例如， `Campaign`)，可識別與您組織所屬之Adobe應用程式的整合。 可能的值包括帳戶名稱、使用者端代碼、租使用者ID或其他應用程式識別碼。 |
| `users` **（必要）** | 一個陣列，包含您要存取或刪除其資訊之至少一個使用者的集合。 單一請求中最多可提供1000個使用者ID。 每個使用者物件包含下列資訊： <ul><li>`key`：使用者的識別碼，用於限定回應資料中的個別作業ID。 最佳實務是為這個值選擇唯一且易於識別的字串，以便日後可以輕鬆參考或查閱。</li><li>`action`：列出對使用者資料所需採取的動作的陣列。 根據您要採取的動作，此陣列必須包括 `access`， `delete`，或兩者。</li><li>`userIDs`：使用者的身分識別集合。 單一使用者可擁有的身分數量限製為九個。 每個身分都包含 `namespace`， a `value`，和名稱空間限定詞(`type`)。 請參閱 [附錄](appendix.md) 以取得這些必要屬性的詳細資訊。</li></ul> 如需更詳細的說明，請參閱： `users` 和 `userIDs`，請參閱 [疑難排解指南](../troubleshooting-guide.md#user-ids). |
| `include` **（必要）** | 要包含在處理中的一系列Adobe產品。 如果此值遺失或空白，將會拒絕要求。 僅包含貴組織與其整合的產品。 請參閱以下小節： [接受的產品值](appendix.md) 詳細資訊。 |
| `expandIDs` | 選擇性屬性，設定為時 `true`，代表應用程式中ID處理的最佳化(目前僅支援 [!DNL Analytics])。 如果省略，此值會預設為 `false`. |
| `priority` | Adobe Analytics使用的選用屬性，可設定處理請求的優先順序。 接受的值為 `normal` 和 `low`. 若 `priority` 省略，預設行為為 `normal`. |
| `analyticsDeleteMethod` | 選擇性屬性，指定Adobe Analytics應如何處理個人資料。 這個屬性接受兩個可能的值： <ul><li>`anonymize`：特定使用者ID集合所參考的所有資料都會設為匿名。 若 `analyticsDeleteMethod` 省略，此為預設行為。</li><li>`purge`：所有資料都會完全移除。</li></ul> |
| `mergePolicyId` | 向Real-Time Customer Profile提出隱私權請求時(`profileService`)，您可以選擇性地提供特定 [合併原則](../../profile/merge-policies/overview.md) ，以便用於ID拼接。 透過指定合併原則，隱私權請求可在傳回客戶資料時包含區段資訊。 每個請求只能指定一個合併原則。 如果未提供合併原則，則回應中不會包含分段資訊。 |
| `regulation` **（必要）** | 隱私權工作的法規。 接受下列值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>請參閱以下文章的概觀： [支援的法規](../regulations/overview.md) 以取得上述值所代表之隱私權法規的詳細資訊。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回新建立工作的詳細資訊。

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| 属性 | 描述 |
| --- | --- |
| `jobId` | 作業唯讀、系統產生的唯一ID。 此值用於查詢特定工作的下一個步驟。 |

{style="table-layout:auto"}

成功提交工作請求後，您可以繼續的下一個步驟 [檢查工作狀態](#check-status).

## 檢查工作的狀態 {#check-status}

您可以擷取特定工作的相關資訊，例如其目前的處理狀態，方法是加入該工作的 `jobId` 在GET請求的路徑中 `/jobs` 端點。

>[!IMPORTANT]
>
>先前建立之工作的資料只能在工作完成日期後30天內擷取。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{JOB_ID}` | 您要查閱之工作的ID。 此ID會傳回至 `jobId` 在成功的API回應中 [建立工作](#create-job) 和 [列出所有工作](#list). |

{style="table-layout:auto"}

**请求**

以下請求會擷取下列工作之詳細資訊： `jobId` 請求路徑中會提供。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的回應會傳回指定工作的詳細資訊。

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| 属性 | 描述 |
| --- | --- |
| `productStatusResponse` | 內的每個物件 `productResponses` 陣列包含有關特定工作目前狀態的資訊 [!DNL Experience Cloud] 應用程式。 |
| `productStatusResponse.status` | 工作的目前狀態類別。 請參閱下表，瞭解以下清單 [可用狀態類別](#status-categories) 以及它們對應的意義。 |
| `productStatusResponse.message` | 工作的特定狀態，對應於狀態類別。 |
| `productStatusResponse.responseMsgCode` | 收到的產品回應訊息的標準代碼 [!DNL Privacy Service]. 此訊息的詳細資訊提供於 `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 有關工作狀態的更詳細說明。 類似狀態的訊息可能因產品而異。 |
| `productStatusResponse.results` | 對於特定狀態，某些產品可能會傳回 `results` 提供未涵蓋之其他資訊的物件 `responseMsgDetail`. |
| `downloadURL` | 如果工作的狀態為 `complete`，此屬性會提供一個URL來將工作結果下載為ZIP檔案。 工作完成後60天內可下載此檔案。 |

{style="table-layout:auto"}

### 工作狀態類別 {#status-categories}

下表列出不同的可能工作狀態類別及其對應含義：

| 狀態類別 | 含义 |
| -------------- | -------- |
| `complete` | 工作已完成，且會從每個應用程式上傳檔案（如有需要）。 |
| `processing` | 應用程式已確認工作且目前正在處理中。 |
| `submitted` | 工作已提交給每個適用的應用程式。 |
| `error` | 處理作業時某些失敗 — 擷取個別作業詳細資料可能會獲得更具體的資訊。 |

{style="table-layout:auto"}

>[!NOTE]
>
>提交的工作可能保留在 `processing` 指出是否有仍在處理的相依子作業。

## 后续步骤

您現在知道如何使用 [!DNL Privacy Service] API。 如需有關如何使用使用者介面執行相同工作的資訊，請參閱 [Privacy ServiceUI總覽](../ui/overview.md).
