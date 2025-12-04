---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK创建目标服务器的API调用。
title: 创建目标服务器配置
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: e1dd6ae9bf28014e8e84de85bdf67707744ea0ad
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 5%

---

# 创建目标服务器配置

创建目标服务器是使用Destination SDK创建自己的目标的第一步。 目标服务器包括[服务器](../../functionality/destination-server/server-specs.md)和[模板](../../functionality/destination-server/templating-specs.md)规范、[消息格式](../../functionality/destination-server/message-format.md)以及[文件格式](../../functionality/destination-server/file-formatting.md)选项（用于基于文件的目标）的配置选项。

此页面展示了可用于使用`/authoring/destination-servers` API端点创建自己的目标服务器的API请求和有效负荷。

有关可通过此端点配置的功能的详细说明，请参阅以下文章：

* [使用Destination SDK创建目标的服务器规范](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK创建的目标模板规范](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [消息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [文件格式配置](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;**&#x200B;**。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标服务器API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 创建目标服务器配置 {#create}

您可以通过向`POST`端点发出`/authoring/destination-servers`请求来创建新的目标服务器配置。

>[!TIP]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API格式**

```http
POST /authoring/destination-servers
```

根据您创建的目标类型，您需要配置一个稍有不同的目标服务器类型。

### 创建静态架构目标服务器 {#static-destination-servers}

在下面的选项卡中查看使用[静态架构](../../functionality/destination-configuration/schema-configuration.md#attributes-schema)的目标服务器的示例。

以下示例负载包括每种目标服务器类型支持的所有参数。 您不需要在请求中包含所有参数。 负载可根据您的需求进行自定义。

选择下面的每个选项卡以查看相应的API请求。

>[!BEGINTABS]

>[!TAB 实时（流）]

**创建实时（流）目标服务器**

您需要创建类似于以下所示的实时（流）目标服务器，以便配置基于实时（流）API的集成。

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
| `name` | 字符串 | *必填。*&#x200B;表示您的服务器的友好名称，仅对Adobe可见。 合作伙伴或客户看不到此名称。 示例`Moviestar destination server`。 |
| `destinationServerType` | 字符串 | *必填。对于实时（流）目标，*&#x200B;设置为`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字符串 | *必需。* <ul><li>如果Adobe需要转换以下`PEBBLE_V1`字段中的URL，请使用`value`。 如果您具有像`https://api.moviestar.com/data/{{customerData.region}}/items`这样的端点，其中`region`部分可以因客户而异，请使用此选项。 在这种情况下，您还需要在`region`目标配置[(../destination-configuration/create-destination-configuration.md)中将](../../functionality/destination-configuration/customer-data-fields.md)配置为[客户数据字段]。 </li><li> 如果Adobe端不需要转换，例如，如果您有类似`NONE`的端点，则使用`https://api.moviestar.com/data/items`。</li></ul> |
| `urlBasedDestination.url.value` | 字符串 | *必填。*&#x200B;填写Experience Platform应连接到的API终结点的地址。 |
| `httpTemplate.httpMethod` | 字符串 | *必填。* Adobe将在对服务器的调用中使用的方法。 选项为`GET`、`PUT`、`POST`、`DELETE`、`PATCH`。 |
| `httpTemplate.requestBody.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `httpTemplate.requestBody.value` | 字符串 | *必填。*&#x200B;此字符串是字符转义版本，用于将Experience Platform客户的数据转换为您的服务期望的格式。<br> <ul><li> 有关如何编写模板的信息，请阅读[使用模板部分](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 有关字符转义的更多信息，请参阅[RFC JSON标准第七节](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 有关简单转换的示例，请参阅[配置文件属性](../../functionality/destination-server/message-format.md#attributes)转换。 </li></ul> |
| `httpTemplate.contentType` | 字符串 | *必填。*&#x200B;您的服务器接受的内容类型。 此值很可能为`application/json`。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!TAB Amazon S3]

**创建Amazon S3目标服务器**

您需要创建类似于以下所示的[!DNL Amazon S3]目标服务器，以便配置基于文件的[!DNL Amazon S3]目标。

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
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于[!DNL Amazon S3]，将此项设置为`FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedS3Destination.bucket.value` | 字符串 | 此目标使用的[!DNL Amazon S3]存储段的名称。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedS3Destination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 不适用 | 有关如何配置这些设置的详细信息，请参阅[文件格式配置](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!TAB SFTP]

**创建[!DNL SFTP]目标服务器**

您需要创建类似于以下所示的[!DNL SFTP]目标服务器，以便配置基于文件的[!DNL SFTP]目标。

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
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
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
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于[!DNL SFTP]目标，请将此项设置为`FILE_BASED_SFTP`。 |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedSFTPDestination.rootDirectory.value` | 字符串 | 目标存储的根目录。 |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedSFTPDestination.hostName.value` | 字符串 | 目标存储的主机名。 |
| `port` | 整数 | SFTP文件服务器端口。 |
| `encryptionMode` | 字符串 | 指示是否使用文件加密。 支持的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 不适用 | 有关如何配置这些设置的详细信息，请参阅[文件格式配置](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!TAB Azure Data Lake Storage]

**创建[!DNL Azure Data Lake Storage]目标服务器**

您需要创建类似于以下所示的[!DNL Azure Data Lake Storage]目标服务器，以便配置基于文件的[!DNL Azure Data Lake Storage]目标。

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
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于[!DNL Azure Data Lake Storage]目标，请将此项设置为`FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAdlsGen2Destination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 不适用 | 有关如何配置这些设置的详细信息，请参阅[文件格式配置](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!TAB Azure Blob存储]

**创建[!DNL Azure Blob Storage]目标服务器**

您需要创建类似于以下所示的[!DNL Azure Blob Storage]目标服务器，以便配置基于文件的[!DNL Azure Blob Storage]目标。

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
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于[!DNL Azure Blob Storage]目标，请将此项设置为`FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.container.value` | 字符串 | 此目标使用的[!DNL Azure Blob Storage]容器的名称。 |
| `fileConfigurations` | 不适用 | 有关如何配置这些设置的详细信息，请参阅[文件格式配置](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!TAB 数据登陆区(DLZ)]

**创建[!DNL Data Landing Zone (DLZ)]目标服务器**

您需要创建一个[!DNL Data Landing Zone (DLZ)]目标服务器，类似于配置基于文件的[!DNL Data Landing Zone (DLZ)]目标时所显示的目标服务器。

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
      "useCase": "dlz_destination"
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
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于[!DNL Data Landing Zone]目标，请将此项设置为`FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedDlzDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 不适用 | 有关如何配置这些设置的详细信息，请参阅[文件格式配置](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!TAB Google云存储]

**创建[!DNL Google Cloud Storage]目标服务器**

您需要创建一个[!DNL Google Cloud Storage]目标服务器，类似于配置基于文件的[!DNL Google Cloud Storage]目标时所显示的目标服务器。

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
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对于[!DNL Google Cloud Storage]目标，请将此项设置为`FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字符串 | 此目标使用的[!DNL Google Cloud Storage]存储段的名称。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |
| `fileConfigurations` | 不适用 | 有关如何配置这些设置的详细信息，请参阅[文件格式配置](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!ENDTABS]

### 创建动态架构目标服务器 {#dynamic-schema-servers}

动态架构允许您动态检索支持的目标属性，并根据自己的API生成架构。 您需要先为动态架构配置目标服务器，然后才能配置架构。

在下面的选项卡中查看使用[动态架构](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration)的目标服务器的示例。

以下有效负载示例包含动态架构服务器所需的所有参数。

>[!BEGINTABS]

>[!TAB 动态架构服务器]

**创建动态架构服务器**

您需要创建类似于以下所示的动态架构服务器，以便配置从您自己的API端点检索其配置文件架构的目标。 与静态架构相反，动态架构不使用`profileFields`数组。 动态架构会改用动态架构服务器，该服务器会连接到您自己的API，并在其中检索架构配置。

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
| `name` | 字符串 | *必填。*&#x200B;表示您的动态架构服务器的友好名称，仅对Adobe可见。 |
| `destinationServerType` | 字符串 | *必填。对于动态架构服务器，*&#x200B;设置为`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字符串 | *必需。* <ul><li>如果Adobe需要转换以下`PEBBLE_V1`字段中的URL，请使用`value`。 如果您具有类似以下的端点，请使用此选项： `https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 如果Adobe端不需要转换，例如，如果您有类似`NONE`的端点，则使用`https://api.moviestar.com/data/items`。</li></ul> |
| `urlBasedDestination.url.value` | 字符串 | *必填。*&#x200B;填写Experience Platform应连接到的API端点地址，并检索架构字段以作为激活工作流映射步骤中的目标字段填充。 |
| `httpTemplate.httpMethod` | 字符串 | *必填。* Adobe将在对服务器的调用中使用的方法。 对于动态架构服务器，请使用`GET`。 |
| `responseFields.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `responseFields.value` | 字符串 | *必填。*&#x200B;此字符串是一个字符转义转换模板，它将从合作伙伴API收到的响应转换为将在Experience Platform UI中显示的合作伙伴架构。<br> <ul><li> 有关如何编写模板的信息，请阅读[使用模板部分](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 有关字符转义的更多信息，请参阅[RFC JSON标准第七节](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 有关简单转换的示例，请参阅[配置文件属性](../../functionality/destination-server/message-format.md#attributes)转换。 </li></ul> |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++


>[!ENDTABS]


### 创建动态下拉目标服务器 {#dynamic-dropdown-servers}

根据您自己的API，使用[动态下拉列表](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors)动态检索和填充下拉客户数据字段。 例如，您可以检索要用于目标连接的现有用户帐户列表。

您需要先为动态下拉列表配置目标服务器，然后才能配置动态下拉列表客户数据字段。

请参阅以下选项卡中的目标服务器示例，该示例用于从API动态检索要在下拉选择器中显示的值。

以下有效负载示例包含动态架构服务器所需的所有参数。

>[!BEGINTABS]

>[!TAB 动态下拉服务器]

**创建动态下拉服务器**

您需要创建一个动态下拉服务器，类似于当您配置从您自己的API端点检索下拉客户数据字段值的目标时，下面显示的服务器。

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
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `name` | 字符串 | *必填。*&#x200B;表示动态下拉服务器的友好名称，仅对Adobe可见。 |
| `destinationServerType` | 字符串 | *必填。对于动态下拉服务器，*&#x200B;设置为`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字符串 | *必需。* <ul><li>如果Adobe需要转换以下`PEBBLE_V1`字段中的URL，请使用`value`。 如果您具有类似以下的端点，请使用此选项： `https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 如果Adobe端不需要转换，例如，如果您有类似`NONE`的端点，则使用`https://api.moviestar.com/data/items`。</li></ul> |
| `urlBasedDestination.url.value` | 字符串 | *必填。*&#x200B;填写Experience Platform应连接到的API端点地址并检索下拉值。 |
| `httpTemplate.httpMethod` | 字符串 | *必填。* Adobe将在对服务器的调用中使用的方法。 对于动态下拉服务器，请使用`GET`。 |
| `httpTemplate.headers` | 对象 | *Optiona.l*&#x200B;包含连接到动态下拉服务器所需的任何标头。 |
| `responseFields.templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `responseFields.value` | 字符串 | *必填。*&#x200B;此字符串是一个字符转义转换模板，它将从API收到的响应转换为Experience Platform UI中显示的值。<br> <ul><li> 有关如何编写模板的信息，请阅读[使用模板部分](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 有关字符转义的更多信息，请参阅[RFC JSON标准第七节](https://tools.ietf.org/html/rfc8259#section-7)。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态200以及新创建的目标服务器配置的详细信息。

+++

>[!ENDTABS]

## API错误处理 {#error-handling}

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何通过Destination SDK `/authoring/destination-servers` API端点创建新的目标服务器。

要了解有关可使用此端点执行的操作的更多信息，请参阅以下文章：

* [检索目标服务器配置](retrieve-destination-server.md)
* [更新目标服务器配置](update-destination-server.md)
* [删除目标服务器配置](delete-destination-server.md)

要了解此端点在目标创作过程中的位置，请参阅以下文章：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
