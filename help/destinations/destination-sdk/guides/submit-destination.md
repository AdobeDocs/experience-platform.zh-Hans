---
description: 此頁面提供您需要提交以複查使用Destination SDK製作的生產目的地的所有資訊。
title: 送出供檢閱以Destination SDK撰寫的生產目的地
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# 送出供檢閱以Destination SDK撰寫的生產目的地

## 概述 {#overview}

>[!IMPORTANT]
>
>* 此處記錄的程式僅適用於提交生產（公用）目的地的合作夥伴。 如果您要建立私人目的地供自己使用，則不需要製作這些材料並與Adobe分享。
>
>* Adobe審閱目的地發佈要求的標準回應時間為5個工作日。
>
>* 如果Adobe團隊要求您在初次提交後對設定進行任何更新，則您必須在進行更新後提交另一個目的地發佈請求。
>
>* 即使您的目的地在Experience Platform目錄中上線後，如果您需要對設定進行任何更新，則必須提交新的目的地發佈請求，才能將更新反映在設定中。


將目的地發佈至之前 [Experience Platform目的地目錄](/help/destinations/catalog/overview.md)，您必須向Adobe提供有關目的地和您執行之測試的某些資訊，以確保使用者在啟用您平台的資料時，享有最佳體驗。

此頁面列出提交或更新您使用Adobe Experience Platform Destination SDK編寫的目的地時，所需提供的所有資訊。 若要在Adobe Experience Platform中成功提交目的地，請傳送電子郵件至 <aepdestsdk@adobe.com> 其中包括：

* 目的地解決的使用案例說明。 只有當您提交新的目的地設定時，才需要執行此操作。
* 目的地提交原因的說明。 只有在更新現有的目的地設定時，才需要此設定。
* 使用測試目的地API端點對您的目的地執行HTTP呼叫後的測試結果。 請與Adobe共用對您的目的地端點發出的API呼叫，以及從您的目的地端點接收的API回應。
* 檔案型目的地的其他需求：
   * 使用測試API將請求和回應範例共用至 [使用範例設定檔測試您的檔案型目的地](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * 附加目的地產生的範例檔案，並匯出至儲存位置。
   * 提交您已成功將匯出的檔案從儲存位置擷取到系統中的某些形式證明。
* 證明您已使用針對您的目的地提交目的地發佈請求 [目的地發佈API](../publishing-api/create-publishing-request.md).
* 檔案PR （提取請求），遵循 [自助服務檔案程式](../docs-framework/documentation-instructions.md).
* 影像檔案，會在Experience Platform目的地目錄中顯示為目的地卡片的標誌。

您可以在下列各節中找到有關每個專案的詳細資訊：

## 使用案例說明 {#use-case-description}

提供目的地為Experience Platform客戶解決的使用案例說明。 您的說明可能類似於現有合作夥伴的使用案例：

* [pinterest](/help/destinations/catalog/advertising/pinterest.md)：從您的客戶清單、造訪過您網站的人或已在Pinterest上與您的內容互動的人中建立對象。
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases)：DataX API適用於廣告商，如果廣告商想要鎖定在Verizon Media (VMG)中電子郵件地址作為輸入的特定受眾群組，則可以使用VMG的近乎即時API快速建立新區段並推送所需的受眾群組。

## 更新原因 {#reason-for-update}

>[!NOTE]
>
>只有在更新現有設定時，才需要此區段。

提供您提交解決現有目的地問題的簡短說明。 例如，當您從Beta版移至一般可用性時，提交內容可能會更新目的地的名稱、說明和標誌。 或者，您的提交可能會修正目的地設定中發現的錯誤。

## 使用測試目的地API後的測試結果 {#testing-api-response}

使用後提供測試結果 [測試目的地API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) 端點，以對您的目的地執行HTTP呼叫。 这包括：

* 使用測試API向目的地端點提出完整API請求（標頭和內文）。
* 從您的目的地端點接收的API回應。

例如，您的請求和回應看起來可能類似於以下範例：

**请求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**响应**

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

## 檔案型目的地的其他需求 {#additional-file-based-destination-requirements}

針對以檔案為基礎的目的地，您必須提供其他證明，證明您已正確設定目的地。 請務必加入下列專案：

### 測試API回應 {#testing-api-response-file-based}

使用測試API將請求和回應範例納入 [使用範例設定檔測試您的檔案型目的地](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### 附加匯出的檔案 {#attach-exported-file}

在您的 [提交電子郵件](#download-sample-email)，附加您設定之目的地匯出至儲存位置的CSV檔案。

### 成功擷取的證明 {#proof-of-successful-ingestion}

最後，您必須提供某種形式的證明，證明資料匯出至您提供的儲存位置後，已成功內嵌至您的系統。 請提供以下任何專案：

* 熒幕擷取畫面或簡短的熒幕擷取視訊，讓您從儲存位置手動擷取檔案，並將其擷取到您的系統中。
* 熒幕擷取畫面或簡短的熒幕擷取視訊，其中系統的UI會確認Experience Platform產生的檔案名稱已成功擷取至系統中。
* 您系統中的記錄行，這些Adobe可以與檔案名稱或從Experience Platform產生的資料相關聯。

## 證明您已提交目的地發佈請求 {#destination-publishing-request-proof}

成功測試目的地後，您必須使用 [目的地發佈API](../publishing-api/create-publishing-request.md) 將目的地提交至Adobe以供檢閱和發佈。

提供您目的地之發佈要求的ID。 如需如何擷取發佈請求ID的詳細資訊，請閱讀如何 [擷取目的地發佈請求](../publishing-api/retrieve-publishing-request.md).

## 適用於產品化整合的目的地檔案PR （提取請求） {#documentation-pr}

如果您是獨立軟體廠商(ISV)或系統整合商(SI)，請建立 [產品化整合](../overview.md#productized-custom-integrations)，您必須使用 [自助服務檔案程式](../docs-framework/documentation-instructions.md) ，為您的目的地建立產品檔案頁面。 在提交程式中，請為目的地檔案提供提取請求(PR)。

## 您目的地的標誌 {#logo}

目的地目錄包含每個目的地卡的標誌。 在您的提交電子郵件中，加入含有目的地標誌的影像。

影像需求為：
* **格式**: `SVG`
* **大小**：小於2MB

## 下載範例電子郵件 {#download-sample-email}

[下載](../assets/guides/sample-email-submit-destination.rtf) 包含您需要提供以供Adobe之所有資訊的範例電子郵件。
