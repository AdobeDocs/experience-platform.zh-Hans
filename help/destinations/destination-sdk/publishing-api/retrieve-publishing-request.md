---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK擷取目的地發佈請求之詳細資料的API呼叫範例。
title: 擷取目的地發佈請求
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---


# 擷取目的地發佈請求

>[!IMPORTANT]
>
>只有在您提交產品化（公用）目的地以供其他Experience Platform客戶使用時，才需要使用此API端點。 如果您要建立私人目的地以供自己使用，則不需要使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

設定並測試目的地後，您可以將其提交至Adobe以供稽核和發佈。 讀取 [提交以Destination SDK撰寫的目的地，以供複查](../guides/submit-destination.md) 至於所有其他步驟，您必須在目的地提交程式中執行。

在下列情況下，使用發佈目的地API端點提交發佈請求：

* 身為Destination SDK合作夥伴，您想要讓所有Experience Platform組織都能提供已生產化的目的地，以供所有Experience Platform客戶使用；
* 您製作 *任何更新* 至您的設定。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## Destination Publishing API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 列出目的地發佈請求 {#retrieve-list}

您可以透過向以下網站提出GET請求，擷取為您的IMS組織提交的所有目標清單： `/authoring/destinations/publish` 端點。

**API格式**

使用下列API格式來擷取您帳戶的所有發佈請求。

```http
GET /authoring/destinations/publish
```

使用下列API格式來擷取特定的發佈請求，定義由 `{DESTINATION_ID}` 引數。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**请求**

以下兩個請求會擷取您IMS組織的所有發佈請求或特定發佈請求，具體取決於您是否傳遞 `DESTINATION_ID` 請求中的引數。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 擷取所有發佈請求]

+++请求

下列請求將依據以下內容，擷取您提交的發佈請求清單 [!DNL IMS Org ID] 和沙箱設定。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

以下回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，其中包含為了發佈而提交且您有權存取的所有目的地清單。 一 `configId` 對應至一個目的地的發佈要求。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您已提交以進行發佈的目的地設定的目的地ID。 |
| `publishDetailsList.configId` | 字符串 | 您提交之目的地的目的地發佈要求唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 傳回目的地可用的Experience Platform組織。 <br> <ul><li> 對象 `"destinationType": "PUBLIC"`，此引數會傳回 `"*"`，這表示所有Experience Platform組織都可使用目的地。</li><li> 對象 `"destinationType": "DEV"`，此引數會傳回您用來編寫和測試目的地的組織ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目的地發佈請求的狀態。 可能的值包括 `TEST`， `REVIEW`， `APPROVED`， `PUBLISHED`， `DENIED`， `REVOKED`， `DEPRECATED`. 具有值的目的地 `PUBLISHED` 為上線狀態，可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目的地的型別。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 對應至您Experience Platform組織中的目的地。 `PUBLIC` 對應至您已提交發佈的目的地。 以Git術語來思考這兩個選項，其中 `DEV` 版本代表您的本機編寫分支，而 `PUBLIC` version代表遠端主要分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 以紀元時間提交目的地以供發佈的日期。 |

{style="table-layout:auto"}

+++

>[!TAB 擷取特定發佈請求]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要擷取其發佈狀態的目的地ID。 |

+++

+++响应

如果您傳入 `DESTINATION_ID` 在API呼叫中，回應會傳回HTTP狀態200，其中包含指定目的地發佈請求的詳細資訊。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您已提交以進行發佈的目的地設定的目的地ID。 |
| `publishDetailsList.configId` | 字符串 | 您提交之目的地的目的地發佈要求唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 傳回目的地可用的Experience Platform組織。 <br> <ul><li> 對象 `"destinationType": "PUBLIC"`，此引數會傳回 `"*"`，這表示所有Experience Platform組織都可使用目的地。</li><li> 對象 `"destinationType": "DEV"`，此引數會傳回您用來編寫和測試目的地的組織ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目的地發佈請求的狀態。 可能的值包括 `TEST`， `REVIEW`， `APPROVED`， `PUBLISHED`， `DENIED`， `REVOKED`， `DEPRECATED`. 具有值的目的地 `PUBLISHED` 為上線狀態，可供Experience Platform客戶使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目的地的型別。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 對應至您Experience Platform組織中的目的地。 `PUBLIC` 對應至您已提交發佈的目的地。 以Git術語來思考這兩個選項，其中 `DEV` 版本代表您的本機編寫分支，而 `PUBLIC` version代表遠端主要分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 以紀元時間提交目的地以供發佈的日期。 |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。