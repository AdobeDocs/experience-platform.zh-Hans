---
description: 此頁面是透過Adobe Experience Platform Destination SDK建立目的地伺服器所使用的API呼叫的範例。
title: 建立目的地伺服器設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 9%

---


# 建立目的地伺服器設定

使用Destination SDK建立自己的目的地時，第一步是建立目的地伺服器。 目的地伺服器包含 [伺服器](../../functionality/destination-server/server-specs.md) 和 [範本](../../functionality/destination-server/templating-specs.md) 規格， [訊息格式](../../functionality/destination-server/message-format.md)，以及 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 選項（適用於檔案型目的地）。

此頁面以範例說明API請求和裝載，您可使用這些API請求和裝載來建立自己的目的地伺服器。 `/authoring/destination-servers` api端點。

如需可透過此端點設定的功能的詳細說明，請閱讀以下文章：

* [以Destination SDK建立的目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [以Destination SDK建立的目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [消息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 開始使用目的地伺服器API作業 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 建立目的地伺服器設定 {#create}

您可以建立新的目的地伺服器組態，方法是 `POST` 向以下專案提出的請求： `/authoring/destination-servers` 端點。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API格式**

```http
POST /authoring/destination-servers
```

根據您建立的目的地型別，您需要設定稍微不同的目的地伺服器型別。 請參閱下方標籤中目標伺服器的範例，瞭解Destination SDK支援的每個目標型別。

以下範例裝載包含每個目的地伺服器型別支援的所有引數。 您不需要在請求中包含所有引數。 可根據您的需求自訂裝載。

選取下方的每個標籤，以檢視對應的API請求。

>[!BEGINTABS]

>[!TAB 即時（串流）]

**建立即時（串流）目的地伺服器**

您需要建立即時（串流）目的地伺服器，類似於當您設定即時（串流） API型整合時顯示的伺服器。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `name` | 字符串 | *必需。* 代表伺服器的易記名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 示例 `Moviestar destination server`. |
| `destinationServerType` | 字符串 | *必需。* 設定為 `URL_BASED` 適用於即時（串流）目的地。 |
| `urlBasedDestination.url.templatingStrategy` | 字符串 | *必需.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 欄位。 如果您擁有類似以下的端點，請使用此選項 `https://api.moviestar.com/data/{{customerData.region}}/items`，其中 `region` 部分可能會因客戶而異。 在此情況下，您也需要設定 `region` as a [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 在 [目的地設定](../destination-configuration/create-destination-configuration.md. </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有如下端點： `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 字符串 | *必需。* 填入Experience Platform應連線的API端點位址。 |
| `httpTemplate.httpMethod` | 字符串 | *必需。* Adobe將在對伺服器呼叫中使用的方法。 選項包括 `GET`， `PUT`， `POST`， `DELETE`， `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `httpTemplate.requestBody.value` | 字符串 | *必需。* 此字串是字元逸出版本，可將Platform客戶的資料轉換為您的服務預期格式。 <br> <ul><li> 如需如何寫入範本的詳細資訊，請閱讀 [使用範本區段](../../functionality/destination-server/message-format.md#using-templating). </li><li> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 如需簡單轉換的範例，請參閱 [設定檔屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |
| `httpTemplate.contentType` | 字符串 | *必需。* 您的伺服器接受的內容型別。 此值很有可能 `application/json`. |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Amazon S3]

**建立Amazon S3目的地伺服器**

您需要建立 [!DNL Amazon S3] 目的地伺服器，類似於當您設定檔案型伺服器時顯示的伺服器 [!DNL Amazon S3] 目的地。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
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
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Amazon S3]，將此專案設為 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedS3Destination.bucket.value` | 字符串 | 的名稱 [!DNL Amazon S3] 要由此目的地使用的貯體。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedS3Destination.path.value` | 字符串 | 存放匯出檔案的目標資料夾路徑。 |
| `fileConfigurations` | 不适用 | 另請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB SFTP]

**建立 [!DNL SFTP] 目的地伺服器**

您需要建立 [!DNL SFTP] 目的地伺服器，類似於當您設定檔案型伺服器時顯示的伺服器 [!DNL SFTP] 目的地。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
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
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL SFTP] 目的地，設定為 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedSftpDestination.rootDirectory.value` | 字符串 | 目的地儲存體的根目錄。 |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedSftpDestination.hostName.value` | 字符串 | 目的地儲存體的主機名稱。 |
| `port` | 整数 | SFTP檔案伺服器連線埠。 |
| `encryptionMode` | 字符串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 不适用 | 另請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Azure Data Lake儲存]

**建立 [!DNL Azure Data Lake Storage] 目的地伺服器**

您需要建立 [!DNL Azure Data Lake Storage] 目的地伺服器，類似於當您設定檔案型伺服器時顯示的伺服器 [!DNL Azure Data Lake Storage] 目的地。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
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
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Azure Data Lake Storage] 目的地，設定為 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedAdlsGen2Destination.path.value` | 字符串 | 存放匯出檔案的目標資料夾路徑。 |
| `fileConfigurations` | 不适用 | 另請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Azure Blob 存储]

**建立 [!DNL Azure Blob Storage] 目的地伺服器**

您需要建立 [!DNL Azure Blob Storage] 目的地伺服器，類似於當您設定檔案型伺服器時顯示的伺服器 [!DNL Azure Blob Storage] 目的地。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
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
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Azure Blob Storage] 目的地，設定為 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.path.value` | 字符串 | 存放匯出檔案的目標資料夾路徑。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.container.value` | 字符串 | 的名稱 [!DNL Azure Blob Storage] 此目的地要使用的容器。 |
| `fileConfigurations` | 不适用 | 另請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB 資料登陸區(DLZ)]

**建立 [!DNL Data Landing Zone (DLZ)] 目的地伺服器**

您需要建立 [!DNL Data Landing Zone (DLZ)] 目的地伺服器，類似於當您設定檔案型伺服器時顯示的伺服器 [!DNL Data Landing Zone (DLZ)] 目的地。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
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
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Data Landing Zone] 目的地，設定為 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedDlzDestination.path.value` | 字符串 | 存放匯出檔案的目標資料夾路徑。 |
| `fileConfigurations` | 不适用 | 另請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Google雲端儲存空間]

