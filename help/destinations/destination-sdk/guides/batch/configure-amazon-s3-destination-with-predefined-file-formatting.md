---
description: 瞭解如何使用Destination SDK以預先定義的檔案格式選項和自訂檔案名稱設定來設定Amazon S3目的地。
title: 使用預先定義的檔案格式選項和自訂檔案名稱設定來設定Amazon S3目的地。
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# 設定 [!DNL Amazon S3] 具有預先定義檔案格式選項和自訂檔案名稱設定的目的地

## 概述 {#overview}

本頁面說明如何使用Destination SDK以預先定義的預設值來設定Amazon S3目的地 [檔案格式選項](configure-file-formatting-options.md) 和自訂 [檔案名稱設定](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

此頁面顯示以下專案可用的所有組態選項： [!DNL Amazon S3] 目的地。 您可以視需要編輯下列步驟中顯示的配置，或刪除配置的某些部分。

如需以下所使用引數的詳細說明，請參閱 [目的地SDK中的設定選項](../../functionality/configuration-options.md).

## 先决条件 {#prerequisites}

在繼續進行下列步驟之前，請閱讀 [Destination SDK快速入門](../../getting-started.md) 頁面以取得必要的Adobe I/O驗證認證，以及使用Destination SDKAPI的其他先決條件。

## 步驟1：建立伺服器和檔案組態 {#create-server-file-configuration}

首先使用 `/destination-server` 端點至 [建立伺服器和檔案組態](../../authoring-api/destination-server/create-destination-server.md).

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**请求**

以下請求會建立新的目的地伺服器設定，由承載中提供的引數設定。
以下裝載包含通用 [!DNL Amazon S3] 設定，具有預先定義的預設值 [CSV檔案格式設定](../../functionality/destination-server/file-formatting.md) 使用者可在Experience PlatformUI中定義的設定引數。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucketName": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}'
```

成功的回應會傳回新的目的地伺服器設定，包括唯一識別碼(`instanceId`)。 將此值儲存為下一個步驟所需的值。

## 步驟2：建立目的地設定 {#create-destination-configuration}

在上一步中建立目的地伺服器和檔案格式設定後，您現在可以使用 `/destinations` API端點以建立目的地設定。

若要在中連線伺服器組態 [步驟1](#create-server-file-configuration) 對於此目的地設定，將 `destinationServerId` 值於下列API請求中使用 `instanceId` 在中建立目的地伺服器時獲得的值 [步驟1](#create-server-file-configuration).

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"File type",
         "description":"Select the exported file type.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

成功的回應會傳回新的目的地設定，包括唯一識別碼(`instanceId`)。 如果您需要進一步提出HTTP請求來更新您的目的地設定，請視需要儲存此值。

## 步驟3：驗證Experience PlatformUI {#verify-ui}

根據上述設定，Experience Platform目錄現在會顯示新的私人目的地卡供您使用。

![熒幕錄製，顯示具有選定目的地卡片的目的地目錄頁面。](../../assets/guides/batch/destination-card.gif)

在以下影像和錄製中，請注意中的選項 [檔案型目的地的啟用工作流程](../../../ui/activate-batch-profile-destinations.md) 符合您在目的地設定中選取的選項。

填寫有關目的地的詳細資料時，請注意顯示的欄位是您在設定中設定的自訂資料欄位。

>[!TIP]
>
>您新增自訂資料欄位至目的地設定的順序不會反映在UI中。 客戶資料欄位一律會以下方熒幕錄製中顯示的順序顯示。

![顯示設定中定義的客戶資料欄位的熒幕記錄。](../../assets/guides/batch/file-configuration-options.gif)

排程匯出間隔時，請注意欄位顯示方式為您在中設定的欄位 `batchConfig` 設定。
![匯出排程選項](../../assets/guides/batch/file-export-scheduling.png)

檢視檔案名稱組態選項時，請注意出現的欄位如何表示 `filenameConfig` 您在設定中設定的選項。
![檔案名稱組態選項](../../assets/guides/batch/file-naming-options.gif)

如果您想要調整任何上述欄位，請重複 [步驟一](#create-server-file-configuration) 和 [二](#create-destination-configuration) 以根據您的需求修改設定。

## 步驟4： （選用）發佈您的目的地 {#publish-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供您自己使用，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

設定目的地後，請使用 [目的地發佈API](../../publishing-api/create-publishing-request.md) 以將您的設定提交至Adobe以供檢閱。

## 步驟5：（選擇性）記錄您的目的地 {#document-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供您自己使用，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

如果您是獨立軟體廠商(ISV)或系統整合商(SI)，請建立 [產品化整合](../../overview.md#productized-custom-integrations)，使用 [自助服務檔案程式](../../docs-framework/documentation-instructions.md) 若要在中建立您目的地的產品檔案頁面 [Experience Platform目的地目錄](../../../catalog/overview.md).

## 后续步骤 {#next-steps}

閱讀本文章，您現在瞭解如何撰寫自訂 [!DNL Amazon S3] 目的地使用Destination SDK。 接下來，您的團隊可以使用 [檔案型目的地的啟用工作流程](../../../ui/activate-batch-profile-destinations.md) 將資料匯出至目的地。
