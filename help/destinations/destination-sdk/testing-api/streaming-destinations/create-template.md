---
description: 了解如何在发布目标之前使用目标测试API测试流目标消息转换模板。
title: 创建和测试消息转换模板
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---


# 创建和测试消息转换模板 {#create-template}

## 概述 {#overview}

作为Destination SDK的一部分，Adobe提供开发人员工具来帮助您配置和测试目标。 本页介绍如何创建和测试消息转换模板。 有关如何测试目标的信息，请阅读 [测试目标配置](streaming-destination-testing-overview.md).

至 **创建和测试消息转换模板** 在Adobe Experience Platform的目标架构和目标支持的消息格式之间，使用 *模板创作工具* 如下所述。  有关源架构和目标架构之间数据转换的更多信息，请参阅 [消息格式文档](../../functionality/destination-server/message-format.md#using-templating).

下图说明了创建和测试报文转换模板如何适应 [目标配置工作流](../../guides/configure-destination-instructions.md) Destination SDK：

![此图显示了创建模板步骤在目标配置工作流中的位置](../../assets/testing-api/create-template-step.png)

## 为什么需要创建和测试消息转换模板 {#why-create-message-transformation-template}

在Destination SDK中创建目标的第一步之一是考虑在从Adobe Experience Platform导出到目标时，如何转换受众成员资格、身份和配置文件属性的数据格式。 在中查找有关AdobeXDM架构与目标架构之间转换的信息 [消息格式文档](../../functionality/destination-server/message-format.md#using-templating).

要使转换成功，必须提供类似于以下示例的转换模板： [创建用于发送区段、身份和配置文件属性的模板](../../functionality/destination-server/message-format.md#segments-identities-attributes).

Adobe提供了一个template工具，允许您创建和测试消息模板，以便将数据从AdobeXDM格式转换为目标支持的格式。 该工具具有两个API端点，您可以使用这些端点：

* 使用 *示例模板API* 以获取示例模板。
* 使用 *渲染模板API* 渲染示例模板，以便您可以将结果与目标的预期数据格式进行比较。 将导出的数据与目标所需的数据格式进行比较后，可以编辑模板。 这样，您生成的导出数据与目标预期的数据格式相匹配。

## 创建模板前要完成的步骤 {#prerequisites}

在创建模板之前，请确保完成以下步骤：

1. [创建目标服务器配置](../../authoring-api/destination-server/create-destination-server.md). 根据您为提供的值，将生成的模板有所不同 `maxUsersPerRequest` 参数。
   * 使用 `maxUsersPerRequest=1` 如果您希望对目标的某个API调用包含单个配置文件，以及其受众资格、身份和配置文件属性。
   * 使用 `maxUsersPerRequest` 其值大于1。
2. [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md) 并将目标服务器配置的ID添加到中 `destinationDelivery.destinationServerId`.
3. [获取目标配置的ID](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 您刚刚创建的，因此您可以在模板创建工具中使用它。
4. 了解 [可以使用哪些函数和过滤器](../../functionality/destination-server/supported-functions.md) 在消息转换模板中。

## 如何使用示例模板API和渲染模板API为您的目标创建模板 {#iterative-process}

>[!TIP]
>
>在构建和编辑消息转换模板之前，您可以调用 [渲染模板API端点](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) 使用简单模板导出原始配置文件，而不应用任何转换。 简单模板的语法为： <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

模板的获取和测试过程是迭代的。 重复以下步骤，直到导出的用户档案与目标的预期数据格式匹配。

1. 首先， [获取示例模板](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. 使用示例模板作为创建自己的草稿的起点。
3. 调用 [渲染模板API端点](../../testing-api/streaming-destinations/create-template.md#render-template-api) 使用您自己的模板。 Adobe根据您的架构生成示例配置文件，并返回结果或任何遇到的错误。
4. 将导出的数据与目标所需的数据格式进行比较。 如果需要，可编辑模板。
5. 重复此过程，直到导出的用户档案与目标的预期数据格式匹配。

## 使用示例模板API获取示例模板 {#sample-template-api}

>[!NOTE]
>
>有关完整的API参考文档，请阅读 [获取示例模板API操作](../../testing-api/streaming-destinations/sample-template-api.md).

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

如果您提供的目标ID对应于具有以下属性的目标配置 [尽力而为聚合](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 和 `maxUsersPerRequest=1` 在聚合策略中，请求返回一个与以下模板类似的示例模板：

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

如果您提供的目标ID对应于目标服务器模板，请使用 [可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 或 [尽力而为聚合](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 替换为 `maxUsersPerRequest` 如果大于一，请求将返回一个与以下模板类似的示例模板：

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

![此视频演示如何使用在线字符转义工具对模板进行字符转义](../../assets/testing-api/escape-characters.gif)

可以使用联机字符转义工具。 上述演示使用 [JSON转义格式化程序](https://jsonformatter.org/json-escape).

## 渲染模板API {#render-template-api}

使用创建消息转换模板后 [示例模板API](create-template.md#sample-template-api)，您可以 [渲染模板](render-template-api.md) 以基于它生成导出的数据。 这允许您验证Adobe Experience Platform将导出到目标的配置文件是否与目标的预期格式匹配。

有关可以进行的调用的示例，请参阅API引用：

* [渲染没有在正文中发送用户档案的模板](render-template-api.md#multiple-profiles-no-body)
* [渲染包含正文中发送的用户档案的模板](render-template-api.md#multiple-profiles-with-body)

编辑模板并调用渲染模板API端点，直到导出的配置文件与目标的预期数据格式匹配。

## 将字符转义模板添加到目标服务器配置

对消息转换模板满意后，将其添加到您的 [目标服务器配置](../../authoring-api/destination-server/create-destination-server.md)，在 `httpTemplate.requestBody.value`.
