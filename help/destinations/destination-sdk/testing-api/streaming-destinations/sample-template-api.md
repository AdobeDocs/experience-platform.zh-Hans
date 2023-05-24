---
description: 瞭解如何使用目的地測試API為您的目的地產生測試訊息轉換範本。
title: 產生範例訊息轉換範本
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# 產生範例訊息轉換範本 {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API端點**： `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

此頁面列出並描述您可以使用執行的所有API作業。 `/authoring/testing/template/sample` API端點，以產生 [訊息轉換範本](../../functionality/destination-server/message-format.md#using-templating) 以取得您的目的地。 如需此端點支援的功能的說明，請閱讀 [建立範本](create-template.md).

## 範例範本API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 取得範例範本 {#generate-sample-template}

您可以透過向以下網站發出GET請求來取得範例範本： `authoring/testing/template/sample/` 端點，並提供您建立範本時依據之目的地設定的目的地ID。

>[!TIP]
>
>* 您應在此使用的目的地ID為 `instanceId` 對應至目的地組態，建立目的地組態時，使用 `/destinations` 端點。 請參閱 [擷取目的地設定](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 以取得更多詳細資料。


**API格式**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要為其產生訊息轉換範本的目的地設定ID。 |

**请求**

以下請求會產生新的範例範本，由承載中提供的引數設定。

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

成功的回應會傳回HTTP狀態200和範本，您可編輯範本以符合預期的資料格式。

如果您提供的目的地ID對應至具有的目的地設定 [最大努力彙總](../../functionality/destination-configuration/aggregation-policy.md) 和 `maxUsersPerRequest=1` 在彙總原則中，要求會傳回類似以下的範例範本：

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

如果您提供的目的地ID對應至目的地伺服器範本，並附有 [可設定的彙總](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 或 [最大努力彙總](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 替換為 `maxUsersPerRequest` 大於一個時，請求會傳回類似以下的範例範本：

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

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/testing/template/sample` api端點。 接下來，您可以使用 [轉譯器範本API端點](render-template-api.md) 根據範本產生匯出的設定檔，並與目的地的預期資料格式進行比較。
