---
description: 本页列出并介绍了您可以使用“/authoring/destinations” API端点执行的所有API操作。
title: 目标API端点操作
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '2572'
ht-degree: 4%

---

# 目标端点API操作 {#destination-configuration}

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/destinations`

本页列出并介绍了您可以使用 `/authoring/destinations` API端点。 有关此端点支持的功能的描述，请阅读 [目标配置](./destination-configuration.md).

## 目标API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 为流目标创建配置 {#create}

您可以通过向 `/authoring/destinations` 端点。

**API格式**

```http
POST /authoring/destinations
```

**请求**

以下请求会创建新的流目标配置，该配置由有效负载中提供的参数进行配置。 以下负载包括接受的流目标的所有参数 `/authoring/destinations` 端点。 请注意，您不必在调用中添加所有参数，并且该模板可根据您的API要求进行自定义。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 指示Experience Platform目录中目标的标题 |
| `description` | 字符串 | 提供Adobe将在目标卡的Experience Platform目标目录中使用的描述。 目标不超过4-5句。 |
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 首次配置目标时。 |
| `customerAuthenticationConfigurations` | 字符串 | 指示用于向服务器验证Experience Platform客户的配置。 请参阅 `authType` 下方的值。 |
| `customerAuthenticationConfigurations.authType` | 字符串 | 流目标支持的值包括： <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> 基于文件的目标支持的值包括： <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `customerDataFields.type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为 `string`, `object`, `integer` |
| `customerDataFields.title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中看到该字段 |
| `customerDataFields.description` | 字符串 | 为自定义字段提供描述。 |
| `customerDataFields.isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `customerDataFields.enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `customerDataFields.pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请输入 `^[A-Za-z]+$` 中。 |
| `uiAttributes.documentationLink` | 字符串 | 指 [目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您的目标名称。 对于名为Moviestar的目标，您将使用 `https://www.adobe.com/go/destinations-moviestar-en`. 请注意，此链接仅在Adobe设置目标处于实时状态且文档已发布后才可用。 |
| `uiAttributes.category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读 [目标类别](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用以下任一值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | 字符串 | `Server-to-server` 是当前唯一可用的选项。 |
| `uiAttributes.frequency` | 字符串 | `Streaming` 是当前唯一可用的选项。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布尔型 | 指示您的目标是否接受标准配置文件属性。 通常，这些属性会在我们的合作伙伴文档中突出显示。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布尔型 | 指示客户是否可以在您的目标中设置自定义命名空间。 |
| `identityNamespaces.externalId.transformation` | 字符串 | _示例配置中未显示_. 例如，当 [!DNL Platform] 客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件。 在这里，您将提供需要应用的转换（例如，将电子邮件转换为小写，然后再转换为哈希）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 用于平台接受 [标准身份命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) （例如IDFA），以便您可以限制Platform用户仅选择这些身份命名空间。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 更改为小写和哈希电子邮件地址或电话号码。 |
| `destinationDelivery.authenticationRule` | 字符串 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统。 例如，如果您还选择了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 [凭据](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字符串 | 的 `instanceId` 的 [目标服务器模板](./destination-server-api.md) 用于此目标。 |
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。 <br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布尔型 | 控制用户是否在目标激活工作流中输入区段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段名称。 |
| `segmentMappingConfig.audienceTemplateId` | 布尔型 | 的 `instanceId` 的 [受众元数据模板](./audience-metadata-api.md) 用于此目标。 |
| `schemaConfig.profileFields` | 数组 | 添加预定义 `profileFields` 如上面的配置所示，用户将可以选择将Experience Platform属性映射到目标侧的预定义属性。 |
| `schemaConfig.profileRequired` | 布尔型 | 使用 `true` 如上面的示例配置所示，用户应该能够在目标侧将配置文件属性从Experience Platform映射到自定义属性。 |
| `schemaConfig.segmentRequired` | 布尔型 | 始终使用 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 布尔型 | 使用 `true` 如果用户能够将身份命名空间从Experience Platform映射到所需的架构，请执行以下操作。 |
| `aggregation.aggregationType` | - | 选择 `BEST_EFFORT` 或 `CONFIGURABLE_AGGREGATION`。上述示例配置包括 `BEST_EFFORT` 聚合。 例如 `CONFIGURABLE_AGGREGATION`，请参阅 [目标配置](./destination-configuration.md#example-configuration) 文档。 与可配置聚合相关的参数在下表中进行了说明。 |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | 整数 | Experience Platform可以在一个HTTP调用中聚合多个导出的配置文件。 指定您的端点在单个HTTP调用中应接收的最大配置文件数。 请注意，这是一种尽力的聚合。 例如，如果您指定值100,Platform可能会在一次调用中发送任意数量小于100的用户档案。 <br> 如果您的服务器不接受每个请求的多个用户，请将此值设置为1。 |
| `aggregation.bestEffortAggregation.splitUserById` | 布尔型 | 如果目标的调用应按身份进行拆分，则使用此标记。 将此标志设置为 `true` 如果服务器在每次调用中仅接受一个标识，则表示给定的命名空间。 |
| `aggregation.configurableAggregation.splitUserById` | 布尔型 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 如果目标的调用应按身份进行拆分，则使用此标记。 将此标志设置为 `true` 如果服务器在每次调用中仅接受一个标识，则表示给定的命名空间。 |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | 整数 | <ul><li>*最小值：1800*</li><li>*最大值：3600*</li><li>请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 在可接受的最小值和最大值之间配置一个值。 与 `maxNumEventsInBatch`，此参数可确定Experience Platform应等待多长时间，直到向您的端点发送API调用。 <br> 例如，如果您对两个参数使用最大值，则Experience Platform将等待3600秒或直到有1万个符合条件的配置文件才进行API调用（以先发生者为准）。 </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | 整数 | <ul><li>*最小值：1000*</li><li>*最大值：10000*</li><li>请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 在可接受的最小值和最大值之间配置一个值。 有关此参数的描述，请参阅 `maxBatchAgeInSecs` 就在上面。</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | 布尔型 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 允许您根据以下参数聚合映射到目标的导出配置文件： <br> <ul><li>区段ID</li><li> 区段状态 </li><li> 标识命名空间 </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | 布尔型 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 将此参数设置为 `true` 要按区段ID对导出到目标的用户档案进行分组。 |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | 布尔型 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 您必须同时设置 `includeSegmentId:true` 和 `includeSegmentStatus:true` 如果要按区段ID和区段状态对导出到目标的用户档案进行分组。 |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | 布尔型 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 将此参数设置为 `true` 如果要按身份命名空间对导出到目标的用户档案进行分组。 |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布尔型 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 使用此参数可指定是否要将导出的用户档案聚合到单个身份（GAID、IDFA、电话号码、电子邮件等）的组中。 |
| `aggregation.configurableAggregation.aggregationKey.groups` | 字符串 | 请参阅示例配置中的参数 [此处](./destination-configuration.md#example-configuration). 如果要按身份命名空间的组对导出到目标的配置文件进行分组，请创建身份组列表。 例如，您可以使用示例中的配置，将包含IDFA和GAID移动标识符的用户档案合并到对目标的一次调用中，以及将电子邮件合并到另一个调用中。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回HTTP状态200，其中包含新创建的目标配置的详细信息。

## 为基于文件的目标创建配置 {#create-file-based}

您可以通过向 `/authoring/destinations` 端点。

**API格式**

```http
POST /authoring/destinations
```

**请求**

以下请求会创建新 [!DNL Amazon S3] 基于文件的目标配置，由有效负载中提供的参数配置。 以下有效负载包括接受的基于文件的目标的所有参数 `/authoring/destinations` 端点。 请注意，您不必在调用中添加所有参数，并且该模板可根据您的API要求进行自定义。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
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
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

有关上述所有参数的详细描述，请参阅 [基于文件的目标配置](file-based-destination-configuration.md).

**响应**

成功响应会返回HTTP状态200，其中包含新创建的目标配置的详细信息。

## 列出目标配置 {#retrieve-list}

您可以通过向 `/authoring/destinations` 端点。

**API格式**


```http
GET /authoring/destinations
```

**请求**

以下请求将根据IMS组织和沙盒配置，检索您有权访问的目标配置列表。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

以下响应会根据您使用的IMS组织ID和沙盒名称，返回HTTP状态200，其中包含您有权访问的目标配置列表。 一个 `instanceId` 对应于一个目标的模板。 响应因简短而被截断。

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true
            }
         },
         "segmentMappingConfig":{
            "mapExperiencePlatformSegmentName":false,
            "mapExperiencePlatformSegmentId":false,
            "mapUserInput":false,
            "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
         },
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 指示Experience Platform目录中目标的标题。 |
| `description` | 字符串 | 提供Adobe将在目标卡的Experience Platform目标目录中使用的描述。 目标不超过4-5句。 |
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 首次配置目标时。 |
| `customerAuthenticationConfigurations` | 字符串 | 指示用于向服务器验证Experience Platform客户的配置。 请参阅 `authType` 下方的值。 |
| `customerAuthenticationConfigurations.authType` | 字符串 | 接受的值为 `OAUTH2, BEARER`. |
| `customerDataFields.name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `customerDataFields.type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为 `string`, `object`, `integer` |
| `customerDataFields.title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中看到该字段 |
| `customerDataFields.description` | 字符串 | 为自定义字段提供描述。 |
| `customerDataFields.isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `customerDataFields.enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `customerDataFields.pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请输入 `^[A-Za-z]+$` 中。 |
| `uiAttributes.documentationLink` | 字符串 | 指 [目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您的目标名称。 对于名为Moviestar的目标，您将使用 `https://www.adobe.com/go/destinations-moviestar-en`. 请注意，此链接仅在Adobe设置目标处于实时状态且文档已发布后才可用。 |
| `uiAttributes.category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读 [目标类别](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用以下任一值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | 字符串 | `Server-to-server` 是当前唯一可用的选项。 |
| `uiAttributes.frequency` | 字符串 | `Streaming` 是当前唯一可用的选项。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布尔型 | 指示您的目标是否接受标准配置文件属性。 通常，这些属性会在我们的合作伙伴文档中突出显示。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布尔型 | 指示客户是否可以在您的目标中设置自定义命名空间。 有关更多信息 [自定义命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) 在Adobe Experience Platform。 |
| `identityNamespaces.externalId.transformation` | 字符串 | _示例配置中未显示_. 例如，当 [!DNL Platform] 客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件。 在这里，您将提供需要应用的转换（例如，将电子邮件转换为小写，然后再转换为哈希）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 用于平台接受 [标准身份命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) （例如IDFA），以便您可以限制Platform用户仅选择这些身份命名空间。 |
| `destinationDelivery.authenticationRule` | 字符串 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统。 例如，如果您还选择了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 [凭据](./authentication-configuration.md) 配置。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字符串 | 的 `instanceId` 的 [目标服务器模板](./destination-server-api.md) 用于此目标。 |
| `destConfigId` | 字符串 | 此字段是自动生成的，不需要您输入。 |
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。 <br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布尔型 | 控制用户是否在目标激活工作流中输入区段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段名称。 |
| `segmentMappingConfig.audienceTemplateId` | 布尔型 | 的 `instanceId` 的 [受众元数据模板](./audience-metadata-management.md) 用于此目标。 要设置受众元数据模板，请阅读 [受众元数据API参考](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## 更新现有目标配置 {#update}

您可以通过向 `/authoring/destinations` 端点并提供要更新的目标配置的实例ID。 在调用的正文中，提供更新的目标配置。

**API格式**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目标配置的ID。 |

**请求**

以下请求会更新现有目标配置，该配置由有效负载中提供的参数配置。 在以下示例调用中，我们正在更新配置 [已创建早期版本](./destination-configuration-api.md#create) 现在接受GAID、IDFA和经过哈希处理的电子邮件标识符作为身份命名空间。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## 检索特定目标配置 {#get}

您可以通过向 `/authoring/destinations` 端点并提供要检索的目标配置的实例ID。

**API格式**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要检索的目标配置的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定目标配置的详细信息。

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## 删除特定目标配置 {#delete}

您可以通过向 `/authoring/destinations` 端点和提供您希望在请求路径中删除的目标配置的ID。

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `id` 要删除的目标配置。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回HTTP状态200以及空的HTTP响应。

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何使用 `/authoring/destinations` API端点。 读取 [如何使用Destination SDK配置目标](./configure-destination-instructions.md) 以了解此步骤在配置目标过程中的适用位置。
