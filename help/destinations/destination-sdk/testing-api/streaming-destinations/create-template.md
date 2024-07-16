---
description: 了解如何在发布目标之前使用目标测试API来测试流式传输目标消息转换模板。
title: 创建和测试消息转换模板
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# 创建和测试消息转换模板 {#create-template}

## 概述 {#overview}

作为Destination SDK的一部分，Adobe提供开发人员工具来帮助您配置和测试目标。 本页介绍如何创建和测试消息转换模板。 有关如何测试目标的信息，请阅读[测试目标配置](streaming-destination-testing-overview.md)。

要在Adobe Experience Platform中的目标架构与目标支持的消息格式之间&#x200B;**创建和测试消息转换模板**，请使用下面进一步描述的&#x200B;*模板创作工具*。  阅读有关[消息格式文档](../../functionality/destination-server/message-format.md#using-templating)中源架构和目标架构之间的数据转换的详细信息。

下面说明了创建和测试消息转换模板如何适应Destination SDK中的[目标配置工作流](../../guides/configure-destination-instructions.md)：

![创建模板步骤适合目标配置工作流的图形](../../assets/testing-api/create-template-step.png)

## 为什么需要创建和测试消息转换模板 {#why-create-message-transformation-template}

在Destination SDK中创建目标的第一步之一是考虑在从Adobe Experience Platform导出到目标时，如何转换受众成员资格、身份和配置文件属性的数据格式。 在[消息格式Adobe](../../functionality/destination-server/message-format.md#using-templating)中查找有关文档XDM架构与目标架构之间转换的信息。

为了转换成功，您必须提供一个转换模板，类似于此示例： [创建一个发送区段、身份和配置文件属性的模板](../../functionality/destination-server/message-format.md#segments-identities-attributes)。

Adobe提供了一个template工具，允许您创建和测试消息模板，以将数据从AdobeXDM格式转换为目标支持的格式。 该工具具有两个API端点，您可以使用这些端点：

* 使用&#x200B;*示例模板API*&#x200B;获取示例模板。
* 使用&#x200B;*渲染模板API*&#x200B;来渲染示例模板，以便您可以将结果与目标预期的数据格式进行比较。 将导出的数据与目标所需的数据格式进行比较后，可以编辑模板。 这样，您生成的导出数据与目标所预期的数据格式相匹配。

## 创建模板前要完成的步骤 {#prerequisites}

在创建模板之前，请确保完成以下步骤：

1. [创建目标服务器配置](../../authoring-api/destination-server/create-destination-server.md)。 根据您为`maxUsersPerRequest`参数提供的值，将生成的模板有所不同。
   * 如果您希望目标的API调用包含单个配置文件，以及其受众资格、身份和配置文件属性，请使用`maxUsersPerRequest=1`。
   * 如果您希望目标的API调用包含多个配置文件及其受众资格、身份和配置文件属性，请使用值大于1的`maxUsersPerRequest`。
2. [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)并在`destinationDelivery.destinationServerId`中添加目标服务器配置的ID。
3. [获取刚刚创建的目标配置的ID](../../authoring-api/destination-configuration/retrieve-destination-configuration.md)，以便在模板创建工具中使用该配置。
4. 了解[您可以在消息转换模板中使用哪些函数和筛选器](../../functionality/destination-server/supported-functions.md)。

## 如何使用示例模板API和渲染模板API为您的目标创建模板 {#iterative-process}

>[!TIP]
>
>在构建和编辑消息转换模板之前，您可以首先使用简单模板调用[渲染模板API端点](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data)，该模板可导出原始配置文件而不应用任何转换。 简单模板的语法为： <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

模板的获取和测试过程是迭代的。 重复以下步骤，直到导出的用户档案与目标的预期数据格式匹配。

1. 首先，[获取示例模板](../../testing-api/streaming-destinations/create-template.md#sample-template-api)。
2. 使用示例模板作为创建自己的草稿的起点。
3. 使用您自己的模板调用[渲染模板API终结点](../../testing-api/streaming-destinations/create-template.md#render-template-api)。 Adobe会根据您的架构生成示例配置文件，并返回结果或任何遇到的错误。
4. 将导出的数据与目标所需的数据格式进行比较。 如果需要，可编辑模板。
5. 重复此过程，直到导出的用户档案与目标的预期数据格式匹配。

## 使用示例模板API获取示例模板 {#sample-template-api}

>[!NOTE]
>
>有关完整的API参考文档，请阅读[获取示例模板API操作](../../testing-api/streaming-destinations/sample-template-api.md)。

将目标ID添加到调用，如下所示，响应将返回与目标ID对应的模板示例。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

如果您提供的目标ID对应于聚合策略中具有[最大努力聚合](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation)和`maxUsersPerRequest=1`的目标配置，则该请求将返回与以下模板类似的示例模板：

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

如果您提供的目标ID对应于具有[可配置的聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)或[最大努力聚合](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation)且其`maxUsersPerRequest`大于一个的目标服务器模板，则请求将返回与以下模板类似的示例模板：

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering audiences by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## 对模板进行字符转义 {#character-escape-template}

在使用模板渲染符合目标预期格式的用户档案之前，您必须对模板进行字符转义，如下面的屏幕录制所示。

![显示如何使用联机字符转义工具对模板进行字符转义的视频](../../assets/testing-api/escape-characters.gif)

您可以使用联机字符转义工具。 上述演示使用[JSON Escape格式化程序](https://jsonformatter.org/json-escape)。

## 呈现模板API {#render-template-api}

使用[示例模板API](create-template.md#sample-template-api)创建消息转换模板后，您可以[渲染模板](render-template-api.md)以基于它生成导出的数据。 这允许您验证Adobe Experience Platform将导出到目标的配置文件是否与目标的预期格式匹配。

有关可以进行的调用的示例，请参阅API参考：

* [呈现模板，其中没有在正文中发送配置文件](render-template-api.md#multiple-profiles-no-body)
* [渲染包含正文中发送的用户档案的模板](render-template-api.md#multiple-profiles-with-body)

编辑模板并调用渲染模板API端点，直到导出的配置文件与目标的预期数据格式匹配。

## 将字符转义模板添加到目标服务器配置

对消息转换模板感到满意后，将其添加到[目标服务器配置](../../authoring-api/destination-server/create-destination-server.md)，位于`httpTemplate.requestBody.value`。
