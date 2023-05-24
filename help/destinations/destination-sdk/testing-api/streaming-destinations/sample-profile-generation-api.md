---
description: 瞭解如何使用目的地測試API為您的串流目的地產生範例設定檔，以用於目的地測試。
title: 根據來源結構描述產生範例設定檔
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---


# 根據來源結構描述產生範例設定檔 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API端點**： `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

此頁面列出並描述您可以使用執行的所有API作業。 `/authoring/sample-profiles` api端點。

## 為不同的API產生不同的設定檔型別 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>使用此API端點可針對兩個不同的使用案例產生範例設定檔。 您可以：
>* 產生設定檔以用於 [製作和測試訊息轉換範本](create-template.md)  — 使用 *目的地ID* 作為查詢引數。
>* 產生設定檔以在對進行呼叫時使用 [測試您的目的地是否已正確設定](streaming-destination-testing-overview.md)  — 使用 *目的地執行個體識別碼* 作為查詢引數。


您可以根據AdobeXDM來源結構描述（在測試目的地時使用）或目的地支援的目標結構描述（在製作範本時使用）來產生範例設定檔。 若要瞭解AdobeXDM來源結構描述和目標結構描述之間的差異，請閱讀 [訊息格式](../../functionality/destination-server/message-format.md) 文章。

請注意，範例設定檔的使用目的不可互換。 根據以下專案產生的設定檔： *目的地ID* 僅可用於製作訊息轉換範本及根據 *目的地執行個體識別碼* 只能用於測試您的目的地端點。

## 範例設定檔產生API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 根據測試目的地時使用的來源結構描述產生範例設定檔 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>新增在此產生的範例設定檔至HTTP呼叫，當 [測試您的目的地](streaming-destination-testing-overview.md).

您可以向以下發出GET要求，根據來源結構描述產生範例設定檔： `authoring/sample-profiles/` 端點，並提供您根據要測試的目的地設定而建立的目的地執行個體的ID。

若要取得目的地執行個體的ID，您必須先在Experience PlatformUI中建立與目的地的連線，才能嘗試測試您的目的地。 閱讀 [啟用目的地教學課程](../../../ui/activation-overview.md) 以及如何取得要用於此API的目的地執行個體ID，請參閱以下秘訣。

>[!IMPORTANT]
>
>* 若要使用此API，您在Experience PlatformUI中必須有與目的地的現有連線。 讀取 [連線到目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 和 [對目的地啟用設定檔和區段](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 以取得詳細資訊。
> * 建立與目的地的連線後，請在以下情況下取得您應用於此端點的API呼叫中的目的地執行個體ID： [瀏覽與目的地的連線](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI影像如何取得目的地執行個體ID](../../assets/testing-api/get-destination-instance-id.png)


**API格式**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查詢引數 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您產生範例設定檔時所依據的目的地執行個體的ID。 |
| `{COUNT}` | *可选*. 您正在產生的範例設定檔數目。 引數可取的值介於 `1 - 1000`. <br> 如果未指定count引數，則產生的設定檔的預設數量由 `maxUsersPerRequest` 中的值 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如果此屬性未定義，則Adobe將產生一個範例設定檔。 |

{style="table-layout:auto"}


**请求**

以下請求會產生範例設定檔，設定者為 `{DESTINATION_INSTANCE_ID}` 和 `{COUNT}` 查詢引數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及與來源XDM結構描述相對應的區段會籍、身分和設定檔屬性。

>[!TIP]
>
> 回應只會傳回目的地執行個體中使用的區段會籍、身分和設定檔屬性。 即使您的來源結構描述有其他欄位，這些欄位也會被忽略。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentMembership` | 描述個人區段會籍的地圖物件。 如需詳細資訊，請參閱 `segmentMembership`，讀取 [區段會籍細節](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | 此設定檔上次符合區段資格的時間戳記。 |
| `xdm:status` | 字串欄位，指出是否已將區段會籍實現為目前請求的一部分。 接受下列值： <ul><li>`realized`：設定檔是區段的一部分。</li><li>`exited`：設定檔正在退出區段，做為目前請求的一部分。</li></ul> |
| `identityMap` | 說明個人的各種身分值及其相關名稱空間的對應型別欄位。 如需詳細資訊，請參閱 `identityMap`，讀取 [結構描述組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style="table-layout:auto"}

## 根據建立訊息轉換範本時要使用的目標結構描述產生範例設定檔 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>在中，使用製作範本時此處產生的範例設定檔 [演算範本步驟](render-template-api.md#multiple-profiles-with-body).

您可以根據向「 」發出GET請求的目標結構描述來產生範例設定檔 `authoring/sample-profiles/` 端點，並提供您建立範本時依據之目的地設定的目的地ID。

>[!TIP]
>
>* 您應在此使用的目的地ID為 `instanceId` 對應至目的地組態，建立目的地組態時，使用 `/destinations` 端點。 請參閱 [擷取目的地設定](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 以取得更多詳細資料。


**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查詢引數 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 目的地設定的ID，系統會根據此ID產生範例設定檔。 |
| `{COUNT}` | *可选*. 您正在產生的範例設定檔數目。 引數可取的值介於 `1 - 1000`. <br> 如果未指定count引數，則產生的設定檔的預設數量由 `maxUsersPerRequest` 中的值 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). 如果此屬性未定義，則Adobe將產生一個範例設定檔。 |

{style="table-layout:auto"}

**请求**

以下請求會產生範例設定檔，設定者為 `{DESTINATION_ID}` 和 `{COUNT}` 查詢引數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及與目標XDM結構描述相對應的區段會籍、身分和設定檔屬性。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在瞭解如何產生範例設定檔，以便 [測試訊息轉換範本](create-template.md) 或 [測試您的目的地是否已正確設定](streaming-destination-testing-overview.md).
