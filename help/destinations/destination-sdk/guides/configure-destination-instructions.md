---
description: 本頁面列出並說明使用Destination SDK設定串流目的地的步驟。
title: 使用Destination SDK設定串流目的地
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 使用Destination SDK設定串流目的地

## 概述 {#overview}

此頁面說明如何使用下列專案的資訊： [目的地SDK中的設定選項](../functionality/configuration-options.md) 以及在其他Destination SDK功能和API參考檔案中設定 [串流目的地](../../destination-types.md#streaming-destinations). 這些步驟會依序排列如下。

## 先决条件 {#prerequisites}

在繼續進行下列步驟之前，請閱讀 [Destination SDK快速入門](../getting-started.md) 頁面以取得必要的Adobe I/O驗證認證，以及使用Destination SDKAPI的其他先決條件。 這假設您已完成合作關係與許可權必要條件，並準備好開始開發您的目的地。

## 在Destination SDK中使用設定選項來設定目的地的步驟 {#steps}

![說明使用Destination SDK端點的步驟](../assets/guides/destination-sdk-steps.png)

## 步驟1：建立伺服器和範本設定 {#create-server-template-configuration}

開始者 [建立伺服器和範本組態](../authoring-api/destination-server/create-destination-server.md) 使用 `/destinations-server` 端點。

以下是設定範例。 請注意，訊息轉換範本位於 `requestBody.value` 引數已在步驟3中解決， [建立轉換範本](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## 步驟2：建立目的地設定 {#create-destination-configuration}

以下顯示的是目的地範本的設定範例，範本是使用 `/destinations` api端點。 另請參閱 [建立目的地設定](../authoring-api/destination-configuration/create-destination-configuration.md) 以取得詳細資訊。

若要在步驟1中將伺服器和範本設定連線至此目的地設定，請將伺服器和範本設定的執行個體ID新增為 `destinationServerId` 此處。

>[!IMPORTANT]
>
>若要建立正確設定的即時（串流）目的地，您必須 *必須* 在中新增至少一個目標身分 `identityNamespaces`，如下所示。 如果未設定目標身分，使用者將無法繼續前往 [對應步驟](../../ui/activate-segment-streaming-destinations.md#mapping) 啟動工作流程的。

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## 步驟3：建立訊息轉換範本 — 使用範本化語言指定訊息輸出格式 {#create-transformation-template}

您必須根據目的地支援的裝載，建立範本，將匯出的資料格式從AdobeXDM格式轉換為目的地支援的格式。 請參閱區段中的範本範例 [使用範本語言進行身分、屬性和區段成員資格轉換](../functionality/destination-server/message-format.md#using-templating) 並使用 [範本製作工具](../testing-api/streaming-destinations/create-template.md) 由Adobe提供。

在您建立適合您的訊息轉換範本後，請將其新增至您在步驟1中建立的伺服器和範本設定。

```json {line-numbers="true" highlight="13-14"}
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## 步驟4：建立對象中繼資料設定 {#create-audience-metadata-configuration}

對於某些目的地，Destination SDK需要您設定對象中繼資料設定，以程式設計方式在您的目的地建立、更新或刪除對象。 請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md) 瞭解何時需要設定此設定及如何設定的相關資訊。

如果您使用對象中繼資料設定，則必須將其連線到您在步驟2中建立的目的地設定。 將對象中繼資料設定的例項ID新增至目的地設定，做為 `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "audienceMetadataConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```


## 步驟5：設定驗證 {#set-up-authentication}

視您是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上面的目的地設定中，您可以使用為目的地設定驗證 `/destination` 或 `/credentials` 端點。

如果您已選取 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在目的地設定中，且您的目的地支援OAuth 2驗證方法，請閱讀 [OAuth 2驗證](../functionality/destination-configuration/oauth2-authentication.md).

如果您已選取 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，您必須建立 [認證設定](../credentials-api/create-credential-configuration.md).

## 步驟6：測試您的目的地 {#test-destination}

使用先前步驟中的設定端點設定目的地後，您可以使用 [目的地測試工具](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) 測試Adobe Experience Platform與目的地之間的整合。

在測試目的地的程式中，您必須使用Experience PlatformUI來建立區段，並啟用至目的地。 請參考以下兩個資源，瞭解如何在Experience Platform中建立區段的指示：

* [建立區段檔案頁面](/help/segmentation/ui/overview.md#create-segment)
* [建立區段影片逐步解說](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## 步驟7：發佈您的目的地 {#publish-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供您自己使用，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

設定並測試目的地後，請使用 [目的地發佈API](../publishing-api/create-publishing-request.md) 以將您的設定提交至Adobe以供檢閱。

## 步驟8：記錄您的目的地 {#document-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供您自己使用，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

如果您是獨立軟體廠商(ISV)或系統整合商(SI)，請建立 [產品化整合](../overview.md#productized-custom-integrations)，使用 [自助服務檔案程式](../docs-framework/documentation-instructions.md) 若要在中建立您目的地的產品檔案頁面 [Experience Platform目的地目錄](/help/destinations/catalog/overview.md).

## 步驟9：提交目的地以供Adobe複查 {#submit-for-review}

>[!NOTE]
>
>如果您要建立私人目的地以供您自己使用，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

最後，在Experience Platform目錄中發佈目的地並對所有Experience Platform客戶可見之前，您必須正式提交目的地以供Adobe檢閱。 尋找如何操作的完整資訊 [送出供檢閱在Destination SDK中製作的生產目的地](../guides/submit-destination.md).
