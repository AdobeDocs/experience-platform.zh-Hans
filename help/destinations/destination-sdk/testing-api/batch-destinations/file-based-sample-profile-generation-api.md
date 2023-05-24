---
description: 此頁面說明如何使用Destination SDK中的/sample-profiles API端點，根據來源結構描述產生範例設定檔。 您可以使用這些範例設定檔來測試以檔案為基礎的目的地設定。
title: 根據來源結構描述產生範例設定檔
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---


# 根據來源結構描述產生範例設定檔

測試以檔案為基礎的目的地的第一個步驟是使用 `/sample-profiles` 端點，以根據您現有的來源結構描述產生範例設定檔。

範例設定檔可協助您瞭解設定檔的JSON結構。 此外，它們也會提供您預設值，讓您可使用自己的設定檔資料進行自訂，以便進行進一步的目的地測試。

## 快速入门 {#getting-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 先决条件 {#prerequisites}

開始使用 `/sample-profiles` 端點，確定您符合以下條件：

* 您有一個透過Destination SDK建立的檔案型目的地，且您可以在下列位置中看到 [目的地目錄](../../../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中為您目的地建立至少一個啟用流程。 此 `/sample-profiles` 端點會根據您在啟動流程中定義的來源結構描述建立設定檔。 請參閱 [啟動教學課程](../../../ui/activate-batch-profile-destinations.md) 以瞭解如何建立啟用流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應在API呼叫中使用的目的地執行個體ID。

   ![UI影像顯示如何從URL取得目的地執行個體ID。](../../assets/testing-api/get-destination-instance-id.png)

## 產生用於目的地測試的範例設定檔 {#generate-sample-profiles}

您可以透過向以下發出GET請求，根據您的來源結構描述產生範例設定檔： `/sample-profiles` 具有您要測試之目的地的目的地執行個體ID的端點。

**API格式**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 查詢引數 | 描述 |
| -------- | ----------- |
| `destinationInstanceId` | 您要產生範例設定檔的目標執行個體ID。 請參閱 [必備條件](#prerequisites) 區段，以瞭解有關如何取得此ID的詳細資訊。 |
| `count` | *可选*. 您要產生的範例設定檔數目。 引數可取的值介於 `1 - 1000`. 如果此屬性未定義，則API會產生單一範例設定檔。 |

**请求**

以下請求會根據目的地執行個體中定義的來源結構描述產生範例設定檔，並具有對應的 `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及與來源XDM結構描述相對應的區段會籍、身分和設定檔屬性。

>[!NOTE]
>
> 回應只會傳回目的地執行個體中使用的區段會籍、身分和設定檔屬性。 即使您的來源結構描述有其他欄位，這些欄位也會被忽略。

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![此影像顯示從UI到API回應欄位的對應。](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 属性 | 描述 |
| -------- | ----------- |
| `segmentMembership` | 描述個人區段會籍的地圖物件。 如需詳細資訊，請參閱 `segmentMembership`，讀取 [區段會籍細節](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | 此設定檔上次符合區段資格的時間戳記。 |
| `status` | 字串欄位，指出是否已將區段會籍實現為目前請求的一部分。 接受下列值： <ul><li>`realized`：設定檔是區段的一部分。</li><li>`exited`：設定檔正在退出區段，做為目前請求的一部分。</li></ul> |
| `identityMap` | 說明個人的各種身分值及其相關名稱空間的對應型別欄位。 如需詳細資訊，請參閱 `identityMap`，請參閱 [結構描述組合的基礎](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在知道如何根據您在目的地設定的來源結構描述產生範例設定檔 [啟用流程](../../../ui/activate-batch-profile-destinations.md).

您現在可以自訂這些設定檔，或在API傳回時加以使用，以 [測試以檔案為基礎的目的地設定](file-based-destination-testing-api.md).