**建立 [!DNL Google Cloud Storage] 目的地伺服器**

您需要建立 [!DNL Google Cloud Storage] 目的地伺服器，類似於當您設定檔案型伺服器時顯示的伺服器 [!DNL Google Cloud Storage] 目的地。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
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
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Google Cloud Storage] 目的地，設定為 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字符串 | 的名稱 [!DNL Google Cloud Storage] 要由此目的地使用的貯體。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字符串 | 存放匯出檔案的目標資料夾路徑。 |
| `fileConfigurations` | 不适用 | 另請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB 動態結構描述伺服器]

**建立動態結構描述伺服器**

設定從您自己的API端點擷取其設定檔結構描述的目的地時，您需要建立類似於以下顯示的動態結構描述伺服器。 相對於靜態結構描述，動態結構描述不會使用 `profileFields` 陣列。 動態結構描述會改用動態結構描述伺服器，該伺服器會從其中擷取結構描述設定，連線到您自己的API。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `name` | 字符串 | *必需。* 代表動態結構描述伺服器的易記名稱，僅對Adobe可見。 |
| `destinationServerType` | 字符串 | *必需。* 設定為 `URL_BASED` 適用於動態結構描述伺服器。 |
| `urlBasedDestination.url.templatingStrategy` | 字符串 | *必需.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 欄位。 如果您有類似以下的端點，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有如下端點： `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 字符串 | *必需。* 填寫Experience Platform應連線的API端點位址，並擷取結構描述欄位，以填入為啟動工作流程對應步驟中的目標欄位。 |
| `httpTemplate.httpMethod` | 字符串 | *必需。* Adobe將在對伺服器呼叫中使用的方法。 對於動態結構描述伺服器，請使用 `GET`. |
| `responseFields.templatingStrategy` | 字符串 | *必需。*&#x200B;使用 `PEBBLE_V1`。 |
| `responseFields.value` | 字符串 | *必需。* 此字串是字元逸出轉換範本，可將從合作夥伴API收到的回應轉換為將顯示在平台UI中的合作夥伴結構描述。 <br> <ul><li> 如需如何寫入範本的詳細資訊，請閱讀 [使用範本區段](../../functionality/destination-server/message-format.md#using-templating). </li><li> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 如需簡單轉換的範例，請參閱 [設定檔屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK建立新的目的地伺服器 `/authoring/destination-servers` api端點。

若要進一步瞭解您可以使用此端點做什麼，請參閱下列文章：

* [擷取目的地伺服器設定](retrieve-destination-server.md)
* [更新目的地伺服器設定](update-destination-server.md)
* [刪除目的地伺服器設定](delete-destination-server.md)

若要瞭解此端點適用於目的地撰寫程式的位置，請參閱下列文章：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)