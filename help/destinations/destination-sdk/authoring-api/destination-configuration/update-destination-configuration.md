---
description: 本页说明了用于通过Adobe Experience Platform Destination SDK更新现有目标配置的API调用。
title: 更新目标配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---


# 更新目标配置

本页介绍了可用于使用更新现有目标配置的API请求和有效负载 `/authoring/destinations` API端点。

>[!TIP]
>
>只有在使用 [发布API](../../publishing-api/create-publishing-request.md) 并提交更新以供Adobe审核。

有关目标配置功能的详细说明，请阅读以下文章：

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

## 更新目标配置 {#update}

您可以更新 [现有](create-destination-configuration.md) 目标配置 `PUT` 请求 `/authoring/destinations` 包含更新有效负载的端点。

>[!TIP]
>
>API端点： `platform.adobe.io/data/core/activation/authoring/destinations`

获取现有目标配置及其对应的 `{INSTANCE_ID}`，请参阅关于 [检索目标配置](retrieve-destination-configuration.md).

**API格式**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目标配置的ID。 获取现有目标配置及其对应的 `{INSTANCE_ID}`，请参阅 [检索目标配置](retrieve-destination-configuration.md). |

+++请求

以下请求会更新我们在中创建的目标 [此示例](create-destination-configuration.md#create) 不同 `filenameConfig` 选项。

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++响应

成功响应会返回HTTP状态200，其中包含更新的目标配置的详细信息。

+++

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何通过Destination SDK更新目标配置 `/authoring/destinations` API端点。

要进一步了解使用此端点可以执行的操作，请参阅以下文章：

* [创建目标配置](create-destination-configuration.md)
* [检索目标配置](retrieve-destination-configuration.md)
* [删除目标配置](delete-destination-configuration.md)