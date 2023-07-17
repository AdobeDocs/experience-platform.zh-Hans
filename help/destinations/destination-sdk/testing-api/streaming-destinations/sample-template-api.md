---
description: 了解如何使用目标测试API为您的目标生成测试消息转换模板。
title: 生成示例消息转换模板
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# 生成示例消息转换模板 {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API端点**： `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

本页列出并描述了可以使用执行的所有API操作。 `/authoring/testing/template/sample` API端点，用于生成 [消息转换模板](../../functionality/destination-server/message-format.md#using-templating) 您的目的地。 有关此端点支持的功能的说明，请阅读 [创建模板](create-template.md).

## 示例模板API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 获取示例模板 {#generate-sample-template}

您可以向以下网站发出GET请求，以获取示例模板： `authoring/testing/template/sample/` 端点，并提供目标配置的目标ID，您将基于此ID创建模板。

>[!TIP]
>
>* 您应在此处使用的目标ID是 `instanceId` 对应于使用创建的目标配置 `/destinations` 端点。 请参阅 [检索目标配置](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 了解更多详细信息。

**API格式**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要为其生成消息转换模板的目标配置的ID。 |

**请求**

以下请求会生成一个新的示例模板，该模板由有效负载中提供的参数配置。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回带有一个示例模板的HTTP状态200，您可以编辑该示例模板以匹配预期的数据格式。

如果您提供的目标ID对应于具有以下属性的目标配置 [尽力而为聚合](../../functionality/destination-configuration/aggregation-policy.md) 和 `maxUsersPerRequest=1` 在聚合策略中，请求返回一个与以下模板类似的示例模板：

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

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用 `/authoring/testing/template/sample` API端点。 接下来，您可以使用 [渲染模板API端点](render-template-api.md) 根据模板生成导出的用户档案，并将其与目标预期的数据格式进行比较。
