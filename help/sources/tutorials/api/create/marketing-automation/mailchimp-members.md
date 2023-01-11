---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 使用流服务API为Mailchimp成员创建数据流
description: 了解如何使用流服务API将Adobe Experience Platform与MailChimp成员连接。
exl-id: 900d4073-129c-47ba-b7df-5294d25a7219
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 1%

---

# 为创建数据流 [!DNL Mailchimp Members] 使用流量服务API

以下教程将指导您完成创建源连接和要引入的数据流的步骤 [!DNL Mailchimp Members] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 先决条件

连接之前 [!DNL Mailchimp] 要使用OAuth 2刷新代码的Adobe Experience Platform，您必须先检索 [!DNL MailChimp.] 请参阅 [[!DNL Mailchimp] OAuth 2指南](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) 有关查找访问令牌的详细说明。

## 创建基本连接 {#base-connection}

检索到 [!DNL Mailchimp] 身份验证凭据，您现在可以启动创建数据流的过程，以便 [!DNL Mailchimp Members] 数据到平台。 创建数据流的第一步是创建基本连接。

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

[!DNL Mailchimp] 支持基本身份验证和OAuth 2刷新代码。 有关如何使用这两种身份验证类型进行身份验证的指导，请参阅以下示例。

### 创建 [!DNL Mailchimp] 基本连接使用基本身份验证

创建 [!DNL Mailchimp] 基本连接使用基本身份验证，向POST请求 `/connections` 端点 [!DNL Flow Service] API，同时为您的 `authorizationTestUrl`, `username`和 `password`.

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Mailchimp]:

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Members base connection with basic authentication",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
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
| `connectionSpec.id` | 源的连接规范ID。 此ID可在您的源通过注册和批准之后进行检索 [!DNL Flow Service] API。 |
| `auth.specName` | 用于将源连接到平台的身份验证类型。 |
| `auth.params.authorizationTestUrl` | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则在创建源连接步骤期间会自动检查凭据。 |
| `auth.params.username` | 与您的 [!DNL Mailchimp] 帐户。 基本身份验证需要此功能。 |
| `auth.params.password` | 与您的 [!DNL Mailchimp] 帐户。 基本身份验证需要此功能。 |

**响应**

成功的响应会返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中，需要此ID才能浏览源的文件结构和内容。

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

### 创建 [!DNL Mailchimp] 使用OAuth 2刷新代码的基本连接

创建 [!DNL Mailchimp] 使用OAuth 2刷新代码进行基本连接，然后向 `/connections` 端点，同时为您的 `authorizationTestUrl`和 `accessToken`.

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Members base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
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
| `connectionSpec.id` | 源的连接规范ID。 在使用注册您的源后，可以检索此ID [!DNL Flow Service] API。 |
| `auth.specName` | 用于向平台验证源的验证类型。 |
| `auth.params.authorizationTestUrl` | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则在创建源连接步骤期间会自动检查凭据。 |
| `auth.params.accessToken` | 用于验证源的相应访问令牌。 基于OAuth的身份验证需要此设置。 |

**响应**

成功的响应会返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中，需要此ID才能浏览源的文件结构和内容。

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

## 探索您的来源 {#explore}

使用上一步中生成的基本连接ID，您可以通过执行GET请求来浏览文件和目录。

>[!TIP]
>
>检索已接受的格式类型 `{SOURCE_PARAMS}`，则必须对整个进行编码 `list_id` 字符串。 例如， `"list_id": "10c097ca71"` 在base64中编码等于 `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`.

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

执行GET请求以浏览源的文件结构和内容时，必须包括下表中列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步中生成的基本连接ID。 |
| `{OBJECT_TYPE}` | 要浏览的对象的类型。 对于REST源，此值默认为 `rest`. |
| `{OBJECT}` | 要浏览的对象。 |
| `{FILE_TYPE}` | 仅当查看特定目录时，才需要此参数。 其值表示要浏览的目录的路径。 |
| `{PREVIEW}` | 一个布尔值，用于定义连接的内容是否支持预览。 |
| `{SOURCE_PARAMS}` | 您的 `list_id`. |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回查询文件的结构。

