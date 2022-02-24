---
description: 服务器和模板规范可以通过公共端点“/authoring/destination-servers”在Adobe Experience Platform Destination SDK中配置。
title: 服务器和模板规范的配置选项Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 8%

---

# 流目标服务器和模板规范的配置选项

## 概述 {#overview}

可以通过公共端点在Adobe Experience Platform Destination SDK中配置服务器和模板规范 `/authoring/destination-servers`. 读取 [目标API端点操作](./destination-server-api.md) 有关可对端点执行的操作的完整列表。

## 服务器规范 {#server-specs}

![服务器配置突出显示](./assets/server-configuration.png)

客户将能够通过HTTP导出将数据从Adobe Experience Platform激活到您的目标。 服务器配置包含有关接收消息的服务器（服务器端）的信息。

此过程会将用户数据作为一系列HTTP消息传送到您的目标平台。 以下参数构成HTTP服务器规范模板。

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | *必需。* 表示服务器的友好名称，仅对Adobe可见。 合作伙伴或客户看不到此名称。 示例 `Moviestar destination server`. |
| `destinationServerType` | 字符串 | *必需。* 设置为 `URL_BASED` 用于流目标。 |
| `templatingStrategy` | 字符串 | *必需.* <ul><li>使用 `PEBBLE_V1` 如果在 `value` 字段。 如果您具有如下端点，请使用此选项： `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> 使用 `NONE` 如果Adobe端不需要转换，例如，如果您具有如下端点： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字符串 | *必需。* 填写Experience Platform应连接到的API端点的地址。 |

{style=&quot;table-layout:auto&quot;}

## 模板规范 {#template-specs}

![高亮显示模板配置](./assets/template-configuration.png)

模板规范允许您配置如何将导出的消息格式化到目标。 Adobe使用类似于 [金子](https://jinja.palletsprojects.com/en/2.11.x/) 将XDM架构中的字段转换为目标支持的格式。 有关转换的更多信息，请访问以下链接：

* [消息格式](./message-format.md)
* [对身份、属性和区段成员资格转换使用模板语言 ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe [开发人员工具](./create-template.md) 可帮助您创建和测试消息转换模板。

## 流目标示例配置  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
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

| 参数 | 类型 | 描述 |
|---|---|---|
| `httpMethod` | 字符串 | *必需。* Adobe在对服务器的调用中将使用的方法。 选项包括 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | 字符串 | *必需。* 使用 `PEBBLE_V1`. |
| `value` | 字符串 | *必需。* 此字符串是字符转义版本，可将Platform客户的数据转换为您的服务预期的格式。 <br> 有关如何编写模板的信息，请阅读 [使用模板段](./message-format.md#using-templating). <br> 有关字符转义的更多信息，请参阅 [RFC JSON标准，第七节](https://tools.ietf.org/html/rfc8259#section-7). <br> 有关简单转换的示例，请参阅 [配置文件属性](./message-format.md#attributes) 转换。 |
| `contentType` | 字符串 | *必需。* 服务器接受的内容类型。 此值极有可能 `application/json`. |

{style=&quot;table-layout:auto&quot;}