---
description: 了解如何使用Destination SDK构建的目标配置受众类型。
title: 配置受众数据类型
exl-id: c56fb0f9-adb2-4fb2-ab06-c0398d828600
source-git-commit: 5d84ea1baa96c288d9d37606122e0a41880478b9
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 2%

---

# 配置受众数据类型

使用Destination SDK构建目标连接器时，您可以定义将导出到目标的受众类型。 配置正确的受众数据类型可确保您的目标收到与其预期用例相符的正确数据，无论该数据是用于营销活动、基于帐户的策略还是数据分析。

查看下面的受众数据类型，了解它们之间的差异，并确定集成所需的类型。 然后，请阅读页面上下面进一步部分，了解如何配置目标以导出不同的受众类型。

| 受众数据类型 | 描述 | 用例 |
|---------|----------|---------|
| [人员受众](../../../../segmentation/types/people-audiences.md) | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](../../../../segmentation/types/account-audiences.md) | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](../../../../segmentation/types/prospect-audiences.md) | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](../../../../catalog/datasets/overview.md) | 存储在Adobe Experience Platform数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

支持的受众数据类型取决于您创建的目标类型。
请参阅下表，了解哪些目标类型支持哪些受众数据类型。

| 目标类型 | 人员受众 | 帐户受众 | 潜在客户受众 | 数据集 |
|---------|----------|---------|---------|---------|
| 流式处理 | ✓ | ✓ | X | X |
| 基于文件 | ✓ | ✓ | ✓ | ✓ |

{style="table-layout:auto"}

## `sources`数组 {#sources}

`sources`数组指定目标支持的受众数据类型。 帐户受众、潜在客户受众和数据集导出需要此变量，而人员受众不需要此变量，因为默认情况下支持此类变量。

```json
"sources":[
   "ACCOUNTS" // Specifies that this destination supports account audiences
]
```

`sources`数组接受以下值：

* `"ACCOUNTS"`：指定目标支持导出帐户受众。
* `"UNIFIED_PROFILE_PROSPECTS"`：指定目标支持导出潜在客户受众。
* `"DATASETS"`：指定目标支持数据集的导出。

根据要导出到目标的受众类型，请查看以下部分以了解目标配置示例。

## 导出人员受众 {#people-audiences}

默认情况下，所有目标类型都支持人员受众，因此不需要特定的`sources`值。 要生成支持人员受众的目标，您根本不需要使用`sources`数组，因为这是默认行为。

+++ 支持人员受众的流媒体目标配置示例

这是导出人员受众的流目标的示例。 请注意配置中没有`sources`阵列。”

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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
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

+++

## 导出帐户受众 {#account}

当您要为基于帐户的营销配置[!DNL B2B]目标时，请考虑将帐户受众支持添加到您的目标。 例如，您可以使用基于帐户的受众检索所有帐户的记录，这些帐户没有标题为[!DNL Chief Operating Officer (COO)]或[!DNL Chief Marketing Officer (CMO)]的任何人员的联系信息。

要构建支持导出帐户受众的目标，请将以下配置代码片段添加到您的[目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)。

```json
"sources":[
   "ACCOUNTS" // Specifies that this destination supports account audiences
] 
```

+++ 支持帐户受众的流媒体目标配置示例

```shell {line-numbers="true" highlight="12-14"}
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
   "sources":[
      "ACCOUNTS"
   ],
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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
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

+++

## 导出目标客户受众 {#prospect}

当您想要定位尚未成为客户但与目标受众共享特征的个人时，请考虑向目标添加潜在受众支持。 利用潜在客户配置文件，您可以使用来自可信第三方合作伙伴的属性来补充您的客户配置文件。 有关详细信息，请参阅此[潜在客户用例](../../../../rtcdp/partner-data/prospecting.md)。

要构建支持导出潜在客户受众的目标，请将下面的配置代码段添加到您的[目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)。


```json
"sources":[
   "UNIFIED_PROFILE_PROSPECTS" // Specifies that this destination supports prospect audiences
] 
```

+++ 支持潜在客户的流式目标配置示例

```shell {line-numbers="true" highlight="12-14"}
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
   "sources":[
      "UNIFIED_PROFILE_PROSPECTS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
            "GZIP",
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
            "json",
            "parquet"
         ],
         "default":"parquet"
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
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
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

+++

## 导出数据集 {#datasets}

当您希望导出未按受众兴趣或资格进行分组或构建的原始数据集时，请考虑向目标添加数据集导出支持。 您可以将此数据用于报表、数据科学工作流和许多其他用例。 例如，作为管理员、数据工程师或分析师，您可以从Experience Platform导出数据以与数据仓库同步，在[!DNL BI]分析工具、外部云[!DNL ML]工具中使用，或存储在您的系统中以满足长期存储需求。

要构建支持导出数据集的目标，请将以下配置代码段添加到您的[目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)。

```json
"sources":[
   "DATASETS" // Specifies that this destination supports dataset exports
]
```

+++ 支持数据集导出的基于文件的目标配置示例

```shell {line-numbers="true" highlight="12-14"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with dataset export capability",
   "description":"Amazon S3 destination with dataset export capability",
   "status":"TEST",
   "sources":[
      "DATASETS"
   ],
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
            "GZIP",
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
            "json",
            "parquet"
         ],
         "default":"parquet"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-dataset-export-en",
      "category":"cloudStorage",
      "frequency":"Batch",
      "monitoringSupported":true,
      "flowRunsSupported":true
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"19c8fc89-9b73-4e0f-893e-549410b23f39"
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT"
   },
   "destinationDelivery":[
      {
         "authenticationRule":"PLATFORM_AUTHENTICATION",
         "authenticationId":"2fff57e1-6603-4927-8a9c-147c90839bdb",
         "destinationServerId":"e59de90a-6df6-471a-bd55-11f7bdb52fae"
      }
   ],
   "inputSchemaId":"70d0bd4734cc49c98d48c4b162e9a1b7",
   "schemaConfig":{
      "useCustomerSchemaForAttributeMapping":false,
      "requiredMappingsOnly":false,
      "profileRequired":false,
      "segmentRequired":false,
      "identityRequired":false
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":false,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"FIRST_FULL_THEN_INCREMENTAL",
      "allowedExportModes":[
         
      ],
      "allowedScheduleFrequency":[
         
      ],
      "defaultFrequency":"EVERY_HOUR",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            
         ],
         "defaultFilenameAppendOptions":[
            
         ],
         "defaultFilename":""
      },
      "datasetBatchConfig":{
         "allowedFoldernameAppendOptions":[
            "DESTINATION",
            "DATASET_ID",
            "DATASET_NAME",
            "EXPORT_TIME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFoldernameAppendOptions":[
            "DATASET_ID",
            "EXPORT_TIME"
         ],
         "allowedExportModes":[
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
         ],
         "allowedScheduleFrequency":[
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_12_HOURS",
            "EVERY_8_HOURS",
            "ONCE"
         ]
      },
      "allowDedupKeyFieldSelection":false
   },
   "maxProfileAttributes":9000,
   "maxIdentityAttributes":1000,
   "destConfigId":"069280b7-40fc-490c-85c4-3bcae17b5441",
   "backfillHistoricalProfileData":true
}
```

+++

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何为目标配置受众数据类型。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证配置](customer-authentication.md)
* [OAuth2授权](oauth2-authorization.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