```json
{ 
"data": [
    {
        "list_id": "10c097ca71",
        "_links": [
            {
                "rel": "self",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
            },
            {
                "rel": "parent",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
            },
            {
                "rel": "create",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "POST",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
            }
        ],
        "members": [
            {
                "id": "cff65fb4c5f5828666ad846443720efd",
                "email_address": "kendallt2134@gmail.com",
                "unique_email_id": "72c758cbf1",
                "contact_id": "874a0d6e9ddb89d8b4a31e416ead2d6f",
                "full_name": "Kendall Roy",
                "web_id": 547094062,
                "email_type": "html",
                "status": "subscribed",
                "consents_to_one_to_one_messaging": true,
                "merge_fields": {
                    "FNAME": "Kendall",
                    "LNAME": "Roy",
                    "ADDRESS": {
                        "country": "US"
                    }
                },
                "stats": {
                    "avg_open_rate": 0,
                    "avg_click_rate": 0
                },
                "ip_opt": "103.43.112.97",
                "timestamp_opt": "2021-06-01T15:31:36+00:00",
                "member_rating": 2,
                "last_changed": "2021-06-01T15:31:36+00:00",
                "vip": false,
                "location": {
                    "latitude": 0,
                    "longitude": 0,
                    "gmtoff": 0,
                    "dstoff": 0
                },
                "source": "Admin Add",
                "tags_count": 0,
                "list_id": "10c097ca71",
                "_links": [
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        },
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
                        },
                        {
                            "rel": "update",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PATCH",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PATCH.json"
                        },
                        {
                            "rel": "upsert",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PUT",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PUT.json"
                        },
                        {
                            "rel": "delete",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "DELETE"
                        },
                        {
                            "rel": "activity",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Activity/Response.json"
                        },
                        {
                            "rel": "goals",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/goals",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Goals/Response.json"
                        },
                        {
                            "rel": "notes",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/notes",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Notes/CollectionResponse.json"
                        },
                        {
                            "rel": "events",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/events",
                            "method": "POST",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Events/POST.json"
                        },
                        {
                            "rel": "delete_permanent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/actions/delete-permanent",
                            "method": "POST"
                        }
                    ]
                }
            ]  
        }
    ]
}
```

## 创建源连接 {#source-connection}

您可以通过向 [!DNL Flow Service] API。 源连接由连接ID、源数据文件的路径和连接规范ID组成。

要创建源连接，还必须为数据格式属性定义枚举值。

为基于文件的源使用以下枚举值：

| 数据格式 | 枚举值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 镶木 | `parquet` |

对于所有基于表的源，将值设置为 `tabular`.

**API格式**

```https
POST /sourceConnections
```

**请求**

