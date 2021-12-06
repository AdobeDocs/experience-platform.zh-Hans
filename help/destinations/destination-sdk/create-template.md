---
description: 作为Destination SDK的一部分，Adobe提供了开发人员工具，可帮助您配置和测试目标。 本页介绍如何创建和测试消息转换模板。
title: 创建和测试消息转换模板
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: aa5898369d41ba48a1416a0b4ea82f6345333d18
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 创建和测试消息转换模板 {#create-template}

## 概述 {#overview}

作为Destination SDK的一部分，Adobe提供了开发人员工具，可帮助您配置和测试目标。 本页介绍如何创建和测试消息转换模板。 有关如何测试目标的信息，请阅读 [测试目标配置](./test-destination.md).

至 **创建和测试消息转换模板** 在Adobe Experience Platform中的目标架构与目标支持的消息格式之间，使用 *模板创作工具* 下文进一步描述。  有关源模式和目标模式之间数据转换的更多信息，请参阅 [消息格式文档](./message-format.md#using-templating).

下图说明了如何创建和测试消息转换模板 [目标配置工作流](./configure-destination-instructions.md) 在Destination SDK中：

![创建模板步骤在目标配置工作流中所处位置的图形](./assets/create-template-step.png)

## 为何需要创建和测试消息转换模板 {#why-create-message-transformation-template}

在Destination SDK中创建目标的第一步之一是，考虑在从Adobe Experience Platform导出到目标时，区段成员资格、身份和配置文件属性的数据格式是如何转换的。 在 [消息格式文档](./message-format.md#using-templating).

要使转换成功，必须提供转换模板，如下示例所示： [创建用于发送区段、身份和配置文件属性的模板](./message-format.md#segments-identities-attributes).

Adobe提供了一个模板工具，允许您创建和测试消息模板，以将AdobeXDM格式的数据转换为目标支持的格式。 该工具有两个可使用的API端点：
* 使用 *模板API示例* 以获取示例模板。
* 使用 *呈现模板API* 渲染示例模板，以便将结果与目标的预期数据格式进行比较。 将导出的数据与目标所预期的数据格式进行比较后，您可以编辑模板。 这样，您生成的导出数据就会与目标所需的数据格式匹配。

## 在创建模板之前完成的步骤 {#prerequisites}

在准备好创建模板之前，请确保完成以下步骤：

1. [创建目标服务器配置](./destination-server-api.md). 根据为 `maxUsersPerRequest` 参数。
   * 使用 `maxUsersPerRequest=1` 如果您希望对目标的API调用包含单个配置文件，以及其区段资格、身份和配置文件属性。
   * 使用 `maxUsersPerRequest` 值大于1的值。
2. [创建目标配置](./destination-configuration-api.md#create) ，并在 `destinationDelivery.destinationServerId`.
3. [获取目标配置的ID](./destination-configuration-api.md#retrieve-list) 创建的模板，以便在模板创建工具中使用。

## 如何使用示例模板API和渲染模板API为目标创建模板 {#iterative-process}

>[!TIP]
>
>在制作和编辑消息转换模板之前，您可以首先调用 [呈现模板API端点](./render-template-api.md#render-exported-data) 使用可导出原始配置文件且不应用任何转换的简单模板。 简单模板的语法为： <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

获取和测试模板的过程是迭代的。 重复以下步骤，直到导出的用户档案与目标的预期数据格式匹配。

1. 首先， [获取示例模板](./create-template.md#sample-template-api).
2. 使用示例模板作为起点，创建您自己的草稿。
3. 调用 [呈现模板API端点](./create-template.md#render-template-api) 模板。 Adobe会根据您的架构生成示例用户档案，并返回结果或遇到的任何错误。
4. 将导出的数据与目标所需的数据格式进行比较。 如果需要，请编辑模板。
5. 重复此过程，直到导出的用户档案与目标的预期数据格式匹配为止。

## 使用示例模板API获取示例模板 {#sample-template-api}

>[!NOTE]
>
>有关完整的API参考文档，请阅读 [获取示例模板API操作](./sample-template-api.md).

向调用中添加目标ID，如下所示，响应将返回与目标ID对应的模板示例。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

如果您提供的目标ID与 [最佳工作聚合](./destination-configuration.md#best-effort-aggregation) 和 `maxUsersPerRequest=1` 在聚合策略中，请求会返回与以下模板类似的示例模板：

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
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

如果您提供的目标ID与 [可配置聚合](./destination-configuration.md#configurable-aggregation) 或 [最佳工作聚合](./destination-configuration.md#best-effort-aggregation) with `maxUsersPerRequest` 大于1，请求会返回与以下模板类似的示例模板：

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
                {#- Alternative syntax for filtering segments by status: -#}
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

使用模板渲染与目标预期格式匹配的配置文件之前，必须对模板进行字符转义，如以下屏幕记录所示。

![显示如何使用在线字符转义工具对模板进行字符转义的视频](./assets/escape-characters.gif)

您可以使用联机字符转义工具。 上述演示使用 [JSON转义格式器](https://jsonformatter.org/json-escape).

## 呈现模板API {#render-template-api}

在使用 [模板API示例](./create-template.md#sample-template-api)，您可以 [呈现模板](./render-template-api.md) 以根据生成导出数据。 这允许您验证Adobe Experience Platform将导出到目标的用户档案是否与目标的预期格式匹配。

有关可以进行的调用示例，请参阅API引用：

* [渲染主体中未发送用户档案的模板](./render-template-api.md#multiple-profiles-no-body)
* [呈现在主体中发送用户档案的模板](./render-template-api.md#multiple-profiles-with-body)

编辑模板并调用渲染模板API端点，直到导出的配置文件与目标的预期数据格式匹配为止。

## 将字符转义模板添加到目标服务器配置

对消息转换模板满意后，将其添加到 [目标服务器配置](./server-and-template-configuration.md)，在 `httpTemplate.requestBody.value`.
