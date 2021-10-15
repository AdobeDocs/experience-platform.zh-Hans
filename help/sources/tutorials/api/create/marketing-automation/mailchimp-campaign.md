---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 使用流服务API为MailChimp营销活动创建数据流
topic-legacy: tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform与MailChimp Campaign连接。
source-git-commit: c8d94af6185785a0e4bfce9889c04405ed223b1f
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 2%

---

# 使用流服务API为[!DNL MailChimp Campaign]创建数据流

以下教程将指导您完成创建源连接和数据流以使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[!DNL MailChimp Campaign]数据导入平台的步骤。

## 先决条件

在使用OAuth 2刷新代码将[!DNL MailChimp]连接到Adobe Experience Platform之前，必须先检索[!DNL MailChimp.]的访问令牌。有关查找访问令牌的详细说明，请参阅[[!DNL MailChimp] OAuth 2指南](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/)。

## 创建基本连接 {#base-connection}

在检索到[!DNL MailChimp]身份验证凭据后，您现在可以开始创建数据流以将[!DNL MailChimp Campaign]数据导入平台的过程。 创建数据流的第一步是创建基本连接。

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

[!DNL MailChimp] 支持基本身份验证和OAuth 2刷新代码。有关如何使用这两种身份验证类型进行身份验证的指导，请参阅以下示例。

### 使用基本身份验证创建[!DNL MailChimp]基本连接

要使用基本身份验证创建[!DNL MailChimp]基本连接，请向[!DNL Flow Service] API的`/connections`端点发出POST请求，同时为`host`、`authorizationTestUrl`、`username`和`password`提供凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL MailChimp]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with basic authentication",
      "description": "MailChimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基本连接的名称。 确保基本连接的名称具有描述性，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 源的连接规范ID。 在通过[!DNL Flow Service] API注册并批准源后，即可检索此ID。 |
| `auth.specName` | 用于将源连接到平台的身份验证类型。 |
| `auth.params.host` | 用于连接到[!DNL MailChimp] API的根URL。 根URL的格式为`https://{DC}.api.mailchimp.com`，其中`{DC}`表示与您的帐户对应的数据中心。 |
| `auth.params.authorizationTestUrl` | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则在创建源连接步骤期间会自动检查凭据。 |
| `auth.params.username` | 与您的[!DNL MailChimp]帐户对应的用户名。 基本身份验证需要此功能。 |
| `auth.params.password` | 与您的[!DNL MailChimp]帐户对应的密码。 基本身份验证需要此功能。 |

**响应**

成功的响应返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中，需要此ID才能浏览源的文件结构和内容。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### 使用OAuth 2刷新代码创建[!DNL MailChimp]基本连接

要使用OAuth 2刷新代码创建[!DNL MailChimp]基本连接，请在提供`host`、`authorizationTestUrl`和`accessToken`的凭据时向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL MailChimp]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基本连接的名称。 确保基本连接的名称具有描述性，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 源的连接规范ID。 使用[!DNL Flow Service] API注册源后，可以检索此ID。 |
| `auth.specName` | 用于向平台验证源的验证类型。 |
| `auth.params.host` | 用于连接到[!DNL MailChimp] API的根URL。 根URL的格式为`https://{DC}.api.mailchimp.com`，其中`{DC}`表示与您的帐户对应的数据中心。 |
| `auth.params.authorizationTestUrl` | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则在创建源连接步骤期间会自动检查凭据。 |
| `auth.params.accessToken` | 用于验证源的相应访问令牌。 基于OAuth的身份验证需要此设置。 |

**响应**

