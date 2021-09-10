---
description: 本页列出并介绍了您可以使用“/authoring/destinations” API端点执行的所有API操作。
title: 目标API端点操作
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '2381'
ht-degree: 4%

---

# 目标端点API操作 {#destination-configuration}

>[!IMPORTANT]
>
>**API端点**:  `platform.adobe.io/data/core/activation/authoring/destinations`

本页列出并描述了可使用`/authoring/destinations` API端点执行的所有API操作。 有关此端点支持的功能的说明，请阅读[目标配置](./destination-configuration.md)。

## 目标API操作快速入门 {#get-started}

在继续操作之前，请查看[快速入门指南](./getting-started.md) ，了解成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 为目标创建配置 {#create}

通过向`/authoring/destinations`端点发出POST请求，可以创建新的目标配置。

**API格式**


```http
POST /authoring/destinations
```

**请求**

以下请求会创建一个新的目标配置，该配置由有效负载中提供的参数进行配置。 以下负载包括`/authoring/destinations`端点接受的所有参数。 请注意，您不必在调用中添加所有参数，并且该模板可根据您的API要求进行自定义。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
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
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。首次配置目标时，请使用`TEST`。 |
| `customerAuthenticationConfigurations` | 字符串 | 指示用于向服务器验证Experience Platform客户的配置。 有关已接受的值，请参阅下面的`authType`。 |
| `customerAuthenticationConfigurations.authType` | 字符串 | 接受的值为`OAUTH2, BEARER`。 |
| `customerDataFields.name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `customerDataFields.type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为`string`、`object`、`integer` |
| `customerDataFields.title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中看到该字段 |
| `customerDataFields.description` | 字符串 | 为自定义字段提供描述。 |
| `customerDataFields.isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `customerDataFields.enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `customerDataFields.pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请在此字段中输入`^[A-Za-z]+$`。 |
| `uiAttributes.documentationLink` | 字符串 | 指目标的[目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog)中的文档页面。 使用`http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是目标的名称。 对于名为Moviestar的目标，您应使用`http://www.adobe.com/go/destinations-moviestar-en`。 |
| `uiAttributes.category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读[目标类别](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用以下任一值：`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 |
| `uiAttributes.connectionType` | 字符串 | `Server-to-server` 是当前唯一可用的选项。 |
| `uiAttributes.frequency` | 字符串 | `Streaming` 是当前唯一可用的选项。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布尔型 | 指示您的目标是否接受标准配置文件属性。 通常，这些属性会在我们的合作伙伴文档中突出显示。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布尔型 | 指示客户是否可以在您的目标中设置自定义命名空间。 |
| `identityNamespaces.externalId.allowedAttributesTransformation` | 字符串 | _示例配置中未显示_。例如，当[!DNL Platform]客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件时，便会使用。 在这里，您将提供需要应用的转换（例如，将电子邮件转换为小写，然后再转换为哈希）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | _示例配置中未显示_。用于平台接受[标准身份命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces)（例如IDFA）时的情况，因此您可以限制Platform用户仅选择这些身份命名空间。 <br> 使用时，您 `acceptedGlobalNamespaces`可以使用小 `"requiredTransformation":"sha256(lower($))"` 写和哈希电子邮件地址或电话号码。要查看此参数的使用方式，请在[更新目标配置](./destination-configuration-api.md#update)下的更多部分中查看配置。 |
| `destinationDelivery.authenticationRule` | 字符串 | 指示[!DNL Platform]客户如何连接到您的目标。 接受的值为`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。 <br> <ul><li>如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统，请使用`CUSTOMER_AUTHENTICATION`。 例如，如果您还在`customerAuthenticationConfigurations`中选择了`authType: OAUTH2`或`authType:BEARER`，则可以选择此选项。 </li><li> 如果Adobe与目标之间存在全局身份验证系统，且[!DNL Platform]客户不需要提供任何身份验证凭据即可连接到您的目标，则使用`PLATFORM_AUTHENTICATION`。 在这种情况下，必须使用[Credentials](./credentials-configuration.md)配置创建凭据对象。 </li><li>如果向目标平台发送数据不需要任何身份验证，则使用`NONE`。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字符串 | 用于此目标的[目标服务器模板](./destination-server-api.md)的`instanceId`。 |
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。<br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布尔型 | 控制用户是否在目标激活工作流中输入区段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段名称。 |
| `segmentMappingConfig.audienceTemplateId` | 布尔型 | 用于此目标的[受众元数据模板](./audience-metadata-api.md)的`instanceId`。 |
| `schemaConfig.profileFields` | 数组 | 如上面的配置所示，当您添加预定义的`profileFields`时，用户将可以选择将Experience Platform属性映射到目标侧的预定义属性。 |
| `schemaConfig.profileRequired` | 布尔型 | 如果用户应该能够将配置文件属性从Experience Platform映射到目标侧的自定义属性，请使用`true` ，如上面的示例配置中所示。 |
| `schemaConfig.segmentRequired` | 布尔型 | 始终使用`segmentRequired:true`。 |
| `schemaConfig.identityRequired` | 布尔型 | 如果用户应能够将身份命名空间从Experience Platform映射到所需的架构，请使用`true`。 |
| `aggregation.aggregationType` | - | 选择 `BEST_EFFORT` 或 `CONFIGURABLE_AGGREGATION`。虽然上述示例配置包括这两种聚合类型，但您只需为目标选择其中一种聚合类型。 |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | 整数 | Experience Platform可以在一个HTTP调用中聚合多个导出的配置文件。 指定您的端点在单个HTTP调用中应接收的最大配置文件数。 请注意，这是一种尽力的聚合。 例如，如果您指定值100,Platform可能会在一次调用中发送任意数量小于100的用户档案。 <br> 如果您的服务器不接受每个请求的多个用户，请将此值设置为1。 |
| `aggregation.bestEffortAggregation.splitUserById` | 布尔型 | 如果目标的调用应按身份进行拆分，则使用此标记。 如果服务器在给定的命名空间中每次调用仅接受一个标识，则将此标记设置为`true`。 |
| `aggregation.configurableAggregation.splitUserById` | 布尔型 | 如果目标的调用应按身份进行拆分，则使用此标记。 如果服务器在给定的命名空间中每次调用仅接受一个标识，则将此标记设置为`true`。 |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | 整数 | *最大值：3600*。这与`maxNumEventsInBatch`一起确定Experience Platform在向端点发送API调用之前应等待多长时间。 <br> 例如，如果您对两个参数使用最大值，则Experience Platform将等待3600秒或直到有10.000个符合条件的配置文件才进行API调用，以先发生的为准。 |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | 整数 | *最大值：1000*。请参阅上方的`maxBatchAgeInSecs`。 |
| `aggregation.configurableAggregation.aggregationKey` | 布尔型 | 允许您根据以下参数聚合映射到目标的导出配置文件：<br> <ul><li>区段ID</li><li> 区段状态 </li><li> 标识命名空间 </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | 布尔型 | 如果要按区段ID对导出到目标的配置文件进行分组，请将此参数设置为`true`。 |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | 布尔型 | 如果要按区段ID和区段状态对导出到目标的配置文件进行分组，则必须同时设置`includeSegmentId:true`和`includeSegmentStatus:true`。 |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | 布尔型 | 如果要按身份命名空间对导出到目标的用户档案进行分组，请将此参数设置为`true`。 |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布尔型 | 使用此参数可指定是否要将导出的用户档案聚合到单个身份（GAID、IDFA、电话号码、电子邮件等）的组中。 |
| `aggregation.configurableAggregation.aggregationKey.groups` | 字符串 | 如果要按身份命名空间的组对导出到目标的配置文件进行分组，请创建身份组列表。 例如，您可以使用示例中的配置，将包含IDFA和GAID移动标识符的用户档案合并到对目标的一次调用中，以及将电子邮件合并到另一个调用中。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回HTTP状态200，其中包含新创建的目标配置的详细信息。

## 列出目标配置 {#retrieve-list}

您可以通过向`/authoring/destinations`端点发出GET请求，来检索IMS组织的所有目标配置的列表。

**API格式**


```http
GET /authoring/destinations
```

**请求**

以下请求将根据IMS组织和沙盒配置，检索您有权访问的目标配置列表。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

以下响应会根据您使用的IMS组织ID和沙盒名称，返回HTTP状态200，其中包含您有权访问的目标配置列表。 一个`instanceId`对应于一个目标的模板。 响应因简短而被截断。

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
         "aggregation":{
            "aggregationType":"CONFIGURABLE_AGGREGATION",
            "configurableAggregation":{
               "splitUserById":true,
               "maxBatchAgeInSecs":0,
               "maxNumEventsInBatch":0,
               "aggregationKey":{
                  "includeSegmentId":true,
                  "includeSegmentStatus":true,
                  "includeIdentity":true,
                  "oneIdentityPerGroup":false,
                  "groups":[
                     {
                        "namespaces":[
                           "IDFA",
                           "GAID"
                        ]
                     },
                     {
                        "namespaces":[
                           "EMAIL"
                        ]
                     }
                  ]
               }
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
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
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。首次配置目标时，请使用`TEST`。 |
| `customerAuthenticationConfigurations` | 字符串 | 指示用于向服务器验证Experience Platform客户的配置。 有关已接受的值，请参阅下面的`authType`。 |
| `customerAuthenticationConfigurations.authType` | 字符串 | 接受的值为`OAUTH2, BEARER`。 |
| `customerDataFields.name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `customerDataFields.type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为`string`、`object`、`integer` |
| `customerDataFields.title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中看到该字段 |
| `customerDataFields.description` | 字符串 | 为自定义字段提供描述。 |
| `customerDataFields.isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `customerDataFields.enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `customerDataFields.pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请在此字段中输入`^[A-Za-z]+$`。 |
| `uiAttributes.documentationLink` | 字符串 | 指目标的[目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog)中的文档页面。 使用`http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是目标的名称。 对于名为Moviestar的目标，您应使用`http://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读[目标类别](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories)。 使用以下任一值：`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | 字符串 | `Server-to-server` 是当前唯一可用的选项。 |
| `uiAttributes.frequency` | 字符串 | `Streaming` 是当前唯一可用的选项。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布尔型 | 指示您的目标是否接受标准配置文件属性。 通常，这些属性会在我们的合作伙伴文档中突出显示。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布尔型 | 指示客户是否可以在您的目标中设置自定义命名空间。 在Adobe Experience Platform中阅读有关[自定义命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces)的更多信息。 |
| `identityNamespaces.externalId.allowedAttributesTransformation` | 字符串 | _示例配置中未显示_。例如，当[!DNL Platform]客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件时，便会使用。 在这里，您将提供需要应用的转换（例如，将电子邮件转换为小写，然后再转换为哈希）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | _示例配置中未显示_。用于平台接受[标准身份命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces)（例如IDFA）时的情况，因此您可以限制Platform用户仅选择这些身份命名空间。 |
| `destinationDelivery.authenticationRule` | 字符串 | 指示[!DNL Platform]客户如何连接到您的目标。 接受的值为`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。 <br> <ul><li>如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统，请使用`CUSTOMER_AUTHENTICATION`。 例如，如果您还在`customerAuthenticationConfigurations`中选择了`authType: OAUTH2`或`authType:BEARER`，则可以选择此选项。 </li><li> 如果Adobe与目标之间存在全局身份验证系统，且[!DNL Platform]客户不需要提供任何身份验证凭据即可连接到您的目标，则使用`PLATFORM_AUTHENTICATION`。 在这种情况下，必须使用[Credentials](./credentials-configuration.md)配置创建凭据对象。 </li><li>如果向目标平台发送数据不需要任何身份验证，则使用`NONE`。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字符串 | 用于此目标的[目标服务器模板](./destination-server-api.md)的`instanceId`。 |
| `inputSchemaId` | 字符串 | 此字段是自动生成的，不需要您输入。 |
| `destConfigId` | 字符串 | 此字段是自动生成的，不需要您输入。 |
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。<br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |
| `segmentMappingConfig.mapUserInput` | 布尔型 | 控制用户是否在目标激活工作流中输入区段映射ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布尔型 | 控制目标激活工作流中的区段映射ID是否为Experience Platform区段名称。 |
| `segmentMappingConfig.audienceTemplateId` | 布尔型 | 用于此目标的[受众元数据模板](./audience-metadata-management.md)的`instanceId`。 要设置受众元数据模板，请阅读[受众元数据API引用](./audience-metadata-api.md)。 |

{style=&quot;table-layout:auto&quot;}

## 更新现有目标配置 {#update}

您可以通过向`/authoring/destinations`端点发出PUT请求并提供要更新的目标配置的实例ID来更新现有的目标配置。 在调用的正文中，提供更新的目标配置。

**API格式**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目标配置的ID。 |

**请求**

以下请求会更新现有目标配置，该配置由有效负载中提供的参数配置。 在以下示例调用中，我们将更新之前](./destination-configuration-api.md#create)创建的配置[，以现在接受GAID、IDFA和哈希电子邮件标识符作为身份命名空间。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "backfillHistoricalProfileData":true
}
```

## 检索特定目标配置 {#get}

通过向`/authoring/destinations`端点发出GET请求并提供要检索的目标配置的实例ID，可以检索有关特定目标配置的详细信息。

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed",
   "backfillHistoricalProfileData":true
}
```


## 删除特定目标配置 {#delete}

您可以通过向`/authoring/destinations`端点发出DELETE请求并提供您希望在请求路径中删除的目标配置的ID来删除指定的目标配置。

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 要删除的目标配置的`id`。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回HTTP状态200以及空的HTTP响应。

## API错误处理

目标SDK API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅平台疑难解答指南中的[API状态代码](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[请求标头错误](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道如何使用`/authoring/destinations` API端点配置目标。 请阅读[如何使用目标SDK配置目标](./configure-destination-instructions.md) ，以了解此步骤在配置目标过程中的适用位置。
