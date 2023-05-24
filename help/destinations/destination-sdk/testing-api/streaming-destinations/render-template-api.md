---
description: 瞭解如何使用目的地測試API，根據您的訊息轉換範本，驗證串流目的地的輸出。
title: 驗證匯出的設定檔結構
exl-id: e64ea89e-6064-4a05-9730-e0f7d7a3e1db
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 1%

---


# 驗證匯出的設定檔結構 {#render-template-api-operations}

>[!IMPORTANT]
>
>**API端點**： `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

此頁面列出並描述您可以使用執行的所有API作業。 `/authoring/testing/template/render` API端點，用於根據您的 [訊息轉換範本](../../functionality/destination-server/message-format.md#using-templating). 如需此端點支援的功能的說明，請閱讀 [建立範本](create-template.md).

## 開始使用轉譯器範本API作業 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 根據訊息轉換範本演算匯出的設定檔 {#render-exported-data}

您可以透過向以下專案發出POST請求來演算匯出的設定檔： `authoring/testing/template/render` 端點，並提供目的地設定的目的地ID以及您使用建立的範本 [範例範本API端點](sample-template-api.md).

您可以先使用簡單範本來匯出原始設定檔而不套用任何轉換，然後移至更複雜的範本，將轉換套用至設定檔。 簡單範本的語法為： <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

>[!TIP]
>
>* 您應在此使用的目的地ID為 `instanceId` 對應至目的地組態，建立目的地組態時，使用 `/destinations` 端點。 請參閱 [擷取目的地設定](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 以取得更多詳細資料。


**API格式**


```http
POST authoring/testing/template/render
```

| 請求引數 | 描述 |
| -------- | ----------- |
| `destinationId` | 您要為其呈現匯出設定檔的目的地設定ID。 |
| `template` | 根據您轉譯匯出設定檔的範本之字元逸出版本。 |
| `profiles` | *可选*. 您可以將設定檔新增至請求內文。 如果您未新增任何設定檔，Experience Platform會自動產生設定檔，並將其新增至請求。 <br> 如果您想要將設定檔新增至呼叫內文，可以使用產生一些設定檔 [範例設定檔產生API](sample-profile-generation-api.md). |

{style="table-layout:auto"}

請注意，轉譯器範本API端點傳回的回應會根據目的地彙總原則而有所不同。 如果您的目的地具有可設定的彙總原則，則也會在回應中傳回決定如何彙總設定檔的彙總金鑰。 閱讀關於 [彙總原則](../../functionality/destination-configuration/aggregation-policy.md) 以取得更多詳細資料。

| 回應引數 | 描述 |
| -------- | ----------- |
| `aggregationKey` | 代表匯出至目的地時彙總設定檔的原則。 此引數為選用引數，只有在目的地彙總原則設定為時才會出現 `CONFIGURABLE_AGGREGATION`. |
| `profiles` | 顯示請求中提供的設定檔，或如果請求中未提供設定檔，則顯示自動產生的設定檔。 |
| `output` | 根據提供的訊息轉換範本，以逸出字串形式呈現一個或多個設定檔 |

以下各節提供上述兩種情況的詳細請求和回應。

* [最大努力彙總和包含在請求內文中的設定檔](#best-effort)
* [請求內文中包含的可設定彙總和設定檔](#configurable-aggregation)

### 使用盡最大努力彙總和請求內文中包含的單一設定檔來呈現匯出的設定檔 {#best-effort}

**请求**

以下請求會轉譯符合目的地預期格式的匯出設定檔。 在此範例中，目的地ID會對應至具有盡最大努力彙總的目的地設定，而範例設定檔會包含在請求內文中。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "947c1c46-008d-40b0-92ec-3af86eaf41c1",
    "template": "{#- THIS is an example template for a single profile -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"identities\": [\r\n    {%- for idMapEntry in input.profile.identityMap -%}\r\n    {%- set namespace = idMapEntry.key -%}\r\n        {%- for identity in idMapEntry.value %}\r\n        {\r\n            \"type\": \"{{ namespace }}\",\r\n            \"id\": \"{{ identity.id }}\"\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n        {%- for segment in input.profile.segmentMembership.ups | added %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n        {#- Alternative syntax for filtering segments by status: -#}\r\n        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "gaid": [
                    {
                        "id": "gaid-BLAcJ"
                    }
                ],
                "idfa": [
                    {
                        "id": "idfa-Iv5AG"
                    }
                ],
                "email": [
                    {
                        "id": "email-rbN62"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**响应**

回應會傳迴轉譯範本的結果，或任何遇到的錯誤。
成功的回應會傳回HTTP狀態200以及匯出資料的詳細資訊。 在中尋找匯出的設定檔 `output` 引數，當作逸出字串。
失敗的回應會傳回HTTP狀態400以及所發生錯誤的說明。

```json
{
    "results": [
        {
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                                "status": "realized"
                            },
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                                "status": "exited"
                            },
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "gaid": [
                            {
                                "id": "gaid-BLAcJ"
                            }
                        ],
                        "idfa": [
                            {
                                "id": "idfa-Iv5AG"
                            }
                        ],
                        "email": [
                            {
                                "id": "email-rbN62"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"identities\": [\r\n        {\r\n            \"type\": \"gaid\",\r\n            \"id\": \"gaid-BLAcJ\"\r\n        },\r\n        {\r\n            \"type\": \"idfa\",\r\n            \"id\": \"idfa-Iv5AG\"\r\n        },\r\n        {\r\n            \"type\": \"email\",\r\n            \"id\": \"email-rbN62\"\r\n        }\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            \"segmentid1\",\r\n            \"segmentid2\"\r\n        ],\r\n        \"remove\": [\r\n            \"segmentid3\"\r\n        ]\r\n    }\r\n}"
        }
    ]
}    
```

### 呈現具有可設定彙總的匯出設定檔和包含在請求內文中的設定檔 {#configurable-aggregation}

**请求**


以下請求會轉譯多個符合目的地預期格式的匯出設定檔。 在此範例中，目的地ID會對應至具有可設定彙總的目的地設定。 請求內文中包含兩個設定檔，每個設定檔都具有三個區段資格和五個身分。 您可以使用產生設定檔以在呼叫時傳送 [範例設定檔產生API](sample-profile-generation-api.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
    "destinationId": "c2bc84c5-589c-43a1-96ea-becfa941f5be",
    "template": "{#- THIS is an example template for multiple profiles -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"profiles\": [\r\n    {%- for profile in input.profiles %}\r\n        {\r\n            \"identities\": [\r\n            {%- for idMapEntry in profile.identityMap -%}\r\n            {%- set namespace = idMapEntry.key -%}\r\n                {%- for identity in idMapEntry.value %}\r\n                {\r\n                    \"type\": \"{{ namespace }}\",\r\n                    \"id\": \"{{ customerData }}\"\r\n                }{%- if not loop.last -%},{%- endif -%}\r\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n            {% endfor %}\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                {%- for segment in profile.segmentMembership.ups | added %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ],\r\n                \"remove\": [\r\n                {#- Alternative syntax for filtering segments by status: -#}\r\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ]\r\n            }\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ]\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947859Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-biCbJ"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-0Q3hp"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-mN1Hw"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-MVw4L"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-2OjnN"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        },
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948187Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-fxt2p"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-sboQe"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-MRelR"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-M46ze"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-40Vrf"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**响应**

回應會傳迴轉譯範本的結果，或任何遇到的錯誤。
成功的回應會傳回HTTP狀態200以及匯出資料的詳細資訊。 在回應中通知如何根據區段會籍和身分彙總設定檔。 在中尋找匯出的設定檔 `output` 引數，當作逸出字串。
失敗的回應會傳回HTTP狀態400以及所發生錯誤的說明。

```json
{
    "results": [
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        }
    ]
}
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道如何使用訊息轉換範本產生符合目的地預期資料格式的匯出設定檔。 讀取 [如何使用Destination SDK設定您的目的地](../../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
