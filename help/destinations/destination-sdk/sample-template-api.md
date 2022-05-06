---
description: 本页列出并描述了您可以使用“/authoring/testing/template/sample” API端点执行的所有API操作，以获取目标的测试消息转换模板。
title: 获取示例模板API操作
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 1%

---

# 获取示例模板API操作 {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API端点**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

本页列出并介绍了您可以使用 `/authoring/testing/template/sample` API端点，用于生成 [消息转换模板](./message-format.md#using-templating) 你的目的地。 有关此端点支持的功能的描述，请阅读 [创建模板](./create-template.md).

## 模板API操作示例快速入门 {#get-started}

在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 获取示例模板 {#generate-sample-template}

您可以通过向 `authoring/testing/template/sample/` 端点，并提供基于您创建模板的目标配置的目标ID。

>[!TIP]
>
>* 您在此应使用的目标ID是 `instanceId` 对应于目标配置的 `/destinations` 端点。 请参阅 [目标配置API引用](./destination-configuration-api.md#retrieve-list).


**API格式**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要为其生成消息转换模板的目标配置的ID。 |

**请求**

以下请求会生成一个新的示例模板，该模板由有效负载中提供的参数进行配置。

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

成功响应会返回HTTP状态200，其中包含一个示例模板，您可以编辑该模板以匹配预期的数据格式。

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

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用 `/authoring/testing/template/sample` API端点。 接下来，您可以使用 [呈现模板API端点](./render-template-api.md) ，以根据模板生成导出的用户档案，并将其与目标的预期数据格式进行比较。
