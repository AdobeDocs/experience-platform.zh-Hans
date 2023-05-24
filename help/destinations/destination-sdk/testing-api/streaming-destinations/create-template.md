---
description: 瞭解如何使用目的地測試API，在發佈目的地之前測試串流目的地訊息轉換範本。
title: 建立及測試訊息轉換範本
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---


# 建立及測試訊息轉換範本 {#create-template}

## 概述 {#overview}

在Destination SDK過程中，Adobe會提供開發人員工具，協助您設定和測試目的地。 此頁面說明如何建立和測試訊息轉換範本。 如需如何測試目的地的詳細資訊，請閱讀 [測試您的目的地設定](streaming-destination-testing-overview.md).

至 **建立及測試訊息轉換範本** 在Adobe Experience Platform的目標結構描述和目的地支援的訊息格式之間，使用 *範本製作工具* 如下所述。  深入瞭解中的來源和目標結構描述之間的資料轉換 [訊息格式檔案](../../functionality/destination-server/message-format.md#using-templating).

以下說明建立和測試訊息轉換範本如何符合 [目的地設定工作流程](../../guides/configure-destination-instructions.md) Destination SDK：

![建立範本步驟符合目的地設定工作流程的圖形](../../assets/testing-api/create-template-step.png)

## 為何需要建立和測試訊息轉換範本 {#why-create-message-transformation-template}

在Destination SDK中建立目的地的首要步驟之一，就是思考將區段會籍、身分和設定檔屬性的資料格式從Adobe Experience Platform匯出至目的地時，如何進行轉換。 在中尋找有關AdobeXDM結構描述和您的目的地結構描述之間轉換的資訊 [訊息格式檔案](../../functionality/destination-server/message-format.md#using-templating).

若要轉換成功，您必須提供轉換範本，類似於以下範例： [建立可傳送區段、身分和設定檔屬性的範本](../../functionality/destination-server/message-format.md#segments-identities-attributes).

Adobe提供範本工具，可讓您建立並測試訊息範本，將資料從AdobeXDM格式轉換為目的地支援的格式。 此工具有兩個API端點可供您使用：

* 使用 *範例範本API* 以取得範例範本。
* 使用 *轉譯器範本API* 以轉譯範例範本，使您可以將結果與目的地的預期資料格式進行比較。 將匯出的資料與目的地預期的資料格式比較後，您可以編輯範本。 如此一來，您產生的匯出資料就會符合目的地預期的資料格式。

## 建立範本前需完成的步驟 {#prerequisites}

在您準備好建立範本之前，請務必完成下列步驟：

1. [建立目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 根據您為提供的值，將產生的範本會有所不同 `maxUsersPerRequest` 引數。
   * 使用 `maxUsersPerRequest=1` 如果您希望目的地的API呼叫包含單一設定檔，以及其區段資格、身分和設定檔屬性。
   * 使用 `maxUsersPerRequest` 大於一的值（如果您希望目的地的API呼叫包含多個設定檔，以及其區段資格、身分和設定檔屬性）。
2. [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md) 並將目的地伺服器設定的ID新增至 `destinationDelivery.destinationServerId`.
3. [取得目的地設定的ID](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 您剛剛建立的，所以您可以在範本建立工具中使用它。
4. 瞭解 [您可以使用哪些函式和篩選器](../../functionality/destination-server/supported-functions.md) 在訊息轉換範本中。

## 如何使用範例範本API和轉譯範本API為您的目的地建立範本 {#iterative-process}

>[!TIP]
>
>在建立及編輯訊息轉換範本之前，您可以先呼叫 [轉譯範本API端點](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) 使用簡單範本匯出原始設定檔，而不套用任何轉換。 簡單範本的語法為： <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

取得和測試範本的程式是反複進行的。 重複下列步驟，直到匯出的設定檔符合目的地預期的資料格式。

1. 首先， [取得範例範本](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. 使用範例範本作為建立您自己的草稿的起點。
3. 呼叫 [轉譯範本API端點](../../testing-api/streaming-destinations/create-template.md#render-template-api) 使用您自己的範本。 Adobe會根據您的結構描述產生範例設定檔，並傳回結果或任何遇到的錯誤。
4. 將匯出的資料與目的地預期的資料格式進行比較。 如有需要，請編輯範本。
5. 重複此程式，直到匯出的設定檔符合目的地預期的資料格式。

## 使用範本範例API取得範本範例 {#sample-template-api}

>[!NOTE]
>
>如需完整的API參考檔案，請閱讀 [取得範例範本API作業](../../testing-api/streaming-destinations/sample-template-api.md).

將目的地ID新增至呼叫，如下所示，回應會傳回與目的地ID對應的範本範例。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

如果您提供的目的地ID對應至具有的目的地設定 [最大努力彙總](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 和 `maxUsersPerRequest=1` 在彙總原則中，要求會傳回類似以下的範例範本：

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

## 逸出範本的字元 {#character-escape-template}

在使用範本轉譯符合目的地預期格式的設定檔之前，您必須對範本進行字元逸出，如下面的熒幕錄製所示。

![此影片說明如何使用線上字元逸出工具來逸出範本](../../assets/testing-api/escape-characters.gif)

您可以使用線上字元逸出工具。 上述示範使用 [JSON逸出格式器](https://jsonformatter.org/json-escape).

## 轉譯器範本API {#render-template-api}

使用建立訊息轉換範本後 [範例範本API](create-template.md#sample-template-api)，您可以 [演算範本](render-template-api.md) 以根據它產生匯出的資料。 這可讓您驗證Adobe Experience Platform要匯出至目的地的設定檔是否符合目的地的預期格式。

請參考API參考以取得您可以進行的呼叫範例：

* [演算沒有在正文中傳送設定檔的範本](render-template-api.md#multiple-profiles-no-body)
* [使用傳送於內文中的設定檔演算範本](render-template-api.md#multiple-profiles-with-body)

編輯範本並呼叫轉譯器範本API端點，直到匯出的設定檔符合目的地的預期資料格式為止。

## 將您的字元逸出範本新增至目的地伺服器設定

在您滿意訊息轉換範本後，請將其新增至您的 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md)，在 `httpTemplate.requestBody.value`.