成功的响应返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中，需要此ID才能浏览源的文件结构和内容。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 探索您的来源 {#explore}

使用上一步中生成的基本连接ID，您可以通过执行GET请求来浏览文件和目录。 执行GET请求以浏览源的文件结构和内容时，必须包括下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步中生成的基本连接ID。 |
| `{OBJECT_TYPE}` | 要浏览的对象的类型。 对于REST源，此值默认为`rest`。 |
| `{OBJECT}` | 要浏览的对象。 |
| `{FILE_TYPE}` | 仅当查看特定目录时，才需要此参数。 其值表示要浏览的目录的路径。 |
| `{PREVIEW}` | 一个布尔值，用于定义连接的内容是否支持预览。 |
| `{SOURCE_PARAMS}` | `campaign_id`的base64编码字符串。 |

>[!TIP]
>
>要检索`{SOURCE_PARAMS}`的已接受的format-type，必须在base64中对整个`campaignId`字符串进行编码。 例如，在base64中编码的`{"campaignId": "c66a200cda"}`等于`eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回查询文件的结构。

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## 创建源连接 {#source-connection}

您可以通过向[!DNL Flow Service] API发出POST请求来创建源连接。 源连接由连接ID、源数据文件的路径和连接规范ID组成。

要创建源连接，还必须为数据格式属性定义枚举值。

为基于文件的源使用以下枚举值：

| 数据格式 | 枚举值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 镶木 | `parquet` |

对于所有基于表的源，将值设置为`tabular`。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下请求为[!DNL MailChimp]创建源连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 确保源连接的名称具有描述性，因为您可以使用该名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | [!DNL MailChimp]的基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 要摄取的[!DNL MailChimp]数据的格式。 |
| `params.campaignId` | [!DNL MailChimp]营销活动ID标识特定的[!DNL MailChimp]营销活动，然后允许您向列表/受众发送电子邮件。 |

**响应**

成功的响应会返回新创建源连接的唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## 创建目标XDM架构 {#target-schema}

要在Platform中使用源数据，必须创建目标架构以根据您的需求构建源数据。 然后，目标架构用于创建包含源数据的Platform数据集。

通过对[架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

有关如何创建目标XDM架构的详细步骤，请参阅关于[使用API](../../../../../xdm/api/schemas.md)创建架构的教程。

### 创建目标数据集 {#target-dataset}

通过向[Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)执行POST请求，并提供有效负载中目标架构的ID，可以创建目标数据集。

有关如何创建目标数据集的详细步骤，请参阅关于[使用API](../../../../../catalog/api/create-dataset.md)创建数据集的教程。

## 创建目标连接 {#target-connection}

目标连接表示所摄取数据所登陆目标的连接。 要创建目标连接，必须提供与[!DNL Data Lake]对应的固定连接规范ID。 此ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

现在，您拥有目标架构（目标数据集）的唯一标识符，以及与[!DNL Data Lake]的连接规范ID。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含集客源数据的数据集。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求为[!DNL MailChimp]创建目标连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称具有描述性，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 与[!DNL Data Lake]对应的连接规范ID。 此固定ID是：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 要引入平台的[!DNL MailChimp]数据的格式。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |


**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此ID是后续步骤所必需的。

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>[!DNL MailChimp Campaign]当前不支持数据准备函数。

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## 创建流 {#flow}

将[!DNL MailChimp]数据引入平台的最后一个步骤是创建数据流。 现在，您已准备以下必需值：

* [源连接ID](#source-connection)
* [Target连接ID](#target-connection)

数据流负责从源中调度和收集数据。 通过在有效负载中提供先前提到的值时执行POST请求，可以创建数据流。

要计划摄取，您必须首先将开始时间值设置为以秒为单位的新纪元时间。 然后，您必须将频率值设置为以下五个选项之一：`once`、`minute`、`hour`、`day`或`week`。 间隔值指定两个连续摄取与创建一次性摄取(`once`)之间的周期，不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于`15`。


**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 数据流的名称。 确保数据流的名称具有描述性，因为您可以使用该名称查找有关数据流的信息。 |
| `description` | （可选）可包含的属性，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID是：`6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流量规范ID的相应版本。 此值默认为`1.0`。 |
| `sourceConnectionIds` | 在前面的步骤中生成的[源连接ID](#source-connection)。 |
| `targetConnectionIds` | 在前面的步骤中生成的[目标连接ID](#target-connection)。 |
| `scheduleParams.startTime` | 首次摄取数据开始时的指定开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为`once`时，不需要间隔，对于其他频率值，间隔应大于或等于`15`。 |

**响应**

成功的响应会返回新创建数据流的ID(`id`)。 您可以使用此ID来监视、更新或删除您的数据流。

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## 监控数据流

创建数据流后，您可以监视通过其摄取的数据，以查看有关流量运行、完成状态和错误的信息。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**请求**

以下请求检索现有数据流的规范。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回有关流运行的详细信息，包括有关其创建日期、源连接和目标连接以及流运行的唯一标识符(`id`)的信息。

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "MailChimp Campaign dataflow",
            "description": "MailChimp Campaign dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "etag": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "sourceConnectionIds": [
                "d6557bf1-7347-415f-964c-9316bd4cbf56"
            ],
            "targetConnectionIds": [
                "9463fe9c-027d-4347-a423-894fcd105647"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
                        "connectionSpec": {
                            "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "9601747c-6874-4c02-bb00-5732a8c43086",
                            "connectionSpec": {
                                "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "9463fe9c-027d-4347-a423-894fcd105647",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633377385",
                "frequency": "minute",
                "interval": 15
            },
            "runs": "/flows/be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da/runs",
            "lastOperation": {
                "started": 1633377421476,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "84f95788-3e83-4ce0-8e45-c0a89117c6f1",
                "state": "failed",
                "startedAtUTC": 1633377445979,
                "completedAtUTC": 1633377487082
            }
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `items` | 包含与您的特定流程运行关联的元数据的单个有效负荷。 |
| `id` | 显示与数据流对应的ID。 |
| `state` | 显示数据流的当前状态。 |
| `inheritedAttributes` | 包含定义流的属性，如其相应的基连接、源连接和目标连接的ID。 |
| `scheduleParams` | 包含有关数据流的摄取计划的信息，如其开始时间（以纪元时间表示）、频率和间隔。 |
| `transformations` | 包含有关应用于数据流的转换属性的信息。 |
| `runs` | 显示流程的相应运行ID。 您可以使用此ID来监视特定流程运行。 |

## 更新数据流

要更新数据流的运行计划、名称和描述，请在提供您要使用的流ID、版本和新计划的同时，向[!DNL Flow Service] API执行PATCH请求。

>[!IMPORTANT]
>
>发出PATCH请求时需要`If-Match`标头。 此标头的值是要更新的连接的唯一版本。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求更新了您的流程运行计划以及数据流的名称和描述。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Campaign Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Campaign Dataflow Updated"
          }
      ]'
```

| 参数 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的流量ID和更新的标记。 在提供流ID的同时，您可以通过向[!DNL Flow Service] API发出GET请求来验证更新。

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 删除数据流

使用现有的流ID，可以通过向[!DNL Flow Service] API执行DELETE请求来删除数据流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要删除的数据流的唯一`id`值。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。 您可以通过尝试对数据流进行查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，表示数据流已被删除。

## 更新连接

要更新连接的名称、说明和凭据，请在提供基本连接ID、版本和要使用的新信息时，向[!DNL Flow Service] API执行PATCH请求。

>[!IMPORTANT]
>
>发出PATCH请求时需要`If-Match`标头。 此标头的值是要更新的连接的唯一版本。

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 要更新的连接的唯一`id`值。 |

**请求**

以下请求提供了新名称和描述以及一组新的凭据，用于更新您与的连接。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Campaign Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Campaign Connection"
      }
  ]'
```

| 参数 | 描述 |
| --------- | ----------- |
| `op` | 操作调用，用于定义更新连接所需的操作。 操作包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的基本连接ID和更新的标记。 在提供连接ID的同时，您可以通过向[!DNL Flow Service] API发出GET请求来验证更新。

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 删除连接

现有基本连接ID后，对[!DNL Flow Service] API执行DELETE请求。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 要删除的基本连接的唯一`id`值。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对连接进行查询(GET)请求来确认删除。