以下请求会为 [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest listId",
      "description": "MailChimp Members source connection to ingest listId",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "data": {
          "format": "json",
      },
      "params": {
          "listId": "10c097ca71"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 确保源连接的名称具有描述性，因为您可以使用该名称查找有关源连接的信息。 |
| `description` | （可选）可包含的属性，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | 基本连接ID为 [!DNL Mailchimp]. 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 的格式 [!DNL Mailchimp] 要摄取的数据。 |
| `params.listId` | 也称为受众ID， [!DNL Mailchimp] 列表ID允许将受众数据传输到其他集成。 |

**响应**

成功的响应会返回唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

```json
{
    "id": "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc",
    "etag": "\"6b02b65d-0000-0200-0000-6154bfbe0000\""
}
```

## 创建目标XDM架构 {#target-schema}

要在Platform中使用源数据，必须创建目标架构以根据您的需求构建源数据。 然后，目标架构用于创建包含源数据的Platform数据集。

通过对 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅 [使用API创建模式](../../../../../xdm/api/schemas.md).

### 创建目标数据集 {#target-dataset}

通过对 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅 [使用API创建数据集](../../../../../catalog/api/create-dataset.md).

## 创建目标连接 {#target-connection}

目标连接表示所摄取数据所登陆目标的连接。 要创建目标连接，必须提供与 [!DNL Data Lake]. 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

现在，您的唯一标识符是目标架构（目标数据集）和与 [!DNL Data Lake]. 使用这些标识符，您可以使用 [!DNL Flow Service] 用于指定将包含集客源数据的数据集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求会为 [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Members target connection",
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
| `description` | （可选）可包含的属性，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 与 [!DNL Data Lake]. 此固定ID是： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 的格式 [!DNL Mailchimp] 要引入平台的数据。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |


**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此ID是后续步骤所必需的。

```json
{
    "id": "8db5fb4a-6ce8-4370-afc0-1765e39535a5",
    "etag": "\"960093ce-0000-0200-0000-6154da3e0000\""
}
```

## 创建映射 {#mapping}

要将源数据摄取到目标数据集，必须先将其映射到目标数据集所附加的目标架构。 这是通过对执行POST请求来实现的 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) ，在请求有效负载中定义数据映射。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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

| 属性 | 描述 |
| --- | --- |
| `xdmSchema` | 的ID [目标XDM架构](#target-schema) 生成。 |
| `mappings.destinationXdmPath` | 源属性映射到的目标XDM路径。 |
| `mappings.sourceAttribute` | 需要映射到目标XDM路径的源属性。 |
| `mappings.identity` | 一个布尔值，用于指定是否将映射集标记为 [!DNL Identity Service]. |

**响应**

成功的响应会返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要此值才能创建数据流。

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

## 创建流 {#flow}

最后一步 [!DNL Mailchimp] 数据到平台即是创建数据流。 现在，您已准备以下必需值：

* [源连接ID](#source-connection)
* [Target连接ID](#target-connection)
* [映射ID](#mapping)

数据流负责从源中调度和收集数据。 通过在有效负载中提供先前提到的值时执行POST请求，可以创建数据流。

要计划摄取，您必须首先将开始时间值设置为以秒为单位的新纪元时间。 然后，您必须将频率值设置为以下五个选项之一： `once`, `minute`, `hour`, `day`或 `week`. 间隔值可指定两个连续摄取和创建一次性摄取之间的周期，而无需设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于 `15`.


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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Members dataflow",
      "description": "MailChimp Members dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc"
      ],
      "targetConnectionIds": [
          "8db5fb4a-6ce8-4370-afc0-1765e39535a5"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                  "mappingVersion": 0
              }
          }
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
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID是： `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 流量规范ID的相应版本。 此值默认为 `1.0`. |
| `sourceConnectionIds` | 的 [源连接ID](#source-connection) 生成。 |
| `targetConnectionIds` | 的 [目标连接ID](#target-connection) 生成。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入平台时，需要使用此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 生成。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为 `0`. |
| `scheduleParams.startTime` | 首次摄取数据开始时的指定开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`, `minute`, `hour`, `day`或 `week`. |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 将频率设置为时，不需要间隔 `once` 且应大于或等于 `15` 的其他频率值。 |

**响应**

成功的响应会返回ID(`id`)。 您可以使用此ID来监视、更新或删除您的数据流。

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"2e01f11d-0000-0200-0000-615649660000\""
}
```

## 附录

以下部分提供了有关可以监视、更新和删除数据流的步骤的信息。

### 监控数据流

创建数据流后，您可以监视通过其摄取的数据，以查看有关流量运行、完成状态和错误的信息。 有关完整的API示例，请阅读 [使用API监控源数据流](../../monitor.md).

### 更新数据流

通过向发出PATCH请求，更新数据流的详细信息（如其名称和描述），以及其运行计划和关联的映射集 `/flows` 端点 [!DNL Flow Service] API，同时提供数据流的ID。 发出PATCH请求时，必须提供数据流的唯一 `etag` 在 `If-Match` 标题。 有关完整的API示例，请阅读 [使用API更新源数据流](../../update-dataflows.md).

### 更新您的帐户

通过向执行PATCH请求，更新源帐户的名称、说明和凭据 [!DNL Flow Service] API，同时将基本连接ID作为查询参数提供。 发出PATCH请求时，必须提供源帐户的唯一 `etag` 在 `If-Match` 标题。 有关完整的API示例，请阅读 [使用API更新源帐户](../../update.md).

### 删除数据流

通过执行对的DELETE请求删除数据流 [!DNL Flow Service] API，同时提供要作为查询参数一部分删除的数据流的ID。 有关完整的API示例，请阅读 [使用API删除数据流](../../delete-dataflows.md).

### 删除您的帐户

通过向执行DELETE请求删除您的帐户 [!DNL Flow Service] API，同时提供要删除的帐户的基本连接ID。 有关完整的API示例，请阅读 [使用API删除源帐户](../../delete.md).