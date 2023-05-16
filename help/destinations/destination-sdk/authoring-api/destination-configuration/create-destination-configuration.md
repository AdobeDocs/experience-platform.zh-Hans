---
description: 了解如何构建API调用，以通过Adobe Experience Platform Destination SDK创建目标配置。
title: 创建目标配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---


# 创建目标配置

本页介绍了可用于使用创建您自己的目标配置的API请求和有效负载 `/authoring/destinations` API端点。

有关可通过此端点配置的功能的详细说明，请阅读以下文章：

* [客户身份验证配置](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2身份验证](../../functionality/destination-configuration/oauth2-authentication.md)
* [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md)
* [UI属性](../../functionality/destination-configuration/ui-attributes.md)
* [架构配置](../../functionality/destination-configuration/schema-configuration.md)
* [身份命名空间配置](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目标投放](../../functionality/destination-configuration/destination-delivery.md)
* [受众元数据配置](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [受众元数据配置](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [聚合策略](../../functionality/destination-configuration/aggregation-policy.md)
* [批量配置](../../functionality/destination-configuration/batch-configuration.md)
* [历史用户档案资格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标配置API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](../../getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 创建目标配置 {#create}

您可以通过向 `/authoring/destinations` 端点。

>[!TIP]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API格式**

```http
POST /authoring/destinations
```

以下请求会创建新 [!DNL Amazon S3] 目标配置，由有效负载中提供的参数配置。 以下有效负载包括接受的基于文件的目标的所有参数 `/authoring/destinations` 端点。

请注意，您不必向API调用添加所有参数，并且有效负载可根据API要求进行自定义。

+++请求

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
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
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

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 指示Experience Platform目录中目标的标题。 |
| `description` | 字符串 | 提供Adobe将在目标卡的Experience Platform目标目录中使用的描述。 目标不超过4-5句。 ![显示目标描述的Platform UI图像。](../../assets/authoring-api/destination-configuration/destination-description.png "目标描述"){width="100" zoomable="yes"} |
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 首次配置目标时。 |
| `customerAuthenticationConfigurations.authType` | 字符串 | 指示用于向目标服务器验证Experience Platform客户的配置。 请参阅 [客户身份验证配置](../../functionality/destination-configuration/customer-authentication.md) 以详细了解支持的身份验证类型。 |
| `customerDataFields.name` | 字符串 | 为要引入的自定义字段提供名称。 <br/><br/> 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 ![显示客户数据字段的Platform UI图像。](../../assets/authoring-api/destination-configuration/customer-data-fields.png "客户数据字段"){width="100" zoomable="yes"} |
| `customerDataFields.type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为 `string`, `object`, `integer`. <br/><br/> 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 |
| `customerDataFields.title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中可看到该字段。 <br/><br/> 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 |
| `customerDataFields.description` | 字符串 | 为自定义字段提供描述。 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 |
| `customerDataFields.isRequired` | 布尔值 | 指示目标设置工作流中是否需要此字段。 <br/><br/> 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 |
| `customerDataFields.enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 <br/><br/> 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 |
| `customerDataFields.default` | 字符串 | 定义 `enum` 列表。 |
| `customerDataFields.pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请输入 `^[A-Za-z]+$` 中。 <br/><br/> 请参阅 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 以详细了解这些设置。 |
| `uiAttributes.documentationLink` | 字符串 | 指 [目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您的目标名称。 对于名为Moviestar的目标，您将使用 `https://www.adobe.com/go/destinations-moviestar-en`. 请注意，此链接仅在Adobe设置目标处于实时状态且文档已发布后才可用。 <br/><br/> 请参阅 [UI属性](../../functionality/destination-configuration/ui-attributes.md) 以详细了解这些设置。 ![显示文档链接的Platform UI图像。](../../assets/authoring-api/destination-configuration/documentation-url.png "文档URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读 [目标类别](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用以下任一值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> 请参阅 [UI属性](../../functionality/destination-configuration/ui-attributes.md) 以详细了解这些设置。 |
| `uiAttributes.connectionType` | 字符串 | 连接类型，具体取决于目标。 支持的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | 字符串 | 是指目标支持的数据导出类型。 设置为 `Streaming` （对于基于API的集成），或 `Batch` 将文件导出到目标时。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布尔值 | 指示客户是否可以将标准配置文件属性映射到您正在配置的标识。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布尔值 | 指示客户是否可以映射属于 [自定义命名空间](/help/identity-service/namespaces.md#manage-namespaces) 到您配置的标识。 |
| `identityNamespaces.externalId.transformation` | 字符串 | _示例配置中未显示_. 例如，当 [!DNL Platform] 客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件。 在这里，您将提供需要应用的转换（例如，将电子邮件转换为小写，然后再转换为哈希）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 指示 [标准身份命名空间](/help/identity-service/namespaces.md#standard) （例如，IDFA）客户可以映射到您正在配置的身份。 <br> 使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 更改为小写和哈希电子邮件地址或电话号码。 |
| `destinationDelivery.authenticationRule` | 字符串 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统。 例如，如果您还选择了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 [凭据API](../../credentials-api/create-credential-configuration.md) 配置。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字符串 | 的 `instanceId` 的 [目标服务器模板](../destination-server/create-destination-server.md) 用于此目标。 |
| `backfillHistoricalProfileData` | 布尔值 | 控制在将区段激活到目标时是否导出历史配置文件数据。 始终将此参数设置为 `true`. |
| `segmentMappingConfig.mapUserInput` | 布尔值 | 控制用户是否在目标激活工作流中输入区段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布尔值 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布尔值 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段名称。 |
| `segmentMappingConfig.audienceTemplateId` | 布尔值 | 的 `instanceId` 的 [受众元数据模板](../../metadata-api/create-audience-template.md) 用于此目标。 |
| `schemaConfig.profileFields` | 数组 | 添加预定义 `profileFields` 如上面的配置所示，用户将可以选择将Experience Platform属性映射到目标侧的预定义属性。 |
| `schemaConfig.profileRequired` | 布尔值 | 使用 `true` 如上面的示例配置所示，用户应该能够在目标侧将配置文件属性从Experience Platform映射到自定义属性。 |
| `schemaConfig.segmentRequired` | 布尔值 | 始终使用 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 布尔值 | 使用 `true` 如果用户能够将身份命名空间从Experience Platform映射到所需的架构，请执行以下操作。 |

{style="table-layout:auto"}

+++

+++响应

成功响应会返回HTTP状态200，其中包含新创建的目标配置的详细信息。

+++

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何通过Destination SDK创建新目标配置 `/authoring/destinations` API端点。

要进一步了解使用此端点可以执行的操作，请参阅以下文章：

* [检索目标配置](retrieve-destination-configuration.md)
* [更新目标配置](update-destination-configuration.md)
* [删除目标配置](delete-destination-configuration.md)

要了解此端点在目标创作过程中的位置，请参阅以下文章：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
