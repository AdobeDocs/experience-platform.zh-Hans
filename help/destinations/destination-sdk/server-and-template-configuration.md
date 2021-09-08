---
description: 可以在Adobe Experience Platform目标SDK中通过公共端点“/authoring/destination-servers”配置服务器和模板规范。
title: 目标SDK中服务器和模板规范的配置选项
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 7%

---

# 服务器和模板规范的配置选项

## 概述 {#overview}

可以在Adobe Experience Platform目标SDK中通过公共端点`/authoring/destination-servers`配置服务器和模板规范。 请阅读[目标API端点操作](./destination-server-api.md) ，以获取可对端点执行的操作的完整列表。

## 示例配置 {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
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

## 服务器规范 {#server-specs}

![服务器配置突出显示](./assets/server-configuration.png)

客户将能够通过HTTP导出将数据从Adobe Experience Platform激活到您的目标。 服务器配置包含有关接收消息的服务器（服务器端）的信息。

此过程会将用户数据作为一系列HTTP消息传送到您的目标平台。 以下参数构成HTTP服务器规范模板。

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 表示服务器的友好名称，仅对Adobe可见。 合作伙伴或客户看不到此名称。 示例 `Moviestar destination server`. |
| `destinationServerType` | 字符串 | `URL_BASED` 是当前唯一可用的选项。 |
| `templatingStrategy` | 字符串 | <ul><li>如果Adobe需要转换下面`value`字段中的URL，请使用`PEBBLE_V1`。 如果您具有如下端点，请使用此选项：`https://api.moviestar.com/data/{{endpoint.region}}/items` </li><li> 如果Adobe端不需要转换，例如，如果您具有如下端点，则使用`NONE`:`https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字符串 | 填写Experience Platform应连接到的API端点的地址。 |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## 模板规范 {#template-specs}

![高亮显示模板配置](./assets/template-configuration.png)

模板规范允许您配置如何将导出的消息格式化到目标。 Adobe使用类似于[Jinja](https://jinja.palletsprojects.com/en/2.11.x/)的模板语言将XDM架构中的字段转换为目标支持的格式。 有关转换的更多信息，请访问以下链接：

* [消息格式](./message-format.md)
* [对身份、属性和区段成员资格转换使用模板语言 ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe提供了[开发人员工具](./create-template.md)，可帮助您创建和测试消息转换模板。

| 参数 | 类型 | 描述 |
|---|---|---|
| `httpMethod` | 字符串 | Adobe在对服务器的调用中将使用的方法。 选项包括`GET`、`PUT`、`POST`、`DELETE`、`PATCH`。 |
| `templatingStrategy` | 字符串 | 使用 `PEBBLE_V1`. |
| `value` | 字符串 | 此字符串是字符转义版本，可将Platform客户的数据转换为您的服务预期的格式。 <br> 有关如何编写模板的信息，请阅读使用 [模板一节](./message-format.md#using-templating)。<br> 有关字符转义的更多信息，请参 [阅RFC JSON标准第七节](https://tools.ietf.org/html/rfc8259#section-7)。<br> 有关简单转换的示例，请参阅配置文件属 [性](./message-format.md#attributes) 信息。 |
| `contentType` | 字符串 | 服务器接受的内容类型。 该值很可能为`application/json`。 |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
