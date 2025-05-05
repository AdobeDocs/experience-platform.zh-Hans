---
description: 了解如何格式化发送到端点的HTTP请求。 使用/authoring/destination-servers端点在Adobe Experience Platform Destination SDK中配置目标服务器模板化规范。
title: 使用Destination SDK创建的目标模板规范
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# 使用Destination SDK创建的目标模板规范

使用目标服务器配置的模板规范部分配置如何格式化发送到目标的HTTP请求。

在模板规范中，您可以定义如何在XDM架构和平台支持的格式之间转换配置文件属性字段。

模板规范是实时（流）目标的目标服务器配置的一部分。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅[配置选项](../configuration-options.md)文档中的关系图，或参阅如何[使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-server-template-configuration)的指南。

您可以通过`/authoring/destination-servers`端点配置目标的模板规范。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标服务器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目标服务器配置](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;**&#x200B;**。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 否 |

## 配置模板规范 {#configure-template-spec}

Adobe使用类似于[Jinja](https://jinja.palletsprojects.com/en/2.11.x/)的模板化语言将字段从XDM架构转换为目标支持的格式。

![模板配置突出显示](../../assets/functionality/destination-server/template-configuration.png)

有关转换的更多信息，请访问以下链接：

* [消息格式](message-format.md)
* [使用模板语言进行身份、属性和受众成员资格转换](message-format.md#using-templating)

>[!TIP]
>
>Adobe提供了一个[开发人员工具](../../testing-api/streaming-destinations/create-template.md)，可帮助您创建和测试消息转换模板。

请参阅下面的HTTP请求模板示例，以及每个参数的说明。

```json
{
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
| `httpMethod` | 字符串 | *必填。* Adobe将在对服务器的调用中使用的方法。 支持的方法： `GET`、`PUT`、`POST`、`DELETE`、`PATCH`。 |
| `templatingStrategy` | 字符串 | *必填。*&#x200B;使用`PEBBLE_V1`。 |
| `value` | 字符串 | *必填。*&#x200B;此字符串是模板的字符转义版本，用于将Experience Platform发送的HTTP请求格式化为目标所需的格式。 <br>有关如何写入模板的信息，请阅读[上使用模板](message-format.md#using-templating)的部分。 <br>有关字符转义的更多信息，请参阅[RFC JSON标准第七节](https://tools.ietf.org/html/rfc8259#section-7)。 <br>有关简单转换的示例，请参阅[配置文件属性](message-format.md#attributes)转换。 |
| `contentType` | 字符串 | *必填。*&#x200B;您的服务器接受的内容类型。 根据转换模板生成的输出类型，这可以是任何受支持的[HTTP应用程序内容类型](https://www.iana.org/assignments/media-types/media-types.xhtml#application)。 在大多数情况下，此值应设置为`application/json`。 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解什么是模板规范以及如何对其进行配置。

要了解有关其他目标服务器组件的更多信息，请参阅以下文章：

* [使用Destination SDK创建目标的服务器规范](server-specs.md)
* [消息格式](message-format.md)
* [文件格式配置](file-formatting.md)
