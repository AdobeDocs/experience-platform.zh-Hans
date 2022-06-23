---
description: 此配置允许您指示目标名称、类别、描述、徽标等基本信息。 此配置中的设置还可确定Experience Platform用户如何对您的目标进行身份验证、该目标如何显示在Experience Platform用户界面中，以及可导出到您目标的身份。
title: （测试版）用于Destination SDK的基于文件的目标配置选项
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 89e05ed522aed697ba3a2f06137546fd5673920d
workflow-type: tm+mt
source-wordcount: '2304'
ht-degree: 5%

---

# （测试版）基于文件的目标配置 {#destination-configuration}

## 概述 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基于文件的目标支持目前处于测试阶段。 文档和功能可能会发生更改。

此配置允许您指示基于文件的目标的基本信息，如目标名称、类别、描述等。 此配置中的设置还可确定Experience Platform用户如何对您的目标进行身份验证、该目标如何显示在Experience Platform用户界面中，以及可导出到您目标的身份。

此配置还会将目标工作所需的其他配置（目标服务器和受众元数据）连接到此配置。 了解如何在 [下文](./destination-configuration.md#connecting-all-configurations).

您可以使用 `/authoring/destinations` API端点。 读取 [目标API端点操作](./destination-configuration-api.md) 有关可对端点执行的操作的完整列表。

## Amazon S3目标配置示例 {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
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
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
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
            "name":"phoneNo",
            "title":"phoneNo",
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
            "SEGMENT_ID",
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 指示Experience Platform目录中目标的标题。 |
| `description` | 字符串 | 在Experience Platform目标目录中，提供目标卡的描述。 目标不超过4-5句。 |
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 首次配置目标时。 |
| `maxProfileAttributes` | 字符串 | 指示客户可导出到目标的配置文件属性的最大数量。 默认值为 `2000`。 |
| `maxIdentityAttributes` | 字符串 | 指示客户可导出到目标的身份命名空间的最大数量。 默认值为 `10`。 |

{style=&quot;table-layout:auto&quot;}

## 客户身份验证配置 {#customer-authentication-configurations}

目标配置中的此部分将生成 [配置新目标](/help/destinations/ui/connect-destination.md) Experience Platform用户界面中的页面，用户可将Experience Platform连接到他们与您的目标拥有的帐户。

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

取决于 [身份验证选项](authentication-configuration.md##supported-authentication-types) 您在 `authType` 字段中，将为用户生成Experience Platform页面，如下所示：

### Amazon S3身份验证 {#s3}

配置Amazon S3身份验证类型时，需要用户输入S3凭据。

![UI通过S3身份验证呈现](assets/s3-authentication-ui.png)

### Azure Blob身份验证  {#blob}

配置Azure Blob身份验证类型时，需要用户输入连接字符串。

![UI通过Blob身份验证呈现](assets/blob-authentication-ui.png)

### 具有密码身份验证的SFTP

使用密码身份验证类型配置SFTP时，用户需要输入SFTP用户名和密码，以及SFTP域和端口（默认端口为22）。

![UI通过SFTP进行密码身份验证来呈现](assets/sftp-password-authentication-ui.png)

### 通过SSH密钥身份验证的SFTP

使用SSH密钥身份验证类型配置SFTP时，需要用户输入SFTP用户名和SSH密钥，以及SFTP域和端口（默认端口为22）。

![通过SFTP通过SSH密钥身份验证来呈现UI](assets/sftp-key-authentication-ui.png)

## 客户数据字段 {#customer-data-fields}

在Experience PlatformUI中连接到目标时，使用此部分要求用户填写特定于您目标的自定义字段。

在以下示例中， `customerDataFields` 要求用户输入其目标的名称，并提供 [!DNL Amazon S3] 存储段名称和文件夹路径，以及压缩类型、文件格式和其他几个文件导出选项。

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中可看到该字段。 |
| `description` | 字符串 | 为自定义字段提供描述。 |
| `type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为 `string`, `object`, `integer`. |
| `isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请输入 `^[A-Za-z]+$` 中。 |
| `enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `default` | 字符串 | 定义 `enum` 列表。 |

{style=&quot;table-layout:auto&quot;}

## UI属性 {#ui-attributes}

此部分引用上述配置中的UI元素，Adobe应在Adobe Experience Platform用户界面中将其用于您的目标。

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `documentationLink` | 字符串 | 指 [目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您的目标名称。 对于名为Moviestar的目标，您将使用 `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读 [目标类别](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). 使用以下任一值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | 字符串 | 您在其中托管要在目标目录卡中显示的图标的URL。 |
| `connectionType` | 字符串 | 连接类型，具体取决于目标。 支持的值： <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | 布尔型 | 指示目标连接是否包含在 [流运行UI](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). 将此参数设置为 `true`: <ul><li>的 **[!UICONTROL 上次数据流运行日期]** 和 **[!UICONTROL 上次数据流运行状态]** 显示在目标浏览页面中。</li><li>的 **[!UICONTROL 数据流运行]** 和 **[!UICONTROL 激活数据]** 选项卡。</li></ul> |
| `monitoringSupported` | 布尔型 | 指示目标连接是否包含在 [监控UI](../ui/destinations-workspace.md#browse). 将此参数设置为 `true`, **[!UICONTROL 在监控中查看]** 选项。 |
| `frequency` | 字符串 | 是指目标支持的数据导出类型。 设置为 `Batch` （对于基于文件的目标）。 |

{style=&quot;table-layout:auto&quot;}

## 目标投放 {#destination-delivery}

```json
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
   ]
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authenticationRule` | 字符串 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过以下任一方法登录您的系统： <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 [凭据](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `destinationServerId` | 字符串 | 的 `instanceId` 的 [目标服务器配置](./destination-server-api.md) 用于此目标。 |

{style=&quot;table-layout:auto&quot;}

## 区段映射配置 {#segment-mapping}

目标配置的此部分与区段元数据（如区段名称或ID）在Experience Platform与目标之间共享的方式相关。

通过 `audienceTemplateId`，此部分还会将此配置与 [受众元数据配置](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段名称。 |
| `mapExperiencePlatformSegmentId` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段ID。 |
| `mapUserInput` | 布尔型 | 控制用户是否在目标激活工作流中输入区段映射ID。 |
| `audienceTemplateId` | 布尔型 | 的 `instanceId` 的 [受众元数据模板](./audience-metadata-management.md) 用于此目标。 要设置受众元数据模板，请阅读 [受众元数据API参考](./audience-metadata-api.md). |

## 映射步骤中的架构配置 {#schema-configuration}

在中使用参数 `schemaConfig` 以启用目标激活工作流的映射步骤。 通过使用下面描述的参数，您可以确定Experience Platform用户是否可以将配置文件属性和/或身份映射到基于文件的目标。

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
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
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `profileFields` | 数组 | 添加预定义 `profileFields`，则Experience Platform用户可以选择将平台属性映射到目标中的预定义属性。 |
| `profileRequired` | 布尔型 | 使用 `true` 如上面的示例配置所示，用户应该能够在目标侧将配置文件属性从Experience Platform映射到自定义属性。 |
| `segmentRequired` | 布尔型 | 始终使用 `segmentRequired:true`. |
| `identityRequired` | 布尔型 | 使用 `true` 用户应能够将身份命名空间从Experience Platform映射到所需的架构。 |

{style=&quot;table-layout:auto&quot;}

### 映射步骤中的动态架构配置 {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK支持合作伙伴定义的模式。 合作伙伴定义的架构允许用户将配置文件属性和标识映射到目标合作伙伴定义的自定义架构，与 [流目标](destination-configuration.md#schema-configuration) 工作流。

在中使用参数  `dynamicSchemaConfig` 定义您自己的架构，以便Platform配置文件属性和/或身份可以映射到该架构。

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `profileRequired` | 布尔型 | 使用 `true` 如上面的示例配置所示，用户应该能够在目标侧将配置文件属性从Experience Platform映射到自定义属性。 |
| `segmentRequired` | 布尔型 | 始终使用 `segmentRequired:true`. |
| `identityRequired` | 布尔型 | 使用 `true` 用户应能够将身份命名空间从Experience Platform映射到所需的架构。 |
| `destinationServerId` | 字符串 | 的 `instanceId` 的 [目标服务器配置](./destination-server-api.md) 用于此目标。 |
| `authenticationRule` | 字符串 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过以下任一方法登录您的系统： <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 [凭据](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `value` | 字符串 | 要在Experience Platform用户界面中的映射步骤中显示的架构名称。 |
| `responseFormat` | 字符串 | 始终设置为 `SCHEMA` 定义自定义架构时。 |

{style=&quot;table-layout:auto&quot;}

## 身份和属性 {#identities-and-attributes}

此部分中的参数可确定目标接受的身份。 此配置还会在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Experience Platform用户界面的中，用户可将身份和属性从其XDM架构映射到目标中的架构。


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

您必须指明 [!DNL Platform] 标识客户能够导出到您的目标。 例如 [!DNL Experience Cloud ID]，经过哈希处理的电子邮件，设备ID([!DNL IDFA], [!DNL GAID])。 这些值包括 [!DNL Platform] 客户可以映射到来自您目标的身份命名空间的身份命名空间。 您还可以指示客户是否可以将自定义命名空间映射到您的目标支持的身份。

身份命名空间不需要 [!DNL Platform] 和你的目的地。
例如，客户可以映射 [!DNL Platform] [!DNL IDFA] 命名空间 [!DNL IDFA] 命名空间，或者它们可以映射相同的 [!DNL Platform] [!DNL IDFA] 命名空间 [!DNL Customer ID] 命名空间。

## 批量配置 {#batch-configuration}

本节将介绍上述配置中的文件导出设置，该Adobe应在Adobe Experience Platform用户界面中用于您的目标。

```json
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
         "SEGMENT_ID",
         "DATETIME"
      ],
      "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
   }
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `allowMandatoryFieldSelection` | 布尔型 | 设置为 `true` 以允许客户指定哪些配置文件属性是必需的。 默认值为 `false`。请参阅 [必需属性](../ui/activate-batch-profile-destinations.md#mandatory-attributes) 以了解更多信息。 |
| `allowDedupeKeyFieldSelection` | 布尔型 | 设置为 `true` 允许客户指定重复数据删除键。 默认值为 `false`。请参阅 [重复数据删除键](../ui/activate-batch-profile-destinations.md#deduplication-keys) 以了解更多信息。 |
| `defaultExportMode` | 枚举 | 定义默认的文件导出模式。 支持的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 默认值为 `DAILY_FULL_EXPORT`。请参阅 [批量激活文档](../ui/activate-batch-profile-destinations.md#scheduling) 有关文件导出计划的详细信息。 |
| `allowedExportModes` | 列表 | 定义客户可用的文件导出模式。 支持的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 列表 | 定义客户可用的文件导出频率。 支持的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 枚举 | 定义默认文件导出频率。支持的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 默认值为 `DAILY`。 |
| `defaultStartTime` | 字符串 | 定义文件导出的默认开始时间。 使用24小时文件格式。 默认值为“00:00”。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字符串 | *必需*. 可供用户选择的可用文件名宏列表。 这可确定要将哪些项目附加到导出的文件名（区段ID、组织名称、导出日期和时间等）中。 设置 `defaultFilename`，请确保避免复制宏。 <br><br>支持的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>无论您定义宏的顺序如何，Experience PlatformUI都将始终按此处显示的顺序显示宏。 <br><br> 如果 `defaultFilename` 为空， `allowedFilenameAppendOptions` 列表必须至少包含一个宏。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字符串 | *必需*. 用户可取消选中的预选默认文件名宏。<br><br> 此列表中的宏是 `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | 字符串 | *可选*. 为导出的文件定义默认的文件名宏。 用户无法覆盖这些内容。 <br><br>定义的任何宏 `allowedFilenameAppendOptions` 将在 `defaultFilename` 宏。 <br><br>如果 `defaultFilename` 为空，则必须在 `allowedFilenameAppendOptions`. |


### 文件名配置 {#file-name-configuration}

使用文件名配置宏来定义导出的文件名应包含的内容。 下表中的宏描述了在 [文件名配置](../ui/activate-batch-profile-destinations.md#file-names) 屏幕。

作为最佳实践，您应始终包含 `SEGMENT_ID` 宏。 区段ID是唯一的，因此将它们包含在文件名中是确保文件名也唯一的最佳方法。

| 宏 | UI标签 | 描述 | 示例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目标] | UI中的目标名称。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 区段ID] | 平台生成的唯一区段ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 区段名称] | 用户定义的区段名称 | VIP订阅者 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目标ID] | 目标实例的唯一、平台生成的ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目标名称] | 目标实例的用户定义的名称。 | 我2022年的广告去向 |
| `ORGANIZATION_NAME` | [!UICONTROL 组织名称] | Adobe Experience Platform中的客户组织名称。 | 我的组织名称 |
| `SANDBOX_NAME` | [!UICONTROL 沙盒名称] | 客户使用的沙盒的名称。 | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和时间] | `DATETIME` 和 `TIMESTAMP` 这两种格式都定义了文件的生成时间，但格式不同。 <br><br><ul><li>`DATETIME` 使用以下格式：YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP` 使用10位Unix格式。 </li></ul> `DATETIME` 和 `TIMESTAMP` 互斥，且不能同时使用。 | <ul><li>`DATETIME`:20220509_210543</li><li>`TIMESTAMP`:1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自定义文本] | 要包含在文件名中的用户定义的自定义文本。 不能在中使用 `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和时间] | 生成文件时的10位时间戳（Unix格式）。 | 1652131584 |


![显示带有预选宏的文件名配置屏幕的UI图像](assets/file-name-configuration.png)

上图中显示的示例使用以下文件名宏配置：

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## 历史用户档案资格 {#profile-backfill}

您可以使用 `backfillHistoricalProfileData` 参数来确定是否应将历史配置文件资格导出到您的目标。

```json
   "backfillHistoricalProfileData":true
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。 <br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |

## 此配置如何连接目标的所有必需信息 {#connecting-all-configurations}

您的某些目标设置必须通过 [目标服务器](./server-and-file-configuration.md) 或 [受众元数据配置](./audience-metadata-management.md). 此处描述的目标配置通过引用以下两个其他配置来连接所有这些设置：

* 使用 `destinationServerId` 引用为目标设置的目标服务器和模板配置。
* 使用 `audienceMetadataId` 引用为您的目标设置的受众元数据配置。
