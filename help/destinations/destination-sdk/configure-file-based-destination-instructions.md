---
description: 本页列出并描述了使用Destination SDK配置基于文件的目标的步骤。
title: （测试版）使用Destination SDK配置基于文件的目标
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 77c80c391ef6677f95af81ef15272380687e6789
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# （测试版）使用Destination SDK配置基于文件的目标

## 概述 {#overview}

>[!IMPORTANT]
>
>使用Adobe Experience Platform Destination SDK配置和提交基于文件的目标目前尚处于测试阶段。 文档和功能可能会发生更改。

本页介绍如何使用 [目标SDK中的配置选项](./configuration-options.md) 和其他Destination SDK功能和API参考文档中的 [基于文件的目标](../../destinations/destination-types.md#file-based). 这些步骤按如下顺序排列。

## 先决条件 {#prerequisites}

在前进到下述步骤之前，请阅读 [Destination SDK入门](./getting-started.md) 页面，以了解有关获取使用Adobe I/OAPI所需的Destination SDK身份验证凭据以及其他先决条件的信息。

## 使用Destination SDK中的配置选项设置目标的步骤 {#steps}

![使用Destination SDK端点的图示步骤](./assets/destination-sdk-steps-batch.png)

## 步骤1:创建服务器和文件配置 {#create-server-file-configuration}

首先，使用 `/destinations-server` 端点（读取） [API参考](./destination-server-api.md))。

下面显示了 [!DNL Amazon S3] 目标。 要配置其他类型的基于文件的目标，请查看其对应的 [服务器配置](server-and-file-configuration.md).

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

## 步骤2:创建目标配置 {#create-destination-configuration}

以下是使用 `/destinations` API端点。 有关此配置的更多信息，请参阅 [目标配置](./file-based-destination-configuration.md).

要将步骤1中的服务器和文件配置连接到此目标配置，请将服务器和模板配置的实例ID添加为 `destinationServerId` 这里。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
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
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## 步骤3:创建受众元数据配置 {#create-audience-metadata-configuration}

对于某些目标，Destination SDK要求您配置受众元数据配置，以编程方式创建、更新或删除目标中的受众。 请参阅 [受众元数据管理](./audience-metadata-management.md) 有关何时需要设置此配置以及如何进行此配置的信息。

如果您使用受众元数据配置，则必须将其连接到在步骤2中创建的目标配置。 将受众元数据配置的实例ID添加到目标配置中，如 `audienceTemplateId`.

## 步骤4:设置身份验证 {#set-up-authentication}

取决于您是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上述目标配置中，您可以使用 `/destination` 或 `/credentials` 端点。

* 如果已选择 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在目标配置中，请参阅以下部分，了解基于文件的目标的Destination SDK支持的身份验证类型：

   * [Amazon S3身份验证](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Azure数据湖存储](authentication-configuration.md#adls)
   * [Google云存储](authentication-configuration.md#gcs)
   * [使用SSH密钥进行SFTP身份验证](authentication-configuration.md#sftp-ssh)
   * [使用密码进行SFTP身份验证](authentication-configuration.md#sftp-password)

* 如果已选择 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，请参阅 [身份验证配置](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## 步骤5:发布目标 {#publish-destination}

配置和测试目标后，请使用 [目标发布API](./destination-publish-api.md) 将配置提交到Adobe以供审核。

## 步骤6:记录目标 {#document-destination}

如果您是独立软件供应商(ISV)或系统集成商(SI)，创建 [产品化集成](./overview.md#productized-custom-integrations)，则使用 [自助文档流程](./docs-framework/documentation-instructions.md) 要在 [Experience Platform目标目录](/help/destinations/catalog/overview.md).
